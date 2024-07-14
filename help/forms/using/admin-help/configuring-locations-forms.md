---
title: 設定Forms的位置
description: 瞭解如何設定AEM表單的位置。 您可以指定屬性的檔案位置、表單的位置、種子PDF檔案和快取位置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# 設定Forms的位置 {#configuring-locations-for-forms}

您可以指定屬性的URL、URI和檔案位置，例如Web根目錄、要擷取之表單的位置、PDForm轉換中使用的種子PDF檔案，以及快取位置。

1. 在Administration Console中，按一下「服務> Forms」。
1. 在「位置」下，指定適當的選項。 選項如下所述。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**基礎URL：**&#x200B;影像和指令碼等表單資源所在的基礎URL。 HTML轉換需要此值，其中包含外部相依性的HREF參照，例如影像或指令碼。 其中一個這類指令碼是xfasubset.js，這是HTML表單執行XFA智慧型所需的指令碼。 此值必須是內容根URI的HTTP對等值。

>[!NOTE]
>
>基本URL僅支援HTTP或儲存區域通訊協定。 不支援file:///之類的通訊協定。 如果您需要存取資源（例如自訂CSS或數位簽名URI），請使用適當的API引數值來指定絕對位置。

當相依性路徑為絕對路徑時，會忽略基礎URL值。 否則，相依性路徑會與基礎URL結合。

預設值為空字串。

以下範例指向相同的內容（使用內容根URI和基本URL）：

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI：** Forms Web應用程式的URL。 如果將Forms Web應用程式和使用者端應用程式部署在相同的應用程式伺服器上；系統會使用Forms API Web根URL，您可以將此方塊保留空白。

如果Forms Web應用程式和使用者端應用程式未部署至相同的應用程式伺服器，請在此方塊中提供Forms Web應用程式的URL，如下列範例所示：

`https://<host name>:<port>/FormServer`

其中`host name`和`port`是主控Forms Web應用程式的伺服器的伺服器名稱和連線埠號碼。

預設值為空字串。

**網頁根URI：**&#x200B;應用程式的網頁根。 此值會與透過AEM Forms SDK指定的sTargetURL引數（以相對形式提供sTargetURL時）結合，以建構絕對URL來存取應用程式專屬的網頁內容。

預設值為空字串。

**內容根URI：**&#x200B;從中擷取表單的URI或絕對位置。 此值會與sFormQuery引數（透過API指定）結合，以建構擷取之表單的絕對路徑。 此值可參考可使用HTTP存取的目錄或Web位置。

預設值為空字串。

**XCI組態URI：**&#x200B;找到用於轉譯之XCI檔案的相對或絕對位置。 若為相對值，則假設XCI檔案位在可部署的AEM Forms EAR檔案中。

預設值為 `com/adobe/formServer/PA/pa.xci`。

**字型對應URI：**&#x200B;字型對應檔案的相對或絕對位置。 如需相對值，假設此檔案位在可部署的AEM Forms EAR檔案中。

字型對應檔案可用來建立表單中HTML轉換的自訂字型對應，因此可讓您指定在使用者端電腦無法使用字型時，要取代哪些字型。

預設值為 `com/adobe/formServer/client-font-map.properties`。

下列專案是字型對應檔案中專案的範例：

`Arial=Arial,Helvetica,sans-serif`

**種子PDF檔：**&#x200B;用於PDFForm轉換以最佳化傳遞的初始PDF檔。 種子PDF檔案會指定自訂的PDF檔案（僅包含XFA資料流、影像和字型資源），以附加表單設計和資料。 表單會由Acrobat 7轉譯或更新版本，並套用至PDForm轉換。

預設值為空字串。

**快取位置：**&#x200B;指定Forms磁碟快取的位置。 當您變更此設定時，會重設目前位置的所有現有快取資訊，並在新位置建立新的快取。 選取下列其中一個選項：

**預設位置：**&#x200B;這是預設選取範圍。 選取此選項時，會在從屬於您正在使用的應用程式伺服器的位置建立快取：

* **JBoss：** [JBoss首頁]\server\[安裝型別]\svcdata\FormServer\Cache
* **WebLogic：** [WebLogic首頁]\user_projects\domains\[aem-forms網域名稱]\adobe\[Forms伺服器名稱]\FormServer\Cache
* **WebSphere：** [IBM首頁]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC Temp Directory：**&#x200B;快取是在AEM Forms暫存目錄的子目錄中建立的，該目錄是在管理主控台的[設定] > [核心系統設定] > [設定] > [暫存目錄位置]下指定的。 子目錄名為adobeform_[servername]。

>[!NOTE]
>
>如果您使用暫時清除公用程式，雖然刪除這些目錄不會影響功能，但在建立新快取之前，可能會在短時間內大幅影響效能。 為避免此問題，在清除AEM表單臨時目錄時，請勿刪除這些目錄。
