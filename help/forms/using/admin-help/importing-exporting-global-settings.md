---
title: 匯入和匯出全域設定
description: 您可以匯入和匯出Workspace的搜尋範本定義和全域設定。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# 匯入和匯出全域設定 {#importing-and-exporting-global-settings}

您可以匯入和匯出Workspace的搜尋範本定義和全域設定。

>[!NOTE]
>
>AEM Forms版本已棄用Flex工作區。

例如，您可以從某個環境匯出搜尋範本定義和全域設定，然後將其匯入另一個環境，藉此從開發環境移至生產環境。

匯出全域設定檔案後，您可以在XML或文字編輯器中修改設定。 不過，您只想編輯JChannelConnectionProperties、formViewOnly和specialRoutes設定。 如需詳細資訊，請參閱[Workspace全域設定](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果您變更全域設定檔案中的事件屬性，則必須重新啟動伺服器。

## 匯入搜尋範本定義 {#import-a-search-template-definition}

1. 在管理控制檯中，按一下服務> Workspace >全域管理。
1. 在「匯入搜尋範本定義」方塊下，按一下「選擇檔案」並選取搜尋範本。 您只能匯入原本從Workspace例項匯出的搜尋範本定義。
1. 按一下「匯入」。

## 匯出搜尋範本定義 {#export-a-search-template-definition}

1. 在「全域管理」頁面的「匯出搜尋範本定義」下，按一下「列出全部」。
1. 在搜尋範本清單中，選取要匯出的範本。

   >[!NOTE]
   >
   >您可以選取多個範本，但只會匯出最後選取的範本。

1. 按一下「匯出」 ，然後將檔案儲存在電腦上。

## 匯入全域設定 {#import-global-settings}

1. 在「全域管理」頁面的「匯入全域設定」下，按一下「選擇檔案」並選取全域設定檔案。 全域設定檔案必須是XML格式。
1. 按一下「匯入」。

## 匯出全域設定 {#export-global-settings}

1. 在「全域管理」頁面的「匯出全域設定」下，按一下「匯出」。
1. 將檔案儲存在電腦上。

## Workspace全域設定 {#workspace-global-settings}

您可以修改全域設定檔案；不過，您只想編輯JChannelConnectionProperties、formViewOnly和specialRoutes設定。

>[!NOTE]
>
>AEM Forms版本已棄用Flex工作區。

Workspace全域設定檔案包含下列設定：

### specialRoutes設定 {#specialroutes-settings}

*specialRoutes*&#x200B;設定在Workspace中指定特殊路由（核准和拒絕）的屬性。 在某些情況下，這些路由的按鈕會顯示在Workspace的工作卡片上，使用者可以不開啟表單而選取它們。 您可以修改全域設定檔案中的specialRoutes設定，以新增核准和拒絕的自訂名稱，或建立其他路由。

**client_specialRoutes_routes_approve_style：** Workspace佈景主題中的樣式名稱，可識別核准按鈕圖示。 樣式必須包含啟用圖示和停用圖示的值。 若要定義自訂按鈕的樣式，您必須使用下列範本：
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Workspace CSS檔案內嵌於workspace-theme.swf檔案（位於adobe-workspace-client.ear > adobe-workspace-client.war檔案）。 若要變更Workspace的外觀，您必須重新編譯workspace-theme.swf檔案。

**client_specialRoutes_routes_deny_names：** Workbench使用者可用來解譯為「拒絕」的字串種類。 字串區分大小寫。 例如，預設值為deny。 如果Workbench使用者在處理序中使用了「拒絕」一詞，將無法辨識該詞。 必須將「拒絕」一詞加入此設定，才能自訂路由按鈕並套用樣式。

**client_specialRoutes_routes_deny_style：** Workspace主題檔案中用於識別拒絕按鈕圖示的樣式名稱。 樣式必須包含啟用圖示和停用圖示的值。 若要定義自訂按鈕的樣式，您必須使用下列範本：
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names：** Workbench使用者可用來解譯為「核准」的各種字串。 字串區分大小寫。 例如，預設值為approve。 如果Workbench使用者在處理序中使用「核准」一詞，則無法辨識該詞。 必須將「核准」一詞新增至此設定，才能自訂路由按鈕並套用樣式。

**client_specialRoutes_names：**&#x200B;用來從資源檔尋找自訂字串值的金鑰。 此設定中的每個專案都必須包含名稱和樣式的值。

### 群組設定 {#jgroup-settings}

這些設定只有在您從AdobeLiveCycleES 2.5或更早版本升級後才出現。

**server_remoteevents_ClientTimeoutMilliseconds：** JGroup等待事件訊息的最長時間。 此設定不應變更。

**server_remoteevents_ServerTimeoutMilliseconds：**&#x200B;在伺服器上接收JGroup訊息的逾時。 此選項設定從伺服器傳送訊息至使用者端的延遲。

**server_remoteevents_JChannelConnectionProperties：**&#x200B;用來在伺服器（RemoteEvent服務處理服務事件）與Workspace的所有執行個體之間通訊的JGroup的連線內容。

您可能需要變更多點傳送IP位址(mcast_addr)、多點傳送IP連線埠(mcast_port)的UDP值，以及多點傳送封包(ip_ttl)的TTL。 預設情況下，多點傳送IP位址和連線埠值是隨機產生的，通常不需要變更這些值。 但是，如果貴公司對於多點傳送IP位址的特定多點傳送範圍有任何網路原則，您可能需要變更值。

>[!NOTE]
>
>TTL必須大於叢集中伺服器之間的網路交換器數目；但是，如果值設定得太高，可能會造成多點傳送封包進入子網路，並捨棄這些封包。

此設定中的其餘屬性不應變更。

**server_remoteevents_JGroupName：**&#x200B;用於遠端事件通訊的JGroup名稱。 此值是隨機產生的，以避免叢集中的衝突。 此值不應變更。

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### formView設定 {#formview-settings}

**client_formView_openFormInFullScreen：**&#x200B;若要以全熒幕模式顯示Workspace中的所有表單，請將此選項設定為true。 依預設，此選項會設為false，且表單不會以全熒幕模式顯示。 User服務包含以全熒幕模式開啟與工作相關聯之檔案的選項。 這可讓您根據每個處理序來控制顯示。

**client_routes_formViewOnly：**&#x200B;設定為True時，路由不會顯示在Workspace的卡片檢視或清單檢視中。 預設值為False，表示路由會顯示在卡片檢視和清單檢視中。

### 其他設定 {#other-settings}

**client_mimeTypes_openOutsideBrowser：**&#x200B;在Workspace瀏覽器執行個體外部開啟的MIME檔案型別。 如果貴組織的流程需要額外的MIME型別，請在此處指定。 預設值為：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching：**&#x200B;快取自訂工作使用者介面。

**server_debugLevel：**&#x200B;請勿變更此設定。

**client_pollingInterval：**&#x200B;設定(JEE上已棄用的AEM表單) Flex Workspace上使用的輪詢間隔（以秒為單位），以偵測新的和修改的工作。 預設值為3秒。 這在AEM Forms Workspace中無法運作。

**client_systemContext_name：**&#x200B;指定要在AEM Forms Workspace中工作附件的「新增者」欄位（在「附件」索引標籤中）中顯示的自訂名稱（例如「公民」）。

若要定義自訂名稱：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>對於示範應用程式，預設顯示名稱為&#x200B;**公民**。 對於您建立的自訂應用程式，預設顯示名稱為&#x200B;**系統內容帳戶**。
>
>**client_idleTimeout：**&#x200B;當使用者在特定時間內保持非使用中時，AEM Forms Workspace工作階段就會過期。 若要啟用此功能，請將專案新增至全域設定&lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>。 您可以指定值0來停用閒置逾時。 時間長度以秒為單位指定。
