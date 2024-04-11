---
title: 匯出為 CSV
description: 將頁面的相關資訊匯出至本機系統上的CSV檔案
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 26%

---

# 匯出為 CSV{#export-to-csv}

**建立CSV報表** 可讓您將頁面的相關資訊匯出至本機系統上的CSV檔案。

* 下載的檔案稱為 `export.csv`
* 內容取決於您選取的屬性。
* 您可以定義路徑以及匯出的深度。

>[!NOTE]
>
>系統會使用瀏覽器的下載功能與預設目的地。

此 **建立CSV匯出** 精靈可讓您選取：

* 要匯出的屬性
   * 中繼資料
      * 名稱
      * 已修改
      * 已發佈
      * 範本
      * 工作流程
   * 轉換
      * 已翻譯
   * 分析
      * 頁面檢視
      * 獨特訪客
      * 頁面逗留時間
* 深度
   * 父路徑
   * 僅導向子項
   * 其他層級的子項
   * 層級

產生的結果 `export.csv` 檔案可在Excel或任何其他相容的應用程式中開啟。

![etc-01](assets/etc-01.png)

建立 **CSV報表** 瀏覽「 」時可使用此選項 **網站** 主控台（在清單檢視中）：這是 **建立** 下拉式功能表：

![etc-02](assets/etc-02.png)

若要建立CSV匯出：

1. 開啟 **網站** 主控台，視需要導覽至所需位置。
1. 從工具列中，依序選 **取「建立****CSV報表** 」以開啟精靈：

   ![etc-03](assets/etc-03.png)

1. 選取要匯出的必要屬性。
1. 選取「**建立**」。
