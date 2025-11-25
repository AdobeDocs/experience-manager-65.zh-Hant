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
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 26%

---

# 匯出為 CSV{#export-to-csv}

**建立CSV報表**&#x200B;可讓您將頁面的相關資訊匯出至本機系統上的CSV檔案。

* 下載的檔案名為`export.csv`
* 內容取決於您選取的屬性。
* 您可以定義路徑以及匯出的深度。

>[!NOTE]
>
>系統會使用瀏覽器的下載功能與預設目的地。

**建立CSV匯出**&#x200B;精靈可讓您選取：

* 要匯出的屬性
   * 後設資料
      * 名稱
      * 修改日期
      * 已發佈
      * 範本
      * 工作流程
   * 翻譯
      * 已翻譯
   * 分析
      * 頁面檢視量
      * 獨特訪客
      * 頁面逗留時間
* 深度
   * 父路徑
   * 僅導向子項
   * 其他層級的子項
   * 層級

產生的`export.csv`檔案可以用Excel或任何其他相容的應用程式開啟。

![etc-01](assets/etc-01.png)

瀏覽&#x200B;**網站**&#x200B;主控台（在清單檢視中）時，可以使用建立&#x200B;**CSV報表**&#x200B;選項：它是&#x200B;**建立**&#x200B;下拉式功能表的選項：

![etc-02](assets/etc-02.png)

若要建立CSV匯出：

1. 開啟&#x200B;**網站**&#x200B;主控台，視需要導覽至所需位置。
1. 從工具列中，依序選 **取「建立**&#x200B;**CSV報表** 」以開啟精靈：

   ![etc-03](assets/etc-03.png)

1. 選取要匯出的必要屬性。
1. 選取「**建立**」。
