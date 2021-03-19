---
title: 從Dynamic Media-混合模式移轉至Dynamic Media- S7模式
description: 瞭解如何將您的Dynamic Media-混合模式實例遷移至Dynamic Media- S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# 從Dynamic Media-雜交種到Dynamic Media-Scene7{#about-migrating}

Dynamic Media-Hybrid是Dynamic Media與Adobe Experience Manager整合的舊版軟體。 Hybrid版本最初於(AEMAdobe Experience Manager)6.1推出。雖然Adobe繼續支援混合模式，但它不是首選模式(Dynamic Media-Scene7是首選模式)。 它也不支援新功能，例如智慧型裁切和全景影像。 而Dynamic Media-Scene7則有。

Dynamic Media-Hybrid和Dynamic Media-Scene7之間的其他主要差異包括：

* URL的結構。
* 擷取影片。
* 建立和儲存影像轉譯。
* 雲端設定和認證（布建）。

當您從Dynamic Media-Hybrid移至Dynamic Media-Scene7時，有兩種選擇。 第一種選擇是簡單地為Dynamic Media-Scene7提供新的例AEM子。 第二個選擇是將您現有的Dynamic Media-Hybrid移轉至Dynamic Media-Scene7。 此選項在下表格中概述了移動過程中要執行的步驟和注意事項。

>[!IMPORTANT]
>
>Adobe建議您不要在即時生產例項上將Dynamic Media-Scene7混合實施移轉至Dynamic Media-。

## 選項1 —— 在{#provision-new-dms7}上提供新的Dynamic Media-Scene7AEM實例

考慮從Adobe Experience Manager的Dynamic Media-Scene7新實例開始。 除了透過Dynamic MediaCloud Service擷取和處理資產外，強烈建議您對資產使用、工作流程和元件進行Adobe稽核。 在許多情況下，自訂元件和工作流程可以由新的立即可用功能取代。

## 選項2 —— 將現有的Dynamic Media-Hybrid實例遷移到Dynamic Media-Scene7{#process-for-migrating}

| 步驟 | 任務 | 考量事項 |
|---|---|---|
| 1 | 仿製Dynamic Media-混合作者實例。 | 您應將現有的Dynamic Media-混合作者執行個體保留為備援用途，直到此移轉程式的其餘步驟順利完成為止。 |
| 2 | 在Dynamic Media-Scene7模式下啟動克隆的作者實例。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7證書配置Dynamic Media。 | Adobe需要批准Dynamic Media-Scene7布建。 您將擁有同時支援的動態MediaM-Hybrid和Dynamic Media-Scene7環境。 |
| 4 | 建立移轉套裝，以視需要收錄資產。<br>刪除在初始擷取至Dynamic Media-Hybrid時建立的本機PTIFF。 | 如果您的「Dynamic Media-混合」實例中目前有所有資產，則其克隆已包含全部資產。 因此，不需要搭售。 |
| 5 | 執行資產更新工作流程，將資產同步至Dynamic MediaCloud Service。 | Adobe建議以批次完成更新工作流，以允許壓縮。 |
| 6 | 移轉檢視器、影像和視訊預設集。 |  |
| 7 | 瀏覽每個「網頁內容管理」參考的資產，並更新其相關的URL。 |  |
| 8 | 移轉任何自訂工作流程以支援新的Dynamic Media-Scene7模式（手動更新）。 |  |
| 9 | 驗證您的「網頁內容管理」上傳和設定。 |  |
| 10 | 經過驗證後，請取得核准以停用「Dynamic Media-混合作者」（保留為後退版）。 |  |
| 11 | 在Dynamic Media-Scene7成功使用約一個月後，刪除Dynamic Media-混合作者實例。 |  |
