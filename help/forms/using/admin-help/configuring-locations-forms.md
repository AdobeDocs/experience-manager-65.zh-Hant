---
title: 配置Forms的位置
seo-title: Configuring locations for Forms
description: 瞭解如何配置Forms的位置。
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

# 配置Forms的位置 {#configuring-locations-for-forms}

可以指定屬性的URL、URI和檔案位置，如Web根、要檢索的表單的位置、PDFForm轉換中使用的種子PDF檔案以及快取位置。

1. 在管理控制台中，按一下「服務」>「Forms」。
1. 在「位置」(Locations)下，指定相應的選項。 下面介紹了這些選項。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**基本URL:** 表單資源（如影像和指令碼）所在的基URL。 此值是HTML轉換(包括對外部依賴項（如影像或指令碼）的HREF引用)所必需的。 此類指令碼之一是xfasubset.js，這是HTML表單執行XFA智慧所必需的。 此值必須等效於內容根URI的HTTP。

>[!NOTE]
>
>基本URL僅支援HTTP或儲存庫協定。 它不支援file:///等協定。 如果需要訪問自定義CSS或數字簽名URI等資源，請使用相應的API參數值指定絕對位置。

當依賴關係路徑為絕對路徑時，將忽略基URL值。 否則，依賴關係路徑與基本URL組合。

預設值為空字串。

以下示例指向相同的內容（使用內容根URI和基URL）:

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI:** FormsWeb應用程式的URL。 如果FormsWeb應用程式和客戶端應用程式部署在同一應用伺服器上，則可以將此框留空；將使用FormsAPI web根URL。

如果FormsWeb應用程式和客戶端應用程式未部署到同一應用程式伺服器，請在此框中提供FormsWeb應用程式的URL，如本示例所示：

`https://<host name>:<port>/FormServer`

位置 `host name`和 `port` 是承載FormsWeb應用程式的伺服器的伺服器名稱和埠號。

預設值為空字串。

**Web根URI:** 應用程式的Web根目錄。 此值與通過表單SDK指定的sTargetURL參數（當sTargetURL以相對方式提供時）組合AEM，以構建絕對URL來訪問特定於應用程式的Web內容。

預設值為空字串。

**內容根URI:** 從中檢索表單的URI或絕對位置。 此值與通過API指定的sFormQuery參陣列合，以構建檢索到的表單的絕對路徑。 此值可以引用HTTP可訪問的目錄或Web位置。

預設值為空字串。

**XCI配置URI:** 找到用於呈現的XCI檔案的相對或絕對位置。 對於相對值，假定XCI檔案駐留在可部署表單AEMEAR檔案中。

預設值為 `com/adobe/formServer/PA/pa.xci`。

**字型映射URI:** 字型映射檔案的相對或絕對位置。 對於相對值，假定此檔案駐留在可部署表單AEMEAR檔案中。

字型映射檔案用於建立自定義字型映射以在表單中進行HTML轉換，因此允許您指定在客戶端電腦上沒有字型時將替換哪些字型。

預設值為 `com/adobe/formServer/client-font-map.properties`。

以下條目是font-mapping檔案中條目的示例：

`Arial=Arial,Helvetica,sans-serif`

**種子PDF檔案：** 用於PDFForm轉換以優化傳遞的初始PDF檔案。 種子PDF檔案指定附加了表單設計和資料的自定義PDF檔案（僅包含XFA流、影像和字型資源）。 表單由Acrobat 7或更高版本渲染，並適用於PDFForm轉換。

預設值為空字串。

**快取位置：** 指定Forms磁碟快取的位置。 更改此設定時，將重置當前位置的所有現有快取資訊，並在新位置建立新快取。 選擇以下選項之一：

**預設位置：** 這是預設選擇。 選擇此選項後，將在依賴於正在使用的應用程式伺服器的位置建立快取：

* **JBoss:** [JBoss首頁]\server\[安裝類型]\svcdata\FormServer\Cache
* **WebLogic:** [WebLogic首頁]\user_projects\domains\[aem-forms域名]\adobe\[forms伺服器名]\FormServer\Cache
* **WebSphere:** [IBM家]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC臨時目錄：** 快取是在表單臨時目錄的子AEM目錄中建立的，該目錄在管理控制台的「設定」>「核心繫統設定」>「配置」>「臨時目錄的位置」下指定。 子目錄名為adobeform_[伺服器名稱]。

>[!NOTE]
>
>如果您使用的是臨時清洗實用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，它會在短時間內顯著影響效能。 要避免此問題，請在清除表單臨時目錄時AEM不要刪除這些目錄。
