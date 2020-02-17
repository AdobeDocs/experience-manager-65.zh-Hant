---
title: 編輯頁面屬性
seo-title: 編輯頁面屬性
description: 頁面的屬性會依頁面的性質而有所不同。 例如，有些頁面可能會連線至即時副本，而其他頁面則未連線，且即時副本資訊會視需要提供。
seo-description: 頁面的屬性會依頁面的性質而有所不同。 例如，有些頁面可能會連線至即時副本，而其他頁面則未連線，且即時副本資訊會視需要提供。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些視頁面性質而定。 例如，有些頁面可能會連線至即時副本，而其他頁面則未連線，且即時副本資訊會視需要提供。

## 頁面內容 {#page-properties}

屬性分佈在多個頁籤中：

### 基本 {#basic}

* **標題**

   頁面標題會顯示在不同的位置。 例如，「網站 **」標籤清單** ，以及「網 **站** 」卡片／清單檢視。

   這是必要欄位。

* **標記**

   您可以在此處新增標籤，或從頁面移除標籤，方法是更新選取方塊中的清單：

   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 您可以在空的選取方塊中輸入名稱，以輸入全新的標籤。

      當您按下Enter時，實際會建立新標籤。 然後，新標籤會顯示在方塊中，右側有一個小星號表示它是新標籤。

   * 透過下拉式功能，您可從現有標籤中選取。
   * 當您將滑鼠移至選取方塊中的標籤項目上時，會顯示x;這可用於移除此頁面的標籤。

* **於導覽中隱藏**

   切換開關，指出頁面導覽中是顯示還是隱藏。

* **頁面標題**

   要在頁面上使用的標題。

* **導覽標題**

   您可以指定個別標題以用於導覽（例如，如果您想要更簡潔的內容）。 如果為空白， **則使** 用「標題」。

* **子標題**

   頁面上使用的副標題。

* **說明**

   您對頁面的說明、其用途或您要新增的任何其他詳細資訊。

* **開啟時間**

   啟動發佈頁面的日期和時間。 發佈時，此頁面將保持休眠，直到指定時間為止。

   請將這些欄位留空，以便立即發佈頁面（一般情形）。

* **關閉時間**

   發佈頁面將停用的時間。

   再次將這些欄位留空，以供您要立即發佈的頁面使用。

* **虛名 URL**

   可讓您輸入此頁面的虛名URL。 這可讓您擁有更短、表達能力更強的URL。

   例如，如果「虛名URL」設為w `elcome`至由網站h的路徑／所 `v1.0/startpage`識別的頁 `ttp://example.com,` 面，則h `ttp://example.com/welcome`會是h的虛名URL `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虛名URL:
   >
   >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援regex模式。


* **重新導向虛名 URL**

   指出您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **語言**

   頁面語言。

* **重新導向**

   指出此頁面應自動重新導向至的頁面。

* **設計**

   指定要 [用於](/help/sites-developing/designer.md) 本頁的設計。

* **別名**

   指定要與此頁一起使用的別名。

* **啟用已關閉的使用者群組**

   啟用（或停用）關閉 [的使用者群組](/help/sites-administering/cug.md) (CUG)。

* **登入頁面**

   用於登入的頁面。

* **公認群組**

   可登入CUG的群組。

* **領域**

   CUG的領域名稱。

* **匯出設定**

   指定匯出設定。

### 縮圖 {#thumbnail}

* **頁面縮圖**

   顯示頁面縮圖影像。 您可以：

   * **產生預覽**

      產生頁面的預覽以做為縮圖。

   * **上傳影像**

      上傳影像以當做縮圖使用。

### 雲端服務 {#cloud-services}

* **雲端服務**

   定義雲端服 [務的屬性](/help/sites-developing/extending-cloud-config.md)。

### 個性化 {#personalization}

* **個性化**

   選取品 [牌以指定定位範圍](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

### 權限 {#permissions}

* **權限** （觸控最佳化UI）

   檢視有 [效權限並新增權限](/help/sites-administering/user-group-ac-admin.md)。

### Blueprint {#blueprint}

* **Blueprint**

   在多網站管理中定義Blueprint [頁面的屬性](/help/sites-administering/msm.md)。 控制修改將傳播至即時副本的情況。

### 即時副本 {#live-copy}

* **即時副本**

   在多網站管理中定義即時副 [本頁面的屬性](/help/sites-administering/msm.md)。 控制從Blueprint傳播修改的情況。

### 網站結構 {#site-structure}

* 提供提供整個網站功能的頁面連結，例如 **「註冊頁面**」 **、「離線頁面**」等。

## 編輯頁面屬性 {#editing-page-properties-2}

### 編輯特定頁面的頁面屬性 {#editing-page-properties-for-a-specific-page}

「頁面屬性」可定義頁面在網站上出現的各種屬性，例如標題等。

1. 開啟您要編輯的頁面。

1. 在sidekick中開啟「頁 **面** 」標籤，然 **後選取「頁面屬性……」**

   這會開啟包含多個標籤的對話方塊。

1. 進行所需的更改，然後按一下「 **確定** 」保存。

