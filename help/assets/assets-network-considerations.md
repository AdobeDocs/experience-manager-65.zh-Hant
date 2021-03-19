---
title: 網路考量與需求
description: 在設計 [!DNL Adobe Experience Manager Assets] 部署時討論網路注意事項。
contentOwner: AG
role: 架構師、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---


# [!DNL Assets] 網路注意事項  {#assets-network-considerations}

瞭解網路與瞭解[!DNL Adobe Experience Manager Assets]一樣重要。 網路可能會影響上傳、下載和使用者體驗。 繪製網路拓撲圖有助於確定網路中必須修復的瓶頸和次優化區域，以改進網路效能和用戶體驗。

請確定您在網路圖中包含以下內容：

* 從用戶端裝置（例如電腦、行動裝置和平板電腦）連線至網路。
* 公司網路的拓撲。
* 從公司網路和[!DNL Experience Manager]環境上行到Internet。
* [!DNL Experience Manager]環境的拓撲。
* 定義[!DNL Experience Manager]網路介面的同時使用者。
* 已定義[!DNL Experience Manager]部署的工作流。

## 從客戶端設備到公司網路的連接{#connectivity-from-the-client-device-to-the-corporate-network}

首先，繪製個別客戶端設備與公司網路之間的連接圖。 在此階段，識別共用資源，例如WiFi連線，讓多位使用者存取相同的點或乙太網交換機，以上傳和下載資產。

![chlimage_1-353](assets/chlimage_1-353.png)

客戶機設備以多種方式連接到公司網路，如共用WiFi、乙太網到共用交換機和VPN。 識別和瞭解此網路上的阻塞點對於[!DNL Assets]規劃和修改網路非常重要。

在圖的左上角，有三台設備被描繪成共用48 Mbps WiFi接入點。 如果所有設備同時上傳，則WiFi網路頻寬在設備之間共用。 與整個系統相比，用戶可通過該分割的通道為三個客戶端遇到不同的瓶頸。

測量WiFi網路的真實速度是一項挑戰，因為慢速設備可能會影響接入點上的其他客戶端。 如果您打算將WiFi用於資產互動，請同時執行來自多個客戶端的速度測試，以評估吞吐量。

圖的左下角顯示了通過獨立通道連接到公司網路的兩個設備。 因此，每台設備的最低速度為10 Mbps和100 Mbps。

右側顯示的電腦在VPN上游的公司網路上有限，速度為1 Mbps。 1Mbps連線的使用者體驗與1Gbps連線的使用者體驗大不相同。 根據用戶交互的資產大小，其VPN上行鏈路可能不足以完成任務。

## 公司網路的拓撲{#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

該圖表顯示公司網路內的上行鏈路速度高於通常使用的速度。 這些管道是共用資源。 如果共用交換機需要處理50個客戶機，則可能是一個瓶頸。 在初始圖中，只有兩台電腦共用特定連接。

## 從公司網路和[!DNL Experience Manager]環境{#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}上行到Internet

![chlimage_1-355](assets/chlimage_1-355.png)

在Internet和VPC連接上考慮未知因素非常重要，因為由於峰值負載或大型提供商中斷，Internet上的頻寬可能會受到損害。 一般而言，網際網路連線是可靠的。 不過，它有時會引入阻塞點。

在從公司網路到網際網路的上行鏈路上，可以有其他使用頻寬的服務。 請務必瞭解資產的專用頻寬或優先順序。 例如，如果1 Gbps鏈路的利用率已達80%，則您只能為[!DNL Experience Manager Assets]分配最多20%的頻寬。

企業防火牆和Proxy也可以以多種不同的方式改變頻寬。 此類型的裝置可使用服務品質、使用者的頻寬限制或主機的位元速率限制來排列頻寬優先順序。 這些是需要檢查的重要阻斷點，因為它們可以顯著影響[!DNL Assets]使用者體驗。

在此示例中，企業有10 Gbps上行鏈路。 它應該足夠大，適合多個客戶。 此外，防火牆規定主機速率限制為10 Mbps。 此限制可能會將到單台主機的流量限制為10 Mbps，即使到Internet的上行鏈路為10 Gbps。

這是最小的面向客戶的瓶頸。 但是，您可以評估是否有更改或配置允許清單，該清單由負責此防火牆的網路操作組負責。

從示例圖中，您可以得出六個設備共用概念性的10Mbps通道。 視運用的資產規模而定，這可能不足以滿足使用者的期望。

## [!DNL Experience Manager]環境{#topology-of-the-aem-environment}的拓撲

![chlimage_1-356](assets/chlimage_1-356.png)

要設計[!DNL Experience Manager]環境的拓撲，需要詳細瞭解系統配置以及網路在用戶環境中的連接方式。

範例案例包括一個包含5個伺服器的發佈群、一個S3二進位儲存區，以及設定了Dynamic Media。

調度程式與兩個實體（外部世界和[!DNL Experience Manager]部署）共用100Mbps的連接。 若要同時上傳和下載作業，您應將此數字除以2。 連接的外部儲存器使用單獨的連接。

[!DNL Experience Manager]部署與多個服務共用1 Gbps連接。 從網路拓撲的角度看，它相當於共用一個具有不同服務的通道。

從客戶端設備到[!DNL Experience Manager]部署，查看網路時，最小的瓶頸似乎是10 Mbit企業防火牆限制。 您可以在[資產調整指南](assets-sizing-guide.md)中的調整大小計算器中使用這些值來判斷使用者體驗。

## 已定義[!DNL Experience Manager]部署{#defined-workflows-of-the-aem-deployment}的工作流

在考慮網路效能時，請務必考慮系統中將發生的工作流程和發佈。 此外，您使用的S3或其他網路連接儲存和I/O請求佔用網路頻寬。 因此，即使在完全優化的網路中，效能也可能受到磁碟I/O的限制。

若要簡化資產擷取的程式（尤其是上傳大量資產時），請探索資產工作流程並進一步瞭解其設定。

在評估內部工作流拓撲時，應分析以下內容：

* 編寫資產的程式
* 修改資產／中繼資料時觸發的工作流程／事件
* 讀取資產的程式

以下是一些需要考慮的項目：

* 元XMP資料讀／寫回復
* 自動啟動和複製
* 浮水印
* 子資產擷取／頁面擷取
* 重疊的工作流程。

以下是資產工作流程定義的客戶範例。

![chlimage_1-357](assets/chlimage_1-357.png)
