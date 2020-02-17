---
title: 匯出至 CSV
seo-title: 匯出至 CSV
description: 將您頁面的相關資訊匯出至本機系統上的CSV檔案
seo-description: 將您頁面的相關資訊匯出至本機系統上的CSV檔案
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 匯出至 CSV{#export-to-csv}

**「建立CSV報表** 」可讓您將有關頁面的資訊匯出至本機系統上的CSV檔案。

* 下載的檔案稱為 `export.csv`
* 內容取決於您選擇的屬性。
* 可定義路徑和導出深度。

>[!NOTE]
>
>使用瀏覽器的下載功能和預設目標。

「建 **立CSV匯出** 」精靈可讓您選擇：

* 要匯出的屬性
   * 中繼資料
      * 名稱
      * 修改時間
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

產生的 `export.csv` 檔案可在Excel或任何其他相容應用程式中開啟。

![]() ![etc-01](assets/etc-01.png)

瀏覽Sites **控制台時** （在「清單」檢視中），可使用「建立 **CSV報表** 」選項：它是「建立」( **Create** )下拉菜單的選項：

![etc-02](assets/etc-02.png)

若要建立CSV匯出：

1. 開啟 **Sites** Console，視需要導覽至所需位置。
1. 從工具列中，依序選 **取「建立****CSV報表** 」以開啟精靈：

   ![etc-03](assets/etc-03.png)

1. 選擇要導出的必需屬性。
1. 選擇 **建立**。
