---
title: 封裝管理員
description: 瞭解使用封裝管理程式進行AEM封裝管理的基本知識。
feature: Administering
role: Admin
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
solution: Experience Manager, Experience Manager Sites
source-git-commit: c705667e60ccfbc4612ef3212dbe549e6bea66a9
workflow-type: tm+mt
source-wordcount: '3568'
ht-degree: 1%

---


# 封裝管理員 {#working-with-packages}

套件可讓您匯入和匯出存放庫內容。 您可以使用套件來安裝新內容、安裝新功能、在執行個體之間傳輸內容以及備份存放庫內容。

使用封裝管理員，您可以在AEM執行個體和本機檔案系統之間傳輸封裝，以進行開發。

## 什麼是套件？ {#what-are-packages}

套件是一個zip檔案，以檔案系統序列化形式存放庫內容，稱為儲存庫序列化，提供易於使用和編輯的檔案和資料夾表示法。 套件中包含的內容是使用篩選器來定義。

套件也包含儲存庫中繼資訊，包括篩選器定義和匯入組態資訊。 套件中可包含不用於套件提取的其他內容屬性，例如說明、視覺影像或圖示。 這些額外的內容屬性僅供內容套件取用者參考。

>[!NOTE]
>
>套件表示建置套件時內容的目前版本。 其中不包含AEM保留在存放庫中的任何內容舊版本。

## 封裝管理員 {#package-manager}

封裝管理員會管理AEM安裝上的封裝。 在您[指派必要的許可權](#permissions-needed-for-using-the-package-manager)之後，您就可以使用封裝管理員執行各種動作，包括設定、建置、下載和安裝封裝。

### 必要許可權 {#required-permissions}

若要建立、修改、上傳和安裝套件，使用者必須在以下節點上擁有適當的許可權：

* 完整權利，不包括`/etc/packages`上的刪除
* 包含套件內容的節點

>[!CAUTION]
>
>授予封裝的許可權可能會導致敏感資訊洩漏和資料遺失。
>
>若要限制這些風險，強烈建議僅針對專用子樹狀結構授予特定群組許可權。

### 存取封裝管理員 {#accessing}

您可以透過三種方式存取「封裝管理員」：

1. 從AEM主功能表> **工具** > **部署** > **套件**
1. 使用頂端切換器列從[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)
1. 直接存取`http://<host>:<port>/crx/packmgr/`

### 封裝管理員UI {#ui}

封裝管理員分為四個主要功能區域：

* **左側導覽面板** — 此面板可讓您篩選及排序封裝清單。
* **封裝清單** — 這是執行個體上按照左側導覽面板中的選取專案篩選和排序的封裝清單。
* **活動記錄** — 此面板一開始會最小化，並展開以詳細說明封裝管理員的活動，例如建置或安裝封裝時。 「活動記錄」標籤中還有額外的按鈕可執行下列動作：
   * **清除記錄檔**
   * **顯示/隱藏**
* **工具列** — 工具列包含[左側導覽面板]和[封裝清單]的重新整理按鈕，以及搜尋、建立和上傳封裝的按鈕。

![封裝管理員UI](assets/package-manager-ui.png)

按一下左側導覽面板中的選項，會立即篩選封裝清單。

按一下封裝名稱會展開「封裝清單」中的專案，以顯示有關封裝的詳細資訊。

![已展開的封裝詳細資料](assets/package-expand.png)

展開封裝詳細資訊時，可以透過工具列按鈕對封裝執行許多動作。

* [編輯](#edit-package)
* [建置](#building-a-package)
* [重新安裝](#reinstalling-packages)
* [下載](#downloading-packages-to-your-file-system)
* [共用](#share)

**更多**&#x200B;按鈕下方有進一步的動作。

* [刪除](#deleting-packages)
* [適用範圍](#package-coverage)
* [內容](#viewing-package-contents-and-testing-installation)
* [折行](#rewrapping-a-package)
* [其他版本](#other-versions)
* [解除安裝](#uninstalling-packages)
* [測試安裝](#viewing-package-contents-and-testing-installation)
* [驗證](#validating-packages)
* [複寫](#replicating-packages)

### 封裝狀態 {#package-status}

封裝清單中的每個專案都有一個狀態指示器，讓您一眼就知道封裝的狀態。 將游標暫留在狀態上會顯示工具提示，其中包含狀態的詳細資訊。

![封裝狀態](assets/package-status.png)

如果封裝已變更或從未建置，則狀態會以連結的形式顯示，以採取快速動作來重建或安裝封裝。

## 封裝設定 {#package-settings}

套件基本上是一組篩選器，以及根據這些篩選器的存放庫資料。 使用封裝管理員UI，您可以按一下封裝，然後按&#x200B;**編輯**&#x200B;按鈕來檢視封裝的詳細資料，包括下列設定。

* [一般設定](#general-settings)
* [封裝篩選器](#package-filters)
* [套件相依性](#package-dependencies)
* [進階設定](#advanced-settings)
* [套件熒幕擷取畫面](#package-screenshots)

### 一般設定 {#general-settings}

您可以編輯各種封裝設定來定義資訊，例如封裝說明、相依性和提供者詳細資訊。

**封裝設定**&#x200B;對話方塊可在[建立](#creating-a-new-package)或[編輯](#viewing-and-editing-package-information)封裝時，透過&#x200B;**編輯**&#x200B;按鈕使用。 完成任何變更後，按一下[儲存]。****

![編輯封裝對話方塊，一般設定](assets/general-settings.png)

| 欄位 | 說明 |
|---|---|
| 名稱 | 封裝的名稱 |
| 群組 | 若要組織封裝，您可以鍵入新群組的名稱或選取現有群組 |
| 版本 | 用於版本的文字 |
| 說明 | 允許格式化HTML標示的封裝的簡短說明 |
| 縮圖 | 隨套件清單一起出現的圖示 |

#### 封裝縮圖 {#thumbnails}

縮圖提供封裝所包含內容的快速參考視覺表示。 然後這會顯示在封裝清單中，並且有助於輕鬆識別封裝或封裝類別。

以下是用於正式套件的慣例範例：

官方Hotfix

![官方Hotfix縮圖](assets/official-hotfix.png)

擴充功能的正式AEM安裝

![正式AEM安裝或擴充功能縮圖](assets/official-installation.png)

Official Service Pack

![官方AEM Service Pack圖示](assets/official-service-pack.png)

對您的套件使用唯一的圖示。 請勿重複使用Adobe使用的圖示。

### 封裝篩選器 {#package-filters}

篩選器會識別要包含在封裝中的存放庫節點。 **篩選器定義**&#x200B;指定了下列資訊：

* 要包含的內容的&#x200B;**根路徑**
* **根路徑下包含或排除特定節點的**&#x200B;規則

使用&#x200B;**+**&#x200B;按鈕新增規則。 使用&#x200B;**-**&#x200B;按鈕移除規則。

規則會根據其順序套用，因此請使用&#x200B;**向上**&#x200B;和&#x200B;**向下**&#x200B;箭頭按鈕視需要放置規則。

篩選器可包含零個或多個規則。 未定義規則時，套件會包含根路徑下的所有內容。

您可以為封裝定義一或多個篩選定義。 使用多個篩選器以包含來自多個根路徑的內容。

![篩選器索引標籤](assets/edit-filter.png)

建立規則時，您可以定義規則運算式（也稱為regex、regexp或rational運算式），以指定要包含或排除的所有節點。

| 規則型別 | 說明 |
|---|---|
| include | 包含將包含指定目錄中符合規則運算式的所有檔案和資料夾。 包含&#x200B;**將不會**&#x200B;包含指定根路徑下的其他檔案或資料夾。 |
| 排除 | 排除將排除符合規則運算式的所有檔案和資料夾。 |

當您首次[建立封裝時，最常會定義封裝篩選器。](#creating-a-new-package)不過，它們也可在稍後編輯，之後應重新建置封裝，以根據新的篩選定義更新其內容。

>[!TIP]
>
>一個封裝可以包含多個篩選定義，以便來自不同位置的節點可以輕鬆合併到一個封裝中。

>[!TIP]
>
>如需背景資訊，請參閱[Apache Jackrabbit - Workspace篩選器](https://jackrabbit.apache.org/filevault/filter.html)檔案。

### 相依性 {#dependencies}

![相依性索引標籤](assets/dependencies.png)

| 欄位 | 說明 | 範例/詳細資料 |
|---|---|---|
| 測試方式 | 鎖定此封裝為目標或與其相容的產品名稱和版本。 | `6.5` |
| 已修正的問題 | 允許列出此套件所修正之錯誤詳細資料的文字欄位，每行一個錯誤 | - |
| 取決於 | 列出其他必要的套件，以便在安裝時讓目前的套件如預期般執行 | `groupId:name:version` |
| 取代 | 此封裝取代的已棄用封裝清單 | `groupId:name:version` |

### 進階設定 {#advanced-settings}

![進階設定標籤](assets/advanced-settings.png)

| 欄位 | 說明 | 範例/詳細資料 |
|---|---|---|
| 名稱 | 封裝提供者的名稱 | `WKND Media Group` |
| URL | 提供者的URL | `https://wknd.site` |
| 連結 | 提供者頁面的封裝特定連結 | `https://wknd.site/package/` |
| 需要 | 定義安裝套件時是否有任何限制 | **管理員** — 套件只能以管理員許可權安裝&#x200B;<br>**重新啟動** — 安裝套件後必須重新啟動AEM |
| AC 處理 | 指定當匯入封裝時，如何處理封裝中定義的存取控制資訊 | **忽略** — 保留存放庫中的ACL <br>**覆寫** — 覆寫存放庫中的ACL <br>**合併** — 合併這兩組ACL <br>**合併保留** — 將內容中的存取控制項與封裝提供的存取控制項合併，方法是加入內容中不存在的主體的存取控制專案&#x200B;<br>**清除** — 清除ACL |

### 套件熒幕擷取畫面 {#package-screenshots}

您可以將多個熒幕擷取畫面附加至封裝，以提供內容顯示方式的視覺化表示。

![熒幕擷取畫面索引標籤](assets/screenshots.png)

## 封裝動作 {#package-actions}

可以對套件執行許多動作。

### 建立封裝 {#creating-a-new-package}

1. [Access封裝管理員。](#accessing)

1. 按一下&#x200B;**建立封裝**。

   >[!TIP]
   >
   >如果您的執行個體有許多套件，可能會有資料夾結構。 在這種情況下，在建立新封裝之前可以更輕鬆地導覽到所需的目標資料夾。

1. 在&#x200B;**新封裝**&#x200B;對話方塊中，輸入下列欄位：

   ![新封裝對話方塊](assets/new-package-dialog.png)

   * **封裝名稱** — 選取描述性名稱，以協助您（和其他人）輕鬆識別封裝的內容。

   * **版本** — 這是文字欄位，可供您指出版本。 這會附加至封裝名稱，以形成zip檔案的名稱。

   * **群組** — 這是目標群組（或資料夾）名稱。 群組可協助您組織套件。 如果群組尚不存在，則會建立該群組的資料夾。 如果您將群組名稱保留為空白，它會在主封裝清單中建立封裝。

1. 按一下&#x200B;**確定**&#x200B;以建立封裝。

1. AEM會在套裝程式清單頂端列出新套裝程式。

   ![新封裝](assets/new-package.png)

1. 按一下&#x200B;**編輯**&#x200B;以定義[封裝內容。完成編輯設定後，](#package-contents)按一下&#x200B;**儲存**。

1. 您現在可以[建置](#building-a-package)您的封裝。

不一定要在建立套件後立即建置套件。 未建置的套件不包含任何內容，且僅由套件的篩選資料和其他中繼資料組成。

### 建置套件 {#building-a-package}

封裝通常會在您[建立封裝](#creating-a-new-package)的同時建置，但您稍後可以返回建置或重新建置封裝。 如果存放庫中的內容已變更或封裝篩選器已變更，此功能會很有用。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 按一下&#x200B;**建置**。 對話方塊會要求您確認是否要建置封裝，因為任何現有的封裝內容都會被覆寫。

1. 按一下&#x200B;**確定**。 AEM會建置套件，在活動清單中列出新增到套件的所有內容。 完成時，AEM會顯示已建置封裝的確認，並且（當您關閉對話方塊時）會更新封裝清單資訊。

### 編輯封裝 {#edit-package}

將套件上傳到AEM後，您可以修改其設定。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 按一下「編輯&#x200B;**」**，並視需要更新&#x200B;**[封裝設定](#package-settings)**。

1. 按一下&#x200B;**儲存**&#x200B;以儲存。

您可能需要[重建封裝](#building-a-package)，才能根據您所做的變更更新其內容。

### 重新包裝封裝 {#rewrapping-a-package}

建立套件後，即可重新包裝。 重新包裝會變更封裝資訊，而不使用縮圖、說明等，而不會變更封裝內容。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 按一下「編輯&#x200B;**」**，並視需要更新&#x200B;**[封裝設定](#package-settings)**。

1. 按一下&#x200B;**儲存**&#x200B;以儲存。

1. 按一下「**更多** > **重新換行**」，對話方塊將會要求確認。

### 檢視其他封裝版本 {#other-versions}

由於每個封裝版本都會以任何其他封裝的形式出現在清單中，因此「封裝管理員」可以找到所選封裝的其他版本。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 按一下&#x200B;**更多** > **其他版本**，就會開啟對話方塊，其中包含相同封裝的其他版本清單，以及狀態資訊。

### 檢視封裝內容和測試安裝 {#viewing-package-contents-and-testing-installation}

建立套件後，您可以檢視內容。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 若要檢視內容，請按一下&#x200B;**更多** > **內容**，封裝管理員會在活動記錄檔中列出封裝的整個內容。

   ![封裝內容](assets/package-contents.png)

1. 若要執行安裝練習，請按一下[其他] **** > [測試安裝] **，並在活動記錄檔中報告封裝管理程式所取得的結果，如同已執行安裝一樣。**

   ![測試安裝](assets/test-install.png)

### 正在將封裝下載至您的檔案系統 {#downloading-packages-to-your-file-system}

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 按一下封裝詳細資訊區域中的&#x200B;**下載**&#x200B;按鈕或封裝的連結檔案名稱。

1. AEM會將套件下載到您的電腦。

### 共用封裝 {#share}

Package Share是一項集中式公用服務，可分發內容套件。 封裝共用已由[Software Distribution](#software-distribution)取代，而且此按鈕不再有效。

### 從您的檔案系統上傳套件 {#uploading-packages-from-your-file-system}

1. [Access封裝管理員。](#accessing)

1. 選取要將封裝上傳到的群組資料夾。

1. 按一下&#x200B;**上傳封裝**&#x200B;按鈕。

1. 提供關於上傳之封裝的必要資訊。

   ![封裝上傳對話方塊](assets/package-upload-dialog.png)

   * **封裝** — 使用&#x200B;**瀏覽……**&#x200B;按鈕，從您的本機檔案系統選取所需的封裝。
   * **強制上傳** — 如果已有同名的套件，此選項會強制上傳並覆寫現有的套件。

1. 按一下[確定]****&#x200B;即可上傳選取的封裝，並相應地更新封裝清單。

封裝內容現在存在於AEM上，但若要讓內容可供使用，請確定[安裝封裝](#installing-packages)。

### 正在驗證封裝 {#validating-packages}

由於套件可以修改現有內容，因此在安裝前驗證這些變更通常會有幫助。

#### 驗證選項 {#validation-options}

封裝管理員可以執行下列驗證：

* [OSGi套件匯入](#osgi-package-imports)
* [覆蓋](#overlays)
* [ACL](#acls)

##### 驗證 OSGi 封裝匯入 {#osgi-package-imports}

**檢查的內容**

此驗證會檢查所有JAR檔案（OSGi套裝）的套件，擷取其`manifest.xml` （其中包含所述OSGi套裝所依賴的版本化相依性），並以正確版本驗證AEM執行個體匯出所述相依性。

**報告方式**

任何無法由AEM執行個體滿足的版本化相依性都會列在「封裝管理員」的「活動記錄」中。

**錯誤狀態**

如果不滿足相依性，則具有這些相依性的套件中的OSGi套件組合將不會啟動。 這會導致中斷的應用程式部署，因為依賴未啟動OSGi套件組合的任何專案都將無法正常運作。

**錯誤解決**

若要解決因未滿足的OSGi套件組合所導致的錯誤，必須調整包含未滿足之匯入的套件組合中的相依性版本。

##### 驗證覆蓋 {#overlays}

**檢查的內容**

此驗證會決定要安裝的套件是否包含已在目的地AEM執行個體中覆蓋的檔案。

例如，假設在`/apps/sling/servlet/errorhandler/404.jsp`有一個現有的覆蓋，一個包含`/libs/sling/servlet/errorhandler/404.jsp`的封裝，因此它將變更`/libs/sling/servlet/errorhandler/404.jsp`的現有檔案。

**如何匯出**

任何此類覆蓋圖會在「封裝管理員」的「活動記錄」中說明。

**錯誤狀態**

錯誤狀態表示套件正嘗試部署已覆蓋的檔案，因此套件中的變更將會被覆蓋覆寫（因此「隱藏」）且不會生效。

**錯誤解決**

若要解決此問題，`/apps`中覆蓋檔案的維護者必須檢閱`/libs`中覆蓋檔案的變更，並視需要將變更合併至覆蓋( `/apps`)，然後重新部署覆蓋檔案。

>[!NOTE]
>
>如果覆蓋的內容已正確併入覆蓋檔案中，則驗證機制無法調解。 因此，即使進行了必要的變更，此驗證仍會繼續報告衝突。

##### 驗證 ACL {#acls}

**檢查的內容**

此驗證會檢查要新增哪些許可權、如何處理這些許可權（合併/取代），以及目前的許可權是否會受到影響。

**報告方式**

在「封裝管理員」的「活動記錄」中說明這些許可權。

**錯誤狀態**

無法提供明確的錯誤。 驗證只會指出安裝套件是否會新增或影響任何新的ACL許可權。

**錯誤解決**

使用驗證提供的資訊，可以在CRXDE中檢閱受影響的節點，並且可以根據需要在套件中調整ACL。

>[!CAUTION]
>
>根據最佳實務，建議套件不要影響AEM提供的ACL，因為這樣可能會導致非預期的行為。

#### 正在執行驗證 {#performing-validation}

套件的驗證可以透過兩種不同的方式完成：

* [透過封裝管理員UI](#via-package-manager)
* [透過HTTPPOST請求，例如使用cURL](#via-post-request)

上傳套件後但安裝套件前應一律進行驗證。

##### 透過封裝管理程式進行封裝驗證 {#via-package-manager}

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 若要驗證封裝，請按一下&#x200B;**更多** > **驗證**，

1. 在隨後出現的模型對話方塊中，使用核取方塊選取驗證型別，並按一下&#x200B;**驗證**&#x200B;開始驗證。

1. 接著會執行選取的驗證，結果會顯示在「封裝管理員」的「活動記錄」中。

##### 透過HTTPPOST要求進行套件驗證 {#via-post-request}

Post請求會採用下列形式。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

`type`引數可以是任何以逗號分隔的無順序清單，包含：

* `osgiPackageImports`
* `overlays`
* `acls`

如果未明確傳遞，`type`的值預設為`osgiPackageImports`。

使用cURL時，執行類似下列的陳述式：

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

透過POST要求驗證時，回應會以JSON物件的形式傳回。

### 檢視封裝涵蓋範圍 {#package-coverage}

套件是由其篩選器所定義。 您可以讓「封裝管理員」將封裝的篩選器套用至您現有的存放庫內容，以顯示封裝的篩選器定義所涵蓋的存放庫內容。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟封裝詳細資訊。

1. 按一下&#x200B;**更多** > **涵蓋範圍**。

1. 涵蓋範圍詳細資訊會列在活動記錄中。

### 安裝套件 {#installing-packages}

上傳封裝只會將封裝內容新增到存放庫，但無法存取。 安裝上傳的套件以使用套件的內容。

>[!CAUTION]
>
>安裝套件可能會覆寫或刪除現有內容。 只有在您確定套件不會刪除或覆寫您需要的內容時，才上傳套件。

在安裝套件之前，封裝管理員會自動建立包含將被覆寫內容的快照套件。 如果您解除安裝套裝軟體，將會重新安裝此快照。

>[!CAUTION]
>
>* 如果您正在安裝數位資產，您必須：
>  首先，停用WorkflowLauncher。
>  使用OSGi控制檯的元件選單選項來停用
>  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* 接著，安裝完成後，重新啟用WorkflowLauncher。
>
>停用WorkflowLauncher可確保Assets Importer架構不會（無意中）在安裝時操控資產。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，從封裝清單開啟您要安裝的封裝詳細資訊。

1. 按一下專案詳細資料中的&#x200B;**Install**&#x200B;按鈕或套件狀態中的&#x200B;**Install**&#x200B;連結。

1. 對話方塊將會要求確認，並允許指定其他選項。

   * **僅擷取** — 僅擷取封裝，因此不會建立快照，因此無法解除安裝
   * **儲存臨界值** — 觸發自動儲存之前的暫時節點數目（如果您遇到並行修改例外狀況會增加）
   * **擷取子封裝** — 啟用自動擷取子封裝
   * **存取控制處理** — 指定安裝封裝時，封裝中定義的存取控制資訊的處理方式（選項與[進階封裝設定](#advanced-settings)相同）
   * **相依性處理** — 指定安裝期間相依性的處理方式

1. 按一下&#x200B;**安裝**。

1. 活動記錄檔會詳細說明安裝進度。

安裝完成並成功後，封裝清單會更新，封裝狀態中會出現&#x200B;**已安裝**&#x200B;這個字。

### 重新安裝套件 {#reinstalling-packages}

重新安裝封裝會在已安裝的封裝上執行相同的步驟，這些封裝會在[最初安裝封裝時處理。](#installing-packages)

### 以檔案系統為基礎的上傳與安裝 {#file-system-based-upload-and-installation}

安裝套件時，您可以完全放棄套件管理員。 AEM可以偵測位於主機本機檔案系統特定位置的套件，並自動上傳及安裝這些套件。

1. 在AEM安裝資料夾下，jar和`license.properties`檔案旁邊有`crx-quicksart`資料夾。 在`crx-quickstart`下建立名為`install`的資料夾，產生路徑`<aem-home>/crx-quickstart/install`。

1. 在此資料夾中，新增您的封裝。 它們會自動上傳並安裝在您的執行個體上。

1. 上傳和安裝完成後，您可以在封裝管理員中檢視套件，就像您已使用封裝管理員UI進行安裝一樣。

如果執行個體正在執行，當您將其新增至封裝至`install`資料夾時，上傳和安裝會立即開始

如果執行個體未執行，則會在啟動時依字母順序安裝置於`install`資料夾中的封裝。

### 解除安裝套件 {#uninstalling-packages}

解除安裝套裝軟體會將儲存區域的內容還原成安裝前由「套裝軟體管理員」自動建立的快照。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，開啟您要從封裝清單解除安裝的封裝詳細資料。

1. 按一下&#x200B;**更多** > **解除安裝**，從存放庫中移除此套件的內容。

1. 對話方塊將會要求確認並列出進行的所有變更。

1. 套裝軟體會被移除並套用快照。 處理程式的進度會顯示在活動記錄檔中。

### 刪除封裝 {#deleting-packages}

刪除封裝只會從「封裝管理員」刪除其詳細資料。 如果已經安裝此套件，則不會刪除安裝的內容。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，開啟您要從封裝清單中刪除之封裝的封裝詳細資訊。

1. 封裝管理員會要求您確認要刪除封裝。 按一下&#x200B;**確定**&#x200B;以確認刪除。

1. 套件資訊會遭到刪除，而詳細資訊會回報於活動記錄中。

### 正在複製封裝 {#replicating-packages}

複製套件的內容以將其安裝在發佈執行個體上。

1. [Access封裝管理員。](#accessing)

1. 按一下封裝名稱，開啟您要從封裝清單復寫之封裝的詳細資訊。

1. 按一下&#x200B;**更多** > **復寫**。

1. 會複製套件，並在活動記錄中報告詳細資訊。

## Software Distribution {#software-distribution}

AEM套件可用於在AEM環境中建立和共用內容。

[Software Distribution](https://downloads.experiencecloud.adobe.com)是一項集中式服務，旨在簡化AEM封裝的搜尋和下載。

如需詳細資訊，請參閱[軟體發佈檔案。](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

>[!NOTE]
>
>Package Manager目前並未與Software Distribution整合，因為它與先前的Package Share服務整合。 因此，「封裝管理員」中的「封裝共用」的共用按鈕和其他連結不再運作。 解決方案是將套件下載到您的本機磁碟。
