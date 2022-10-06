---
title: 配置Forms位置
seo-title: Configuring locations for Forms
description: 了解如何為Forms設定位置。
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# 配置Forms位置 {#configuring-locations-for-forms}

您可以指定屬性的URL、URI和檔案位置，如Web根、要檢索的表單位置、PDFForm轉換中使用的種子PDF檔案，以及快取位置。

1. 在管理主控台中，按一下「服務> Forms」。
1. 在「位置」下，指定適當的選項。 選項如下所述。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**基本URL:** 表單資源（例如影像和指令碼）所在的基本URL。 對於包含外部相依性（如影像或指令碼）的HREF參考的HTML轉換，此值是必需的。 其中一個指令碼是xfasubset.js，這是HTML表單執行XFA智慧所需的指令碼。 此值必須等同於內容根URI的HTTP。

>[!NOTE]
>
>基本URL僅支援HTTP或存放庫通訊協定。 不支援file:///等通訊協定。 如果您需要存取資源，例如自訂CSS或數位簽章URI，請使用適當的API參數值來指定絕對位置。

當相依性路徑為絕對路徑時，會忽略基本URL值。 否則，相依性路徑會與基礎URL結合。

預設值為空字串。

以下範例指向相同的內容（使用「內容根URI」和「基本URL」）:

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI:** Forms Web應用程式的URL。 如果Forms Web應用程式和客戶端應用程式部署在同一應用程式伺服器上，則可將此框留空；將會使用Forms API網頁根URL。

如果Forms Web應用程式和用戶端應用程式未部署至相同的應用程式伺服器，請在此方塊中提供Forms Web應用程式的URL，如以下範例所示：

`https://<host name>:<port>/FormServer`

其中 `host name`和 `port` 是托管Forms Web應用程式之伺服器的伺服器名稱和埠號。

預設值為空字串。

**Web根URI:** 應用程式的Web根目錄。 此值會與sTargetURL參數（當sTargetURL以相對方式提供時）結合，並透過AEM表單SDK指定，以建構絕對URL來存取應用程式專用的Web內容。

預設值為空字串。

**內容根URI:** 從中檢索表單的URI或絕對位置。 此值會與透過API指定的sFormQuery參數結合，以建構擷取之表單的絕對路徑。 此值可參考使用HTTP存取的目錄或Web位置。

預設值為空字串。

**XCI配置URI:** 找到用於呈現的XCI檔案的相對或絕對位置。 對於相對值，假設XCI檔案位於可部署的AEM forms EAR檔案中。

預設值為 `com/adobe/formServer/PA/pa.xci`。

**字型映射URI:** 字型映射檔案的相對或絕對位置。 對於相對值，假定此檔案位於可部署的AEM Forms EAR檔案中。

字型映射檔案用於為表單中的HTML轉換建立自定義字型映射，因此允許您指定當客戶端電腦上沒有字型時將替換的字型。

預設值為 `com/adobe/formServer/client-font-map.properties`。

以下條目是字型映射檔案中條目的示例：

`Arial=Arial,Helvetica,sans-serif`

**種子PDF檔案：** 用於PDFForm轉換以最佳化傳送的初始PDF檔案。 種子PDF檔案會指定附加於表單設計和資料的自訂PDF檔案（僅包含XFA資料流、影像和字型資源）。 表單由Acrobat 7或更新版本轉譯，並套用至PDFForm轉換。

預設值為空字串。

**快取位置：** 指定Forms磁碟快取的位置。 更改此設定時，當前位置的所有現有快取資訊都會重置，並在新位置建立新快取。 選取下列其中一個選項：

**預設位置：** 這是預設選取項目。 選中此選項時，快取將建立在與所使用的應用程式伺服器相關的位置：

* **JBoss:** [JBoss首頁]\server\[安裝類型]\svcdata\FormServer\Cache
* **WebLogic:** [WebLogic首頁]\user_projects\domains\[aem-forms網域名稱]\adobe\[forms伺服器名稱]\FormServer\Cache
* **WebSphere:** [IBM首頁]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC臨時目錄：** 快取建立在AEM Forms臨時目錄的子目錄中，該子目錄在管理控制台的「設定>核心繫統設定>配置>臨時目錄的位置」下指定。 子目錄名為adobeform_[servername].

>[!NOTE]
>
>如果您使用臨時清除實用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，它會在短時間內大幅影響效能。 要避免此問題，清除AEM表單臨時目錄時，請勿刪除這些目錄。
