---
title: 編輯頁面屬性
description: 頁面的屬性可能會因頁面的性質而異。 例如，有些頁面可能已連線至即時副本，有些頁面則未連線，因此即時副本資訊將可酌情使用。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 9%

---

# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些值可能會因頁面性質而異。 例如，有些頁面可能已連線至即時副本，有些頁面則未連線，因此即時副本資訊將可酌情使用。

## 頁面內容 {#page-properties}

屬性分佈於數個索引標籤中：

### 基本 {#basic}

* **標題**

  頁面的標題會顯示在各種位置。 例如， **網站** 索引標籤清單和 **網站** 卡片/清單檢視。

  這是必要欄位。

* **標記**

  您可以在此處更新選取方塊中的清單，在頁面中新增或移除標籤：

   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 在空白選取方塊中輸入名稱，即可輸入全新的標籤。

     當您按下Enter鍵時，系統會實際建立新標籤。 然後，新標籤將顯示在方塊中，右側會顯示一個小星號，表示它是新標籤。

   * 使用下拉式功能，您可以從現有標籤中選取。
   * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x；這可用來為此頁面移除該標籤。

* **於導覽中隱藏**

  切換開關可指出頁面在頁面導覽中顯示或隱藏。

* **頁面標題**

  要在頁面上使用的標題。

* **導覽標題**

  您可以指定單獨的標題以用於導覽（例如，如果您想要更精簡的內容）。 如果為空， **標題** 已使用。

* **子標題**

  用於頁面上的子標題。

* **說明**

  頁面的說明、用途或您要新增的任何其他詳細資訊。

* **開啟時間**

  啟動已發佈頁面的日期和時間。 發佈後，此頁面將保持休眠狀態，直到指定的時間。

  對於您要立即發佈的頁面（一般案例），請將這些欄位保留空白。

* **關閉時間**

  停用已發佈頁面的時間。

  同樣地，請將這些欄位留空，以便您立即發佈頁面。

* **虛名 URL**

  可讓您輸入此頁面的虛名URL。 如此可讓您擁有更短且更能表達需知的URL。

  例如，如果虛名URL設為w `elcome`至路徑/所識別的頁面 `v1.0/startpage`針對網站h `ttp://example.com,` 然後h `ttp://example.com/welcome`會是h的虛名URL `ttp://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >虛名 URL:
  >
  >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
  >* 不支援規則運算式模式。

* **重新導向虛名 URL**

  指示您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **語言**

  頁面語言。

* **重新導向**

  指出此頁面應該自動重新導向的頁面。

* **Design**

  指出 [設計](/help/sites-developing/designer.md) 用於此頁面。

* **別名**

  指定要用於此頁面的別名。

* **啟用已關閉的使用者群組**

  啟用（或停用）使用 [封閉式使用者群組](/help/sites-administering/cug.md) (CUG)。

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

     產生頁面預覽，以做為縮圖使用。

   * **上傳影像**

     上傳要做為縮圖的影像。

### 雲端服務 {#cloud-services}

* **雲端服務**

  定義屬性 [雲端服務](/help/sites-developing/extending-cloud-config.md).

### 個人化 {#personalization}

* **個人化**

  選取 [品牌以指定目標定位的範圍](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### 權限 {#permissions}

* **許可權** （觸控最佳化的UI）

  檢視 [有效許可權和新增許可權](/help/sites-administering/user-group-ac-admin.md).

### 藍圖 {#blueprint}

* **藍圖**

  在中定義Blueprint頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制將修改傳播至即時副本的情況。

### Live Copy {#live-copy}

* **即時副本**

  在中定義即時副本頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制從Blueprint傳播修改的情況。

### 網站結構 {#site-structure}

* 提供全網站功能頁面的連結，例如 **註冊頁面**， **離線頁面**，以及其他專案。

## 編輯頁面屬性 {#editing-page-properties-2}

### 編輯特定頁面的頁面屬性 {#editing-page-properties-for-a-specific-page}

頁面屬性可定義頁面的各種屬性，例如標題，當這些屬性出現在網站和其他專案上時。

1. 開啟您要編輯的頁面。

1. 在sidekick中開啟 **頁面** 索引標籤，然後選取 **頁面屬性……**

   這會開啟含有多個索引標籤的對話方塊。

1. 進行您需要的變更，然後按一下 **確定** 以儲存。
