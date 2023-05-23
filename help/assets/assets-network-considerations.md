---
title: 網路注意事項和要求
description: 討論設計網路時的網路考慮事項 [!DNL Adobe Experience Manager Assets] 部署。
contentOwner: AG
role: Architect, Admin
feature: Developer Tools
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# [!DNL Assets] 網路注意事項 {#assets-network-considerations}

瞭解您的網路與瞭解您的網路同樣重要 [!DNL Adobe Experience Manager Assets]。 網路可影響上載、下載和用戶體驗。 繪製網路拓撲圖有助於確定網路中必須修復的瓶頸和次優化區域，以提高網路效能和用戶體驗。

確保在網路圖中包括以下內容：

* 從客戶端設備（例如，電腦、移動和平板電腦）到網路的連接。
* 公司網路的拓撲。
* 從公司網路和 [!DNL Experience Manager] 環境。
* 拓撲 [!DNL Experience Manager] 環境。
* 定義的同時使用者 [!DNL Experience Manager] 網路介面。
* 定義的工作流 [!DNL Experience Manager] 部署。

## 從客戶端設備到公司網路的連接 {#connectivity-from-the-client-device-to-the-corporate-network}

首先繪製單個客戶端設備與公司網路之間的連接圖。 在此階段，確定共用資源，如WiFi連接，其中多個用戶訪問同一點或乙太網交換機以上載和下載資產。

![chlimage_1-353](assets/chlimage_1-353.png)

客戶端設備以各種方式連接到公司網路，如共用WiFi、乙太網到共用交換機和VPN。 識別和瞭解此網路上的關鍵點對於 [!DNL Assets] 規劃和修改網路。

在圖的左上角，三台設備被描述為共用一個48 Mbps WiFi接入點。 如果所有設備同時上載，則WiFi網路頻寬在設備之間共用。 與整個系統相比，用戶可在該分割通道上遇到用於三個客戶機的不同的阻塞點。

測量WiFi網路的真實速度是個挑戰，因為速度較慢的設備可能會影響接入點上的其他客戶端。 如果計畫將WiFi用於資產交互，請同時執行來自多個客戶端的速度test以評估吞吐量。

圖的左下角顯示了通過獨立渠道連接到公司網路的兩台設備。 因此，每個設備可以使用10 Mbps和100 Mbps的最低速度。

右側顯示的電腦在VPN上的上游有限，速度為1 Mbps。 1Mbps連接的用戶體驗與1Gbps連接上的用戶體驗大不相同。 根據用戶與之交互的資產規模，其VPN上行鏈路可能不足以完成任務。

## 企業網路拓撲 {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

該圖顯示了公司網路內比通常使用的更高的上行鏈路速度。 這些管道是共用資源。 如果共用交換機應能處理50個客戶機，則它可能是一個瓶頸。 在初始圖中，只有兩台電腦共用特定連接。

## 從公司網路和 [!DNL Experience Manager] 環境 {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

考慮Internet和VPC連接上的未知因素非常重要，因為由於峰值負載或大規模提供商中斷，整個Internet的頻寬可能會受到損害。 總的來說，網際網路連接是可靠的。 但是，它有時會引入「咽喉」。

在從公司網路到網際網路的上行鏈路上，可以使用頻寬提供其他服務。 瞭解有多少頻寬可以專用或按優先順序排列資產非常重要。 例如，如果1 Gbps鏈路已處於80%的利用率，則您最多只能分配20%的頻寬 [!DNL Experience Manager Assets]。

企業防火牆和代理還可以通過多種不同的方式塑造頻寬。 此類設備可以使用服務質量、每個用戶的頻寬限制或每台主機的比特率限制來確定頻寬優先順序。 這些是需要檢查的重要要點，因為它們可以顯著影響 [!DNL Assets] 用戶體驗。

在本示例中，企業有10 Gbps上行鏈路。 它應該足夠大，可以容納幾個客戶。 此外，防火牆規定主機速率限制為10 Mbps。 此限制可能會將到單台主機的流量限制為10 Mbps，即使到網際網路的上行鏈路為10 Gbps。

這是最小的面向客戶的瓶頸。 但是，您可以評估是否更改或配置允許清單，該清單由負責此防火牆的網路操作組負責。

從示例圖中，您可以得出以下結論：六個設備共用一個概念性的10Mbps通道。 根據槓桿資產的規模，這可能不足以滿足用戶的期望。

## 拓撲 [!DNL Experience Manager] 環境 {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

設計拓撲 [!DNL Experience Manager] 環境需要詳細瞭解系統配置以及網路在用戶環境中的連接方式。

示例方案包括一個包含五台伺服器的發佈場、一個S3二進位儲存區和配置了Dynamic Media。

調度員與兩個實體共用100Mbps的連接，外界和 [!DNL Experience Manager] 部署。 對於同時上載和下載操作，應將此數字除以二。 連接的外部儲存使用單獨的連接。

的 [!DNL Experience Manager] 部署與多個服務共用1Gbps連接。 從網路拓撲的角度看，它相當於使用不同的服務共用一個通道。

查看從客戶端設備到 [!DNL Experience Manager] 部署時，最小的阻塞點似乎是10 Mbit企業防火牆節流。 您可以在中的大小計算器中使用這些值 [資產規模確定指南](assets-sizing-guide.md) 確定用戶體驗。

## 定義的工作流 [!DNL Experience Manager] 部署 {#defined-workflows-of-the-aem-deployment}

在考慮網路效能時，考慮系統中將要發生的工作流和發佈可能非常重要。 此外，您使用的S3或其他網路連接儲存和I/O請求會佔用網路頻寬。 因此，即使在完全優化的網路中，效能也可能受磁碟I/O的限制。

要簡化資產接收（尤其是在上載大量資產時）的流程，請瀏覽資產工作流並瞭解有關其配置的更多資訊。

評估內部工作流拓撲時，應分析以下內容：

* 編寫資產的過程
* 修改資產/元資料時觸發的工作流/事件
* 讀取資產的過程

以下是需要考慮的項目：

* XMP元資料讀/寫
* 自動激活和複製
* 水印
* 子元件攝取/頁面提取
* 重疊的工作流。

以下是資產工作流定義的客戶示例。

![chlimage_1-357](assets/chlimage_1-357.png)
