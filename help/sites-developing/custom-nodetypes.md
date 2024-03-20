---
title: 自訂節點型別
description: Adobe Experience Manager (AEM)以Sling為基礎，並使用JCR存放庫和兩者都提供的節點型別，但AEM也提供了一系列自訂節點型別
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 5%

---

# 自訂節點型別{#custom-node-types}

由於Adobe Experience Manager (AEM)是以Sling為基礎，並使用JCR存放庫，因此這兩者提供的節點型別都可供使用：

* [JCR節點型別](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling節點型別](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除了這些節點型別之外，AEM還提供了一系列自訂節點型別。

## 稽核 {#audit}

### cq：AuditEvent {#cq-auditevent}

**說明**

定義稽核事件節點的節點型別。

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

### cq：Comment {#cq-comment}

**說明**

定義註解節點的節點型別。

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

### cq：CommentAttachment {#cq-commentattachment}

**說明**

定義 `commentattachment` 節點

**定義**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq：CommentContent {#cq-commentcontent}

**說明**

定義評論內容節點的節點型別

**定義**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq：GeoLocation {#cq-geolocation}

**說明**

以小數位數(DD)定義地理位置的Mixin

* `@prop latitude`  — 使用小數位數編碼為雙精度的latitude
* `@prop longitude`  — 使用小數位數編碼為雙倍的經度

**定義**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq：Trackback {#cq-trackback}

**說明**

定義引用回溯節點的節點型別。

**定義**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## 核心 {#core}

### cq:Page {#cq-page}

**說明**

定義預設CQ頁面。

* `@node jcr:content`  — 頁面的主要內容。

**定義**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq：PseudoPage {#cq-pseudopage}

**說明**

定義將節點標示為虛擬頁面的mixin型別。 換言之，這表示它們可以調整為適用於Page和WCM編輯支援。

**定義**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**說明**

定義頁面內容的預設節點，具有WCM使用的最小屬性。

* `@prop jcr:title`  — 頁面標題。
* `@prop jcr:description`  — 此頁面的說明。
* `@prop cq:template`  — 用來建立頁面的範本路徑。
* `@prop cq:allowedTemplates`  — 用來決定允許範本之路徑的規則運算式清單。
* `@prop pageTitle`  — 標題顯示在 `<title>` 標籤之間。
* `@prop navTitle`  — 導覽中使用的標題。
* `@prop hideInNav`  — 指定是否要在導覽中隱藏頁面。
* `@prop onTime`  — 此頁面生效的時間。
* `@prop offTime`  — 此頁面失效的時間。
* `@prop cq:lastModified`  — 上次修改頁面（或其段落）的日期。
* `@prop cq:lastModifiedBy`  — 最後一個變更頁面（或其段落）的使用者。
* `@prop jcr:language`  — 頁面內容的語言。

>[!NOTE]
>
>頁面內容不必使用此型別。

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

定義CQ範本。

* `@node jcr:content`  — 新頁面的預設內容。
* `@node icon.png`  — 包含特性圖示的檔案。
* `@node thumbnail.png`  — 儲存特徵縮圖影像的檔案。
* `@node workflows`  — 自動指派工作流程設定。 設定遵循下列結構：
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents`  — 規則運算式模式，用於決定允許做為父範本的範本路徑。
* `@prop allowedChildren`  — 規則運算式模式，可決定允許做為子範本的範本路徑。
* `@prop ranking`  — 在建立頁面對話方塊的範本清單中的位置。

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
* `@prop jcr:description`  — 元件的說明。
* `@node dialog`  — 主要對話方塊。
* `@prop dialogPath`  — 主要對話方塊路徑（對話方塊的替代方式）。
* `@node design_dialog`  — 設計對話方塊。
* `@prop cq:cellName`  — 設計儲存格的名稱。
* `@prop cq:isContainer`  — 指出是否為容器元件。 強制使用子元件的儲存格名稱，而非路徑名稱。 例如， `parsys` 是容器元件。 如果未定義此值，則會根據是否存在 `cq:childEditConfig`.
* `@prop cq:noDecoration`  — 如果為True，則無裝飾 `div` 包含此元件時會繪製標籤。
* `@node cq:editConfig`  — 定義編輯列引數的設定。
* `@node cq:childEditConfig`  — 子元件繼承的編輯設定。
* `@node cq:htmlTag`  — 定義新增至「周圍」的其他標籤屬性 `div` 標籤。
* `@node icon.png` — 包含特性圖示的檔案。
* `@node thumbnail.png`  — 儲存特徵縮圖影像的檔案。
* `@prop allowedParents`  — 規則運算式模式，用於決定允許做為父元件的元件路徑。
* `@prop allowedChildren`  — 規則運算式模式，可決定允許做為子元件的元件路徑。
* `@node virtual`  — 包含反映用於元件拖放之虛擬元件的子節點。
* `@prop componentGroup`  — 元件群組的名稱，用於元件拖放。
* `@node cq:infoProviders`  — 包含子節點，每個子節點都有屬性 `className` 這指的是 `PageInfoProvider`.

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

### cq：ComponentMixin {#cq-componentmixin}

**說明**

將CQ元件定義為mixin型別。

**定義**

`[cq:ComponentMixin] > cq:Component mixin`

### cq：EditConfig {#cq-editconfig}

**說明**

定義「編輯列」的設定。

* `@prop cq:dialogMode`  — 對話方塊模式：
   * `floating`  — 用於一般浮動對話方塊
   * `inline`  — 內嵌編輯
   * `auto`  — 自動偵測（視可用空間而定）
* `@node cq:inplaceEditing`  — 為此元件就地編輯設定。
* `@prop cq:layout` — 編輯列的配置：
   * `editbar`  — 編輯列
   * `rollover`  — 滑鼠指向影格
   * `auto`  — 自動偵測
* `@node cq:formParameters` — 要新增至對話方塊表單的其他引數。
* `@prop cq:actions` — 動作清單（編輯列按鈕或功能表專案）。
* `@node cq:actionConfigs`  — 編輯列或功能表專案的Widget設定。
* `@prop cq:emptyText`  — 沒有視覺內容時所顯示的文字。
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

### cq：DropTargetConfig {#cq-droptargetconfig}

**說明**

設定元件的一個放置目標。 此節點的名稱會作為用於拖放的ID。

* `@prop accept`  — 此放置目標接受的MIME型別清單；例如， `["image/*"]`
* `@prop groups`  — 接受來源的拖放群組清單。
* `@prop propertyName`  — 用來儲存參考的屬性名稱。

**定義**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq：VirtualComponent {#cq-virtualcomponent}

**說明**

定義虛擬CQ元件。 目前僅用於新元件拖放精靈。

* `@prop jcr:title`  — 此元件的標題。
* `@prop jcr:description`  — 此元件的說明。
* `@node cq:editConfig`  — 編輯定義編輯列引數的設定。
* `@node cq:childEditConfig` — 編輯子元件繼承的設定。
* `@node icon.png`  — 包含特性圖示的檔案。
* `@node thumbnail.png`  — 儲存特徵縮圖影像的檔案。
* `@prop allowedParents`  — 規則運算式模式，用於決定允許做為父元件的元件路徑。
* `@prop allowedChildren`  — 規則運算式模式，可決定允許做為子元件的元件路徑。
* `@prop componentGroup`  — 元件拖放的元件群組名稱。

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

### cq：EditListenersConfig {#cq-editlistenersconfig}

**說明**

定義要在編輯事件上執行的（使用者端）監聽器。 值必須參考有效的使用者端接聽程式函式或包含預先定義的捷徑：

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate`  — 在建立元件後引發。
* `@prop afteredit`  — 在編輯（修改）元件後引發。
* `@prop afterdelete`  — 在刪除元件後引發。
* `@prop afterinsert`  — 將元件新增至此容器後引發。
* `@prop afterremove`  — 從此容器移除元件後引發。
* `@prop aftermove`  — 在此容器中移動元件後引發。

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

### dam：Thumbnail {#dam-thumbnail}

**說明**

表示DAM資產的縮圖。

**定義**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## 傳遞容器清單 {#delivery-container-list}

### cq：containerList {#cq-containerlist}

**說明**

容器清單。

**定義**

* `[cq:containerList]`
   * `mixin`

## 傳遞頁面 {#delivery-page}

### cq：Cq4PageAttributes {#cq-cq-pageattributes}

**說明**

節點型別 `cq:attributes` 用於ContentBus版本標籤。 此節點只有一系列屬性；其中三個為預先定義的「已建立」、「csd」和「時間戳記」。

* `@prop created (long) mandatory copy`  — 版本資訊的建立時間戳記，通常為上一版本的簽入時間或頁面建立時間。
* `@prop csd (string) mandatory copy` - csd標準屬性，頁面節點的cq：csd屬性副本
* `@prop timestamp (long) mandatory copy`  — 上次版本修改的時間戳記，通常為簽到時間。
* `@prop * (string) copy`  — 其他屬性，以父節點建立版本。

**定義**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq：Cq4ContentPage {#cq-cq-contentpage}

**說明**

節點型別 `cq:contentPage` 包含ContentBus內容頁面的屬性和子節點定義。 只有當此mixin型別新增到型別的節點時 `cq:page`，節點會變成ContentBus內容頁面。

中的專案 `cq:Cq4ContentPage` 為：

* `@prop cq:csd`  — 頁面的ContentBusCSD。
* `@node cq:content`  — 頁面內容。 如果頁面節點處於「現有但不含內容」或「已刪除」狀態，則此子節點不存在。
* `@node cq:attributes`  — 頁面屬性清單（先前稱為版本標籤）。 cq：contentPage型別必須有此節點。 當頁面為節點建立版本時，就會建立屬性節點的版本。

**定義**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## 匯入工具 {#importer}

### cq:PollConfig {#cq-pollconfig}

**說明**

輪詢設定。

* `@prop source (String) mandatory`  — 資料來源URI。 必要項，且不得空白。
* `@prop target (String)`  — 儲存從資料來源擷取之資料的目標位置。 選用且預設為cq：PollConfig節點。
* `@prop interval (Long)`  — 輪詢資料來源中新資料或更新資料的間隔（秒）。 選填，預設為30分鐘（1800秒）。
* [建立Adobe Experience Manager的自訂資料匯入工具服務](https://helpx.adobe.com/experience-manager/using/polling.html)

**定義**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**說明**

方便主要節點型別輕鬆建立輪詢設定節點。

**定義**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## 位置 {#location}

### cq：GeoLocation {#cq-geolocation-1}

**說明**

以小數位數(DD)定義地理位置的Mixin。

* `@prop latitude`  — 使用小數位數編碼為雙精度的Latitude。
* `@prop longitude`  — 使用小數位數編碼為雙倍的經度。

**定義**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## 郵件程式 {#mailer}

### cq：mailerMessage {#cq-mailermessage}

**說明**

MailerService節點型別。 郵件程式會使用具有此mixin的節點作為訊息定義的根節點。

**定義**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq：LiveRelationship {#cq-liverelationship}

**說明**

定義LiveRelationship mixin。 主要來源（控制）節點和即時副本（控制）節點可透過LiveRelationship以虛擬方式連結。

**定義**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq：LiveSync {#cq-livesync}

**說明**

定義LiveSync Mixin。 如果節點與主要來源（控制）節點和即時副本（控制）節點有關聯，則會標示為LiveSync。

* `@prop cq:master` - LiveRelationship的主要來源（控制）路徑。
* `@prop cq:isDeep`  — 定義關係是否適用於子系。
* `@prop cq:syncTrigger`  — 定義同步何時觸發。
* `@node * LiveSyncAction`  — 要在同步時執行的動作

**定義**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq：LiveSyncCanceled {#cq-livesynccancelled}

**說明**

定義LiveSyncCanceled mixin。 取消即時副本（受控）節點的LiveSync行為，該節點可能因其父系之一而與LiveRelationship有關。

* `@prop cq:isCancelledForChildren`  — 定義是否已取消LiveSync；也適用於子系。

**定義**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq：LiveSyncAction {#cq-livesyncaction}

**說明**

定義附加至LiveSync的LiveSyncAction。

* `@prop name`  — 動作名稱
* `@prop value`  — 動作值

**定義**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq：LiveSyncConfig {#cq-livesyncconfig}

**說明**

Live Sync設定。

**定義**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

對於AEM 5.4，在清單末尾新增：

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq：BlueprintAction {#cq-blueprintaction}

**說明**

Blueprint動作

**定義**

* `[cq:BlueprintAction] > nt:unstructured`

## Platform {#platform}

### cq：Console {#cq-console}

**說明**

定義主控台節點的節點型別。

**定義**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## 複製 {#replication}

### cq：ReplicationStatus {#cq-replicationstatus}

**說明**

定義復寫狀態資訊mixin。

* `@prop cq:lastPublished` — 上次發佈頁面的日期（不再使用）。
* `@prop cq:lastPublishedBy` — 上次發佈頁面的使用者（不再使用）。
* `@prop cq:lastReplicated`  — 上次復寫頁面的日期。
* `@prop cq:lastReplicatedBy`  — 上次復寫頁面的使用者。
* `@prop cq:lastReplicationAction`  — 復寫動作：啟動或停用。
* `@prop cq:lastReplicationStatus`  — 復寫狀態（已不再使用）。

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

### cq：ApplicationPrivilege {#cq-applicationprivilege}

**說明**

定義應用程式許可權。

**定義**

* `[cq:ApplicationPrivilege] mixin`

### cq：PrivilegeAcl {#cq-privilegeacl}

**說明**

定義應用程式許可權ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq：PrivilegeAce {#cq-privilegeace}

**說明**

定義應用程式許可權ACE。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq：ApplicationPrivilege {#cq-applicationprivilege-1}

**說明**

定義應用程式許可權。

**定義**

* `[cq:ApplicationPrivilege] mixin`

### cq：PrivilegeAcl {#cq-privilegeacl-1}

**說明**

定義應用程式許可權ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq：PrivilegeAce {#cq-privilegeace-1}

**說明**

定義應用程式許可權ACE。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Site Importer {#site-importer}

### cq：ComponentExtractorSource {#cq-componentextractorsource}

**說明**

定義mixin型別，用於標籤可使用元件提取器開啟的檔案。

**定義**

`[cq:ComponentExtractorSource] mixin`

## 標記 {#tagging}

### cq：Tag {#cq-tag}

**說明**

定義單一標籤，但也可以包含標籤，因此建立分類法

**定義**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**說明**

可標籤內容的抽象基底mixin。

* `@node cq:tags`

**定義**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq：OwnerTaggable {#cq-ownertaggable}

**說明**

僅允許作者/擁有者標籤內容（稽核/管理的標籤）。

**定義**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq：UserTaggable {#cq-usertaggable}

**說明**

任何使用者/公用網站都可以標籤cq：userContent內使用的內容（Web2.0樣式）。

**定義**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq：AllowsUserContent {#cq-allowsusercontent}

**說明**

新增 `cq:userContent` 使用者可修改的子節點。 每個使用者都有自己的 `cq:userContent/<userid>` 子節點，通常具有mixin `cq:UserTaggable`.

**定義**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

擴充變體，更明確地定義 `cq:userContent` 樹

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq：UserContent {#cq-usercontent}

**說明**

可由使用者修改。

**定義**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq：UserData {#cq-userdata}

**說明**

使用者資料

**定義**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## Widget {#widgets}

### cq：ClientLibraryFolder {#cq-clientlibraryfolder}

**說明**

使用者端資料庫資料夾

**定義**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq：Widget {#cq-widget}

**說明**

Widget

**定義**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq：WidgetCollection {#cq-widgetcollection}

**說明**

Widget集合

**定義**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq：Dialog {#cq-dialog}

**說明**

對話方塊

**定義**

* `[cq:Dialog] > cq:Widget orderable`

### cq：Panel {#cq-panel}

**說明**

面板

**定義**

`[cq:Panel] > cq:Widget orderable`

### cq：TabPanel {#cq-tabpanel}

**說明**

索引標籤面板

**定義**

* `[cq:TabPanel]` > `cq:Panel orderable`
   * `- activeTab (long)`

### cq：Field {#cq-field}

**說明**

欄位

**定義**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### Wiki：主題 {#wiki-topic}

**說明**

Wiki主題

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

### wiki：User {#wiki-user}

**說明**

Wiki使用者

**定義**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki：屬性 {#wiki-properties}

**說明**

Wiki屬性

**定義**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## 工作流程 {#workflow}

### cq：Workflow {#cq-workflow}

**說明**

代表工作流程例項。

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

### cq：WorkItem {#cq-workitem}

**說明**

工作專案。

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

### cq：Payload {#cq-payload}

**說明**

總額

**定義**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq：WorkflowData {#cq-workflowdata}

**說明**

工作流程資料

**定義**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq：WorkflowModel {#cq-workflowmodel}

**說明**

自動指派工作流程設定。 設定遵循以下結構：
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

### cq：WorkflowNode {#cq-workflownode}

**說明**

工作流程節點

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

### cq：WorkflowTransition {#cq-workflowtransition}

**說明**

工作流程轉換

**定義**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq：OrTab {#cq-ortab}

**說明**

或索引標籤

**定義**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq：Wait {#cq-wait}

**說明**

等待

**定義**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq：WorkflowStack {#cq-workflowstack}

**說明**

工作流程棧疊

**定義**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq：ProcessStack {#cq-processstack}

**說明**

程式棧疊

**定義**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq：WorkflowLauncher {#cq-workflowlauncher}

**說明**

工作流程啟動器

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
