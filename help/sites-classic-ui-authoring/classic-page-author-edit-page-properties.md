---
title: 編輯頁面屬性
seo-title: 編輯頁面屬性
description: 頁面的屬性可能會因頁面性質而異。 例如，某些頁面可能連線至即時副本，而其他頁面則未連線，且即時副本資訊將可視情況提供。
seo-description: 頁面的屬性可能會因頁面性質而異。 例如，某些頁面可能連線至即時副本，而其他頁面則未連線，且即時副本資訊將可視情況提供。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 8%

---

# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些項目可能會因頁面性質而異。 例如，某些頁面可能連線至即時副本，而其他頁面則未連線，且即時副本資訊將可視情況提供。

## 頁面內容 {#page-properties}

屬性分佈在多個索引標籤中：

### 基本 {#basic}

* **標題**

   頁面標題會顯示在各種位置中。 例如， **Websites**&#x200B;索引標籤清單和&#x200B;**Sites**&#x200B;卡片/清單檢視。

   這是必要欄位。

* **標記**

   您可以在此更新選取方塊中的清單，以從頁面新增或移除標籤：

   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 您可以在空白的選取方塊中輸入名稱，以輸入全新的標籤。

      新標籤實際上會在您點擊Enter時建立。 新標籤隨即會顯示在方塊中，右側會加上小星號，指出為新標籤。

   * 透過下拉式功能，您可以從現有標籤中選取。
   * 將滑鼠移至選取方塊中的標籤項目上時，會顯示x;這可用來移除此頁面的該標籤。

* **於導覽中隱藏**

   切換開關，以指出頁面導覽中是否顯示或隱藏頁面。

* **頁面標題**

   要在頁面上使用的標題。

* **導覽標題**

   您可以指定個別標題以用於導覽（例如，如果您想要更精簡的標題）。 如果空白，則將使用&#x200B;**Title**。

* **子標題**

   用於頁面的副標題。

* **說明**

   您對頁面的說明、其用途或您要新增的任何其他詳細資訊。

* **開啟時間**

   啟動已發佈頁面的日期和時間。 發佈後，此頁面將保持休眠狀態，直到指定的時間。

   對於您要立即發佈的頁面，請將這些欄位保留空白（一般情況）。

* **關閉時間**

   已發佈頁面停用的時間。

   對於您要立即發佈的頁面，請再次將這些欄位保留為空白。

* **虛名 URL**

   可讓您輸入此頁面的虛名URL。 這可讓您擁有更短、表達能力更強的URL。

   例如，若虛名URL設為w `elcome`，設為網站h `ttp://example.com,`的路徑/ `v1.0/startpage`所識別的頁面，則h `ttp://example.com/welcome`將為h `ttp://example.com/content/v1.0/startpage`的虛名URL

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 值必須是唯一的，因此您應注意，值尚未被其他頁面使用。
   >* 不支援regex模式。


* **重新導向虛名 URL**

   指出您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **語言**

   頁面語言。

* **重新導向**

   指定此頁面應自動重新導向的頁面。

* **設計**

   指定要用於此頁面的[design](/help/sites-developing/designer.md)。

* **別名**

   指定要與此頁面一起使用的別名。

* **啟用已關閉的使用者群組**

   啟用（或停用）[封閉用戶組](/help/sites-administering/cug.md)(CUG)的使用。

* **登入頁面**

   用於登入的頁面。

* **公認群組**

   有資格登入CUG的群組。

* **領域**

   CUG的領域名稱。

* **匯出設定**

   指定匯出設定。

### 縮圖 {#thumbnail}

* **頁面縮圖**

   顯示頁面縮圖影像。 您可以：

   * **產生預覽**

      產生頁面的預覽以作為縮圖。

   * **上傳影像**

      上傳影像以作為縮圖。

### 雲端服務 {#cloud-services}

* **雲端服務**

   定義[雲端服務](/help/sites-developing/extending-cloud-config.md)的屬性。

### 個性化 {#personalization}

* **個性化**

   選擇[品牌以指定目標定位的範圍](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

### 權限 {#permissions}

* **權限** （觸控最佳化UI）

   檢視[有效權限並新增權限](/help/sites-administering/user-group-ac-admin.md)。

### Blueprint {#blueprint}

* **Blueprint**

   在[多網站管理](/help/sites-administering/msm.md)中定義Blueprint頁面的屬性。 控制修改將傳播至即時副本的情況。

### 即時副本 {#live-copy}

* **即時副本**

   為[多網站管理](/help/sites-administering/msm.md)內的Live Copy頁面定義屬性。 控制從Blueprint傳播修改的情況。

### 網站結構 {#site-structure}

* 提供提供全網站功能之頁面的連結，例如&#x200B;**註冊頁面**、**離線頁面**&#x200B;等。

## 編輯頁面屬性{#editing-page-properties-2}

### 編輯特定頁面{#editing-page-properties-for-a-specific-page}的頁面屬性

「頁面屬性」會定義頁面出現在網站上的各種屬性，例如標題。

1. 開啟您要編輯的頁面。

1. 在sidekick中，開啟&#x200B;**Page**&#x200B;標籤，然後選取&#x200B;**Page Properties...**

   這會開啟一個包含多個索引標籤的對話方塊。

1. 進行所需的更改，然後按一下「**確定**」以保存。
