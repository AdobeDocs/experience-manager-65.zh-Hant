---
title: 編輯頁面屬性
description: 在Adobe Experience Manager中定義頁面的必要屬性。
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
mini-toc-levels: 2
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 3%

---


# 編輯頁面屬性{#editing-page-properties}

您可以定義頁面的必要屬性。 這些值可能會因頁面性質而異。 例如，有些頁面可能已連線至即時副本，有些頁面則未連線，因此即時副本資訊會適時提供。

## 頁面屬性 {#page-properties}

屬性分佈於數個索引標籤中。

### 基本 {#basic}

#### 標題和標籤 {#tile}

* **標題** — 頁面的標題會顯示在不同的位置
   * 例如，**網站**&#x200B;索引標籤清單和&#x200B;**網站**&#x200B;卡片/清單檢視。
   * 這是必要欄位。
* **標籤** — 您可以在此處更新選取方塊中的清單，以新增或移除頁面上的標籤。
   * 選取標籤後，標籤會列在選取方塊下方。 您可以使用x從此清單中移除標籤。
   * 在空白選取方塊中輸入名稱即可輸入新標籤。
      * 新標籤會在您點選Enter時建立。
      * 新標籤會在右側顯示一個小星號，表示它是新標籤。
   * 使用下拉式清單，您可以從現有標籤中選取。
   * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x，可用來為此頁面移除該標籤。
   * 如需關於標籤的詳細資訊，請參閱[使用標籤。](/help/sites-authoring/tags.md)
* **在導覽中隱藏** — 指示在產生的網站頁面導覽中是顯示還是隱藏頁面

#### 品牌元素 {#branding}

藉由將品牌概要附加至每個頁面標題，跨頁面套用一致的品牌識別。 此功能需要使用2.14.0版或更新版本的[核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)的頁面元件

* **覆寫** — 檢查以在此頁面上定義品牌概要。
   * 此值由任何子頁面繼承，除非它們也設定了&#x200B;**覆寫**&#x200B;值。
* **覆寫值** — 要附加至頁面標題的品牌概要文字
   * 值會附加至頁面標題後的垂直號字元，例如`Cycling Tuscany | Always ready for the WKND`

#### 更多標題和說明 {#more}

* **頁面標題** — 要在頁面上使用的標題
   * 通常由標題元件使用
   * 如果空白，則使用&#x200B;**標題**。
* **導覽標題** — 您可以指定單獨的標題以用於導覽（例如，如果您想要更簡潔的標題）。
   * 如果空白，則使用&#x200B;**標題**。
* **子標題** — 頁面上使用的子標題
* **描述** — 頁面的描述、用途或您要新增的任何其他詳細資訊

#### 開啟/關閉時間 {#on-time}

頁面的開啟/關閉時間是一種暫時隱藏已發佈內容的便利方式。 內容在關閉時仍會留在發佈執行個體上。 關閉頁面不會取消發佈內容。

* **開啟時間** — 已發佈頁面在發佈環境中可見（轉譯）的日期和時間。 頁面必須以手動方式或預先設定的自動復寫方式發佈。

   * 如果已經[發佈，](/help/sites-authoring/publishing-pages.md)此頁面可在發佈執行個體上使用，但會保持隱匿（隱藏）狀態，直到在指定時間才呈現。
   * 如果未發佈且[已設定為自動復寫，](/help/sites-deploying/replication.md)則會自動發佈頁面，然後在指定的時間轉譯。
   * 如果未發佈且未設定為自動復寫，則不會自動發佈頁面，因此嘗試存取該頁面時會顯示404。

* **關閉時間** — 類似於&#x200B;**開啟時間**，且經常與其搭配使用，這會定義發佈頁面在發佈環境中隱藏的時間。

對於您要發佈的頁面，請將這些欄位（**開啟時間**&#x200B;和&#x200B;**關閉時間**）留空，這些欄位可立即使用並在發佈環境中使用，直到它們停用（一般案例）為止。

>[!NOTE]
>如果&#x200B;**開啟時間**&#x200B;或&#x200B;**關閉時間**&#x200B;是過去的時間，且已設定自動復寫，則會立即觸發相關動作。

>[!TIP]
>
>開啟/關閉時間需嚴格處理已發佈的內容（手動或透過自動復寫）。 因此，不會觸發發佈工作流程（例如核准內容的工作流程），開啟/關閉時間也不會影響頁面的發佈狀態。 因此，開啟/關閉時間最適合暫時顯示/隱藏已核准和發佈的內容。
>
>如果您想要發佈包含所有關聯工作流程的新內容，或從您的網站中完全移除（取消發佈內容），請考慮[管理您的出版物。](/help/sites-authoring/publishing-pages.md#manage-publication)

#### 虛名 URL {#vanity-url}

輸入此頁面的虛名URL，此URL可讓您使用較短和/或較具表現力的URL。

例如，如果網站`welcome`的虛名URL設定為`/v1.0/startpage`至由路徑`http://example.com,`識別的頁面，則`http://example.com/welcome`將是`http://example.com/content/v1.0/startpage`的虛名URL

>[!CAUTION]
>
>虛名URL：
>
>* 必須是唯一的。
>* 不支援規則運算式模式。
>* 不應設為現有頁面。

設定Dispatcher以啟用對虛名URL的存取權。 如需詳細資訊，請參閱[啟用對虛名URL的存取權](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#enabling-access-to-vanity-urls-vanity-urls)。

* **新增** — 點選或按一下以新增虛名URL。
* **移除** — 點選或按一下以移除虛名URL。
  **重新導向虛名URL** — 指出您是要讓頁面使用虛名URL，還是重新導向至頁面的實際URL

### 進階 {#advanced}

#### 設定 {#settings}

* **語言** — 頁面語言
* **語言根** — 如果頁面是語言副本的根，則必須檢查
* **重新導向** — 指出此頁面應該自動重新導向的頁面
* **設計** — 指出要用於此頁面的[設計](/help/sites-developing/designer.md)。
* **別名** — 指定要用於此頁面的別名
   * 例如，如果您為頁面`private`定義別名`/content/wknd/us/en/magazine/members-only`，則也可以透過`/content/wknd/us/en/magazine/private`存取此頁面
   * 建立別名會設定頁面節點上的`sling:alias`屬性，這只會影響資源，而不會影響存放庫路徑。
   * 無法發佈編輯器中以別名存取的頁面。 編輯器中的[發佈選項](/help/sites-authoring/publishing-pages.md)僅適用於透過實際路徑存取的頁面。
   * 如需詳細資訊，請參閱SEO和URL管理最佳實務下的[本地化頁面名稱](/help/managing/seo-and-url-management.md#localized-page-names)。

#### 設定 {#configuration}

* **繼承自&lt;*路徑*>** — 啟用/停用頁面&#x200B;**雲端設定**&#x200B;的繼承
* **雲端設定** — 設定的路徑

#### 範本設定 {#templates}

* **允許的範本** - [定義此子分支內可用的範本清單](/help/sites-authoring/templates.md#allowingatemplate)

#### 驗證需求 {#authentication}

* **啟用** — 啟用（或停用）驗證，以便您可以存取頁面
* **登入頁面** — 要用於登入的頁面

>[!NOTE]
>
>已關閉的使用者群組定義於&#x200B;**[許可權](/help/sites-authoring/editing-page-properties.md#permissions)**&#x200B;索引標籤上。

>[!CAUTION]
>
>**[許可權](#permissions)**&#x200B;索引標籤允許根據`granite:AuthenticationRequired` mixin的存在來編輯CUG設定。 如果使用過時的CUG設定來設定頁面許可權，則根據`cq:cugEnabled`屬性的存在，**驗證需求**&#x200B;下會顯示警告訊息，且選項無法編輯，也無法編輯[許可權](/help/sites-authoring/editing-page-properties.md#permissions)。
>
>
>在這種情況下，必須在[傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)中編輯CUG許可權。

#### 匯出 {#export}

* **組態** — 指定匯出組態

#### SEO {#seo}

* **標準URL** — 用於覆寫頁面的標準URL
   * 如果保留為空白，頁面的URL將是其標準URL。
* **Robots標籤** — 使用下拉式清單來選取Robots標籤，以控制搜尋引擎編目程式的行為
   * 有些選項會相互衝突，以較寬鬆的選項優先。
* **產生Sitemap** — 選取時，會為此頁面及其子系產生`sitemap.xml`。

### 影像 {#images}

#### 精選影像 {#featured-image}

此區段用於選取和設定要精選的影像。 這用於參考頁面的元件中；例如，Teaser、頁面清單等。

* **影像** — 您可以&#x200B;**挑選**&#x200B;資產，或瀏覽要上傳的檔案，然後&#x200B;**編輯**&#x200B;或&#x200B;**清除**&#x200B;選取的影像。
* **替代文字** — 用來代表影像含義及/或功能的文字，通常由熒幕朗讀程式使用
* **繼承 — 取自DAM資產的值** — 選取後，替代文字會填入DAM中`dc:description`中繼資料的值。

#### 縮圖 {#thumbnail}

此區段用於選取和設定頁面的影像縮圖。 這用於參考頁面的元件中；例如，Teaser、頁面清單等。

* **產生預覽** — 產生您要做為縮圖使用的頁面預覽
* **上傳影像** — 上傳您要做為縮圖的影像
* **選取影像** — 選取要當作縮圖的現有資產
* **回覆** — 在您變更縮圖後，此選項即可使用。 如果您不想保留變更，則可以在儲存前還原該變更。

### 雲端服務 {#cloud-services}

* **Cloud Service設定** — 定義用於頁面的雲端服務設定
* **繼承自** — 對於即時副本和語言副本，預設會從Blueprint繼承雲端設定。
   * 取消勾選以覆寫繼承

### 個人化 {#personalization}

#### ContextHub 組態 {#contexthub}

* **繼承自** — 預設會從父頁面繼承ContextHub設定。
   * 取消勾選以覆寫繼承。
* **ContextHub路徑** — 選取[ContextHub設定](/help/sites-developing/ch-configuring.md)
* **區段路徑** — 選取[區段路徑](/help/sites-administering/segmentation.md)。

#### 定位組態 {#targeting}

選取[品牌以指定目標定位的範圍。](/help/sites-authoring/target-adobe-campaign.md)

>[!NOTE]
>此選項要求使用者帳戶必須屬於`Target Adminstrators`群組。

### 權限 {#permissions}

使用&#x200B;**許可權**&#x200B;索引標籤來定義哪些使用者、群組或[已關閉的使用者群組(CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=zh-Hant)可以存取和/或修改頁面。

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

此索引標籤僅對做為Blueprint的頁面可見。 藍圖是即時副本的基礎，也是[多網站管理的一部分。](/help/sites-administering/msm.md)

* **轉出** — 啟動Blueprint內容轉出到即時副本
* **即時副本概觀** — 開啟視窗以瀏覽即時副本頁面結構
* **目前的即時副本** — 以所選Blueprint頁面為基礎（即即時副本）的頁面清單
* **轉出設定** — 定義頁面的轉出設定

### Live Copy {#live-copy}

此標籤僅對設定為即時副本的頁面可見。 和[藍圖一樣，](#blueprint)即時副本是[多網站管理的一部分。](/help/sites-administering/msm.md)

* **同步** — 同步即時副本與藍圖，並保留本機修改
* **重設** — 將即時副本重設為Blueprint的狀態，並移除本機修改
* **暫停** — 暫停即時副本，以防止進一步的轉出修改
* **分離** — 從Blueprint分離即時副本

#### 來源 {#source}

* 顯示此即時副本的Blueprint路徑

#### 狀態 {#status}

* 列出頁面的目前即時副本狀態

#### 設定 {#live-copy-config}

* **即時副本繼承** — 如果勾選，即時副本設定將在所有子項上都有效。
* **從父項繼承轉出設定** — 如果勾選，則從頁面的父項繼承轉出設定。
* **選擇轉出設定** — 定義從Blueprint傳播修改的情況，且僅當未選取&#x200B;**從父項繼承轉出設定**&#x200B;時可用
* **排除的路徑清單**

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

   * 索引標籤

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
