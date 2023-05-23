---
title: 自定義節點類型
seo-title: Custom Node Types
description: 基AEM於Sling，並使用JCR儲存庫，其中包含兩者提供的節點類型，AEM但還提供了一系列自定義節點類型
seo-description: AEM is based on Sling and uses a JCR repository with node types offered by both, but AEM also provides a range of custom node types
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 9%

---

# 自定義節點類型{#custom-node-types}

因AEM為基於Sling並使用JCR儲存庫，因此這兩種類型提供的節點類型都可用於：

* [JCR節點類型](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [吊掛節點類型](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外。 提AEM供一系列自定義節點類型。

## 審計 {#audit}

### cq：審計事件 {#cq-auditevent}

**說明**

定義審計事件節點的節點類型。

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**定義**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## 評論 {#comment}

### cq：注釋 {#cq-comment}

**說明**

定義注釋節點的節點類型。

* `@prop userIdentifier`

**定義**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq：注釋附件 {#cq-commentattachment}

**說明**

定義的節點類型 `commentattachment` 節點

**定義**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq：注釋內容 {#cq-commentcontent}

**說明**

定義注釋內容節點的節點類型

**定義**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq：地理位置 {#cq-geolocation}

**說明**

定義以小數度(DD)表示的地理位置的混合

* `@prop latitude` - latitude使用小數度編碼
* `@prop longitude`  — 使用小數度編碼的雙經度

**定義**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq：跟蹤 {#cq-trackback}

**說明**

定義跟蹤節點的節點類型。

**定義**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## 核心 {#core}

### cq:Page {#cq-page}

**說明**

定義預設CQ頁。

* `@node jcr:content`  — 頁面的主要內容。

**定義**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq：偽頁 {#cq-pseudopage}

**說明**

定義將節點標籤為偽頁的混合類型。 這意味著它們可以適應Page和WCM編輯支援。

**定義**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**說明**

定義頁面內容的預設節點，並使用WCM使用的最小屬性。

* `@prop jcr:title`  — 頁面標題。
* `@prop jcr:description`  — 本頁的說明。
* `@prop cq:template`  — 用於建立頁面的模板的路徑。
* `@prop cq:allowedTemplates`  — 用於確定允許模板的路徑的規則運算式清單。
* `@prop pageTitle`  — 標題通常顯示在 `<title>` 標籤。
* `@prop navTitle`  — 導航中通常使用的標題。
* `@prop hideInNav`  — 指定是否在導航中隱藏頁面。
* `@prop onTime`  — 此頁生效的時間。
* `@prop offTime`  — 此頁無效的時間。
* `@prop cq:lastModified`  — 上次修改頁（或其段落）的日期。
* `@prop cq:lastModifiedBy`  — 上次更改頁面（或其段落）的用戶。
* `@prop jcr:language`  — 頁面內容的語言。

>[!NOTE]
>
>頁面內容使用此類型不是強制的。

**定義**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**說明**

定義CQ模板。

* `@node jcr:content`  — 新頁面的預設內容。
* `@node icon.png`  — 保存特徵表徵圖的檔案。
* `@node thumbnail.png`  — 保存特徵縮略圖的檔案。
* `@node workflows`  — 自動分配工作流配置。 配置將遵循以下結構：
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents`  — 常規表達式模式，用於確定允許作為父模板的模板的路徑。
* `@prop allowedChildren`  — 規則運算式模式，確定允許作為子模板的模板的路徑。
* `@prop ranking`  — 在「建立頁」對話框的模板清單中定位。

**定義**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**說明**

定義CQ元件。

* `@prop jcr:title`  — 元件的標題。
* `@prop jcr:description`  — 元件說明。
* `@node dialog`  — 主對話框。
* `@prop dialogPath`  — 主對話路徑（對話的替代）。
* `@node design_dialog`  — 設計對話框。
* `@prop cq:cellName`  — 設計單元格的名稱。
* `@prop cq:isContainer`  — 指示這是否是容器元件。 這將強制使用子元件的單元格名稱而不是路徑名稱。 例如， `parsys` 是容器元件。 如果未定義此值，則根據是否存在 `cq:childEditConfig`。
* `@prop cq:noDecoration`  — 如果為true，則無裝飾 `div` 在包括此元件時將繪製標籤。
* `@node cq:editConfig`  — 定義編輯欄參數的配置。
* `@node cq:childEditConfig`  — 子元件繼承的編輯配置。
* `@node cq:htmlTag`  — 定義添加到「周圍」的附加標籤屬性 `div` 標籤。
* `@node icon.png` — 保存特徵表徵圖的檔案。
* `@node thumbnail.png`  — 保存特徵縮略圖的檔案。
* `@prop allowedParents`  — 常規表達式模式，用於確定允許作為父元件的元件的路徑。
* `@prop allowedChildren`  — 用於確定允許作為子元件的元件的路徑的規則運算式模式。
* `@node virtual`  — 包含反映用於元件拖放的虛擬元件的子節點。
* `@prop componentGroup`  — 用於元件拖放的元件組名稱。
* `@node cq:infoProviders`  — 包含子節點，每個子節點都具有屬性 `className` 是指 `PageInfoProvider`。

**定義**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq：元件混合 {#cq-componentmixin}

**說明**

將CQ元件定義為混合類型。

**定義**

`[cq:ComponentMixin] > cq:Component mixin`

### cq：編輯配置 {#cq-editconfig}

**說明**

定義「編輯欄」的配置。

* `@prop cq:dialogMode`  — 對話框模式：
   * `floating`  — 用於正常浮動對話
   * `inline`  — 行內編輯
   * `auto`  — 自動檢測（取決於可用空間）
* `@node cq:inplaceEditing`  — 為此元件安裝編輯配置。
* `@prop cq:layout` — 編輯欄的佈局：
   * `editbar`  — 編輯欄
   * `rollover`  — 翻轉框架
   * `auto`  — 自動檢測
* `@node cq:formParameters` — 要添加到對話框窗體的其他參數。
* `@prop cq:actions` — 操作清單（編輯欄按鈕或菜單項）。
* `@node cq:actionConfigs`  — 編輯欄或菜單項的小部件配置。
* `@prop cq:emptyText`  — 如果沒有可視內容，則顯示的文本。
* `@node cq:dropTargets`  — 集合 `{@link cq:DropTargetConfig}` 節點。

**定義**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**說明**

配置元件的一個放置目標。 此節點的名稱將用作拖放的ID。

* `@prop accept`  — 此放置目標接受的MIME類型清單；例如 `["image/*"]`
* `@prop groups`  — 接受源的拖放組清單。
* `@prop propertyName`  — 用於儲存引用的屬性的名稱。

**定義**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**說明**

定義虛擬CQ元件。 當前僅用於新元件拖放嚮導。

* `@prop jcr:title`  — 此元件的標題。
* `@prop jcr:description`  — 此元件的說明。
* `@node cq:editConfig`  — 編輯定義編輯欄參數的配置。
* `@node cq:childEditConfig` — 編輯子元件繼承的配置。
* `@node icon.png`  — 保存特徵表徵圖的檔案。
* `@node thumbnail.png`  — 保存特徵縮略圖的檔案。
* `@prop allowedParents`  — 用於確定允許作為父元件的元件的路徑的規則運算式模式。
* `@prop allowedChildren`  — 用於確定允許作為子元件的元件的路徑的規則運算式模式。
* `@prop componentGroup`  — 元件拖放的元件組名稱。

**定義**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq：編輯監聽器配置 {#cq-editlistenersconfig}

**說明**

定義要在編輯事件上執行的（客戶端）偵聽器。 這些值必須引用有效的客戶端偵聽器函式或包含預定義的快捷方式：

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate`  — 建立元件後激發。
* `@prop afteredit`  — 在編輯（修改）元件後觸發。
* `@prop afterdelete`  — 刪除元件後激發。
* `@prop afterinsert`  — 將元件添加到此容器後激發。
* `@prop afterremove`  — 從此容器中刪除元件後觸發。
* `@prop aftermove`  — 在此容器中移動元件後激發。

**定義**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**說明**

DAM資產的內容。

**定義**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**說明**

DAM資產。

**定義**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam：縮略圖 {#dam-thumbnail}

**說明**

用於表示DAM資產的縮略圖。

**定義**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## 交貨容器清單 {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**說明**

容器清單。

**定義**

* `[cq:containerList]`
   * `mixin`

## 交貨頁 {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**說明**

`cq:attributes` 是ContentBus版本標籤的節點類型。 此節點僅具有一系列屬性；其中三個是預定義的&quot;created&quot;、&quot;csd&quot;和&quot;timestampe&quot;。

* `@prop created (long) mandatory copy`  — 建立版本資訊的時間戳，通常是以前版本的簽入時間或建立頁面的時間。
* `@prop csd (string) mandatory copy` - csd標準屬性，頁節點cq:csd屬性的副本
* `@prop timestamp (long) mandatory copy`  — 上次版本修改的時間戳，通常簽入時間。
* `@prop * (string) copy`  — 附加屬性，與父節點版本控制。

**定義**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4內容頁 {#cq-cq-contentpage}

**說明**

節點類型 `cq:contentPage` 包含ContentBus內容頁的屬性和子節點定義。 僅當將此混合類型添加到類型的節點時 `cq:page`，節點將變成ContentBus內容頁面。

中的項 `cq:Cq4ContentPage` 為：

* `@prop cq:csd`  — 本頁的ContentBusCSD。
* `@node cq:content`  — 頁面內容。 如果頁面節點處於「Existing without content」（現有，無內容）」或「Deleted」（已刪除）狀態，則此子節點不存在。
* `@node cq:attributes`  — 頁屬性清單，以前稱為版本標籤。 此節點對於cq:contentPage類型是必需的。 當頁面為節點時，屬性節點的版本化。

**定義**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## 匯入工具 {#importer}

### cq:PollConfig {#cq-pollconfig}

**說明**

輪詢配置。

* `@prop source (String) mandatory`  — 資料源URI，這是必需的，不能為空
* `@prop target (String)`  — 儲存從資料源檢索到的資料的目標位置。 這是可選的，預設為cq:PollConfig節點。
* `@prop interval (Long)`  — 從資料源輪詢新資料或更新資料的間隔（秒）。 這是可選的，預設為30分鐘（1800秒）。
* [為Adobe Experience Manager建立自定義資料導入程式服務](https://helpx.adobe.com/experience-manager/using/polling.html)

**定義**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**說明**

方便了主節點類型，可輕鬆建立輪詢配置節點。

**定義**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## 位置 {#location}

### cq：地理位置 {#cq-geolocation-1}

**說明**

定義以小數度(DD)表示的地理位置的混合。

* `@prop latitude` - Latitude使用小數度編碼為雙精度。
* `@prop longitude`  — 使用小數度編碼為雙精度的經度。

**定義**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## 邁勒 {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**說明**

MailerService節點類型。 郵件器將具有該混合的節點用作消息定義的根節點。

**定義**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq：即時關係 {#cq-liverelationship}

**說明**

定義LiveRelationship混合。 主源（控制）節點和即時拷貝（控制）節點可以通過LiveRelationship虛擬地連結。

**定義**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**說明**

定義LiveSync混合。 如果某個節點與主源（控制）節點和活動副本（控制）節點一起參與LiveRelationship，則該節點被標籤為LiveSync。

* `@prop cq:master` - LiveRelationship的主源（控制）的路徑。
* `@prop cq:isDeep`  — 定義子項是否可用關係。
* `@prop cq:syncTrigger`  — 定義觸發同步的時間。
* `@node * LiveSyncAction`  — 要在同步時執行的操作

**定義**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCanceled {#cq-livesynccancelled}

**說明**

定義LiveSyncCanceled混合。 取消活動副本（受控）節點的LiveSync行為，該節點由於其父節點之一而可能涉及LiveRelationship。

* `@prop cq:isCancelledForChildren`  — 定義是否取消LiveSync;也是給孩子的。

**定義**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**說明**

定義附加到LiveSync的LiveSyncAction。

* `@prop name`  — 操作名稱
* `@prop value`  — 操作值

**定義**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**說明**

即時同步配置。

**定義**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

對AEM於5.4，添加到清單末尾：

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq：藍圖操作 {#cq-blueprintaction}

**說明**

藍圖操作

**定義**

* `[cq:BlueprintAction] > nt:unstructured`

## Platform {#platform}

### cq：控制台 {#cq-console}

**說明**

定義控制台節點的節點類型。

**定義**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## 複製 {#replication}

### cq：複製狀態 {#cq-replicationstatus}

**說明**

定義複製狀態資訊混合。

* `@prop cq:lastPublished` — 上次發佈頁面的日期（不再使用）。
* `@prop cq:lastPublishedBy` — 上次發佈頁面的用戶（不再使用）。
* `@prop cq:lastReplicated`  — 上次複製頁面的日期。
* `@prop cq:lastReplicatedBy`  — 上次複製該頁面的用戶。
* `@prop cq:lastReplicationAction`  — 複製操作：激活或停用。
* `@prop cq:lastReplicationStatus`  — 複製狀態（不再使用）。

**定義**

* `[cq:ReplicationStatus]`
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## 安全性 {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**說明**

定義應用程式權限。

**定義**

* `[cq:ApplicationPrivilege] mixin`

### cq：權限Acl {#cq-privilegeacl}

**說明**

定義應用程式權限ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq：權限 {#cq-privilegeace}

**說明**

定義應用程式權限ACE。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**說明**

定義應用程式權限。

**定義**

* `[cq:ApplicationPrivilege] mixin`

### cq：權限Acl {#cq-privilegeacl-1}

**說明**

定義應用程式權限ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq：權限 {#cq-privilegeace-1}

**說明**

定義應用程式權限ACE。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Site Importer {#site-importer}

### cq：元件提取器源 {#cq-componentextractorsource}

**說明**

定義用於標籤可通過元件提取器開啟的檔案的混合類型。

**定義**

`[cq:ComponentExtractorSource] mixin`

## 標記 {#tagging}

### cq：標籤 {#cq-tag}

**說明**

定義單個標籤，但也可以包含標籤，從而建立分類

**定義**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**說明**

抽象可聚集內容的基混合。

* `@node cq:tags`

**定義**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**說明**

僅允許作者/所有者對內容進行標籤（經審核/管理的標籤）。

**定義**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**說明**

任何用戶/公共網站都可以標籤內容（Web2.0樣式），該內容在cq:userContent內部使用。

**定義**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq：允許用戶內容 {#cq-allowsusercontent}

**說明**

添加 `cq:userContent` 可由用戶修改的子節點。 每個用戶將擁有自己的 `cq:userContent/<userid>` 子節點，通常有混合 `cq:UserTaggable`。

**定義**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

擴展變型，更明確地定義 `cq:userContent` 樹

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq：用戶內容 {#cq-usercontent}

**說明**

可由用戶修改。

**定義**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq：用戶資料 {#cq-userdata}

**說明**

用戶資料

**定義**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## 小部件 {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**說明**

客戶端庫資料夾

**定義**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq：小部件 {#cq-widget}

**說明**

Widget

**定義**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**說明**

小部件集合

**定義**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq：對話框 {#cq-dialog}

**說明**

對話方塊

**定義**

* `[cq:Dialog] > cq:Widget orderable`

### cq：面板 {#cq-panel}

**說明**

面板

**定義**

`[cq:Panel] > cq:Widget orderable`

### cq：頁籤面板 {#cq-tabpanel}

**說明**

頁籤面板

**定義**

* `[cq:TabPanel]` > `cq:Panel orderable`
   * `- activeTab (long)`

### cq：欄位 {#cq-field}

**說明**

欄位

**定義**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## 維基 {#wiki}

### 維客：主題 {#wiki-topic}

**說明**

維客主題

**定義**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### 維客：用戶 {#wiki-user}

**說明**

Wiki用戶

**定義**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### Wiki：屬性 {#wiki-properties}

**說明**

Wiki屬性

**定義**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## 工作流程 {#workflow}

### cq：工作流 {#cq-workflow}

**說明**

表示工作流實例。

**定義**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq：工作項 {#cq-workitem}

**說明**

工作項。

**定義**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq：負載 {#cq-payload}

**說明**

裝載

**定義**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq：工作流資料 {#cq-workflowdata}

**說明**

工作流資料

**定義**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq：工作流模型 {#cq-workflowmodel}

**說明**

自動分配工作流配置。 配置將遵循以下結構：
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**定義**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq：工作流節點 {#cq-workflownode}

**說明**

工作流節點

**定義**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq：工作流轉換 {#cq-workflowtransition}

**說明**

工作流轉換

**定義**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq：或頁籤 {#cq-ortab}

**說明**

或頁籤

**定義**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq：等待 {#cq-wait}

**說明**

等待

**定義**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq：工作流棧 {#cq-workflowstack}

**說明**

工作流堆棧

**定義**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**說明**

進程堆棧

**定義**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**說明**

工作流啟動程式

**定義**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
