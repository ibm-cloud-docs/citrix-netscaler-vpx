---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 術語

Citrix NetScaler 平台同時使用產品特有術語以及基本負載平衡器術語和概念。 

### NetScaler IP (NSIP)

為進行管理而指定的負載平衡器 IP。

### 子網路 IP (SubNet IP, SNIP)

SNIP 是 NetScaler 每次想要與伺服器（或物件）通訊時所使用封包的來源 IP 位址。伺服器也會使用「子網路 IP」來回應 NetScaler。

### 虛擬 IP (Virtual IP, VIP)

VIP 是接收用戶端所傳送要求的 IP 位址。NetScaler 已終止 VIP 的用戶端連線，然後起始與負載平衡服務中已配置伺服器的連線。這可以是公用（網際網路）資料流量的公用 IP 位址，或專用（企業內部網路）資料流量的專用 IP 位址。

### 虛擬伺服器 (Virtual Server)

「虛擬伺服器」（負載平衡術語）指的是 IP 用戶端所連接的 IP 位址、埠與通訊協定組合，以及針對 NetScaler 正在進行負載平衡的特定應用程式傳送資料流量要求的位置。

### 服務 (Service)

用來將要求遞送至特定伺服器的 IP 位址、埠與通訊協定組合。「服務」在配置之後，稍後必須與「虛擬伺服器」相關聯。

### 伺服器物件 (Server Object)

此虛擬實體可讓您將重要名稱指派給實體伺服器，而不是使用其一般 IP 位址。

### 監視器 (Monitor)

此元素可讓您追蹤服務，確保其運作正確。監視器會使用探測及活動信號來追蹤「服務」狀態。
