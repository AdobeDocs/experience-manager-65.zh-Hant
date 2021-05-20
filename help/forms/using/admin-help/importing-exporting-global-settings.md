---
title: 匯入和匯出全域設定
seo-title: 匯入和匯出全域設定
description: 您可以匯入和匯出工作區的搜尋範本定義和全域設定。
seo-description: 您可以匯入和匯出工作區的搜尋範本定義和全域設定。
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 導入和導出全局設定{#importing-and-exporting-global-settings}

您可以匯入和匯出工作區的搜尋範本定義和全域設定。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

例如，您可以從一個環境匯出搜尋範本定義和全域設定，並匯入到另一個環境，以便從開發環境移至生產環境。

導出全局設定檔案後，可以在XML或文本編輯器中修改設定。 但是，您可能只想編輯JChannelConnectionProperties 、 formViewOnly和specialRoutes設定。 如需詳細資訊，請參閱[工作區全域設定](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果更改全局設定檔案中的事件屬性，則必須重新啟動伺服器。

## 導入搜索模板定義{#import-a-search-template-definition}

1. 在管理控制台中，按一下「服務>工作區>全域管理」。
1. 在「導入搜索模板定義」框下，按一下「選擇檔案」並選擇搜索模板。 您只能匯入原本從工作區例項匯出的搜尋範本定義。
1. 按一下「匯入」。

## 導出搜索模板定義{#export-a-search-template-definition}

1. 在「全局管理」(Global Administration)頁面的「導出搜索模板」(Export search template definition)下，按一下「全部列出」(List All)。
1. 在搜索模板清單中，選擇要導出的模板。

   >[!NOTE]
   >
   >您可以選取多個範本，但只會匯出最後選取的範本。

1. 按一下「匯出」 ，然後將檔案儲存在電腦上。

## 導入全局設定{#import-global-settings}

1. 在「全局管理」頁的「導入全局設定」下，按一下「選擇檔案」並選擇全局設定檔案。 全域設定檔案必須是XML格式。
1. 按一下「匯入」。

## 導出全局設定{#export-global-settings}

1. 在「全局管理」頁的「導出全局設定」下，按一下「導出」。
1. 將檔案儲存在電腦上。

## 工作區全局設定{#workspace-global-settings}

您可以修改全域設定檔案；但是，您可能希望編輯的唯一設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

工作區全域設定檔案包含下列設定：

### specialRoutes設定{#specialroutes-settings}

*specialRoutes*&#x200B;設定指定工作區中批准和拒絕的特殊路由的屬性。 某些情況下，這些路由的按鈕會顯示在工作區的任務卡上，用戶無需開啟表單即可選擇它們。 您可以修改全局設定檔案中的specialRoutes設定，以添加用於批准和拒絕的自定義名稱，或建立其他路由。

**client_specialRoutes_approve_style:** 位於工作區主題中的樣式名稱，用於標識批准按鈕表徵圖。樣式必須包含已啟用圖示和已停用圖示的值。 要定義自定義按鈕的樣式，必須使用以下模板：
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }`工作區CSS檔案內嵌於workspace-theme.swf檔案中，此檔案位於adobe-workspace-client.ear > adobe-workspace-client.war檔案中。 要更改工作區的外觀，必須重新編譯工作區 — theme.swf檔案。

**client_specialRoutes_deny_names:** Workbench使用者可用來解譯為「deny」的字串種類。字串會區分大小寫。 例如，預設值為deny。 如果Workbench使用者在程式中使用「拒絕」字詞，則無法辨識該字詞。 必須在此設定中添加「拒絕」字，才能自定義路由按鈕並應用樣式。

**client_specialRoutes_deny_style:** 位於工作區主題檔案中的樣式名稱，用於標識拒絕按鈕表徵圖。樣式必須包含已啟用圖示和已停用圖示的值。 要定義自定義按鈕的樣式，必須使用以下模板：
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_approve_names:** Workbench使用者可用來解譯為「核准」的字串種類。 字串會區分大小寫。 例如，預設值為核准。 如果Workbench使用者在處理中使用「核准」字詞，則無法辨識該字詞。 必須在此設定中添加「批准」字，才能自定義路由按鈕並應用樣式。

**client_specialRoutes_names:** 用於從資源檔案中查找自定義字串值的鍵。此設定中的每個條目都需要包含名稱和樣式的值。

### JGroup設定{#jgroup-settings}

只有在您從AdobeLiveCycleES 2.5或更舊版本升級時，才會顯示這些設定。

**server_remoteevents_ClientTimeoutMillisconds:** JGroup等待事件消息的最大時間。不應變更此設定。

**server_remoteevents_ServerTimeoutMillisconds:** 在伺服器上接收JGroup消息的超時。此選項設定從伺服器向客戶端發送消息的延遲。

**server_remoteevents_JChannelConnectionProperties:** 用於在伺服器（RemoteEvent服務在其上處理服務事件）和工作區的所有實例之間通信的JG組的連接屬性。

您可能需要更改多播IP地址(mcastaddr)、多播IP埠(mcastport)和多播資料包的TTL(ipttl)的UDP值。 預設情況下，組播IP地址和埠值是隨機生成的，通常不需要更改值。 不過，如果貴公司有任何與多播IP位址的特定多播範圍相關的網路原則，則您可能需要變更值。

>[!NOTE]
>
>TTL必須大於群集中伺服器之間的網路交換機數；但是，如果值設定得太高，則可能會導致多播資料包進入子網，在子網中將丟棄這些資料包。

不應變更此設定中的其餘屬性。

**server_remoteevents_JGroupName:** 用於遠程事件通信的JGroup的名稱。此值是隨機產生的，以避免叢集中的衝突。 此值不應變更。

如需JGroup和Workspace的其他資訊，請參閱[JGroup和AEM Forms Workspace — 說明](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html)。

### formView settings {#formview-settings}

**client_formView_openFormInFullScreen:** 若要以全螢幕模式顯示工作區中的所有表單，請將此選項設為true。預設情況下，此選項會設為false，且表單不會以全螢幕模式顯示。 請注意，用戶服務包含一個選項，用於以全螢幕模式開啟與任務關聯的文檔。 這可讓您根據每個程式控制顯示。

**client_routes_formViewOnly:** 設為True時，路由不會顯示在工作區的卡片檢視或清單檢視中。預設值為False，表示路由會顯示在卡片檢視和清單檢視中。

### 其他設定{#other-settings}

**client_mimeTypes_openOutsideBrowser:** 將在Workspace瀏覽器實例外部開啟的文檔的MIME類型。如果貴組織的程式需要其他MIME類型，請在此處指定。 預設值為：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** 快取自訂任務用戶介面。

**server_debugLevel:** 請勿變更此設定。

**client_pollingInterval:** 設定Flex Workspace上(JEE上的AEM表單已過時)所使用的輪詢間隔（以秒為單位），以偵測新的和修改的任務。預設為3秒。 這對AEM Forms Workspace無效。

**client_systemContext_name:** 指定自訂名稱（例如公民），以顯示在AEM Forms Workspace中任務附件的「新增者」欄位（位於「附件」標籤中）中。

若要定義自訂名稱：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>對於Demo應用程式，預設顯示名稱為&#x200B;**Citizen**。 對於您建立的自定義應用程式，預設顯示名稱為&#x200B;**系統上下文帳戶**。
>
>**client_idleTimeout:** 當使用者在特定時間內保持非作用中狀態，AEM Forms Workspace工作階段就會過期。要啟用此功能，請向全局設定&lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>添加一個條目。 您可以指定值0以禁用空閒超時。 以秒為單位指定時間量。
