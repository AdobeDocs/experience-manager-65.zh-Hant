---
title: 匯出為 CSV
seo-title: Export to CSV
description: 將有關頁面的資訊導出到本地系統上的CSV檔案
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 36%

---

# 匯出為 CSV{#export-to-csv}

**建立CSV報告** 允許您將有關頁面的資訊導出到本地系統上的CSV檔案。

* 已下載的檔案稱為 `export.csv`
* 內容取決於您選擇的屬性。
* 可以定義路徑和導出深度。

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
      * 不重複訪客
      * 頁面逗留時間
* 深度
   * 父路徑
   * 僅導向子項
   * 其他層級的子項
   * 層級

結果 `export.csv` 可以在Excel或任何其他相容應用程式中開啟檔案。

![etc-01](assets/etc-01.png)

建立 **CSV報告** 選項在瀏覽時可用 **站點** 控制台（在清單視圖中）:是 **建立** 下拉菜單：

![etc-02](assets/etc-02.png)

要建立CSV導出：

1. 開啟 **Sites** Console，視需要導覽至所需位置。
1. 從工具列中，依序選 **取「建立****CSV報表** 」以開啟精靈：

   ![etc-03](assets/etc-03.png)

1. 選擇要導出的必需屬性。
1. 選擇 **建立**。
