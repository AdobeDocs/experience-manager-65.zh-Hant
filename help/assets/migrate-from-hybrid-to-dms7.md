---
title: 從動態媒體——混合模式移轉至動態媒體- S7模式
description: 瞭解如何將動態媒體——混合模式例項移轉至動態媒體- S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: f466193a259d9e8869d7f79eafda1be20869e4af

---


# 關於從動態媒體——混合媒體移轉至動態媒體-Scene7 {#about-migrating}

Dynamic Media-Hybrid是與Adobe Experience Manager整合的舊版Dynamic Media。 Hybrid版本是首次在AEM(Adobe Experience Manager)6.1中推出。雖然Adobe仍繼續支援混合模式，但並非偏好模式（Dynamic Media-Scene7為偏好模式）。 它也不支援新功能，例如智慧型裁切和全景影像。 而Dynamic Media-Scene7則提供。

Dynamic Media-Hybrid和Dynamic Media-Scene7之間的其他主要差異包括：

* URL的結構。
* 擷取影片。
* 建立和儲存影像轉譯。
* 雲端設定和認證（布建）。

從Dynamic Media-Hybrid移至Dynamic Media-Scene7時，有兩個選項可供使用。 第一個選項是在AEM上只要布建新的Dynamic Media-Scene7例項即可。 第二個選項是將您現有的Dynamic Media-Hybrid執行個體移轉至Dynamic Media-Scene7。 此選項在下表格中概述了移動過程中要執行的步驟和注意事項。

>[!IMPORTANT]
>
>Adobe建議您不要在即時製作執行個體上將動態媒體——混合實作移轉至Dynamic Media-Scene7。

## 選項1 —— 在AEM上布建新的Dynamic Media-Scene7例項 {#provision-new-dms7}

請考慮在Adobe Experience Manager上使用全新布建的Dynamic Media-Scene7例項，以全新開始。 除了透過Dynamic Media Cloud Service擷取和處理資產外，強烈建議Adobe對資產使用、工作流程和元件進行稽核。 在許多情況下，自訂元件和工作流程可以由新的立即可用功能取代。

## 選項2 —— 將您現有的Dynamic Media-Hybrid執行個體移轉至Dynamic Media-Scene7 {#process-for-migrating}

| 步驟 | 任務 | 考量事項 |
|---|---|---|
| 1 | 仿製動態媒體——混合作者實例。 | 您應維護您現有的動態媒體——混合作者執行個體，以便備援，直到此移轉程式的其餘步驟順利完成為止。 |
| 2 | 在Dynamic Media-Scene7模式中啟動複製的Author執行個體。 |  |
| 3 | 在Adobe Experience Manager Cloud Services中，使用Dynamic Media-Scene7認證來設定動態媒體。 | Adobe需要核准Dynamic Media-Scene7布建。 您將擁有同時支援Dynamic MediaM-Hybrid和Dynamic Media-Scene7環境，但時間有限。 |
| 4 | 建立移轉套裝，以視需要收錄資產。<br>刪除初始擷取至Dynamic Media-Hybrid時建立的本機PTIFF。 | 如果您的Dynamic Media-Hybrid實例中目前有所有資產可用，則其克隆已包含所有資產。 因此，不需要搭售。 |
| 5 | 執行資產更新工作流程，將資產同步至Dynamic Media Cloud Service。 | Adobe建議以批次方式完成更新工作流程，以允許壓縮。 |
| 6 | 移轉檢視器、影像和視訊預設集。 |  |
| 7 | 瀏覽每個「網頁內容管理」參考的資產，並更新其相關的URL。 |  |
| 8 | 移轉任何自訂工作流程，以支援新的Dynamic Media-Scene7模式（手動更新）。 |  |
| 9 | 驗證您的「網頁內容管理」上傳和設定。 |  |
| 10 | 經過驗證後，請取得核准以停用動態媒體混合作者（維持為後退）。 |  |
| 11 | 在Dynamic Media-Scene7成功使用約一個月後，請刪除Dynamic Media-Hybrid Author例項。 |  |
