---
title: 編輯內容頁面屬性
description: 定義頁面的必需屬性。
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

您可以定義頁面的必需屬性。 這些內容可能因頁面的性質而異。 例如，某些頁面可能已連接到即時拷貝，而其他頁面則未連接，並且即時拷貝資訊將根據需要可用。

## 頁面內容 {#page-properties}

屬性分佈在多個頁籤上。

### 基本 {#basic}

* **標題**

   頁面標題顯示在不同的位置。 例如， **網站** 清單和 **站點** 卡/清單視圖。

   這是必要欄位。

* **標記**

   在此，您可以通過更新選擇框中的清單來添加標籤，或從頁面中刪除標籤：

   * 選擇標籤後，它將列在選擇框下。 可以使用x從此清單中刪除標籤。
   * 可以通過在空選擇框中鍵入名稱來輸入完全新的標籤。

      * 當您按Enter時，將建立新標籤。
      * 然後，新標籤將在右側顯示，右側有一個小星號，表示它是新標籤。
   * 使用下拉功能，您可以從現有標籤中進行選擇。
   * 將滑鼠移到選擇框中的標籤條目上時，將顯示x，該標籤可用於刪除此頁的標籤。

   有關標籤的詳細資訊，請參見 [使用標籤](/help/sites-authoring/tags.md)。

* **於導覽中隱藏**

   指示在生成站點的頁面導航中是否顯示或隱藏頁面。

* **品牌化**

   通過在每個頁面標題上附加一個品牌輔助資訊，跨頁面應用一致的品牌標識。 此功能需要使用2.14.0版或更高版本的頁面元件 [核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)

   * **覆蓋**  — 選中以定義此頁上的品牌輔助資訊。
      * 值將由任何子頁繼承，除非它們還有 **覆蓋** 值集。
   * **覆蓋值**  — 要附加到頁面標題的品牌輔助資訊的文本。
      * 該值將附加在管道字元（如「循環托斯卡納」）之後的頁標題中 |始終為WKND做好準備&quot;
* **頁面標題**

   要在頁面上使用的標題。 通常由標題元件使用。 如果空 **標題** 的下界。

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

   再次將這些欄位留空以立即執行操作。

* **虛名 URL**

   允許您為此頁面輸入虛榮URL，這可以使您具有更短和/或更豐富的URL。

   例如，如果Vanity URL設定為 `welcome`到路徑標識的頁面 `/v1.0/startpage`的 `http://example.com,` 然後 `http://example.com/welcome`將是 `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虛名 URL:
   >
   >* 必須唯一，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援regex模式。
   >* 不應設定為現有頁。


   您還需要配置Dispatcher以啟用對虛擬URL的訪問。 請參閱 [啟用對虛榮URL的訪問](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) 的子菜單。

* **重新導向虛名 URL**

   指示是否希望頁面使用虛榮URL。

### 進階 {#advanced}

* **語言**

   頁面語言。

* **語言根目錄**

   如果頁面是語言副本的根，則必須選中。

* **重新導向**

   指示此頁面應自動重定向到的頁面。

* **Design**

   指示 [設計](/help/sites-developing/designer.md) 用於此頁。

* **別名**

   指定要與此頁一起使用的別名。

   * 例如，如果定義的別名 `private` 頁 `/content/wknd/us/en/magazine/members-only`，此頁也可通過 `/content/wknd/us/en/magazine/private`
   * 建立別名集 `sling:alias` 頁節點上的屬性，它只影響資源，而不影響儲存庫路徑。
   * 無法發佈編輯器中別名訪問的頁面。 [發佈選項](/help/sites-authoring/publishing-pages.md) 編輯器中的頁面僅可用於通過實際路徑訪問的頁面。
   * 有關詳細資訊，請參閱 [SEO和URL管理最佳實踐下的本地化頁名](/help/managing/seo-and-url-management.md#localized-page-names)。

* **繼承自&lt;*路徑*>**

   指示是否繼承該頁。 以及從哪裡來。

* **雲端設定**

   配置的路徑。

* **允許的範本**

   [定義可用模板清單](/help/sites-authoring/templates.md#allowingatemplate) 在這支支行內。

* **啟用** （身份驗證要求）

   啟用（或禁用）身份驗證以訪問該頁。

   >[!NOTE]
   >
   >在 **[權限](/help/sites-authoring/editing-page-properties.md#permissions)** 頁籤。

   >[!CAUTION]
   >
   >的 **[權限](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** 頁籤允許根據 `granite:AuthenticationRequired` 混音。 如果使用不建議使用的CUG配置配置頁面權限，則根據 `cq:cugEnabled` 屬性，警告消息將顯示在 **身份驗證要求** 不可編輯， [權限](/help/sites-authoring/editing-page-properties.md#permissions) 可編輯。
   >
   >
   >在這種情況下，必須在 [經典UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)。

* **登入頁面**

   用於登錄的頁面。

* **匯出設定**

   指定導出配置。

### 縮圖 {#thumbnail}

顯示頁面縮略圖。 您可以：

* **產生預覽**

   生成要用作縮略圖的頁面預覽。

* **上傳影像**

   上載影像以用作縮略圖。

* **選取影像**

   選擇要用作縮略圖的現有資產。

* **回復**

   在對縮覽圖進行更改後，此選項將可用。 如果您不想保留更改，則可以在保存之前還原該更改。

### 社交媒體 {#social-media}

* **社交媒體分享**

   定義頁面上可用的共用選項。 顯示可供 [共用核心元件](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html)。

   * **為Facebook啟用用戶共用**
   * **為Pinterest啟用用戶共用**
   * **首選XF變體**
定義用於為頁生成元資料的經驗片段變體

### 雲端服務 {#cloud-services}

* **雲端服務**

   定義屬性 [雲服務](/help/sites-developing/extending-cloud-config.md)。

### 個人化 {#personalization}

* **ContextHub 組態**

   選擇 [ContextHub配置](/help/sites-developing/ch-configuring.md) 和 [段路徑](/help/sites-administering/segmentation.md)。

* **定位組態**

   選擇 [要指定目標範圍的品牌](/help/sites-authoring/target-adobe-campaign.md)。

   >[!NOTE]
   >此選項要求用戶帳戶位於 `Target Adminstrators`組。

### 權限 {#permissions}

* **權限**

   在此頁籤中，您可以：

   * [新增權限](/help/sites-administering/user-group-ac-admin.md)
   * [編輯已關閉的使用者群組](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * 查看 [有效權限](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >的 **權限** 頁籤允許根據 `granite:AuthenticationRequired` 混音。 如果使用不建議使用的CUG配置配置頁面權限，則根據 `cq:cugEnabled` 屬性，將顯示一條警告消息，且CUG權限將不可編輯，並且上的「驗證要求」也不可編輯 [高級](/help/sites-authoring/editing-page-properties.md#advanced) 頁籤。
   >
   >
   >在這種情況下，必須在 [經典UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)。

   >[!NOTE]
   >
   >「權限」頁籤不允許建立空的CUG組，這可作為拒絕每個用戶訪問的簡單方法非常有用。 要執行此CRX瀏覽器，必須使用。 查看文檔 [用戶、組和訪問權限管理](/help/sites-administering/user-group-ac-admin.md) 的子菜單。

### 藍圖 {#blueprint}

* **藍圖**

   定義「藍圖」頁的屬性 [多站點管理](/help/sites-administering/msm.md)。 控制將修改傳播到即時副本的情況。

### Live Copy {#live-copy}

* **即時副本**

   在中定義Live Copy頁的屬性 [多站點管理](/help/sites-administering/msm.md)。 控制從藍圖傳播修改的環境。

### 網站結構 {#site-structure}

* 提供指向提供站點範圍功能的頁面的連結，如 **註冊頁**。 **離線頁**&#x200B;其中包括：

## 編輯頁面屬性 {#editing-page-properties-1}

可以定義頁面屬性：

* 從 **站點** 控制台：

   * [建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page) （屬性的子集）

   * 按一下或輕擊 **屬性**

      * 單頁
      * 對於多頁（僅屬性的子集可用於成批編輯）

* 從頁面編輯器：

   * 使用 **頁面資訊** (接著 **開啟屬性**)

### 從站點控制台 — 單頁 {#from-the-sites-console-single-page}

按一下或輕擊 **屬性** 要定義頁面屬性，請執行以下操作：

1. 使用 **站點** 控制台，導航到要查看和編輯其屬性的頁的位置。

1. 選擇 **屬性** 選項：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#selectionmode)

   頁面屬性將使用相應的頁籤顯示。

1. 根據需要查看或編輯屬性。

1. 然後使用 **保存** 保存更新，然後 **關閉** 返回控制台。

### 編輯頁面時 {#when-editing-a-page}

編輯頁面時，您可以使用 **頁面資訊** 要定義頁面屬性，請執行以下操作：

1. 開啟要編輯其屬性的頁面。

1. 選擇 **頁面資訊** 表徵圖以開啟選擇菜單：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 選擇 **開啟屬性** 將開啟一個對話框，允許您按相應的頁籤排序編輯屬性。 工具列右側也提供下列按鈕：

   * **取消**
   * **儲存並關閉**

1. 使用 **保存並關閉** 按鈕。

### 從站點控制台 — 多頁 {#from-the-sites-console-multiple-pages}

從Sites **** Console中，您可以選取數個頁面，然後使用 **View Properties**  (檢視屬性) 來檢視和/或編輯頁面屬性。這稱為頁面屬性的大量編輯。

>[!NOTE]
>
>對「資產」也可進行屬性的批量編輯。 它非常相似，但有幾點不同。 請參閱 [編輯多個資產的屬性](/help/assets/metadata.md) 的雙曲餘切值。
>
>還有 [批量編輯器](/help/sites-administering/bulk-editor.md)，允許您使用GQL(Google查詢語言)從多個頁面搜索內容，然後直接在批量編輯器中編輯內容，然後再將更改保存到原始頁面。

可以通過各種方法選擇多個頁面進行批量編輯，包括：

* 瀏覽 **站點** 控制台
* 使用後 **搜索** 查找一組頁面

![epp-01](assets/epp-01.png)

選取頁面，然後按一下或點選「屬 **性」選項**，就會顯示大量屬性：

![epp-02](assets/epp-02.png)

您只能批量編輯以下頁面：

* 共用相同的資源類型
* 不是livecopy的一部分

   * 如果其中任何頁面都在即時副本中，則開啟屬性時將顯示一條消息。

輸入「批量編輯」後，您可以：

* **檢視**

   查看多頁的「頁面屬性」時，您可以看到：

   * 受影響的頁面清單

      * 如果需要，可以選擇/取消選擇
   * 索引標籤

      * 與查看單頁的屬性一樣，屬性在頁籤下排序。
   * 屬性子集

      * 所有選定頁面上都可用且已明確定義為可用於批量編輯的屬性是可見的。
      * 如果將頁面選擇縮小為一頁，則所有屬性都可見。
   * 具有公用值的公用屬性

      * 在「視圖」模式下，只顯示具有公用值的屬性。
      * 當欄位為多值（例如「標籤」）時，僅在 *全部* 很常見。 如果只有一些是常見的，則只有在編輯時才顯示。

   如果不存在具有公用值的屬性，則顯示一條消息。

* **編輯**

   編輯多個頁面的頁面屬性時：

   * 您可以更新可用欄位中的值。

      * 當您選擇時，新值將應用於所有選定的頁面 **完成**。
      * 當欄位為多值（例如「標籤」）時，可以追加新值或刪除公用值。
   * 通用但各頁具有不同值的欄位將用特殊值（如文本）來表示 `<Mixed Entries>`。


>[!NOTE]
>
>可以將頁面元件配置為指定可用於批量編輯的欄位。 請參閱 [配置頁面以批量編輯頁面屬性](/help/sites-developing/bulk-editing.md)。
