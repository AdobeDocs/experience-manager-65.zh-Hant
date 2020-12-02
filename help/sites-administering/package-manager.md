---
title: 如何使用套件
seo-title: 如何使用套件
description: 瞭解在AEM中使用套件的基本知識。
seo-description: 瞭解在AEM中使用套件的基本知識。
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 03967fcdc9685c9a8bf1dead4bd5e389603ff91b
workflow-type: tm+mt
source-wordcount: '3934'
ht-degree: 1%

---


# 如何使用包{#how-to-work-with-packages}

軟體包可以導入和導出儲存庫內容。 例如，您可以使用軟體包來安裝新功能、在實例之間傳輸內容，以及備份儲存庫內容。

可從以下頁訪問和／或維護包：

* [Package Manager](#package-manager)，您可使用它來管理本機AEM例項中的封裝。

* [軟體散發](#software-distribution)(Software Distribution)，此集中式伺服器同時持有公開可用的套件和您公司專用的套件。公開套件可包含修補程式、新功能、檔案等。

您可以在軟體包管理器、軟體分發和檔案系統之間傳輸軟體包。

## 什麼是套件？{#what-are-packages}

軟體包是以檔案系統序列化（稱為「vault」序列化）形式保存儲存庫內容的zip檔案。 這提供了簡單易用和編輯的檔案和檔案夾表示法。

套件包含使用篩選器選取的頁面內容和專案相關內容。

軟體包還包含保險儲存元資訊，包括過濾器定義和導入配置資訊。 封裝中可包含其他內容屬性（不用於封裝擷取），例如說明、視覺影像或圖示；這些屬性僅用於內容包消費者和資訊用途。

>[!NOTE]
>
>套件代表建立套件時的內容目前版本。 它們不包含AEM保留在儲存庫中的任何舊版內容。

您可以對包執行以下操作或對包執行以下操作：

* 建立新套件；根據需要定義包設定和篩選器
* 預覽套件內容（建立前）
* 建立套件
* 查看包資訊
* 檢視套件內容（建立後）
* 修改現有包的定義
* 重建現有包
* 重新包裝套件
* 從AEM下載套件至您的檔案系統
* 從您的檔案系統將套件上傳至您的本機AEM例項
* 安裝前驗證封裝內容
* 執行乾式運行安裝
* 安裝套件（AEM不會在上傳後自動安裝套件）
* 刪除包
* 從「軟體散發程式庫」下載套件，例如修補程式
* 將套件上傳至「軟體散發程式庫」的公司內部區段

## 軟體包資訊{#package-information}

包定義由各種類型的資訊組成：

* [套件設定](#package-settings)
* [封裝篩選器](#package-filters)
* [封裝螢幕擷取](#package-screenshots)
* [封裝圖示](#package-icons)

### 包設定{#package-settings}

您可以編輯各種「包設定」以定義包描述、相關錯誤、依賴項和提供程式資訊等方面。

當[建立](#creating-a-new-package)或[編輯](#viewing-and-editing-package-information)軟體包時，**軟體包設定**&#x200B;對話框可通過&#x200B;**編輯**&#x200B;按鈕使用，並提供三個頁籤進行配置。 進行任何更改後，按一下&#x200B;**OK**&#x200B;保存這些更改。

![封裝編輯](assets/packagesedit.png)

| **欄位** | **說明** |
|---|---|
| 名稱 | 包的名稱。 |
| 群組 | 要向其添加包的組的名稱，用於組織包。 鍵入新組的名稱，或選擇現有組。 |
| 版本 | 用於自訂版本的文字。 |
| 說明 | 套件的簡短說明。 HTML標籤可用於格式化。 |
| 縮圖 | 隨包清單一起顯示的表徵圖。 按一下「瀏覽」以選取本機檔案。 |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>欄位</strong></th>
   <th><strong>說明</strong></th>
   <th><strong>格式／範例</strong></th>
  </tr>
  <tr>
   <td>名稱</td>
   <td>提供程式的名稱。</td>
   <td><em>AEM Geometrixx<br /> </em></td>
  </tr>
  <tr>
   <td>URL</td>
   <td>提供者的URL。</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>連結</td>
   <td>包特定於提供程式頁的連結。</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>需要<br /> </td>
   <td>
    <ul>
     <li>管理員：選擇具有管理員權限的帳戶只能安裝套件的時間。</li>
     <li>重新啟動：選擇安裝軟體包後需要重新啟動伺服器的時間。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AC 處理</td>
   <td><p>指定導入包時如何處理包中定義的訪問控制資訊：</p>
    <ul>
     <li><strong>忽略</strong></li>
     <li><strong>覆寫</strong></li>
     <li><strong>合併</strong></li>
     <li><strong>清除</strong></li>
     <li><strong>MergePreserve</strong></li>
    </ul> <p>預設值為<strong>Ignore</strong>。</p> </td>
   <td>
    <ul>
     <li><strong>忽略</strong> -保留儲存庫中的ACL</li>
     <li><strong>覆寫</strong> -覆寫儲存庫中的ACL</li>
     <li><strong>合併</strong> -合併兩組ACL</li>
     <li><strong>清除</strong> -清除ACL</li>
     <li><strong>合併保留</strong> -通過添加內容中不存在的承擔者的訪問控制項，將內容中的訪問控制與隨包提供的訪問控制合併</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![包依賴性](assets/packagesdependencies.png)

| **欄位** | **說明** | **格式／範例** |
|---|---|---|
| 已測試 | 此套件的產品名稱和版本已定位至或與相容。 | *AEM6* |
| 修正錯誤／問題 | 一個文本欄位，允許您列出使用此軟體包修復的錯誤的詳細資訊。 請將每個錯誤列在單獨的行上。 | bug-nr摘要 |
| 取決於 | 列出當需要其它包時，需要遵守的相依性資訊，以便使當前包按預期運行。 此欄位在使用修補程式時很重要。 | groupId:name:version |
| 取代 | 此包替換的已過時包的清單。 在安裝之前，請檢查此軟體包是否包含過時軟體包中的所有必要內容，以便不覆蓋任何內容。 | groupId:name:version |

### 包過濾器{#package-filters}

篩選器標識要包含在包中的儲存庫節點。 **過濾器定義**&#x200B;指定以下資訊：

* 要包含的內容的&#x200B;**根路徑**。
* **包** 含或排除根路徑下的特定節點的規則。

篩選器可包含零個或多個規則。 如果未定義規則，則套件會包含根路徑下的所有內容。

您可以為套件定義一或多個篩選定義。 使用多個篩選器來包含來自多個根路徑的內容。

![chlimage_1-189](assets/chlimage_1-109.png)

下表說明這些規則並提供範例：

<table>
 <tbody>
  <tr>
   <th> 規則類型</th>
   <th>說明 </th>
   <th>範例 </th>
  </tr>
  <tr>
   <td> 加入</td>
   <td>您可以定義路徑，或使用規則運算式來指定要包括的所有節點。<br /> <br /> 包含目錄將：
    <ul>
     <li>包括該目錄<i>和</i>中該目錄中的所有檔案和資料夾（即整個子樹）</li>
     <li><strong>不</strong> 包含指定根路徑下的其他檔案或資料夾</li>
    </ul> </td>
   <td>/libs/sling/install(/)。*)? </td>
  </tr>
  <tr>
   <td> 排除</td>
   <td>您可以指定路徑或使用規則運算式來指定要排除的所有節點。<br /> <br /> 排除目錄將排除該目 <i></i> 錄以及該目錄中的所有檔案和資料夾（即整個子樹）。<br /> </td>
   <td>/libs/wcm/foundation/components(/)。*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>一個套件可包含多個篩選定義，因此不同位置的節點可輕鬆結合為一個套件。

在您首次[建立包](#creating-a-new-package)時最常定義包過濾器，但以後也可以編輯它們（在此之後應重建包）。

### 包截屏{#package-screenshots}

您可將螢幕擷取畫面附加至您的套件，以視覺化方式呈現內容的外觀；例如，提供新功能的螢幕擷取。

### 包表徵圖{#package-icons}

您也可以將圖示附加至套件，以提供套件所含內容的快速參考視覺呈現。 然後，這將顯示在包清單中，可幫助您輕鬆標識包或包類。

由於套件可包含圖示，下列慣例用於正式套件：

>[!NOTE]
>
>為避免混淆，請為您的套件使用描述性圖示，而不要使用其中一個官方圖示。

正式的修補程式套件：

![](do-not-localize/chlimage_1-28.png)

正式的AEM安裝或擴充功能套件：

正式功能套件：

![](do-not-localize/chlimage_1-29.png)

## 包管理器{#package-manager}

Package Manager會管理您本機AEM安裝上的套件。 為[分配了必要的權限](#permissions-needed-for-using-the-package-manager)後，您可以使用包管理器執行各種操作，包括配置、構建、下載和安裝包。 要配置的關鍵元素包括：

* [套件設定](#package-settings)
* [封裝篩選器](#package-filters)

### 使用包管理器{#permissions-needed-for-using-the-package-manager}所需的權限

若要授與使用者建立、修改、上傳和安裝套件的權利，您必須在下列位置為使用者提供適當的權限：

* **/etc/packages** （完全權限不包括刪除）
* 包含包內容的節點

有關更改權限的說明，請參閱[設定權限](/help/sites-administering/security.md#setting-page-permissions)。

### 建立新包{#creating-a-new-package}

要建立新包定義，請執行以下操作：

1. 在「AEM歡迎」畫面上，按一下「套件」(**Packages)**(或從「工具」(**Tools)**&#x200B;主控台連按兩下「套件」(Packages)**)。**

1. 然後選擇&#x200B;**Package Manager**。
1. 按一下「建立包」。****

   >[!NOTE]
   >
   >如果實例包含許多包，則可能存在資料夾結構，以便在建立新包之前導航到所需的目標資料夾。

1. 在對話方塊中：

   ![packagagesnew](assets/packagesnew.png)

   輸入：

   * **群組名稱**

      目標群組（或資料夾）名稱。 群組旨在協助您組織套件。

      如果組不存在，將為其建立資料夾。 如果將組名留空，則它將在主包清單（「首頁」>「包」）中建立包。

   * **封裝名稱**

      新包的名稱。 選擇描述性名稱，以協助您（和其他人）輕鬆識別套件內容。

   * **版本**

      用於表示版本的文本欄位。 這將附加至套件名稱，以形成zip檔案的名稱。
   按一下&#x200B;**OK**&#x200B;建立軟體包。

1. AEM會在適當的群組檔案夾中列出新的套件。

   ![packagesitem](assets/packagesitem.png)

   按一下要開啟的表徵圖或包名稱。

   ![packagetemclicked](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >如有需要，您可在稍後階段返回本頁面。

1. 按一下&#x200B;**編輯**&#x200B;以編輯[包設定](#package-settings)。

   在這裡，您可以新增資訊和／或定義特定設定；例如，這些錯誤包括說明、[表徵圖](#package-icons)、相關錯誤和添加提供程式詳細資訊。

   完成編輯設定後，按一下「確定」。****

1. 視需要將&#x200B;**[Screenshots](#package-screenshots)**&#x200B;新增至套件。 建立套件時，有一個例項可供使用，若有需要，請使用&#x200B;**Package Screepth** from sidekick新增更多。

   在&#x200B;**螢幕擷取**&#x200B;區域中按兩下影像元件，新增影像，然後按一下&#x200B;**確定**，以新增實際影像。

1. 定義&#x200B;**[Package Filters](#package-filters)**，方法是從側鍵拖曳&#x200B;**Filter Definition**&#x200B;的例項，然後連按兩下以開啟以進行編輯：

   ![packagesfilter](assets/packagesfilter.png)

   指定下列設定：

   * **根路**
徑要封裝的內容；這可以是子樹的根。
   * **RulesRules**
是可選的；對於簡單的套件定義，不需要指定包含或排除規則。

      如有需要，您可以定義&#x200B;[**Include**&#x200B;或&#x200B;**Exclude**&#x200B;規則](#package-filters)，以精確定義套件內容。

      使用&#x200B;**+**&#x200B;符號新增規則，或使用&#x200B;**-**&#x200B;符號移除規則。 規則會根據其順序套用，以使用&#x200B;**Up**&#x200B;和&#x200B;**Down**&#x200B;按鈕，視需要定位規則。
   然後按一下「確定」以儲存篩選。****

   >[!NOTE]
   >
   >您可以視需要使用任意數量的篩選定義，但必須小心確保這些定義不發生衝突。 使用&#x200B;**預覽**&#x200B;確認包內容。

1. 要確認軟體包將包含的內容，可以使用&#x200B;**預覽**。 這會執行建立程式的乾式執行，並列出實際建立時要新增至封裝的所有項目。
1. 您現在可以[Build](#building-a-package)您的套件。

   >[!NOTE]
   >
   >目前並非必要建立套件，而是可在稍後的時間點完成。

### 生成軟體包{#building-a-package}

軟體包通常與[建立軟體包定義](#creating-a-new-package)同時構建，但您可以在稍後返回生成或重建軟體包。 如果儲存庫中的內容已更改，則此功能非常有用。

>[!NOTE]
>
>在建立套件之前，預覽套件的內容會很有用。 若要這麼做，請按一下「預覽」。****

1. 從&#x200B;**Package Manager**（按一下包表徵圖或名稱）開啟包定義。

1. 按一下&#x200B;**Build**。 對話方塊會要求您確認您確實要建立套件。

   >[!NOTE]
   >
   >當您重建包時，當將覆寫包內容時，這特別重要。

1. 按一下&#x200B;**「確定」**。AEM將建立套件，並列出新增至套件的所有內容。 完成時，AEM會顯示已建立套件的確認，並（當您關閉對話方塊時）更新套件清單資訊。

### 重新包裝{#rewrapping-a-package}軟體包

在建立套件後，如有需要，可重新包裝它。

重新包裝會變更封裝資訊- *而不會變更封裝內容。*&#x200B;套件資訊是縮圖、說明等，換言之，您可使用&#x200B;**套件設定**&#x200B;對話方塊編輯的一切（以開啟此按一下&#x200B;**編輯**）。

重新包裝的主要使用案例是準備套件時。 例如，您可能已有現有的套件，並決定與其他人共用。 您想要新增縮圖並新增說明。 您可以重新建立整個套件，而不需使用其所有功能（這可能需要一些時間，並承擔套件不再與原始套件相同的風險），只要重新包住它，然後新增縮圖和說明即可。

1. 從&#x200B;**Package Manager**（按一下包表徵圖或名稱）開啟包定義。

1. 按一下「編輯&#x200B;****」，並視需要更新「封裝設定」。 ](#package-settings)****[&#x200B;按一下&#x200B;**確定**&#x200B;保存。

1. 按一下&#x200B;**重新包覆**，對話框將要求確認。

### 查看和編輯包資訊{#viewing-and-editing-package-information}

要查看或編輯有關包定義的資訊：

1. 在「包管理器」中，導航到要查看的包。
1. 按一下要查看的包的包表徵圖。 這將開啟包頁，其中列出有關包定義的資訊：

   ![packagesiteclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >您也可以從此頁面編輯和執行套件上的特定動作。
   >
   >可用的按鈕將取決於軟體包是否已構建。

1. 如果已構建包，請按一下&#x200B;**Contents** ，將開啟一個窗口並列出包的整個內容：

### 查看包內容和測試安裝{#viewing-package-contents-and-testing-installation}

建立套件後，您可以檢視內容：

1. 在「包管理器」中，導航到要查看的包。
1. 按一下要查看的包的包表徵圖。 這將開啟包頁面，其中列出有關包定義的資訊。

1. 要查看內容，請按一下&#x200B;**Contents** ，將開啟一個窗口並列出包的整個內容：

   ![packgestcontents](assets/packgescontents.png)

1. 要執行安裝的乾式運行，請按一下「測試安裝」。 ****&#x200B;確認操作後，將開啟一個窗口並列出結果，如同執行了安裝：

   ![packagestinstall](assets/packagestestinstall.png)

### 將軟體包下載到檔案系統{#downloading-packages-to-your-file-system}

本節說明如何使用&#x200B;**Package Manager**&#x200B;從AEM下載套件至您的檔案系統。

1. 在「AEM歡迎」畫面上，按一下「套件&#x200B;****」，然後選取「套件管理員&#x200B;**」。**
1. 導覽至您要下載的套件。

   ![packagesdownload](assets/packagesdownload.png)

1. 按一下您要下載之套件的zip檔案名稱（加底線）所形成的連結；例如`export-for-offline.zip`。

   AEM會將套件下載至您的電腦（使用標準瀏覽器下載對話方塊）。

### 從檔案系統{#uploading-packages-from-your-file-system}上載包

套件上傳可讓您從檔案系統上傳套件至AEM Package Manager。
要上載包：

1. 導航至&#x200B;**軟體包管理器**。 然後，將包上傳到您希望其中的組資料夾。

   ![packagesuploadbutton](assets/packagesuploadbutton.png)

1. 按一下&#x200B;**Upload Package**。

   ![packagesuploadialog](assets/packagesuploaddialog.png)

   * **檔案**

      您可以直接鍵入檔案名，或使用&#x200B;**瀏覽……**&#x200B;對話方塊，從您的本機檔案系統中選取所需的套件（選取後，按一下「確定」****）。

   * **強制上傳**

      如果已存在具有此名稱的包，您可以按一下此命令強制上載（並覆蓋現有包）。
   按一下&#x200B;**OK** ，以便上載新包並列在「包管理器」清單中。

   >[!NOTE]
   >
   >若要讓內容可供AEM使用，請務必[安裝套件](#installing-packages)。

### 驗證軟體包{#validating-packages}

在安裝軟體包之前，您可能希望驗證其內容。 由於軟體包可以修改`/apps`和／或添加、修改和刪除ACL下的覆蓋檔案，因此在安裝前驗證這些更改通常很有用。

#### 驗證選項{#validation-options}

驗證機制可檢查包的下列特性：

* OSGi軟體包導入
* 覆蓋
* ACL

這些選項將在下面詳述。

* **驗證 OSGi 封裝匯入**

   **已檢查項目**

   此驗證會檢查所有JAR檔案（OSGi包）的包，提取其`manifest.xml`（其中包含所述OSGi包所依賴的版本化從屬關係），並驗證AEM實例將所述從屬關係導出為正確的版本。

   **報告方式**

   AEM實例無法滿足的任何版本化從屬關係都列在「包管理器」的&#x200B;**活動日誌**&#x200B;中。

   **錯誤狀態**

   如果不滿足相依性，則包中包含這些相依性的OSGi捆綁包將不會啟動。 這會導致應用程式部署中斷，因為任何依賴未啟動的OSGi套件的應用程式部署都會無法正常運作。

   **錯誤解決方法**

   要解決由於未滿足要求的OSGi捆綁包而導致的錯誤，需要調整捆綁包中具有未滿足要求的導入的相關性版本。

* **驗證覆蓋**

   **已檢查項目**

   此驗證會決定所安裝的套件是否包含已覆蓋在目標AEM例項中的檔案。

   例如，假設`/apps/sling/servlet/errorhandler/404.jsp`有現有覆蓋，則包含`/libs/sling/servlet/errorhandler/404.jsp`的套件，如此會變更`/libs/sling/servlet/errorhandler/404.jsp`的現有檔案。

   **報告方式**

   此類覆蓋在「包管理器」的&#x200B;**活動日誌**&#x200B;中有說明。

   **錯誤狀態**

   錯誤狀態表示套件嘗試部署已覆蓋的檔案，因此套件中的變更將被覆蓋覆蓋（因此「隱藏」），而不會生效。

   **錯誤解決方法**

   要解決此問題，`/apps`中覆蓋檔案的維護人員必須檢閱`/libs`中覆蓋檔案的變更，並視需要將變更整合至覆蓋(`/apps`)，然後重新部署覆蓋檔案。

   >[!NOTE]
   >
   >請注意，驗證機制無法協調重疊內容是否已正確整合至覆蓋檔案。 因此，即使進行了必要的變更，此驗證仍會繼續報告衝突。

* **驗證 ACL**

   **已檢查項目**

   此驗證會檢查要新增哪些權限、如何處理這些權限（合併／取代），以及目前權限是否會受到影響。

   **報告方式**

   這些權限在包管理器的&#x200B;**活動日誌**&#x200B;中有說明。

   **錯誤狀態**

   不能提供任何明確錯誤。 驗證只會指出是否將添加或影響任何新的ACL權限。

   **錯誤解決方法**

   使用驗證提供的資訊，可以在CRXDE中查看受影響的節點，並根據需要在包中調整ACL。

   >[!CAUTION]
   >
   >建議您最好不要將套件影響AEM提供的ACL，因為這可能會導致意外的產品行為。

#### 執行驗證{#performing-validation}

可以通過兩種不同的方式驗證軟體包：

* 透過Package Manager UI
* 透過HTTP POST要求（例如搭配cURL）

>[!NOTE]
>
>在上傳套件後，但在安裝之前，應一律進行驗證。

**通過包管理器進行包驗證**

1. 在`https://<server>:<port>/crx/packmgr`開啟包管理器
1. 在清單中選擇包，然後從標題中選擇&#x200B;**More**&#x200B;下拉式清單，然後從下拉菜單中選擇&#x200B;**Validate**。

   >[!NOTE]
   >
   >這應在上傳內容套件後，但在安裝套件之前完成。

1. 在隨後出現的模態對話框中，使用複選框選擇驗證類型，然後按一下&#x200B;**驗證**&#x200B;開始驗證。 或者，按一下&#x200B;**取消**。

1. 然後，會執行所選的驗證。 結果顯示在「包管理器」的活動日誌中。

**透過HTTP POST要求進行封裝驗證**

POST請求採用下列形式。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>`type`參數可以是任何逗號分隔的無序清單，包括：
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`

>
>
如果未傳遞，則`type`的值預設為`osgiPackageImports`。

以下是使用cURL執行套件驗證的範例。

1. 如果使用cURL，請執行類似下列的語句：

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. 請求的驗證會執行，回應會以JSON物件傳回。

>[!NOTE]
>
>對驗證HTTP POST要求的回應將是具有驗證結果的JSON物件。

### 安裝軟體包{#installing-packages}

上傳套件後，您必須安裝內容。 要安裝軟體包內容並使其正常工作，它必須同時具備：

* 載入至AEM（從您的檔案系統](#uploading-packages-from-your-file-system)上傳或從[軟體散發](#software-distribution)下載）[

* 已安裝

>[!CAUTION]
>
>安裝套件可覆寫或刪除現有內容。 只有在您確定套件不會刪除或覆寫您需要的內容時，才能上傳套件。
>
>若要查看套件的內容或影響，您可以：
>
>* 不修改任何內容，即可對軟體包執行測試安裝：
   >  開啟包（按一下包表徵圖或名稱），然後按一下&#x200B;**測試安裝**。
   >
   >
* 請參閱套件內容清單：
   >  開啟包並按一下&#x200B;**Contents**。

>



>[!NOTE]
>
>在安裝軟體包之前，將建立一個快照軟體包以包含將被覆蓋的內容。
>
>卸載軟體包時，將重新安裝此快照。

>[!CAUTION]
>
>如果您要安裝數位資產，您必須：
>
>* 首先，停用WorkflowLauncher。
   >  使用OSGi控制台的「元件」菜單選項來停用`com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`。
   >
   >
* 接著，在安裝完成後，重新啟動WorkflowLauncher。
>
>
停用WorkflowLauncher可確保Assets匯入工具架構不會（無意中）在安裝時操縱資產。

1. 在包管理器中，導航到要安裝的包。

   **Install**&#x200B;按鈕顯示在尚未安裝的軟體包的一側。

   >[!NOTE]
   >
   >或者，您也可以按一下軟體包表徵圖開啟軟體包，以訪問&#x200B;**Install**&#x200B;按鈕。

1. 按一下&#x200B;**Install**&#x200B;啟動安裝。 對話方塊會要求確認，並列出所有正在進行的變更。 完成後，按一下對話框上的&#x200B;**關閉**。

   安裝軟體包後，軟體包旁會顯示「**Installed**」一詞。

### 基於檔案系統的上載和安裝{#file-system-based-upload-and-installation}

有另一種方式可將套件上傳並安裝至您的例項。 在檔案系統中，您的jar和`license.properties`檔案附帶有`crx-quicksart`資料夾。 您需要在`crx-quickstart`下建立名為`install`的資料夾。 然後，您會有類似的功能：`<aem_home>/crx-quickstart/install`

在此安裝資料夾中，您可以直接添加包。 它們會自動上傳並安裝在您的例項上。 完成後，您可以在「包管理器」中查看包。

如果實例正在運行，將包添加到`install`資料夾將直接啟動上載並安裝實例。 如果實例未運行，則您放在`install`資料夾中的軟體包將按字母順序在啟動時安裝。

>[!NOTE]
>
>您也可以先執行此動作，然後再第一次啟動執行個體。 為此，您需要手動建立`crx-quickstart`資料夾，在資料夾下建立`install`資料夾，並將包放在此處。 然後，當您第一次啟動實例時，這些軟體包將按字母順序安裝。

### 卸載軟體包{#uninstalling-packages}

AEM可讓您解除安裝套件。 此操作將恢復在軟體包安裝前立即建立的快照中受影響的儲存庫內容。

>[!NOTE]
>
>在安裝時，將建立包含將被覆蓋的內容的快照包。
>
>卸載軟體包時，將重新安裝此軟體包。

1. 在「套件管理器」中，導覽至您要解除安裝的套件。
1. 按一下要卸載的包的包表徵圖。
1. 按一下&#x200B;**Uninstall**&#x200B;可從儲存庫中刪除此包的內容。 對話方塊會要求確認，並列出所有正在進行的變更。 完成後，按一下對話框上的&#x200B;**關閉**。

### 刪除包{#deleting-packages}

要從「包管理器」清單中刪除包：

>[!NOTE]
>
>軟體包中安裝的檔案／節點為&#x200B;**not**。

1. 在&#x200B;**Tools**&#x200B;控制台中，展開&#x200B;**Packages**&#x200B;資料夾，在右窗格中顯示包。

1. 按一下您要刪除的套件，以反白顯示它，然後執行下列任一動作：

   * 按一下工具欄菜單中的&#x200B;**Delete**。
   * 按一下右鍵並選擇&#x200B;**Delete**。

   ![包刪除](assets/packagesdelete.png)

1. AEM會要求確認您要刪除套件。 按一下&#x200B;**確定**&#x200B;確認刪除。

>[!CAUTION]
>
>如果此軟體包已安裝，則&#x200B;*installed*&#x200B;內容將&#x200B;**not**&#x200B;刪除。

### 複製軟體包{#replicating-packages}

複製套件的內容以將其安裝到發佈實例：

1. 在&#x200B;**包管理器**&#x200B;中，導航到要複製的包。

1. 按一下要複製的包的表徵圖或名稱以展開它。
1. 在工具欄的&#x200B;**More**&#x200B;下拉式選單中，選擇&#x200B;**Replicate**。

## 套件共用 {#package-share}

Package Share是公開提供來共用Content-Packages的集中式伺服器。

已由[軟體分發](#software-distribution)替換。

## 軟體分發{#software-distribution}

[Software ](https://downloads.experiencecloud.adobe.com) Distribution是專為簡化AEM套件的搜尋和下載而設計的新使用者介面。

如需詳細資訊，請參閱[軟體散發檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)。

>[!CAUTION]
>
>目前，AEM套件管理程式無法與「軟體散發」搭配使用，您可將套件下載至本機磁碟。

