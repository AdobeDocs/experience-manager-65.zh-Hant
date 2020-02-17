---
title: 編輯頁面屬性
seo-title: 編輯頁面屬性
description: 定義頁面的必要屬性
seo-description: 定義頁面的必要屬性
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
translation-type: tm+mt
source-git-commit: 47a284a55f8d8f00ecda7be0bdcb8125cf976e3b

---


# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些視頁面性質而定。 例如，有些頁面可能會連線至即時副本，而其他頁面則未連線，且即時副本資訊會視需要提供。

## 頁面內容 {#page-properties}

屬性分佈在多個頁籤上。

### 基本 {#basic}

* **標題**

   頁面標題會顯示在不同的位置。 例如，「網站 **」標籤清單** ，以及「網 **站** 」卡片／清單檢視。

   這是必要欄位。

* **標記**

   您可以在此處新增標籤，或從頁面移除標籤，方法是更新選取方塊中的清單：

   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 您可以在空的選取方塊中輸入名稱，以輸入全新的標籤。

      * 當您按Enter時，將會建立新標籤。
      * 然後，新標籤會在右側顯示，並加上一個小星號，表示它是新標籤。
   * 透過下拉式功能，您可從現有標籤中選取。
   * 當您將滑鼠移至選取方塊中的標籤項目上時，會顯示x，可用來移除此頁面的標籤。
   如需標籤的詳細資訊，請參 [閱使用標籤](/help/sites-authoring/tags.md)。

* **於導覽中隱藏**

   指出在產生的網站的頁面導覽中是否顯示或隱藏頁面。

* **頁面標題**

   要在頁面上使用的標題。 通常由標題元件使用。 如果空白 **，則** 「標題」將被使用。

* **導覽標題**

   您可以指定個別標題以用於導覽（例如，如果您想要更簡潔的內容）。 如果為空白， **則使** 用「標題」。

* **子標題**

   頁面上使用的副標題。

* **說明**

   您對頁面的說明、其用途，或您要新增的任何其他詳細資訊。

* **開啟時間**

   啟動發佈頁面的日期和時間。 發佈時，此頁面將保持休眠，直到指定時間為止。

   請將這些欄位留空，以便立即發佈頁面（一般情形）。

* **關閉時間**

   發佈頁面將停用的時間。

   請再將這些欄位保留為空白，以便立即採取行動。

* **虛名 URL**

   可讓您輸入此頁面的虛名URL，讓您擁有更短和／或更具表現力的URL。

   例如，如果「虛名URL」設 `welcome`定為網站路徑所識 `/v1.0/startpage`別的 `http://example.com,` 頁面，則 `http://example.com/welcome`虛名URL為 `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虛名URL:
   >
   >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援regex圖樣。
   >* 不應設為現有頁面。


   您還需要配置Dispatcher以啟用對虛名URL的訪問。 如需詳 [細資訊，請參閱啟用虛名URL](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) 的存取權。

* **重新導向虛名 URL**

   指出您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **語言**

   頁面語言。

* **語言根目錄**

   如果頁面是語言副本的根目錄，則必須勾選。

* **重新導向**

   指出此頁面應自動重新導向至的頁面。

* **設計**

   指定要 [用於](/help/sites-developing/designer.md) 本頁的設計。

* **別名**

   指定要與此頁一起使用的別名。

   >[!NOTE]
   >
   >別名設定 `sling:alias` 屬性以定義資源的別名（這僅影響資源，而不影響路徑）。
   >
   >例如：如果為節點節點定 `latin-lang` 義別名， `/content/we-retail/spanish` 則可通過 `/content/we-retail/latin-language`
   >
   >如需詳細資訊，請參 [閱「SEO與URL管理最佳實務」下的「本地化頁面名稱」](/help/managing/seo-and-url-management.md#localized-page-names)。

* **繼承自&lt;*path*>**

   指出頁面是否繼承。 以及從何而來。

* **雲端設定**

   配置的路徑。

* **允許的範本**

   [定義此子分支中可用的模板清單](/help/sites-authoring/templates.md#allowingatemplate) 。

* **啟用** （驗證要求）

   啟用（或停用）驗證的使用以存取頁面。

   >[!NOTE]
   >
   >頁面的已關閉使用者群組是在「權限」標籤 **[上定義](/help/sites-authoring/editing-page-properties.md#permissions)**。

   >[!CAUTION]
   >
   >「權 **[限](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)**」標籤允許根據混音的存在編輯CUG配`granite:AuthenticationRequired`置。 如果頁面權限是使用已過時的CUG設定來設定，則會根據屬性的存在情況，在「驗證要求」下顯示警告訊息，且選項將不可編輯，也不可編輯`cq:cugEnabled`權限&#x200B;****[](/help/sites-authoring/editing-page-properties.md#permissions)。
   >
   >
   >在這種情況下，必須在傳統UI中編輯CUG [權限](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)。

* **登入頁面**

   用於登入的頁面。

* **匯出設定**

   指定匯出設定。

### 縮圖 {#thumbnail}

顯示頁面縮圖影像。 您可以：

* **產生預覽**

   產生頁面的預覽以做為縮圖。

* **上傳影像**

   上傳影像以當做縮圖使用。

* **選取影像**

   選取現有的資產以當做縮圖。

* **回復**

   在您變更縮圖後，此選項便可用。 如果您不想保留變更，可以在儲存前回復該變更。

### 社交媒體 {#social-media}

* **社交媒體分享**

   定義頁面上可用的共用選項。 顯示「共用」核心元件 [可用的選項](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html)。

   * **啟用Facebook的使用者共用**
   * **啟用Pinterest的使用者共用功能**
   * **偏好的XF變數**&#x200B;定義用於產生頁面中繼資料的體驗片段變數

### 雲端服務 {#cloud-services}

* **雲端服務**

   定義雲端服 [務的屬性](/help/sites-developing/extending-cloud-config.md)。

### 個性化 {#personalization}

* **ContextHub 組態**

   選取「 [ContextHub設定](/help/sites-administering/contexthub-config.md) 」和「 [區段路徑」](/help/sites-administering/segmentation.md)。

* **定位組態**

   選取品 [牌以指定定位範圍](/help/sites-authoring/target-adobe-campaign.md)。

### 權限 {#permissions}

* **權限**

   在此頁籤中，您可以：

   * [新增權限](/help/sites-administering/user-group-ac-admin.md)
   * [編輯已關閉的使用者群組](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * 檢視有效 [權限](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >「權 **限** 」標籤允許根據混音的存在編輯CUG配 `granite:AuthenticationRequired` 置。 如果頁面權限是使用已過時的CUG設定來設定的，則會根據屬性的存在而顯示警告訊息，且CUG權限將不可編輯，也不會編輯「 `cq:cugEnabled` Advanced [](/help/sites-authoring/editing-page-properties.md#advanced) 」（進階）標籤上的「Authentication Requirement」（驗證要求）。
   >
   >
   >在這種情況下，必須在傳統UI中編輯CUG [權限](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)。

   >[!NOTE]
   >
   >「權限」標籤不允許建立空的CUG群組，這可當成拒絕每位使用者存取的簡單方式。 要執行此操作，必須使用CRX瀏覽器。 如需詳細資 [訊，請參閱檔案使用者、群組和存取權限管理](/help/sites-administering/user-group-ac-admin.md) 。

### Blueprint {#blueprint}

* **Blueprint**

   在多網站管理中定義Blueprint [頁面的屬性](/help/sites-administering/msm.md)。 控制修改將傳播至即時副本的情況。

### 即時副本 {#live-copy}

* **即時副本**

   在多網站管理中定義即時副 [本頁面的屬性](/help/sites-administering/msm.md)。 控制從Blueprint傳播修改的情況。

### 網站結構 {#site-structure}

* 提供提供整個網站功能的頁面連結，例如 **「註冊頁面**」 **、「離線頁面**」等。

## 編輯頁面屬性 {#editing-page-properties-1}

您可以定義頁面屬性：

* 從Sites控 **制台** :

   * [建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page) （屬性的子集）

   * 按一下或點選「屬 **性」**

      * 適用於單一頁面
      * 對於多個頁面（只有屬性的子集可供整體編輯）

* 從頁面編輯器：

   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從Sites Console —— 單頁 {#from-the-sites-console-single-page}

按一下或點選 **「屬性** 」以定義頁面屬性：

1. 使用 **Sites** Console，導覽至您要檢視和編輯屬性之頁面的位置。

1. 使用下列 **任一項** ，為所需頁面選取「屬性」選項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#selectionmode)
   頁面屬性將使用適當的標籤顯示。

1. 視需要檢視或編輯屬性。

1. 然後使 **用** Save保存更新，然後 **Close** 返回控制台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用「頁 **面資訊** 」來定義頁面屬性：

1. 開啟您要編輯其屬性的頁面。

1. 選擇「頁 **面資訊** 」圖示以開啟選取功能表：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 選擇 **開啟屬性** ，並開啟一個對話框，允許您按相應頁籤進行編輯。 工具列右側也提供下列按鈕：

   * **取消**
   * **儲存並關閉**

1. 使用「 **儲存並關閉** 」按鈕儲存變更。

### 從Sites Console —— 多頁 {#from-the-sites-console-multiple-pages}

從Sites **** Console中，您可以選取數個頁面，然後使用 **View Properties** （檢視屬性）來檢視和／或編輯頁面屬性。 這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>Assets也提供大量屬性編輯功能。 很相似，但有幾點不同。 如需詳 [細資訊，請參閱編輯多個資產的屬性](/help/assets/managing-multiple-assets.md) 。
>
>此外還有「 [Bulk Editor](/help/sites-administering/bulk-editor.md)」（批量編輯器），它允許您使用GQL（Google查詢語言）從多個頁面搜索內容，然後直接在批量編輯器中編輯內容，然後將更改保存到原始頁面。

您可以選取多個頁面，以透過各種方法進行大量編輯，包括：

* 瀏覽Sites主 **控台**
* 使用 **Search** 尋找一組頁面

![epp-01](assets/epp-01.png)

選取頁面，然後按一下或點選「屬 **性」選項**，就會顯示大量屬性：

![epp-02](assets/epp-02.png)

您只能大量編輯下列頁面：

* 共用相同的資源類型
* 不屬於livecopy

   * 如果任何頁面位於即時副本中，則開啟屬性時會顯示訊息。

輸入「批量編輯」後，您可以：

* **檢視**

   在檢視多個頁面的頁面屬性時，您可以看到：

   * 受影響頁面的清單

      * 您可以視需要選取／取消選取
   * 索引標籤

      * 如同檢視單一頁面的屬性，屬性會排在標籤下。
   * 屬性子集

      * 所有選定頁面上都可用且已明確定義為可用於批量編輯的屬性都可見。
      * 如果您將頁面選擇範圍縮小為一個頁面，則所有屬性都會顯示。
   * 具有公用值的公用屬性

      * 只有具有公用值的屬性才會顯示在「視圖」模式中。
      * 當欄位為多值（例如「標籤」）時，只有所有值都是共 *用* ，才會顯示值。 如果只有某些是常見的，則只有在編輯時才會顯示。
   當不存在具有公用值的屬性時，將顯示一條消息。

* **編輯**

   編輯多頁的頁面屬性時：

   * 您可以更新可用欄位中的值。

      * 當您選取「完成」時，新值會套用至所有選取 **的頁面**。
      * 當欄位為多值（例如「標籤」）時，您可以附加新值或移除公用值。
   * 在不同頁面上共有但有不同值的欄位，會以特殊值（例如文字）來標示 `<Mixed Entries>`。 編輯此類欄位時應格外小心，以避免資料遺失。


>[!NOTE]
>
>頁面元件可設定為指定可進行大量編輯的欄位。 請參 [閱設定頁面以大量編輯頁面屬性](/help/sites-developing/bulk-editing.md)。
