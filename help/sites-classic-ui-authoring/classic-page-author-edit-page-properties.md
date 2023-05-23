---
title: 編輯頁面屬性
description: 頁面的屬性可能因頁面的性質而異。 例如，某些頁面可能已連接到即時拷貝，而其他頁面則未連接，並且即時拷貝資訊將根據需要可用。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 8%

---

# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必需屬性。 這些內容可能因頁面的性質而異。 例如，某些頁面可能已連接到即時拷貝，而其他頁面則未連接，並且即時拷貝資訊將根據需要可用。

## 頁面內容 {#page-properties}

這些屬性分佈在多個頁籤上：

### 基本 {#basic}

* **標題**

   頁面標題顯示在不同的位置。 例如， **網站** 清單和 **站點** 卡/清單視圖。

   這是必要欄位。

* **標記**

   在此，您可以通過更新選擇框中的清單來添加標籤，或從頁面中刪除標籤：

   * 選擇標籤後，它將列在選擇框下。 可以使用x從此清單中刪除標籤。
   * 可以通過在空選擇框中鍵入名稱來輸入完全新的標籤。

      當您按Enter鍵時，將實際建立新標籤。 然後，新標籤將顯示在框中，右邊有一個小星號表示它是新標籤。

   * 使用下拉功能，您可以從現有標籤中進行選擇。
   * 將滑鼠懸停在選擇框中的標籤項上時，會出現x;這可用於刪除此頁的標籤。

* **於導覽中隱藏**

   切換開關，指示頁面導航中是否顯示或隱藏頁面。

* **頁面標題**

   要在頁面上使用的標題。

* **導覽標題**

   您可以指定單獨的標題以在導航中使用（例如，如果希望更簡潔一些的話）。 如果為空，則 **標題** 的下界。

* **子標題**

   用於頁面的副標題。

* **說明**

   您對頁面、其用途或要添加的任何其他詳細資訊的說明。

* **開啟時間**

   將激活已發佈頁面的日期和時間。 發佈時，此頁將保持休眠狀態，直到指定時間。

   將這些欄位留空，以便立即發佈頁面（常規方案）。

* **關閉時間**

   將停用已發佈頁面的時間。

   再次將這些欄位留空，以便立即發佈。

* **虛名 URL**

   允許您為此頁面輸入虛榮URL。 這樣，您就可以擁有一個更短、更富表達力的URL。

   例如，如果Vanity URL設定為w `elcome`到路徑/標識的頁面 `v1.0/startpage`網站h `ttp://example.com,` 然後 `ttp://example.com/welcome`會是他的虛榮URL `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 必須唯一，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援regex模式。


* **重新導向虛名 URL**

   指示是否希望頁面使用虛榮URL。

### 進階 {#advanced}

* **語言**

   頁面語言。

* **重新導向**

   指示此頁面應自動重定向到的頁面。

* **Design**

   指示 [設計](/help/sites-developing/designer.md) 用於此頁。

* **別名**

   指定要與此頁一起使用的別名。

* **啟用已關閉的使用者群組**

   啟用（或禁用） [關閉的用戶組](/help/sites-administering/cug.md) (CUG)。

* **登入頁面**

   用於登錄的頁面。

* **公認群組**

   有資格登錄CUG的組。

* **領域**

   CUG的領域名稱。

* **匯出設定**

   指定導出配置。

### 縮圖 {#thumbnail}

* **頁面縮圖**

   顯示頁面縮略圖。 您可以：

   * **產生預覽**

      生成要用作縮略圖的頁面預覽。

   * **上傳影像**

      上載影像以用作縮略圖。

### 雲端服務 {#cloud-services}

* **雲端服務**

   定義屬性 [雲服務](/help/sites-developing/extending-cloud-config.md)。

### 個人化 {#personalization}

* **個人化**

   選擇 [要指定目標範圍的品牌](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

### 權限 {#permissions}

* **權限** （觸控優化UI）

   查看 [有效權限和添加新權限](/help/sites-administering/user-group-ac-admin.md)。

### 藍圖 {#blueprint}

* **藍圖**

   定義「藍圖」頁的屬性 [多站點管理](/help/sites-administering/msm.md)。 控制將修改傳播到即時副本的情況。

### Live Copy {#live-copy}

* **即時副本**

   在中定義Live Copy頁的屬性 [多站點管理](/help/sites-administering/msm.md)。 控制從藍圖傳播修改的環境。

### 網站結構 {#site-structure}

* 提供指向提供站點範圍功能的頁面的連結，如 **註冊頁**。 **離線頁**&#x200B;其中包括：

## 編輯頁面屬性 {#editing-page-properties-2}

### 編輯特定頁的頁面屬性 {#editing-page-properties-for-a-specific-page}

頁面屬性定義頁面的各種屬性（如標題），當這些屬性出現在網站和其他頁面上時。

1. 開啟要編輯的頁面。

1. 在側腿上開啟 **頁面** 選項 **頁面屬性……**

   這將開啟一個具有多個頁籤的對話框。

1. 進行所需更改，然後按一下 **確定** 來保存。
