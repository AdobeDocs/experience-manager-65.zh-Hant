---
title: 從Dynamic Media遷移 — 混合模式到Dynamic Media- S7模式
description: 瞭解如何將您的Dynamic Media實例遷移到Dynamic Media- S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# 從Dynamic Media — 混合型到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media — 混合體是Dynamic Media與Adobe Experience Manager融合的舊版本。 混合版首次在Adobe Experience Manager6.1推出。雖然Adobe繼續支援混合模式，但它不是首選模式；Dynamic Media-Scene7是首選的使用模式。 混合模式也不支援Smart Crop和全景影像等新功能，而Dynamic Media-Scene7則支援這些功能。

Dynamic Media — 混合動力和Dynamic Media-Scene7之間的其他主要差異包括：

* URL的結構
* 攝錄像。
* 建立和儲存影像格式副本。
* 雲配置和憑據（設定）。

當您從Dynamic Media — 混合型轉向Dynamic Media-Scene7時，可以選擇兩種選擇。 第一種選擇是簡單地提供Dynamic Media-Scene7關於Experience Manager的新實例。 第二個選擇是將您現有的Dynamic Media — 混合型實例遷移到Dynamic Media-Scene7。 此選項在下表中概述了移動過程中需要執行的步驟和注意事項。

>[!IMPORTANT]
>
>Adobe建議您不要在即時生產實例上將「Dynamic Media — 混合」實施遷移到Dynamic Media-Scene7。

## 備選案文1 — 規定Dynamic Media-Scene7關於Experience Manager的新實例 {#provision-new-dms7}

只需從Adobe Experience Manager的Dynamic Media-Scene7新實例開始即可。 除了通過Dynamic MediaCloud Service接收和處理資產外，還強烈建議對資產使用情況、工作流程和元件進行Adobe審計。 通常，您可以使用較新的現成功能替換自定義元件和工作流。

## 選項2 — 將您現有的Dynamic Media — 混合型實例遷移到Dynamic Media-Scene7 {#process-for-migrating}

| 步驟 | 任務 | 考量事項 |
|---|---|---|
| 1 | 克隆Dynamic Media — 混合作者實例。 | 維護您現有的Dynamic Media — 混合作者實例以備用，直到此遷移過程中的剩餘步驟成功完成。 |
| 2 | 在Dynamic Media-Scene7模式下啟動克隆的作者實例。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7證書配置Dynamic Media。 | Adobe必須批准Dynamic Media-Scene7設定。 因此，您有併發的Dynamic MediaM-Hybrid和Dynamic Media-Scene7環境，它們受Adobe支援，但時間有限。 |
| 4 | 建立遷移捆綁包，以便您可以根據需要接收資產。<br>刪除在初始接收到Dynamic Media — 混合時建立的本地PTIFF。 | 如果所有資產當前在您的Dynamic Media — 混合實例中都可用，則其克隆中已包括所有資產。 因此，不需要捆綁。 |
| 5 | 運行資產更新工作流，以便將資產同步到Dynamic MediaCloud Service。 | Adobe建議您分批執行更新工作流，以便進行壓縮。 |
| 6 | 遷移查看器、影像和視頻預設。 |  |
| 7 | 瀏覽每個Web內容管理引用的資產並更新其關聯的URL。 |  |
| 8 | 遷移要支援新Dynamic Media-Scene7模式（手動更新）的任何自定義工作流。 |  |
| 9 | 驗證Web內容管理上載和配置。 |  |
| 10 | 驗證後，獲得禁用Dynamic Media — 混合作者的批准（保留為備用）。 |  |
| 11 | 在Dynamic Media-Scene7成功使用約一個月後，刪除Dynamic Media — 混合作者實例。 |  |
