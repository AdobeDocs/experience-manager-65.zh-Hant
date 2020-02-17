---
title: 自訂節點類型
seo-title: 自訂節點類型
description: AEM是以Sling為基礎，並使用JCR儲存庫，其節點類型由兩者提供，但AEM也提供一系列自訂節點類型
seo-description: AEM是以Sling為基礎，並使用JCR儲存庫，其節點類型由兩者提供，但AEM也提供一系列自訂節點類型
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
translation-type: tm+mt
source-git-commit: d83cd0695f69d82e49b1761df2d8c64b0037e1f9

---


# 自訂節點類型{#custom-node-types}

由於AEM是以Sling為基礎，並使用JCR儲存庫，因此這兩個資料庫所提供的節點類型都可供使用：

* [JCR節點類型](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling Node Types](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除了這些。 AEM提供一系列自訂節點類型。

## 審計 {#audit}

### cq:AuditEvent {#cq-auditevent}

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

### cq:CommentAttachment {#cq-commentattachment}

**說明**

定義節點的節點類 `commentattachment` 型

**定義**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

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

### cq:GeoLocation {#cq-geolocation}

**說明**

以十進位度(DD)定義地理位置的混音

* `@prop latitude` - latitude使用小數點編碼為雙精度
* `@prop longitude` -經度編碼，使用小數點進行雙重編碼

**定義**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**說明**

定義跟蹤節點的節點類型。

**定義**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## 核心 {#core}

### cq:Page {#cq-page}

**說明**

定義預設CQ頁面。

* `@node jcr:content` -頁面的主要內容。

**定義**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**說明**

定義將節點標籤為偽頁的混合類型。 這表示它們可適用於Page和WCM編輯支援。

**定義**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**說明**

定義頁面內容的預設節點，其最小屬性由WCM使用。

* `@prop jcr:title` -頁面標題。
* `@prop jcr:description` -本頁的說明。
* `@prop cq:template` -用於建立頁面的模板的路徑。
* `@prop cq:allowedTemplates` -用於確定允許範本的路徑的規則運算式清單。
* `@prop pageTitle` -標籤中通常顯示標 `<title>` 題。
* `@prop navTitle` -導覽中通常使用的標題。
* `@prop hideInNav` -指定頁面是否應隱藏在導覽中。
* `@prop onTime` -此頁面生效的時間。
* `@prop offTime` -此頁面無效的時間。
* `@prop cq:lastModified` -頁面（或其段落）上次修改的日期。
* `@prop cq:lastModifiedBy` -最後一個變更頁面（或其段落）的使用者。
* `@prop jcr:language` -頁面內容的語言。

>[!NOTE]
>
>頁面內容使用此類型並非強制性。

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

* `@node jcr:content` -新頁面的預設內容。
* `@node icon.png` -保存特徵表徵圖的檔案。
* `@node thumbnail.png` -保存特徵縮圖影像的檔案。
* `@node workflows` -自動指派工作流程設定。 配置將遵循以下結構：
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` -規則運算式模式，以決定範本的父範本允許路徑。
* `@prop allowedChildren` -規則運算式模式，以決定允許作為子範本的範本路徑。
* `@prop ranking` -在「建立頁面」對話框的模板清單中的位置。

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

* `@prop jcr:title` -元件的標題。
* `@prop jcr:description` -元件說明。
* `@node dialog` -主對話框。
* `@prop dialogPath` -主對話框路徑（對話框的替代）。
* `@node design_dialog` -設計對話框。
* `@prop cq:cellName` -設計儲存格的名稱。
* `@prop cq:isContainer` -指出此元件是否為容器元件。 這會強制使用子元件的單元格名稱，而不是路徑名稱。 例如，此為 `parsys` 容器元件。 如果未定義此值，則根據是否存在進行檢查 `cq:childEditConfig`。
* `@prop cq:noDecoration` -如果為true，則在包含 `div` 此元件時不會繪製裝飾標籤。
* `@node cq:editConfig` -定義編輯欄參數的配置。
* `@node cq:childEditConfig` -子元件繼承的編輯配置。
* `@node cq:htmlTag` -定義包含元件時新增至「周圍」標 `div` 簽的其他標籤屬性。
* `@node icon.png`-保存特徵表徵圖的檔案。
* `@node thumbnail.png` -保存特徵縮圖影像的檔案。
* `@prop allowedParents` -規則運算式模式，以決定允許做為父元件的元件路徑。
* `@prop allowedChildren` -規則運算式模式，用於確定允許作為子元件的元件的路徑。
* `@node virtual` -包含反映用於拖放元件的虛擬元件的子節點。
* `@prop componentGroup` -用於元件拖放的元件群組名稱。
* `@node cq:infoProviders` -包含子節點，每個子節點都具有 `className` 引用的屬性 `PageInfoProvider`。

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

### cq:ComponentMixin {#cq-componentmixin}

**說明**

將CQ元件定義為混合類型。

**定義**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**說明**

定義「編輯欄」的設定。

* `@prop cq:dialogMode` -對話框模式：
   * `floating` -用於正常浮動對話
   * `inline` -內嵌編輯
   * `auto` -自動偵測（視可用空間而定）
* `@node cq:inplaceEditing` -此元件的就地編輯配置。
* `@prop cq:layout`-編輯列的版面配置：
   * `editbar` -編輯欄
   * `rollover` -滾過框架
   * `auto` -自動偵測
* `@node cq:formParameters`-要添加到對話框表單的其他參數。
* `@prop cq:actions`-動作清單（編輯列按鈕或功能表項目）。
* `@node cq:actionConfigs` -編輯欄或功能表項目的介面工具集設定。
* `@prop cq:emptyText` -如果沒有視覺內容，則顯示的文字。
* `@node cq:dropTargets` -節點的 `{@link cq:DropTargetConfig}` 集合。

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

* `@prop accept` -此放置目標接受的MIME類型清單；例如， `["image/*"]`
* `@prop groups` -接受源的拖放組清單。
* `@prop propertyName` -用於儲存引用的屬性的名稱。

**定義**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**說明**

定義虛擬CQ元件。 這些目前僅用於新元件拖放精靈。

* `@prop jcr:title` -此元件的標題。
* `@prop jcr:description` -此元件的說明。
* `@node cq:editConfig` -編輯定義編輯欄參數的配置。
* `@node cq:childEditConfig`-編輯子元件繼承的配置。
* `@node icon.png` -保存特徵表徵圖的檔案。
* `@node thumbnail.png` -保存特徵縮圖影像的檔案。
* `@prop allowedParents` -規則運算式模式，以決定允許做為父元件的元件路徑。
* `@prop allowedChildren` -規則運算式模式，用於確定允許作為子元件的元件的路徑。
* `@prop componentGroup` -元件拖放的元件組名。

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

### cq:EditListenersConfig {#cq-editlistenersconfig}

**說明**

定義要在編輯事件上執行的（用戶端）監聽器。 這些值必須引用有效的客戶端偵聽器函式或包含預定義的快捷方式：

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` -在建立元件後觸發。
* `@prop afteredit` -在編輯（修改）元件後引發。
* `@prop afterdelete` -刪除元件後觸發。
* `@prop afterinsert` -將元件新增至此容器後引發。
* `@prop afterremove` -從此容器移除元件後引發。
* `@prop aftermove` -在此容器中移動元件後引發。

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

### dam：縮圖 {#dam-thumbnail}

**說明**

以縮圖表示DAM資產。

**定義**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## 傳送容器清單 {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**說明**

容器清單。

**定義**

* `[cq:containerList]`
   * `mixin`

## 傳送頁面 {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**說明**

`cq:attributes` 是ContentBus版本標籤的節點類型。 此節點僅具有一系列屬性；其中3個是預先定義的「已建立」、「csd」和「時間戳記」。

* `@prop created (long) mandatory copy` -建立版本資訊的時間戳記，通常是簽入先前版本的時間或建立頁面的時間。
* `@prop csd (string) mandatory copy` - csd標準屬性，頁面節點的cq:csd屬性副本
* `@prop timestamp (long) mandatory copy` -上次修改版本的時間戳記，通常是簽入時間。
* `@prop * (string) copy` -與父節點版本化的其他屬性。

**定義**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**說明**

節點類型包 `cq:contentPage` 含ContentBus內容頁的屬性和子節點定義。 僅當將此混合類型添加到類型的節點時，節 `cq:page`點才會變成ContentBus內容頁。

項目包 `cq:Cq4ContentPage` 括：

* `@prop cq:csd` -頁面的ContentBus CSD。
* `@node cq:content` -頁面內容。 如果頁面節點處於「Existing without content」（現有而無內容）或「Deleted」（已刪除）狀態，則此子節點不存在。
* `@node cq:attributes` -頁面屬性的清單，先前稱為版本標籤。 此節點是cq:contentPage類型的必備節點。 當頁面為節點版本時，屬性節點版本化。

**定義**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## 匯入工具 {#importer}

### cq:PollConfig {#cq-pollconfig}

**說明**

民調問答設定。

* `@prop source (String) mandatory` -資料來源URI，此為必要項目，且不得為空白
* `@prop target (String)` -儲存從資料源檢索到的資料的目標位置。 這是可選的，並預設為cq:PollConfig節點。
* `@prop interval (Long)` -從資料來源輪詢新資料或更新資料的間隔（秒）。 這是可選的，預設為30分鐘（1800秒）。
* [建立Adobe Experience Manager的自訂資料匯入工具服務](https://helpx.adobe.com/experience-manager/using/polling.html)

**定義**

* `[cq:PollConfig]
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**說明**

方便了主節點類型以輕鬆建立輪詢配置節點。

**定義**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## 位置 {#location}

### cq:GeoLocation {#cq-geolocation-1}

**說明**

以十進位度(DD)定義地理位置的混音。

* `@prop latitude` -使用小數度將緯度編碼為雙倍。
* `@prop longitude` -使用小數度將經度編碼為雙倍。

**定義**

* `[cq:GeoLocation]
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## 邁勒 {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**說明**

MailerService節點類型。 郵件者使用具有該混合的節點作為消息定義的根節點。

**定義**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq:LiveRelathionship {#cq-liverelationship}

**說明**

定義LiveRelation混合。 主節點和從節點可以通過LiveRelationship虛擬連結。

**定義**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**說明**

定義LiveSync混音。 如果某個節點與作為從節點的主節點有關聯，則該節點被標籤為LiveSync。

* `@prop cq:master` - liveRelationship主節點的路徑。
* `@prop cq:isDeep` -定義關係是否適用於子系。
* `@prop cq:syncTrigger` -定義何時觸發同步。
* `@node * LiveSyncAction` -在同步時執行的動作

**定義**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCancelled {#cq-livesynccancelled}

**說明**

定義LiveSyncCancelled混音。 取消從屬節點的LiveSync行為，該行為可能由於其父節點之一而與LiveRelationship相關。

* `@prop cq:isCancelledForChildren` -定義LiveSync是否已取消；也是給孩子的。

**定義**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**說明**

定義附加至LiveSync的LiveSyncAction。

* `@prop name` -動作名稱
* `@prop value` -動作值

**定義**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**說明**

即時同步設定。

**定義**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

對於AEM 5.4，請新增至清單結尾：

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**說明**

Blueprint動作

**定義**

* `[cq:BlueprintAction] > nt:unstructured`

## 平台 {#platform}

### cq:Console {#cq-console}

**說明**

定義控制台節點的節點類型。

**定義**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## 複寫 {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**說明**

定義複製狀態資訊混合。

* `@prop cq:lastPublished`-上次發佈頁面的日期（不再使用）。
* `@prop cq:lastPublishedBy`-上次發佈頁面的使用者（不再使用）。
* `@prop cq:lastReplicated` -上次複製頁面的日期。
* `@prop cq:lastReplicatedBy` -上次複製頁面的用戶。
* `@prop cq:lastReplicationAction` -複製操作：啟用或停用。
* `@prop cq:lastReplicationStatus` -複製狀態（不再使用）。

**定義**

* `[cq:ReplicationStatus]
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

### cq:PrivilegeAcl {#cq-privilegeacl}

**說明**

定義應用程式權限ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

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

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**說明**

定義應用程式權限ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**說明**

定義應用程式權限ACE。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Site Importer {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**說明**

定義混合類型，用於標籤可以使用元件提取器開啟的檔案。

**定義**

`[cq:ComponentExtractorSource] mixin`

## 標記 {#tagging}

### cq:Tag {#cq-tag}

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

抽象可標籤內容的基本混音。

* `@node cq:tags`

**定義**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**說明**

僅允許作者／擁有者標籤內容（協調／管理標籤）。

**定義**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**說明**

任何使用者／公共網站都可以標籤內容（Web2.0樣式），用於cq:userContent內。

**定義**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowsUserContent {#cq-allowsusercontent}

**說明**

添加可 `cq:userContent` 由用戶修改的子節點。 每個使用者都會有自己的 `cq:userContent/<userid>` 子節點，而子節點通常有mixin `cq:UserTaggable`。

**定義**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

擴展變型，更明確地定義樹 `cq:userContent` 狀

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**說明**

可由使用者修改。

**定義**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**說明**

使用者資料

**定義**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## 介面工具集 {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**說明**

用戶端程式庫資料夾

**定義**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

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

Widget系列

**定義**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq：對話方塊 {#cq-dialog}

**說明**

對話方塊

**定義**

* `[cq:Dialog] > cq:Widget orderable`

### cq：面板 {#cq-panel}

**說明**

面板

**定義**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**說明**

Tab面板

**定義**

* `[cq:TabPanel] > cq:Panel orderable&quot;
   * `- activeTab (long)`

### cq：欄位 {#cq-field}

**說明**

欄位

**定義**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## 維客 {#wiki}

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

### 維客：屬性 {#wiki-properties}

**說明**

維客屬性

**定義**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## 工作流程 {#workflow}

### cq：工作流程 {#cq-workflow}

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

### cq:WorkItem {#cq-workitem}

**說明**

工作項目。

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

### cq：裝載 {#cq-payload}

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

### cq:WorkflowData {#cq-workflowdata}

**說明**

工作流程資料

**定義**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**說明**

自動指派工作流程設定。 配置將遵循以下結構：
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

### cq:WorkflowNode {#cq-workflownode}

**說明**

「工作流」節點

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

### cq:WorkflowTransition {#cq-workflowtransition}

**說明**

工作流程轉換

**定義**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**說明**

或標籤

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

### cq:WorkflowStack {#cq-workflowstack}

**說明**

工作流程堆疊

**定義**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**說明**

流程堆疊

**定義**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**說明**

工作流程啟動程式

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
