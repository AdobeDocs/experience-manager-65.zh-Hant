---
title: 導入和導出全局設定
seo-title: Importing and exporting global settings
description: 可以導入和導出Workspace的搜索模板定義和全局設定。
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# 導入和導出全局設定 {#importing-and-exporting-global-settings}

可以導入和導出Workspace的搜索模板定義和全局設定。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

例如，可以通過從一個環境中導出搜索模板定義和全局設定並將它們導入到另一個環境中，從開發環境移動到生產環境。

導出全局設定檔案後，可以在XML或文本編輯器中修改設定。 但是，您可能希望編輯的唯一設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。 有關詳細資訊，請參見 [工作區全局設定](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果在全局設定檔案中更改事件屬性，則必須重新啟動伺服器。

## 導入搜索模板定義 {#import-a-search-template-definition}

1. 在管理控制台中，按一下「服務」>「工作區」>「全局管理」。
1. 在「導入搜索模板定義」框下，按一下「選擇檔案」並選擇搜索模板。 您只能導入最初從Workspace實例導出的搜索模板定義。
1. 按一下「導入」。

## 導出搜索模板定義 {#export-a-search-template-definition}

1. 在「全局管理」(Global Administration)頁面的「導出搜索模板定義」(Export search template definition)下，按一下「全部列出」(List All)。
1. 在搜索模板清單中，選擇要導出的模板。

   >[!NOTE]
   >
   >您可以選擇多個模板，但只導出最後選定的模板。

1. 按一下「Export（導出）」 ，然後將檔案保存在電腦上。

## 導入全局設定 {#import-global-settings}

1. 在「全局管理」頁的「導入全局設定」下，按一下「選擇檔案」並選擇全局設定檔案。 全局設定檔案必須為XML格式。
1. 按一下「導入」。

## 導出全局設定 {#export-global-settings}

1. 在「全局管理」(Global Administration)頁面的「導出全局設定」(Export Global Settings)下，按一下「導出」(Export)。
1. 將檔案保存在電腦上。

## 工作區全局設定 {#workspace-global-settings}

可以修改全局設定檔案；但是，您唯一要編輯的設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

「工作區全局設定」檔案包括以下設定：

### 特殊路由設定 {#specialroutes-settings}

的 *特殊路線* 設定在工作區中指定特殊路由的屬性。 在某些情況下，這些路由的按鈕會顯示在Workspace中的任務卡上，用戶可以在不開啟表單的情況下選擇它們。 您可以修改全局設定檔案中的specialRoutes設定，以添加用於批准和拒絕的自定義名稱或建立附加路由。

**client_specialRoutes_routes_approve_style:** 位於「工作區」主題中的樣式的名稱，該主題標識批准按鈕表徵圖。 樣式必須包括啟用表徵圖和禁用表徵圖的值。 要定義自定義按鈕的樣式，必須使用以下模板：
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Workspace CSS檔案嵌入在workspace-theme.swf檔案中，該檔案位於adobe-workspace-client.ear > adobe-workspace-client.war檔案中。 要更改Workspace的外觀，必須重新編譯workspace-theme.swf檔案。

**client_specialRoutes_routes_deny_names:** Workbench用戶可以用來解釋為「deny」的字串的種類。 字串區分大小寫。 例如，預設值為deny。 如果Workbench用戶在流程中使用「拒絕」一詞，則無法識別該詞。 必須將「拒絕」一詞添加到此設定中，才能自定義路由按鈕並應用其樣式。

**client_specialRoutes_routes_deny_style:** 位於Workspace主題檔案中的樣式的名稱，該檔案標識拒絕按鈕表徵圖。 樣式必須包括啟用表徵圖和禁用表徵圖的值。 要定義自定義按鈕的樣式，必須使用以下模板：
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names:** Workbench用戶可用來解釋為「批准」的字串的種類。 字串區分大小寫。 例如，預設值為approve。 如果Workbench用戶在流程中使用「批准」一詞，則無法識別該詞。 必須將「批准」一詞添加到此設定中，以便自定義路由按鈕並應用其樣式。

**client_specialRoutes_names:** 用於從資源檔案中查找自定義字串值的鍵。 此設定中的每個條目都需要包括名稱和樣式的值。

### JGroup設定 {#jgroup-settings}

僅當從AdobeLiveCycleES 2.5或更低版本升級時，才會顯示這些設定。

**server_remoteevents_ClientTimeoutMilliseconds:** JGroup等待事件消息的最長時間。 不應更改此設定。

**server_remoteevents_ServerTimeoutMillisoness:** 在伺服器上接收JGroup消息的超時。 此選項設定將消息從伺服器發送到客戶端的延遲。

**server_remoteevents_JChannelConnectionProperties:** 用於在伺服器（RemoteEvent服務在其上處理服務事件）和Workspace所有實例之間通信的JGroup的連接屬性。

您可能需要更改多播IP地址(mcastaddr)、多播IP埠(mcastport)和多播資料包(ipttl)的TTL值。 預設情況下，組播IP地址和埠值是隨機生成的，通常不需要更改這些值。 但是，如果您的公司有任何關於多播IP地址的特定多播範圍的網路策略，則可能需要更改這些值。

>[!NOTE]
>
>TTL必須大於群集中伺服器之間的網路交換機數；但是，如果值設定得過高，則會導致多播資料包進入子網，在子網中這些資料包將被丟棄。

不應更改此設定中的其餘屬性。

**server_remoteevents_JGroupName:** 用於遠程事件通信的JGroup的名稱。 此值是隨機生成的，以避免群集中的衝突。 不應更改此值。

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### 表單視圖設定 {#formview-settings}

**client_formView_openFormInFullScreen:** 要在全屏模式下顯示Workspace中的所有表單，請將此選項設定為true。 預設情況下，此選項設定為false，且表單不以全屏模式顯示。 請注意，用戶服務包含一個選項，用於以全屏模式開啟與任務關聯的文檔。 這樣，您就可以按每個進程控制顯示。

**client_routes_formViewOnly:** 如果設定為True，則在Workspace的卡視圖或清單視圖中不顯示路由。 預設值為False，表示路由顯示在卡視圖和清單視圖中。

### 其他設定 {#other-settings}

**client_mimeTypes_openOutsideBrowser:** 將在Workspace瀏覽器實例外部開啟的文檔的MIME類型。 如果組織的進程需要其他MIME類型，請在此處指定。 預設值為：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** 快取自定義任務用戶介面。

**server_debugLevel:** 不要更改此設定。

**client_pollingInterval:** 設定在（JEE上的表單已棄用）Flex工作區上使用的輪詢間隔(AEM秒)，以檢測新的和已修改的任務。 預設值為3秒。 這對AEM Forms工作區無效。

**client_systemContext_name:** 為AEM Forms工作區中任務的附件指定要在「添加者」(Added By)欄位(在「附件」(Attachments)頁籤中顯示的自定義名稱（例如公民）。

要定義自定義名稱，請執行以下操作：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>對於演示應用程式，預設顯示名稱為 **公民**。 對於您建立的自定義應用程式，預設顯示名稱為 **系統上下文帳戶**。
>
>**client_idleTimeout:** 當用戶在特定時間段內保持非活動狀態時，AEM Forms工作區會話將過期。 要啟用該功能，請向「全局設定」添加一個條目 &lt;client_idletimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idletimeout>。 可以指定值0以禁用空閒超時。 時間量以秒為單位指定。
