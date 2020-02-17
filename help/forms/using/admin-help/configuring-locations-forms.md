---
title: 設定表單位置
seo-title: 設定表單位置
description: 瞭解如何設定表單的位置。
seo-description: 瞭解如何設定表單的位置。
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定表單位置 {#configuring-locations-for-forms}

您可以指定屬性的URL、URI和檔案位置，例如Web根目錄、要擷取的表單位置、用於PDFForm轉換的種子PDF檔案，以及快取位置。

1. 在管理控制台中，按一下「服務>表單」。
1. 在「位置」下，指定適當的選項。 以下說明選項。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**** 基本URL:表單資源（例如影像和指令碼）所在的基本URL。 此值是包含外部依賴項（如影像或指令碼）的HREF參考的HTML轉換所必需的。 其中一個指令碼是xfasubset.js，這是HTML表單執行XFA智慧所需的指令碼。 此值必須等同於內容根URI的HTTP。

***注意&#x200B;**:基本URL僅支援HTTP或儲存庫協定。 它不支援file:///等通訊協定。 如果您需要存取資源（例如自訂CSS或數位簽章URI），請使用適當的API參數值來指定絕對位置。*

當相依性路徑為絕對時，會忽略基本URL值。 否則，相依性路徑會與基本URL結合。

預設值為空字串。

下列範例指向相同的內容（使用「內容根URI」和「基本URL」）:

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**** FS web根URI:Forms web應用程式的URL。 如果Forms web應用程式和客戶端應用程式部署在同一應用程式伺服器上，則可以將此框留空；將會使用Forms API web根URL。

如果Forms web應用程式和客戶端應用程式未部署到同一應用程式伺服器，請在此框中提供Forms web應用程式的URL，如本示例所示：

`https://<host name>:<port>/FormServer`

其中 `host name`和 `port` 是代管Forms web應用程式之伺服器的伺服器名稱和埠號。

預設值為空字串。

**** Web根URI:應用程式的Web根目錄。 此值會與sTargetURL參數（當sTargetURL以相對方式提供時）結合，並透過AEM表單SDK指定，以建構絕對URL來存取應用程式特定的Web內容。

預設值為空字串。

**** 內容根URI:從中檢索表單的URI或絕對位置。 此值會與sFormQuery參數（透過API指定）結合，以建構擷取之表單的絕對路徑。 此值可以引用可使用HTTP訪問的目錄或Web位置。

預設值為空字串。

**** XCI配置URI:找到用於渲染的XCI檔案的相對或絕對位置。 對於相對值，會假設XCI檔案位於可部署的AEM表單EAR檔案中。

預設值為 `com/adobe/formServer/PA/pa.xci`。

**** 字型對應URI:字型對應檔案的相對或絕對位置。 若為相對值，則假設此檔案位於可部署的AEM表單EAR檔案中。

字型對應檔案可用來建立自訂的字型對應，以便在表單中轉換HTML，因此您可以指定當用戶端電腦上沒有字型時，要取代的字型。

預設值為 `com/adobe/formServer/client-font-map.properties`。

下列項目是font-mapping檔案中項目的範例：

`Arial=Arial,Helvetica,sans-serif`

**** 種子PDF檔案：用於PDFform轉換的初始PDF檔案，以最佳化傳送。 種子PDF檔案會指定自訂的PDF檔案（僅包含XFA串流、影像和字型資源），並附加表單設計和資料。 表單由Acrobat 7或更新版本轉譯，並套用至PDFForm轉換。

預設值為空字串。

**** 快取位置：指定Forms磁碟快取的位置。 更改此設定時，將重置當前位置的所有現有快取資訊，並在新位置建立新快取。 選擇下列選項之一：

**** 預設位置：這是預設選擇。 選取此選項時，快取會建立在與您所使用之應用程式伺服器相關的位置：

* **** JBoss: [JBoss首]頁\server\[安裝類型]\svcdata\FormServer\Cache
* **** WebLogic: [WebLogic首頁]\user_projects\domains\[aem-forms網域名稱]\adobe\[forms伺服器名稱]\FormServer\Cache
* **** WebSphere: [IBM首頁]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**** LC臨時目錄：快取會建立在AEM forms temp目錄的子目錄中，此目錄會在管理控制台中的「設定>核心繫統設定>組態>臨時目錄位置」下指定。 子目錄名為adobeform_[servername]。

>[!NOTE]
>
>如果您使用臨時清除實用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，它可能會在短時間內顯著影響效能。 若要避免此問題，請勿在清除AEM表單temp目錄時刪除這些目錄。

