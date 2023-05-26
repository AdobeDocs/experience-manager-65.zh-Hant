---
title: 編輯內容頁面屬性
description: 定義頁面的必要屬性。
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 8%

---

# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些值會因頁面性質而異。 例如，某些頁面可能已連線至即時副本，而其他頁面並未連線，即時副本資訊將可酌情使用。

## 頁面內容 {#page-properties}

屬性分佈於數個標籤中。

### 基本 {#basic}

* **標題**

   頁面的標題會顯示在各種位置。 例如， **網站** 索引標籤清單和 **網站** 卡片/清單檢視。

   這是必要欄位。

* **標記**

   您可以在此處更新選取方塊中的清單，從頁面新增或移除標籤：

   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 在空白的選取方塊中輸入名稱，即可輸入全新的標籤。

      * 當您按Enter鍵時，將建立新標籤。
      * 然後，新標籤將顯示並在右側有一個小星號，表示它是新標籤。
   * 使用下拉式清單功能，您可以從現有標籤中選取。
   * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x，可用來移除此頁面的該標籤。

   如需標籤的詳細資訊，請參閱 [使用標籤](/help/sites-authoring/tags.md).

* **於導覽中隱藏**

   指示在產生網站的頁面導覽中是顯示還是隱藏頁面。

* **品牌化**

   藉由將品牌概要附加至每個頁面標題，跨頁面套用一致的品牌識別。 若要使用此功能，需使用2.14.0版或更新版本的頁面元件， [核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)

   * **覆寫**  — 勾選以在此頁面上定義品牌概要。
      * 值將由任何子頁面繼承，除非它們也有其 **覆寫** 值已設定。
   * **覆寫值**  — 要附加至頁面標題的品牌概要的文字。
      * 值會附加至頁面標題後的垂直號字元，例如「騎行Tuscany」 |隨時準備使用WKND」
* **頁面標題**

   頁面上使用的標題。 通常由標題元件使用。 如果清空， **標題** 將會使用。

* **導覽標題**

   您可以指定個別標題以在導覽中使用（例如，如果您想要更簡潔的內容）。 如果為空， **標題** 將會使用。

* **子標題**

   頁面上使用的副標題。

* **說明**

   頁面的說明、用途或您要新增的任何其他詳細資訊。

* **開啟時間**

   啟動已發佈頁面的日期和時間。 發佈後，此頁面將保持休眠狀態，直到指定的時間。

   對於您要立即發佈的頁面（一般情境），請將這些欄位留空。

* **關閉時間**

   已發佈頁面將停用的時間。

   同樣地，請將這些欄位留空以便立即採取行動。

* **虛名 URL**

   可讓您輸入此頁面的虛名URL，這可以讓您有較短和/或較具表現力的URL。

   例如，如果虛名URL設為 `welcome`至路徑所識別的頁面 `/v1.0/startpage`適用於網站 `http://example.com,` 則 `http://example.com/welcome`會是虛名URL `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援規則運算式模式。
   >* 不應設定為現有頁面。


   您也需要設定Dispatcher以啟用對虛名URL的存取權。 另請參閱 [啟用對虛名URL的存取權](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) 以取得更多詳細資料。

* **重新導向虛名 URL**

   指示您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **語言**

   頁面語言。

* **語言根目錄**

   如果頁面是語言副本的根目錄，則必須核取。

* **重新導向**

   指出此頁面應該自動重新導向的頁面。

* **Design**

   指出 [設計](/help/sites-developing/designer.md) 用於此頁面。

* **別名**

   指定要用於此頁面的別名。

   * 例如，如果您定義別名 `private` 用於頁面 `/content/wknd/us/en/magazine/members-only`，則也可以透過存取此頁面 `/content/wknd/us/en/magazine/private`
   * 建立別名會設定 `sling:alias` 屬性，只會影響資源，而不會影響存放庫路徑。
   * 無法發佈編輯器中以別名存取的頁面。 [發佈選項](/help/sites-authoring/publishing-pages.md) 編輯器中的僅供透過實際路徑存取的頁面使用。
   * 如需詳細資訊，請參閱 [根據SEO和URL管理最佳實務將頁面名稱本地化](/help/managing/seo-and-url-management.md#localized-page-names).

* **繼承自&lt;*路徑*>**

   指示頁面是否繼承。 以及從何處取得。

* **雲端設定**

   設定的路徑。

* **允許的範本**

   [定義可用的範本清單](/help/sites-authoring/templates.md#allowingatemplate) 在此支行內。

* **啟用** （驗證需求）

   啟用（或停用）使用驗證來存取頁面。

   >[!NOTE]
   >
   >已關閉的使用者群組定義於 **[許可權](/help/sites-authoring/editing-page-properties.md#permissions)** 標籤。

   >[!CAUTION]
   >
   >此 **[許可權](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** 索引標籤可讓您根據以下專案是否存在，編輯CUG設定： `granite:AuthenticationRequired` mixin. 如果頁面許可權是透過已棄用的CUG設定進行設定，需依據是否存在 `cq:cugEnabled` 屬性，底下將顯示警告訊息 **驗證需求** 且選項將不可編輯，也不會編輯 [許可權](/help/sites-authoring/editing-page-properties.md#permissions) 可編輯。
   >
   >
   >在這種情況下，必須在以下位置編輯CUG許可權： [傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **登入頁面**

   用於登入的頁面。

* **匯出設定**

   指定匯出設定。

### 縮圖 {#thumbnail}

顯示頁面縮圖影像。 您可以：

* **產生預覽**

   產生頁面預覽，以做為縮圖使用。

* **上傳影像**

   上傳要當作縮圖的影像。

* **選取影像**

   選取現有資產以用作縮圖。

* **回復**

   在您變更縮圖後，此選項就會變為可用。 如果您不想保留變更，可以在儲存前還原該變更。

### 社交媒體 {#social-media}

* **社交媒體分享**

   定義頁面上可用的共用選項。 顯示以下專案可用的選項： [共用核心元件](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **啟用Facebook的使用者共用**
   * **啟用Pinterest的使用者共用**
   * **偏好的XF變數**
定義用於產生頁面中繼資料的體驗片段變數

### 雲端服務 {#cloud-services}

* **雲端服務**

   定義屬性 [雲端服務](/help/sites-developing/extending-cloud-config.md).

### 個人化 {#personalization}

* **ContextHub 組態**

   選取 [ContextHub設定](/help/sites-developing/ch-configuring.md) 和 [區段路徑](/help/sites-administering/segmentation.md).

* **定位組態**

   選取 [品牌以指定目標定位的範圍](/help/sites-authoring/target-adobe-campaign.md).

   >[!NOTE]
   >此選項要求使用者帳戶位於 `Target Adminstrators`群組。

### 權限 {#permissions}

* **權限**

   在此索引標籤中，您可以：

   * [新增權限](/help/sites-administering/user-group-ac-admin.md)
   * [編輯已關閉的使用者群組](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * 檢視 [有效許可權](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >此 **許可權** 索引標籤可讓您根據以下專案是否存在，編輯CUG設定： `granite:AuthenticationRequired` mixin. 如果頁面許可權是透過已棄用的CUG設定進行設定，需依據是否存在 `cq:cugEnabled` 屬性，則會顯示警告訊息，且CUG許可權將不可編輯，驗證需求也不會顯示於 [進階](/help/sites-authoring/editing-page-properties.md#advanced) 標籤可編輯。
   >
   >
   >在這種情況下，必須在以下位置編輯CUG許可權： [傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >「許可權」索引標籤不允許建立空的CUG群組，這是拒絕存取每個使用者的簡單方式，會很實用。 若要這麼做，必須使用CRX Explorer。 檢視檔案 [使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md) 以取得詳細資訊。

### 藍圖 {#blueprint}

* **藍圖**

   在中定義Blueprint頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制將修改傳播至即時副本的情況。

### Live Copy {#live-copy}

* **即時副本**

   在中定義即時副本頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制從Blueprint傳播修改的情況。

### 網站結構 {#site-structure}

* 提供提供全網站功能頁面的連結，例如 **註冊頁面**， **離線頁面**，等等。

## 編輯頁面屬性 {#editing-page-properties-1}

您可以定義頁面屬性：

* 從 **網站** 主控台：

   * [建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page) （屬性的子集）

   * 按一下或點選 **屬性**

      * 若為單一頁面
      * 針對多個頁面（只有屬性的子集可用於整體編輯）

* 從頁面編輯器：

   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從Sites Console — 單一頁面 {#from-the-sites-console-single-page}

按一下或點選 **屬性** 若要定義頁面屬性：

1. 使用 **網站** 控制檯中，導覽至您要檢視和編輯屬性的頁面位置。

1. 選取 **屬性** 選項供需要的頁面使用，請使用：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#selectionmode)

   將會使用適當的索引標籤來顯示頁面屬性。

1. 視需要檢視或編輯屬性。

1. 然後使用 **儲存** 儲存您的更新，然後按 **關閉** 以返回主控台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用 **頁面資訊** 若要定義頁面屬性：

1. 開啟您要編輯屬性的頁面。

1. 選取 **頁面資訊** 圖示以開啟選取範圍功能表：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 選取 **開啟屬性** 而且會開啟對話方塊，讓您編輯屬性（依適當的索引標籤排序）。 工具列右側也提供下列按鈕：

   * **取消**
   * **儲存並關閉**

1. 使用 **儲存並關閉** 按鈕以儲存變更。

### 從Sites Console — 多個頁面 {#from-the-sites-console-multiple-pages}

從Sites **** Console中，您可以選取數個頁面，然後使用 **View Properties**  (檢視屬性) 來檢視和/或編輯頁面屬性。這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>您也可以對資產大量編輯屬性。 兩者非常類似，但有些地方有所不同。 另請參閱 [編輯多個資產的屬性](/help/assets/metadata.md) 以取得詳細資訊。
>
>此外， [大量編輯器](/help/sites-administering/bulk-editor.md)，可讓您使用GQL (Google查詢語言)從多個頁面搜尋內容，然後直接在大量編輯器中編輯內容，再將變更儲存至原始頁面。

您可以選取多個頁面，以透過各種方法進行大量編輯，包括：

* 瀏覽 **網站** 主控台
* 使用後 **搜尋** 尋找一組頁面

![epp-01](assets/epp-01.png)

選取頁面，然後按一下或點選「屬 **性」選項**，就會顯示大量屬性：

![epp-02](assets/epp-02.png)

您只能大量編輯符合以下條件的頁面：

* 共用相同的資源型別
* 不是Livecopy的一部分

   * 如果有任何頁面在即時副本中，則會在屬性開啟時顯示訊息。

進入「大量編輯」後，您可以：

* **檢視**

   檢視多個頁面的頁面屬性時，您可以看到：

   * 受影響的頁面清單

      * 您可以視需要選取/取消選取
   * 索引標籤

      * 和檢視單一頁面屬性時一樣，屬性會依索引標籤排序。
   * 屬性的子集

      * 會顯示所有選定頁面上可用的屬性，這些屬性已明確定義為可大量編輯。
      * 如果您將頁面選取範圍縮小至一頁，則會顯示所有屬性。
   * 具有共同值的共同屬性

      * 在「檢視」模式中只會顯示具有通用值的屬性。
      * 當欄位有多個值時（例如「標籤」），只有在 *全部* 很常見。 如果只有部分為通用，則僅在編輯時顯示。

   當不存在具有相同值的屬性時，會顯示訊息。

* **編輯**

   編輯多個頁面的頁面屬性時：

   * 您可以更新可用欄位中的值。

      * 當您選取時，新值將會套用至所有選取的頁面 **完成**.
      * 當欄位有多個值時（例如「標籤」），您可以附加新值或移除通用值。
   * 如果欄位很常見，但不同頁面中的值不同，則會以特殊值（例如文字）標示 `<Mixed Entries>`.


>[!NOTE]
>
>頁面元件可設定為指定可供大量編輯的欄位。 另請參閱 [設定頁面以大量編輯頁面屬性](/help/sites-developing/bulk-editing.md).
