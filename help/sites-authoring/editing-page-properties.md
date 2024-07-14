---
title: 編輯內容頁面屬性
description: 在Adobe Experience Manager中定義頁面的必要屬性。
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 3%

---

# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些值可能會因頁面性質而異。 例如，有些頁面可能已連線至即時副本，有些頁面則未連線，因此即時副本資訊會適時提供。

## 頁面屬性 {#page-properties}

屬性分佈於數個索引標籤中。

### 基本 {#basic}

* **標題**

  頁面的標題會顯示在各種位置。 例如，**網站**&#x200B;索引標籤清單和&#x200B;**網站**&#x200B;卡片/清單檢視。

  這是必要欄位。

* **標籤**

  您可以在此處更新選取方塊中的清單，在頁面中新增或移除標籤：

   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 在空白選取方塊中輸入名稱即可輸入新標籤。

      * 新標籤會在您點選Enter時建立。
      * 新標籤會在右側顯示一個小星號，表示它是新標籤。

   * 使用下拉式清單功能，您可以從現有標籤中選取。
   * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x，可用來為此頁面移除該標籤。

  如需關於標籤的詳細資訊，請參閱[使用標籤](/help/sites-authoring/tags.md)。

* 在導覽中隱藏&#x200B;****

  指示在產生的網站頁面導覽中是顯示還是隱藏頁面。

* **品牌**

  藉由將品牌概要附加至每個頁面標題，跨頁面套用一致的品牌識別。 此功能需要使用2.14.0版或更新版本的[核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)的頁面元件

   * **覆寫** — 檢查以在此頁面上定義品牌概要。
      * 此值由任何子頁面繼承，除非它們也設定了&#x200B;**覆寫**&#x200B;值。
   * **覆寫值** — 要附加至頁面標題的品牌概要文字。
      * 此值會附加至頁面標題後的垂直號字元，例如「騎行Tuscany」 | 隨時準備使用WKND」
* **頁面標題**

  要在頁面上使用的標題。 通常由標題元件使用。 如果空白，則使用&#x200B;**標題**。

* **導覽標題**

  您可以指定單獨的標題以用於導覽（例如，如果您想要更精簡的內容）。 如果空白，則使用&#x200B;**標題**。

* **子標題**

  用於頁面上的子標題。

* **說明**

  頁面的說明、用途或您要新增的任何其他詳細資訊。

* **開啟時間**

  啟動已發佈頁面的日期和時間。 發佈後，此頁面在指定時間之前會一直處於休眠狀態。

  對於您要立即發佈的頁面（一般案例），請將這些欄位保留空白。

* **關閉時間**

  已發佈頁面停用的時間。

  再次將這些欄位留空以便立即採取行動。

* **虛名URL**

  輸入此頁面的虛名URL，此URL可讓您使用較短和/或較具表現力的URL。

  例如，如果網站`http://example.com,`的虛名URL設定為`welcome`至由路徑`/v1.0/startpage`識別的頁面，則`http://example.com/welcome`將是`http://example.com/content/v1.0/startpage`的虛名URL

  >[!CAUTION]
  >
  >虛名URL：
  >
  >* 必須是唯一的。 確定其他頁面尚未使用值。
  >* 不支援規則運算式模式。
  >* 不應設為現有頁面。
  >

  設定Dispatcher以啟用對虛名URL的存取權。 如需詳細資訊，請參閱[啟用對虛名URL的存取權](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls)。

* **重新導向虛名URL**

  指示您是否希望頁面使用虛名URL。

### 進階 {#advanced}

* **語言**

  頁面語言。

* **語言根**

  如果頁面是語言副本的根目錄，則必須選取。

* **重新導向**

  指出此頁面應該自動重新導向的頁面。

* **Design**

  指示要用於此頁面的[設計](/help/sites-developing/designer.md)。

* **別名**

  指定要用於此頁面的別名。

   * 例如，如果您為頁面`/content/wknd/us/en/magazine/members-only`定義別名`private`，則也可以透過`/content/wknd/us/en/magazine/private`存取此頁面
   * 建立別名會設定頁面節點上的`sling:alias`屬性，這只會影響資源，而不會影響存放庫路徑。
   * 無法發佈編輯器中以別名存取的頁面。 編輯器中的[Publish選項](/help/sites-authoring/publishing-pages.md)僅適用於透過實際路徑存取的頁面。
   * 如需詳細資訊，請參閱SEO和URL管理最佳實務下的[本地化頁面名稱](/help/managing/seo-and-url-management.md#localized-page-names)。

* **繼承自&lt;*路徑*>**

  指示頁面是否繼承。 以及來自何處。

* **雲端設定**

  設定的路徑。

* **允許的範本**

  [定義此子分支內可用的範本清單](/help/sites-authoring/templates.md#allowingatemplate)。

* **啟用** （驗證需求）

  啟用（或停用）驗證，以便您可以存取頁面。

  >[!NOTE]
  >
  >已關閉的使用者群組定義於&#x200B;**[許可權](/help/sites-authoring/editing-page-properties.md#permissions)**&#x200B;索引標籤上。

  >[!CAUTION]
  >
  >**[許可權](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)**&#x200B;索引標籤允許根據`granite:AuthenticationRequired` mixin的存在來編輯CUG設定。 如果使用過時的CUG設定來設定頁面許可權，則根據`cq:cugEnabled`屬性的存在，**驗證需求**&#x200B;下會顯示警告訊息，且選項無法編輯，也無法編輯[許可權](/help/sites-authoring/editing-page-properties.md#permissions)。
  >
  >
  >在這種情況下，必須在[傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)中編輯CUG許可權。

* **登入頁面**

  用於登入的頁面。

* **匯出設定**

  指定匯出設定。

### 縮圖 {#thumbnail}

顯示頁面縮圖影像。 您可以：

* **產生預覽**

  產生您要做為縮圖之頁面的預覽。

* **上傳影像**

  上傳您要做為縮圖的影像。

* **選取影像**

  選取要當做縮圖使用的現有資產。

* **回覆**

  在您變更縮圖後，此選項即變為可用。 如果您不想保留變更，則可以在儲存前還原該變更。

### 社交媒體 {#social-media}

* **社群媒體分享**

  定義頁面上可用的共用選項。 公開[共用核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html)可用的選項。

   * **啟用Facebook的使用者共用**
   * **啟用Pinterest的使用者共用**
   * **偏好的XF變化**
定義用來產生頁面中繼資料的體驗片段變數

### 雲端服務 {#cloud-services}

* **Cloud Service**

  定義[雲端服務](/help/sites-developing/extending-cloud-config.md)的屬性。

### 個人化 {#personalization}

* **ContextHub設定**

  選取[ContextHub設定](/help/sites-developing/ch-configuring.md)和[區段路徑](/help/sites-administering/segmentation.md)。

* **目標定位組態**

  選取[品牌以指定鎖定目標](/help/sites-authoring/target-adobe-campaign.md)的範圍。

  >[!NOTE]
  >此選項要求使用者帳戶必須屬於`Target Adminstrators`群組。

### 權限 {#permissions}

* **許可權**

  在此標籤中，您可以：

   * [新增權限](/help/sites-administering/user-group-ac-admin.md)
   * [編輯已關閉的使用者群組](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * 檢視[有效許可權](/help/sites-administering/user-group-ac-admin.md)

  >[!CAUTION]
  >
  >**許可權**&#x200B;索引標籤允許根據`granite:AuthenticationRequired` mixin的存在來編輯CUG設定。 如果使用過時的CUG設定來設定頁面許可權，根據`cq:cugEnabled`屬性的存在，會顯示警告訊息，且CUG許可權無法編輯，[進階](/help/sites-authoring/editing-page-properties.md#advanced)索引標籤上的驗證需求也無法編輯。
  >
  >
  >在這種情況下，必須在[傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)中編輯CUG許可權。

  >[!NOTE]
  >
  >「許可權」標籤不允許建立空的CUG群組，這是拒絕每個使用者存取的簡單方式，十分實用。 若要這麼做，必須使用CRX Explorer。 如需詳細資訊，請參閱檔案[使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md)。

### 藍圖 {#blueprint}

* **藍圖**

  定義[多網站管理](/help/sites-administering/msm.md)中Blueprint頁面的屬性。 控制將修改傳播至即時副本的情況。

### Live Copy {#live-copy}

* **即時副本**

  在[多網站管理](/help/sites-administering/msm.md)中定義即時副本頁面的屬性。 控制從Blueprint傳播修改的情況。

### 網站結構 {#site-structure}

* 提供提供全網站功能頁面的連結，例如&#x200B;**註冊頁面**、**離線頁面**&#x200B;等。

## 編輯頁面屬性 {#editing-page-properties-1}

您可以定義頁面屬性：

* 從&#x200B;**網站**&#x200B;主控台：

   * [建立頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page) （屬性的子集）

   * 按一下或點選&#x200B;**屬性**

      * 針對單一頁面
      * 針對多個頁面（只有屬性的子集可整體編輯）

* 從頁面編輯器：

   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從Sites Console — 單一頁面 {#from-the-sites-console-single-page}

按一下或點選&#x200B;**屬性**&#x200B;以定義頁面屬性：

1. 使用&#x200B;**網站**&#x200B;主控台，導覽至您要檢視及編輯屬性的頁面位置。

1. 使用以下其中一種方式，為必要頁面選取&#x200B;**屬性**&#x200B;選項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#selectionmode)

   頁面屬性會使用適當的索引標籤顯示。

1. 視需要檢視或編輯屬性。

1. 然後使用&#x200B;**儲存**&#x200B;儲存您的更新，接著使用&#x200B;**關閉**，以便您可以返回主控台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用&#x200B;**頁面資訊**&#x200B;來定義頁面屬性：

1. 開啟您要編輯屬性的頁面。

1. 選取&#x200B;**頁面資訊**&#x200B;圖示以開啟選取功能表：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 選取&#x200B;**開啟屬性**，並開啟一個對話方塊讓您編輯屬性（依適當的索引標籤排序）。 工具列右側也提供下列按鈕：

   * **取消**
   * **儲存並關閉**

1. 使用&#x200B;**儲存並關閉**&#x200B;按鈕來儲存變更。

### 從Sites Console — 多個頁面 {#from-the-sites-console-multiple-pages}

從&#x200B;**網站**&#x200B;主控台，您可以選取數個頁面，然後使用&#x200B;**檢視屬性**&#x200B;來檢視和/或編輯頁面屬性。 這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>您也可以為Assets大量編輯屬性。 兩者相似，但有幾處不同。 如需詳細資訊，請參閱[編輯多個Assets的屬性](/help/assets/metadata.md)。
>
>還有[大量編輯器](/help/sites-administering/bulk-editor.md)。 此編輯器可讓您使用GQL (Google查詢語言)從多個頁面搜尋內容，然後直接使用大量編輯器編輯內容，再將變更儲存到原始頁面。

您可以選取多個頁面以透過各種方法進行大量編輯，包括：

* 瀏覽&#x200B;**網站**&#x200B;主控台時
* 使用&#x200B;**搜尋**&#x200B;尋找一組頁面之後

![epp-01](assets/epp-01.png)

選取頁面，然後按一下或點選「**屬性」選項**，就會顯示大量屬性：

![epp-02](assets/epp-02.png)

您只能大量編輯符合以下條件的頁面：

* 共用相同的資源型別
* 不是Livecopy的一部分

   * 如果有任何頁面位於即時副本中，則會在屬性開啟時顯示訊息。

進入「大量編輯」後，您可以執行下列動作：

* **檢視**

  檢視多個頁面的頁面屬性時，您會看到下列內容：

   * 受影響的頁面清單

      * 您可以選取/取消選取（如有必要）

   * 標籤

      * 和檢視單一頁面屬性時一樣，屬性會依索引標籤排序。

   * 屬性的子集

      * 會顯示所有選定頁面上可用的屬性，這些屬性已明確定義為可大量編輯。
      * 如果您將頁面選取範圍縮小至一頁，則會顯示所有屬性。

   * 具有共同值的共同屬性

      * 在「檢視」模式中只會顯示具有相同值的屬性。
      * 當欄位有多個值時（例如Tags），只有在&#x200B;*所有*&#x200B;為通用時，才會顯示值。 如果只有部分相同，則僅在編輯時顯示。

  如果沒有任何具有相同值的屬性存在，則會顯示訊息。

* **編輯**

  編輯多個頁面的頁面屬性時：

   * 您可以更新可用欄位中的值。

      * 當您選取&#x200B;**完成**&#x200B;時，新值會套用至所有選取的頁面。
      * 當欄位有多個值時（例如「標籤」），您可以附加新值或移除通用值。

   * 不同頁面中通用但值不同的欄位，會以特殊值（例如文字`<Mixed Entries>`）表示。

>[!NOTE]
>
>頁面元件可設定為指定可供大量編輯的欄位。 請參閱[設定頁面以大量編輯頁面屬性](/help/sites-developing/bulk-editing.md)。
