---
title: 導入和導出全局設定
seo-title: 導入和導出全局設定
description: 您可以匯入和匯出「工作區」的搜尋範本定義和全域設定。
seo-description: 您可以匯入和匯出「工作區」的搜尋範本定義和全域設定。
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# 導入和導出全局設定 {#importing-and-exporting-global-settings}

您可以匯入和匯出「工作區」的搜尋範本定義和全域設定。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

例如，您可以從一個環境匯出搜尋範本定義和全域設定，然後將它們匯入另一個環境，從開發環境移至生產環境。

匯出全域設定檔案後，您可以在XML或文字編輯器中修改設定。 不過，您唯一想要編輯的設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。 如需詳細資訊，請參閱「工 [作區全域設定」](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果更改了全局設定檔案中的事件屬性，則必須重新啟動伺服器。

## 匯入搜尋範本定義 {#import-a-search-template-definition}

1. 在管理控制台中，按一下「服務>工作區>全域管理」。
1. 在「導入搜索模板定義」框下，按一下選擇檔案並選擇搜索模板。 您只能導入最初從Workspace實例導出的搜索模板定義。
1. 按一下「匯入」。

## 匯出搜尋範本定義 {#export-a-search-template-definition}

1. 在「全局管理」頁的「導出搜索模板定義」下，按一下「全部列出」。
1. 在搜尋範本清單中，選取要匯出的範本。

   >[!NOTE]
   >
   >您可以選取多個範本，但只會匯出最後選取的範本。

1. 按一下「匯出」，然後將檔案儲存在您的電腦上。

## 匯入全域設定 {#import-global-settings}

1. 在「全域管理」頁面的「匯入全域設定」下，按一下「選擇檔案」並選取全域設定檔案。 全域設定檔案必須採用XML格式。
1. 按一下「匯入」。

## 匯出全域設定 {#export-global-settings}

1. 在「全域管理」頁面的「匯出全域設定」下，按一下「匯出」。
1. 將檔案儲存在您的電腦上。

## 工作區全域設定 {#workspace-global-settings}

您可以修改全局設定檔案；不過，您唯一想要編輯的設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

「工作區」全域設定檔案包含下列設定：

### specialRoutes設定 {#specialroutes-settings}

特殊 *路由設定* ，在工作區中指定特殊路由的屬性，批准和拒絕。 在某些情況下，這些路由的按鈕會顯示在工作區的任務卡上，用戶無需開啟表單即可選擇它們。 您可以修改全域設定檔中的specialRoutes設定，以新增自訂名稱以核准和拒絕，或建立其他路由。

**** client_specialRoutes_routes_approve_style:位於「工作區」主題中的樣式名稱，用於標識批准按鈕表徵圖。 樣式必須包含已啟用圖示和停用圖示的值。 要定義自定義按鈕的樣式，必須使用以下模板：工` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` 作區CSS檔案內嵌在workspace-theme.swf檔案中，此檔案位於adobe-workspace-client.ear > adobe-workspace-client.war檔案中。 若要變更工作區的外觀，您必須重新編譯工作區-theme.swf檔案。

**** client_specialRoutes_routes_deny_names:Workbench使用者可用來解讀為「拒絕」的字串種類。 字串區分大小寫。 例如，預設值為deny。 如果Workbench使用者在流程中使用「拒絕」字詞，則無法識別該字詞。 必須在此設定中添加「拒絕」一詞，才能自定義路由按鈕並將樣式應用到該按鈕。

**** client_specialRoutes_routes_deny_style:位於「工作區」主題檔案中的樣式名稱，用於標識拒絕按鈕表徵圖。 樣式必須包含已啟用圖示和停用圖示的值。 `  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` 要定義自定義按鈕的樣式，必須使用以下模板：**** client_specialRoutes_routes_approve_names:Workbench使用者可用來解讀為「核准」的字串種類。 字串區分大小寫。 例如，預設值是核准的。 如果Workbench使用者在流程中使用「核准」字詞，則不會識別該字詞。 必須在此設定中添加「批准」字詞，才能自定義路由按鈕並將樣式應用到該按鈕。

**** client_specialRoutes_names:用於從資源檔案中查找自定義字串值的鍵。 此設定中的每個條目都需要包含名稱和樣式的值。

### JGroup設定 {#jgroup-settings}

這些設定只有在您從Adobe LiveCycle ES 2.5或更舊版本升級後才會顯示。

**** server_remoteevents_ClientTimeoutMillissings:JGgroup等待事件消息的最長時間。 此設定不應變更。

**** server_remoteevents_ServerTimeoutMillissings:在伺服器上接收JGroup消息的超時。 此選項設定從伺服器向客戶端發送消息的延遲。

**** server_remoteevents_JChannelConnectionProperties:用於在伺服器（RemoteEvent服務在其上處理服務事件）和所有Workspace實例之間通信的JGgroup的連接屬性。

您可能需要更改組播IP地址(mcast_addr)、組播IP埠(mcast_port)和組播資料包的TTL(ip_ttl)的UDP值。 預設情況下，組播IP地址和埠值是隨機生成的，通常不需要更改值。 但是，如果貴公司有任何關於多播IP地址的特定多播範圍的網路策略，則可能需要更改這些值。

***注意&#x200B;**:TTL必須大於群集中伺服器之間的網路交換機數；但是，如果值設定過高，則可能導致組播資料包進入子網，在子網中丟棄這些資料包。*

不應更改此設定中的其餘屬性。

**** server_remoteevents_JGroupName:用於遠程事件通信的JGgroup的名稱。 此值會隨機產生，以避免叢集中的衝突。 此值不應變更。

如需JGroups和Workspace的詳細資訊，請參 [閱JGroups和AEM表格工作區——說明](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html)。

### formView設定 {#formview-settings}

**** client_formView_openFormInFullScreen:若要以全螢幕模式在工作區中顯示所有表格，請將此選項設為true。 依預設，此選項會設為false，表單不會以全螢幕模式顯示。 請注意，用戶服務包含以全屏模式開啟與任務關聯的文檔的選項。 這可讓您依每個程式控制顯示。

**** client_routes_formViewOnly:當設為True時，路由不會顯示在「工作區」的卡片檢視或清單檢視中。 預設值為False，表示路由會顯示在卡片檢視和清單檢視中。

### 其他設定 {#other-settings}

**** client_mimeTypes_openOutsideBrowser:將在Workspace瀏覽器實例外部開啟的文檔的MIME類型。 如果您組織的程式需要額外的MIME類型，請在此處指定。 預設值為：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**** client_customUI_caching:快取自訂工作使用者介面。

**** server_debugLevel:請勿變更此設定。

**** client_pollingInterval:設定（JEE上的AEM表單已過時）Flex工作區上使用的輪詢間隔（以秒為單位），以偵測新的和修改的工作。 預設值為3秒。 這不適用於AEM Forms Workspace。

**** client_systemContext_name:為AEM Forms Workspace中的工作附件指定自訂名稱（例如「公民」），以便顯示在「新增者」欄位（位於「附件」標籤）中。

要定義自定義名稱，請執行以下操作：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

**注意**:對 *於示範應用程式，預設顯示名稱為&#x200B;**Citizen**。 對於您所建立的自訂應用程式，預設顯示名稱為「**系統內容帳戶」**。***** client_idleTimeout:當使用者在特定時間段內仍處於非活動狀態時，AEM Forms Workspace工作階段會過期。 若要啟用此功能，請新增項目至「全域設定」&lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>。 您可以指定值0以停用閒置逾時。 時間量以秒為單位指定。
