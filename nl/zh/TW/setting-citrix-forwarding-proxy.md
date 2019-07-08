---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"

keywords: setup, proxy, forward, vip, subnet

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 設定 Citrix Netscaler VPX 作為正向 Proxy
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

正向 Proxy 是內部網路上的用戶端與網際網路之間的單一控制點。Proxy 可讓「網路」或「安全管理者」建立原則，以限制對網際網路網站的存取。

內部網路上的用戶端起始要求時，會使用 Proxy 的 IP 位址來起始網際網路上遠端伺服器的要求。遠端伺服器繼而會回應 Proxy，以將回應傳回給用戶端。

Proxy 一般會與防火牆合併使用，確保內部網路中的用戶端安全。

## 步驟 1：要求在專用網路中使用的 VIP
{: #step-1-request-vips-to-use-in-the-private-network}

從 {{site.data.keyword.BluSoftlayer_notm}} 客戶入口網站中訂購 Citrix NetScaler VPX 負載平衡器時，假設正在要求反向 Proxy。系統會向要求者要求用作虛擬 IP (VIP) 的「公用」IP 數目。

如果是正向 Proxy，則需要在專用網路上設定 VIP。需要開立支援問題單，才能要求專用網路的 VIP。需要的 VIP 數目將決定問題單中所要求的子網路大小。將會在問題單中傳回子網路資訊。

在我們的範例中，我們要求 `/29` 子網路，這會導致下列情況：

* 建立子網路 `10.114.27.0/29`，以用作專用 VIP

* 子網路 IP (SNIP) `10.114.52.101` 及遞送的子網路 `10.114.27.0/29`

* 支援團隊已將 VIP `10.114.27.0-3` 新增至 Citrix NetScaler VPX

## 步驟 2：在 Citrix NetScaler VPX 上啟用負載平衡及快取重新導向特性
{: #step-2-enable-load-balancing-and-cache-redirect-features-on-the-citrix-netscaler-vpx}

依預設，會停用 Citrix NetScaler VPX 負載平衡器上的負載平衡及快取重新導向特性；`enable ns feature cr lb` 指令會啟用它們。


## 步驟 3：建立正向 Proxy
{: #step-3-create-the-forward-proxy}

使用指令行，向 Citrix NetScaler VPX 發出下列指令。在我們的情境中，只會新增兩部 {{site.data.keyword.BluSoftlayer_notm}} DNS 伺服器的其中一部。  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

第 1 行建立重新導向快取。通訊協定為 HTTP，而 `10.114.27.3` 是專用網路上所要求的其中一個 VIP。埠是 HTTP 的預設埠 80，但因為在瀏覽器中將此位址及埠組合用作 Proxy 陳述式，所以可以將埠變更為需要的任何項目。

第 2 行新增將代表「真實」DNS 的負載平衡 VIP。

第 3 行將「真實」DNS 的 IP 位址新增為服務。此位址可以是客戶 DNS，或遞送回 {{site.data.keyword.BluSoftlayer_notm}} 提供的 DNS 解析器。

第 4 行將 VIP 連結至「真實」伺服器。`10.114.27.4` 的所有 DNS 要求都會傳送至 `10.0.80.12`。

第 5 行告知正向 Proxy 虛擬伺服器使用虛擬 DNS 進行名稱解析。

## 配置用戶端
{: #configuring-the-client}

繼續自訂用戶端以使用正向 Proxy 之前，請確定您無法在用戶端上使用 Firefox 瀏覽器來到達公用網站（例如，http://www.ibm.com）。因為用戶端上應該沒有公用介面，所以此要求會失敗。

下列範例會配置 Linux 用戶端。

需要對用戶端進行一些變更。第一項變更是將用戶端上的解析器指向可透過兩種方法之一完成的虛擬 DNS。

您可以手動編輯 `/etc/resolv.conf`，以指向 DNS 的虛擬位址。請注意，用戶端管理工具可能會將這些變更回復為原始設定。  

或者，您可以編輯 `/etc/sysconfig/network-scripts/ifcfg-ethx` 介面，並新增 `DNS1=` 陳述式。設定之後，可以發出服務網路重新啟動指令來反映變更。

在任一情況下，DNS IP 位址都需要配置為虛擬 DNS 位址，而且用戶端的瀏覽器需要配置成將要求指向 Citrix NetScaler VPX 正向 Proxy。

請在 Firefox 內使用下列步驟，以進行必要的變更：

1. 按一下**喜好設定 > 進階 > 網路 > 連線設定**。

* 選取**手動 Proxy 配置**，然後輸入下列項目：

  * **位址：**10.114.27.3

  * **埠：**80

  * 勾選**針對所有通訊協定使用此 Proxy 伺服器**勾選框。

* 按一下**儲存**，然後關閉瀏覽器視窗。

IP 位址 `10.114.27.3` 是在步驟 1 中建立之轉遞快取的 IP 位址。

此時，設定已完成，您可以從專用網路上隔離的資源來存取網際網路。

## 驗證設定
{: #validating-the-setup}

既然已將用戶端配置成使用正向 Proxy，請重試存取公用網站。要求現在應該會成功。

下列顯示指令可以用來驗證正向 Proxy 的狀態。

**show cr policy**：顯示所有現有快取重新導向原則。

**show policy map**：顯示已配置的對映原則及相關的對映原則資訊。

**show cr vserver**：顯示指定的快取重新導向虛擬伺服器，或所有已配置的快取重新導向虛擬伺服器。

**stat cr vserver：**顯示快取重新導向 Vserver 統計資料。

在 Citrix 上配置基本正向 Proxy 相當直接明確。它提供一種方法，可將網際網路上資源的安全路徑提供給內部網路上的用戶端。它也可讓「網路管理者」維護網路的控制層次。

如果在客戶網站上實作，則建議在配置中新增防火牆，以進一步保護資源。
