---
title: 從Dynamic Media — 混合模式移轉至Dynamic Media - S7模式
description: 了解如何將您的Dynamic Media執行個體 — 混合模式移轉至Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7模式，混合模式
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 關於從Dynamic Media-Hybrid移轉至Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是舊版Dynamic Media與Adobe Experience Manager的整合。 混合版本最初在AEM(Adobe Experience Manager)6.1中推出。雖然Adobe持續支援混合模式，但並非偏好模式(Dynamic Media-Scene7為偏好模式)。 也不支援智慧型裁切和全景影像等新功能。 而Dynamic Media-Scene7。

Dynamic Media-Hybrid和Dynamic Media-Scene7之間的其他主要差異包括：

* URL的結構。
* 擷取影片。
* 建立和儲存影像轉譯。
* 雲端設定和憑證（布建）。

從Dynamic Media-Hybrid移至Dynamic Media-Scene7時，有兩個選項可供使用。 第一個選項是在AEM上布建新的Dynamic Media-Scene7例項。 第二個選項是將您現有的Dynamic Media-Hybrid執行個體移轉至Dynamic Media-Scene7。 此選項在下表格中概述了移動過程中需要執行的步驟和注意事項。

>[!IMPORTANT]
>
>Adobe建議您不要在即時生產執行個體上將Dynamic Media-Hybrid實作移轉至Dynamic Media-Scene7。

## 選項1 — 在AEM上布建Dynamic Media-Scene7的新例項 {#provision-new-dms7}

請考慮從Adobe Experience Manager上布建的Dynamic Media-Scene7新例項開始。 除了透過Dynamic MediaCloud Service擷取和處理資產外，強烈建議您對資產使用、工作流程和元件進行Adobe稽核。 在許多情況下，自訂元件和工作流程可能會取代為更新且現成可用的功能。

## 選項2 — 將您現有的Dynamic Media-Hybrid執行個體移轉至Dynamic Media-Scene7 {#process-for-migrating}

| 步驟 | 任務 | 考量事項 |
|---|---|---|
| 1 | 複製Dynamic Media — 混合製作例項。 | 您應保留現有的Dynamic Media — 混合作者例項，以備用，直到此移轉程式中的其餘步驟順利完成為止。 |
| 2 | 在Dynamic Media-Scene7模式中啟動複製的製作執行個體。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7憑證設定Dynamic Media。 | Adobe需要核准Dynamic Media-Scene7布建。 您將有同時支援Dynamic MediaM-Hybrid和Dynamic Media-Scene7環境，且支援時間有限。 |
| 4 | 視需要建立移轉套件以內嵌資產。<br>刪除初始擷取至Dynamic Media-Hybrid期間建立的本機PTIFF。 | 如果所有資產目前都可在您的Dynamic Media — 混合執行個體中使用，原地複製的已包含所有資產。 因此，不需要捆綁。 |
| 5 | 執行資產更新工作流程，將資產同步至Dynamic MediaCloud Service。 | Adobe建議分批完成更新工作流程，以便進行壓縮。 |
| 6 | 移轉檢視器、影像和視訊預設集。 |  |
| 7 | 逐一瀏覽每個參考Web內容管理的資產，並更新其相關聯的URL。 |  |
| 8 | 移轉任何自訂工作流程以支援新的Dynamic Media-Scene7模式（手動更新）。 |  |
| 9 | 驗證您的Web內容管理上傳和配置。 |  |
| 10 | 驗證後，取得停用Dynamic Media — 混合作者的核准（後援維護）。 |  |
| 11 | 在成功使用Dynamic Media-Scene7約一個月後，刪除Dynamic Media-Hybrid Author例項。 |  |
