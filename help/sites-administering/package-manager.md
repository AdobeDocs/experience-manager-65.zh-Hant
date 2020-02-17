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
source-git-commit: 5e10ddb0e5cf24e1915d0840cd380520374e93ea

---


# 如何使用套件{#how-to-work-with-packages}

軟體包可以導入和導出儲存庫內容。 例如，您可以使用軟體包來安裝新功能、在實例之間傳輸內容，以及備份儲存庫內容。

可從以下頁訪問和／或維護包：

* [Package Manager](#package-manager)，您可使用它來管理本機AEM例項中的封裝。

* [Package Share](#package-share)，一種集中式伺服器，可同時持有公開可用的套件，以及您公司專用的套件。 公開套件可包含修補程式、新功能、檔案等。

您可以在包管理器、包共用和檔案系統之間傳輸包。

## 什麼是套件？ {#what-are-packages}

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
* 從「套件共用」程式庫下載套件，例如修補程式
* 將封裝上傳至封裝共用程式庫的公司內部區段

## 包資訊 {#package-information}

包定義由各種類型的資訊組成：

* [套件設定](#package-settings)
* [封裝篩選器](#package-filters)
* [封裝螢幕擷取](#package-screenshots)
* [封裝圖示](#package-icons)

### 套件設定 {#package-settings}

您可以編輯各種「包設定」以定義包描述、相關錯誤、依賴項和提供程式資訊等方面。

建立 **或編輯Package時** ，可通過「編輯」( **Edit** )按鈕使用「包設定 [」(Package Settings)對話框，並提](#creating-a-new-package)[](#viewing-and-editing-package-information) 供了三個用於配置的頁籤。 進行任何更改後，按一下「 **確定** 」(OK)保存這些更改。

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
    </ul> <p>預設值為 <strong>Ignore</strong>。</p> </td>
   <td>
    <ul>
     <li><strong>忽略</strong> -保留儲存庫中的ACL</li>
     <li><strong>覆蓋</strong> -覆蓋儲存庫中的ACL</li>
     <li><strong>合併</strong> -合併兩組ACL</li>
     <li><strong>清除</strong> -清除ACL</li>
     <li><strong>MergePreserve</strong> —— 通過添加內容中不存在承擔者的訪問控制項，將內容中的訪問控制與隨包提供的訪問控制合併</li>
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

### 封裝篩選器 {#package-filters}

篩選器標識要包含在包中的儲存庫節點。 篩選 **器定義** ，指定以下資訊：

* 要 **包含的內容** 的根路徑。
* **包含** 或排除根路徑下特定節點的規則。

篩選器可包含零個或多個規則。 如果未定義規則，則套件會包含根路徑下的所有內容。

您可以為套件定義一或多個篩選定義。 使用多個篩選器來包含來自多個根路徑的內容。

![chlimage_1-109](assets/chlimage_1-109.png)

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
   <td>您可以定義路徑，或使用規則運算式來指定要包括的所有節點。<br /> 包 <br /> 含目錄將：
    <ul>
     <li>包括該 <i>目錄</i> ，以及該目錄中的所有檔案和資料夾（即整個子樹）</li>
     <li><strong>不包含</strong> 指定根路徑下的其他檔案或資料夾</li>
    </ul> </td>
   <td>/libs/sling/install(/)。*)? </td>
  </tr>
  <tr>
   <td> 排除</td>
   <td>您可以指定路徑或使用規則運算式來指定要排除的所有節點。<br /> 排 <br /> 除目錄將排除該目錄 <i>及該目錄中</i> （即整個子樹）的所有檔案和資料夾。<br /> </td>
   <td>/libs/wcm/foundation/components(/)。*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>一個套件可包含多個篩選定義，因此不同位置的節點可輕鬆結合為一個套件。

在您首次建立套件時，通常會定 [義套件篩選](#creating-a-new-package)，但稍後也可以編輯這些篩選（在此之後應重建套件）。

### 封裝螢幕擷取 {#package-screenshots}

您可將螢幕擷取畫面附加至您的套件，以視覺化方式呈現內容的外觀；例如，提供新功能的螢幕擷取。

### 封裝圖示 {#package-icons}

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

## 包管理器 {#package-manager}

Package Manager會管理您本機AEM安裝上的套件。 分配了必 [要的權限後](#permissions-needed-for-using-the-package-manager) ，您可以使用包管理器執行各種操作，包括配置、構建、下載和安裝包。 要配置的關鍵元素包括：

* [套件設定](#package-settings)
* [封裝篩選器](#package-filters)

### 使用包管理器所需的權限 {#permissions-needed-for-using-the-package-manager}

若要授與使用者建立、修改、上傳和安裝套件的權利，您必須在下列位置為使用者提供適當的權限：

* **/etc/packages** （完全權限不包括刪除）
* 包含包內容的節點

如需變 [更權限的指示](/help/sites-administering/security.md#setting-page-permissions) ，請參閱設定權限。

### 建立新包 {#creating-a-new-package}

要建立新包定義，請執行以下操作：

1. 在「AEM歡迎」畫面上，按一下「 **封裝** 」(或從「工具控制台」按兩下「 **封裝******」)。

1. 然後選擇「 **包管理器」**。
1. 按一 **下「建立套件**」。

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
   按一下 **確定** ，建立包。

1. AEM會在適當的群組檔案夾中列出新的套件。

   ![packagesitem](assets/packagesitem.png)

   按一下要開啟的表徵圖或包名稱。

   ![packagetemclicked](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >如有需要，您可在稍後階段返回本頁面。

1. 按一下 **編輯** ，編輯包 [設定](#package-settings)。

   在這裡，您可以新增資訊和／或定義特定設定；例如，這些錯誤包括說明、圖 [示](#package-icons)、相關錯誤和添加提供程式詳細資訊。

   編輯完 **成設定後** ，按一下「確定」。

1. 視需 **[要將螢幕擷取](#package-screenshots)**(Screenshots)新增至套件。 建立套件時，有一個例項可供使用，若有需要，請使用「套件的螢幕擷取」(**Package Screeston**from sidekick)新增更多。

   按兩下「螢幕擷取」區域中的影像元件，新增影像，然後按一下「確 **定」******。

1. 定義「 **[套件篩選](#package-filters)**」，方法是將「篩選定義&#x200B;****」的例項從側腳拖曳，然後按兩下以開啟以進行編輯：

   ![packagesfilter](assets/packagesfilter.png)

   指定：

   * **根路徑**&#x200B;要封裝的內容；這可以是子樹的根。
   * **規則**&#x200B;規則是選用的；對於簡單的套件定義，不需要指定包含或排除規則。

      如有需要，您可以定義「包 [**含&#x200B;**」或「**&#x200B;排除」規則&#x200B;**](#package-filters)，以精確定義套件內容。

      使用+符號 **新增規則** ，或使用 **-符號移除規則** 。 規則會根據其順序套用，因此使用「向上」和「向下」按 **鈕** , **依需要定** 位。
   然後按一 **下「確定** 」以儲存篩選。

   >[!NOTE]
   >
   >您可以視需要使用任意數量的篩選定義，但必須小心確保這些定義不發生衝突。 使用 **預覽** ，確認封裝內容將包含哪些內容。

1. 若要確認套件將包含的內容，您可使用「預 **覽」**。 這會執行建立程式的乾式執行，並列出實際建立時要新增至封裝的所有項目。
1. 您現在可以 [建立](#building-a-package) 套件。

   >[!NOTE]
   >
   >目前並非必要建立套件，而是可在稍後的時間點完成。

### 建立套件 {#building-a-package}

通常，在建立包定義時 [會同時生成包](#creating-a-new-package)，但您可以在稍後返回以生成或重建包。 如果儲存庫中的內容已更改，則此功能非常有用。

>[!NOTE]
>
>在建立套件之前，預覽套件的內容會很有用。 若要這麼做，請按一下「 **預覽**」。

1. 從「包管理器」( **Package Manager** )開啟包定義（按一下包表徵圖或名稱）。

1. 按一 **下Build**。 對話方塊會要求您確認您確實要建立套件。

   >[!NOTE]
   >
   >當您重建包時，當將覆寫包內容時，這特別重要。

1. 按一下 **確定**。 AEM將建立套件，並列出新增至套件的所有內容。 完成時，AEM會顯示已建立套件的確認，並（當您關閉對話方塊時）更新套件清單資訊。

### 重新包裝包 {#rewrapping-a-package}

在建立套件後，如有需要，可重新包裝它。

重新包裝會變更套件資訊- *而不* 變更套件內容。 套件資訊是縮圖、說明等，換言之，您可使用「套件設定」對話方塊編輯的一切 **資訊** (以開啟此按一下「 ****&#x200B;編輯」)。

重新包裝的主要使用案例是準備套件共用時。 例如，您可能已有現有的套件，並決定與其他人共用。 您想要新增縮圖並新增說明。 您可以重新建立整個套件，而不需使用其所有功能（這可能需要一些時間，並承擔套件不再與原始套件相同的風險），只要重新包住它，然後新增縮圖和說明即可。

1. 從「包管理器」( **Package Manager** )開啟包定義（按一下包表徵圖或名稱）。

1. 按一 **下「編輯** 」，並視需 **[要更新「封裝設定](#package-settings)**」。 按一&#x200B;**下「確定**」以儲存。

1. 按一 **下「重排**」，對話方塊會要求確認。

### 查看和編輯包資訊 {#viewing-and-editing-package-information}

要查看或編輯有關包定義的資訊：

1. 在「包管理器」中，導航到要查看的包。
1. 按一下要查看的包的包表徵圖。 這將開啟包頁，其中列出有關包定義的資訊：

   ![packagesiteclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >您也可以從此頁面編輯和執行套件上的特定動作。
   >
   >可用的按鈕將取決於軟體包是否已構建。

1. 如果包已構建，請按一下「 **內容**」(Contents)，將開啟一個窗口並列出包的整個內容：

### 查看包內容和測試安裝 {#viewing-package-contents-and-testing-installation}

建立套件後，您可以檢視內容：

1. 在「包管理器」中，導航到要查看的包。
1. 按一下要查看的包的包表徵圖。 這將開啟包頁面，其中列出有關包定義的資訊。

1. 要查看內容，請單 **擊「內容**」(Contents)，將開啟一個窗口並列出包的整個內容：

   ![packgestcontents](assets/packgescontents.png)

1. 要執行安裝的乾式運行，請按一下「 **測試安裝」**。 確認操作後，將開啟一個窗口並列出結果，如同執行了安裝：

   ![packagestinstall](assets/packagestestinstall.png)

### 將包下載到檔案系統 {#downloading-packages-to-your-file-system}

本節說明如何使用 **Package Manager，將套件從AEM下載至您的檔案系統**。

>[!NOTE]
>
>如需 [](#package-share) 從公共區域和您公司內部的套件共用區域下載修補程式、功能套件和套件的詳細資訊，請參閱套件共用。
>
>從「包共用」中，您可以：
>
>* 直接從「套件共 [用」下載套件至您的本機AEM實例](#downloading-and-installing-packages-from-package-share)。
   >  下載軟體包後，將其導入儲存庫中，之後，您可以使用軟體包管理器立即將其安裝到本地實 **例中**。 這些套件包括修補程式和其他共用套件。
   >
   >
* 從「套件共 [用」下載套件至您的檔案系統](#downloading-packages-to-your-file-system-from-package-share)。
>



1. 在「AEM歡迎」畫面上，按一下「套 **件」**，然後選 **取「套件管理員」**。
1. 導覽至您要下載的套件。

   ![packagesdownload](assets/packagesdownload.png)

1. 按一下您要下載之套件的zip檔案名稱（加底線）所形成的連結；例如 `export-for-offline.zip`。

   AEM會將套件下載至您的電腦（使用標準瀏覽器下載對話方塊）。

### 從檔案系統上載包 {#uploading-packages-from-your-file-system}

套件上傳可讓您從檔案系統上傳套件至AEM Package Manager。

>[!NOTE]
>
>請參 [閱上傳封裝至公司內部的封裝共用](#uploading-packages-to-the-company-internal-package-share) ，將封裝上傳至您公司的「封裝共用」私用區。

要上載包：

1. 導覽至「套 **件管理員」**。 然後，將包上傳到您希望其中的組資料夾。

   ![packagesuploadbutton](assets/packagesuploadbutton.png)

1. 按一 **下「上傳套件**」。

   ![packagesuploadialog](assets/packagesuploaddialog.png)

   * **檔案**

      **您可以直接鍵入檔案名，或使用「瀏**&#x200B;覽……」對話框，從本地檔案系統中選擇所需的包(選擇後按一下「 **確定**」)。

   * **強制上傳**

      如果已存在具有此名稱的包，您可以按一下此命令強制上載（並覆蓋現有包）。
   按一下 **確定** ，以便新包被上載並列在「包管理器」(Package Manager)清單中。

   >[!NOTE]
   >
   >若要讓內容可供AEM使用，請務必安 [裝套件](#installing-packages)。

### 驗證軟體包 {#validating-packages}

在安裝軟體包之前，您可能希望驗證其內容。 由於軟體包可以修改ACL下 `/apps` 的覆蓋檔案和／或添加、修改和刪除ACL，因此在安裝前驗證這些更改通常很有用。

#### 驗證選項 {#validation-options}

驗證機制可檢查包的下列特性：

* OSGi軟體包導入
* 覆蓋
* ACL

這些選項將在下面詳述。

* **驗證 OSGi 封裝匯入**

   **已檢查項目**

   此驗證會檢查所有JAR檔案（OSGi包）的包，提取其 `manifest.xml` （其中包含所述OSGi包依賴的版本化依賴項），並驗證AEM實例將所述依賴項導出為正確版本。

   **報告方式**

   AEM例項無法滿足的任何版本化相依性都會列在「套件管理員」的「活 **動記錄檔** 」中。

   **錯誤狀態**

   如果不滿足相依性，則包中包含這些相依性的OSGi捆綁包將不會啟動。 這會導致應用程式部署中斷，因為任何依賴未啟動的OSGi套件的應用程式部署都會無法正常運作。

   **錯誤解決方法**

   要解決由於未滿足要求的OSGi捆綁包而導致的錯誤，需要調整捆綁包中具有未滿足要求的導入的相關性版本。

* **驗證覆蓋**

   **已檢查項目**

   此驗證會決定所安裝的套件是否包含已覆蓋在目標AEM例項中的檔案。

   例如，若現有覆蓋位於，則包 `/apps/sling/servlet/errorhandler/404.jsp`含的套件 `/libs/sling/servlet/errorhandler/404.jsp`會變更位於的現有檔案 `/libs/sling/servlet/errorhandler/404.jsp`。

   **報告方式**

   此類覆蓋在「套件管理員」的「 **活動記錄** 」中有說明。

   **錯誤狀態**

   錯誤狀態表示套件嘗試部署已覆蓋的檔案，因此套件中的變更將被覆蓋覆蓋（因此「隱藏」），而不會生效。

   **錯誤解決方法**

   若要解決此問題，中覆蓋檔案的維護人員必須檢閱中對覆蓋檔案所做的變更，並視需要將變更併入覆蓋( `/apps``/libs``/apps`)中，然後重新部署覆蓋檔案。

   >[!NOTE]
   >
   >請注意，驗證機制無法協調重疊內容是否已正確整合至覆蓋檔案。 因此，即使進行了必要的變更，此驗證仍會繼續報告衝突。

* **驗證 ACL**

   **已檢查項目**

   此驗證會檢查要新增哪些權限、如何處理這些權限（合併／取代），以及目前權限是否會受到影響。

   **報告方式**

   這些權限在包管理器的 **活動日誌** 中有說明。

   **錯誤狀態**

   不能提供任何明確錯誤。 驗證只會指出是否將添加或影響任何新的ACL權限。

   **錯誤解決方法**

   使用驗證提供的資訊，可以在CRXDE中查看受影響的節點，並根據需要在包中調整ACL。

   >[!CAUTION]
   >
   >建議您最好不要將套件影響AEM提供的ACL，因為這可能會導致意外的產品行為。

#### 執行驗證 {#performing-validation}

可以通過兩種不同的方式驗證軟體包：

* 透過Package Manager UI
* 透過HTTP POST要求（例如搭配cURL）

>[!NOTE]
>
>在上傳套件後，但在安裝之前，應一律進行驗證。

**通過包管理器進行包驗證**

1. 在以下位置開啟包管理器： `https://<server>:<port>/crx/packmgr`
1. 在清單中選取套件，然後從標題中選 **取「更多** 」下拉式清單，然後從下拉式選單中選取「 **驗證** 」。

   >[!NOTE]
   >
   >這應在上傳內容套件後，但在安裝套件之前完成。

1. 在隨後出現的模態對話框中，使用複選框選擇驗證類型，並通過按一下「驗證」( **Validate)開始驗**&#x200B;證。 或者，按一下「 **取消」**。

1. 然後，會執行所選的驗證。 結果顯示在「包管理器」的活動日誌中。

**透過HTTP POST要求進行封裝驗證**

POST請求採用下列形式。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>參數 `type` 可以是任何逗號分隔的無序清單，包括：
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`
>
>
若未傳遞， `type` 則預設 `osgiPackageImports` 值為值。

以下是使用cURL執行套件驗證的範例。

1. 如果使用cURL，請執行類似下列的語句：

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. 請求的驗證會執行，回應會以JSON物件傳回。

>[!NOTE]
>
>對驗證HTTP POST要求的回應將是具有驗證結果的JSON物件。

### 安裝軟體包 {#installing-packages}

上傳套件後，您必須安裝內容。 要安裝軟體包內容並使其正常工作，它必須同時具備：

* 載入至AEM(從您的檔 [案系統上傳](#uploading-packages-from-your-file-system) , [或從套件共用下載](#downloading-and-installing-packages-from-package-share))

* 已安裝

>[!CAUTION]
>
>安裝套件可覆寫或刪除現有內容。 只有在您確定套件不會刪除或覆寫您需要的內容時，才能上傳套件。
>
>若要查看套件的內容或影響，您可以：
>
>* 不修改任何內容，即可對軟體包執行測試安裝：
   >  開啟套件（按一下套件圖示或名稱），然後按一下「 **測試安裝」**。
   >
   >
* 請參閱套件內容清單：
   >  開啟套件，然後按一 **下內容**。
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
   >  使用OSGi控制台的「元件」功能表選項來停用 `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`。
   >
   >
* 接著，在安裝完成後，重新啟動WorkflowLauncher。
>
>
停用WorkflowLauncher可確保Assets匯入工具架構不會（無意中）在安裝時操縱資產。

1. 在包管理器中，導航到要安裝的包。

   「 **Install** （安裝）」按鈕顯示在尚未安裝的包的一側。

   >[!NOTE]
   >
   >或者，您也可以按一下套件圖示來開啟套件，以存取 **Install** （安裝）按鈕。

1. 按一 **下「安裝** 」以開始安裝。 對話方塊會要求確認，並列出所有正在進行的變更。 完成後，按一下 **對話框** 上的「關閉」。

   安裝包 **後** ，軟體包旁邊會出現「Installed（已安裝）」一詞。

### 基於檔案系統的上傳和安裝 {#file-system-based-upload-and-installation}

有另一種方式可將套件上傳並安裝至您的例項。 在檔案系統中，您的jar和 `crx-quicksart` 檔案旁邊有一個文 `license.properties` 件夾。 您需要建立名為的 `install` 資料夾 `crx-quickstart`。 然後，您會有類似的功能： `<aem_home>/crx-quickstart/install`

在此安裝資料夾中，您可以直接添加包。 它們會自動上傳並安裝在您的例項上。 完成後，您可以在「包管理器」中查看包。

如果您的實例正在運行，將包添加到 `install` 資料夾將直接啟動上載和實例上的安裝。 如果實例未運行，則資料夾中放置的包 `install` 將按字母順序在啟動時安裝。

>[!NOTE]
>
>您也可以在第一次啟動例項之前先執行此動作。 為此，您需要手動建立檔案 `crx-quickstart` 夾，在其下 `install` 建立資料夾，並將資料夾放在那裡。 然後，當您第一次啟動實例時，這些軟體包將按字母順序安裝。

### 卸載軟體包 {#uninstalling-packages}

AEM可讓您解除安裝套件。 此操作將恢復在軟體包安裝前立即建立的快照中受影響的儲存庫內容。

>[!NOTE]
>
>在安裝時，將建立包含將被覆蓋的內容的快照包。
>
>卸載軟體包時，將重新安裝此軟體包。

1. 在「套件管理器」中，導覽至您要解除安裝的套件。
1. 按一下要卸載的包的包表徵圖。
1. 按一下 **卸載** ，從儲存庫中刪除此包的內容。 對話方塊會要求確認，並列出所有正在進行的變更。 完成後，按一下 **對話框** 上的「關閉」。

### 刪除包 {#deleting-packages}

要從「包管理器」清單中刪除包：

>[!NOTE]
>
>不會刪除包中安裝的檔案/ **節點** 。

1. 在「工 **具** 」控制台中，展開「套件 **** 」檔案夾，在右側窗格中顯示套件。

1. 按一下您要刪除的套件，以反白顯示它，然後執行下列任一動作：

   * 在工具 **列選單中** ，按一下「刪除」。
   * 按一下右鍵並選擇「刪 **除」**。
   ![包刪除](assets/packagesdelete.png)

1. AEM會要求確認您要刪除套件。 按一 **下「確定** 」以確認刪除。

>[!CAUTION]
>
>如果此套件已安裝，則不 *會刪除***已安裝** 的內容。

### 複製軟體包 {#replicating-packages}

複製套件的內容以將其安裝到發佈實例：

1. 在包管 **理器中**，導航到要複製的包。

1. 按一下要複製的包的表徵圖或名稱以展開它。
1. 在工具 **列的** 「更多」下拉式選單中，選取「復 **制」**。

## Package Share {#package-share}

Package Share是公開提供來共用Content-Packages的集中式伺服器。

透過Package Share，您可以下載這些套件，其中可包含正式的修補程式、功能集、更新或其他使用者產生的範例內容。

您也可以在公司內上傳及共用套件。

### 對包共用的訪問 {#access-to-package-share}

對包共用沒有匿名訪問；也就是說，只有註冊的使用者才能檢視、下載和上傳套件。

我們的合作夥伴和客戶可以存取套件共用。 必須提交註冊詳細資訊，才能分配訪問權限。

要獲得對包共用的訪問權：

* 使用登 [入頁面](#signing-in-to-package-share)
* 第一次使用登入頁面時，您需要：

   * [註冊Adobe ID](#registering-for-package-share) 和／或驗 [證您現有的Adobe ID](#validating-your-adobe-id)
   * 以便您的 [套件共用帳戶](#package-share-account) (Package Share Account)

>[!NOTE]
>
>任何尚未指派給客戶的Package Share用戶，都必須加入社群，才能查看這些資源，方法是按一下Package Share login旁邊的 **Join** 。

#### 登入套件共用 {#signing-in-to-package-share}

1. 在「AEM歡迎」畫面上，按一下「 **工具**」。
1. 然後選擇「 **Package Share」（封裝共用）**。 您必須執行下列任一操作：

   * 使用您的Adobe ID登入
   * [建立Adobe ID](#registering-for-package-share)
   >[!NOTE]
   >
   >您第一次使用Adobe ID登入時，必須完成電子 [郵件位址的驗證](#validating-your-adobe-id)。

   >[!NOTE]
   >
   >如果您忘記密碼，請使用「說 [明頁面](https://enterprise-dev.adobe.com/content/edev/en/registration/account.html) 」連結（也位於登入對話方塊中）。

#### 驗證您的Adobe ID {#validating-your-adobe-id}

您第一次使用Adobe ID登入「套件共用」時，您的電子郵件位址將會經過驗證。

1. 您將會收到一封包含連結的電子郵件。
1. 您必須按一下此連結。
1. 網頁將會開啟。

   以開啟此網頁的動作為驗證。

1. 登入將會繼續。

1. 您將會收到一封包含連結的電子郵件。
1. 您必須按一下此連結。
1. 網頁將會開啟。 以開啟此網頁的動作為驗證。
1. 登入將會繼續。

#### 註冊軟體包共用 {#registering-for-package-share}

如果您需要存取「封裝共用」，則必須註冊Adobe ID:

* 「套 [件共用登入」頁面](#signing-in-to-package-share) ，提供註冊Adobe ID的連結。
* 您可以從特定Adobe案頭軟體註冊Adobe ID。
* 或者，您也可以在 [Adobe登入頁面上線上註冊](https://www.adobe.com/cfusion/membership/index.cfm?nf=1&nl=1)。

Adobe ID可透過提供：

* 您的電子郵件地址
* 您選擇的密碼
* 您的姓名和居住地國家等其他資訊

#### 套件共用帳戶 {#package-share-account}

您的應用程式的有效性將會在下列之前檢查：

* 您的使用者帳戶是使用必要／允許的權限建立。
* 您的帳戶會新增至您公司的群組。

>[!NOTE]
>
>來自其中一個合作夥伴公司的使用者也可以是其客戶群的成員。

#### 網路考量事項 {#network-considerations}

**IPv6**

嘗試從純IPv6環境訪問包共用時可能會遇到問題。

這是因為軟體包共用是伺服器上托管的服務，這意味著您的連接是通過網際網路上的各種網路建立的。 不能保證所有連接網路都支援IPv6;如果不是，連接可能會失敗。

為避免此問題，您可以從IPv4網路訪問「包共用」，下載該包，然後將其上傳到IPv6環境。

**HTTP代理**

如果您的公司執行需要驗證的http proxy，則目前無法使用「封裝共用」。

只有當您的AEM伺服器可存取網際網路而不需要驗證時，才能使用Package Share。 若要為使用http用戶端（包括套件共用）的所有服務設定proxy，請使用Day Commons HTTP Client 3.1套件的 [OSGi組態](/help/sites-deploying/osgi-configuration-settings.md)。

### 內部封裝共用 {#inside-package-share}

In Package Share包排列在樹子樹中：

* Adobe提供的Adobe套件。
* 由其他公司提供且由Adobe公開的共用套件。
* 您的公司套件為私人。

![chlimage_1-110](assets/chlimage_1-110.png)

### 搜索和篩選包 {#searching-and-filtering-packages}

「封裝共用」提供搜尋列，您可用來搜尋特定關鍵字或／和標籤。 關鍵字和標籤都支援多個值。

* 若要搜尋多個關鍵字，您必須依空格分隔每個關鍵字。
* 要搜索多個標籤，您必須在包樹中選擇每個標籤。

您也可以將篩選摘要列右側的條件運算子從OR變更為AND。

### 從包共用下載和安裝包 {#downloading-and-installing-packages-from-package-share}

若要從Package Share下載套件並將它們安裝在您的本機執行個體上，從AEM執行個體存取Package Share會更輕鬆。 這將下載軟體包，並立即在軟體包管理器中註冊它，從中可以安裝軟體包。

1. 在「AEM歡迎」畫面中，按一下「 **工具**」，然後選 **取「套件共用** 」以開啟「套件共用」頁面。
1. 使用您的帳戶詳細資訊，登入「套件共用」。 會顯示著陸頁面，列出Adobe資料夾、共用資料夾和您公司專屬的資料夾。

   >[!NOTE]
   >
   >在開始從Package Share下載套件之前，請確定您擁有必要 [的存取權](#access-to-package-share)。

1. 導覽至您要下載的套件，然後按一下「下 **載」**。

1. 返回或導覽至AEM例 **項上的Package Manager** 。 然後導覽至您剛下載的套件。

   >[!NOTE]
   >
   >若要尋找您下載的套件，請依照與「套件共用」中相同的路徑進行。 例如，如果您從「套件共用」中的下列路徑下載套件：
   >
   >**套件** >公 **用** >修補 **程式**
   然後，在本地實例的「包管理器」中，該包也將顯示在：
   **套件** >公 **用** >修補 **程式**

1. 按一 **下「安裝** 」，將套件安裝至您的本機AEM安裝。

   >[!NOTE]
   如果實例上已安裝了軟體包，則軟體包旁會出現「 **Installed** （已安裝）」指示符，而不是「 **Install** （安裝）」按鈕。

   >[!CAUTION]
   安裝軟體包可以覆蓋儲存庫中的現有內容。 因此，我們建議您先執行「 **測試安裝** 」。 這可讓您檢查套件包含的內容是否與您現有的內容衝突。

### 從包共用將包下載到檔案系統 {#downloading-packages-to-your-file-system-from-package-share}

[下載和安裝](#downloading-and-installing-packages-from-package-share) ，非常方便，但如有需要，您也可以下載套件並儲存至本機檔案系統：

1. 在「套件共用」中，按一下套件圖示或名稱。
1. 按一下「 **資產** 」標籤。
1. 按一 **下「下載至磁碟」**。

### 上傳套件 {#uploading-a-package}

透過「封裝共用」，您可以將封裝上傳至您公司內部的封裝共用區域。 這可讓您在公司內分享。

這些套件 *不適用於* 一般AEM社群，但適用於所有在您公司註冊的使用者。

若要上傳您公司內部的套件共用套件：

>[!CAUTION]
若要將套件上傳至「封裝共用」，您必須先在本機「套件管理員」上建立以貴公司命名的群組資料夾。 例如geometrixx。 所有要上載以供共用的包都必須放置在此組資料夾中。
不能共用「包管理器」主清單或其他資料夾中的包。

1. 開啟「套 **件管理器** 」，並導覽至您要上傳的套件。

1. 按一下套件圖示以開啟它。
1. 按一 **下「共用** 」以開啟對話方塊，將套件上傳至「套件共用」。
1. 如果尚未登錄到「包共用」，則需要輸入您的登錄憑據。

   當您登入時，AEM會顯示要上傳之套件的詳細資訊：

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 按一 **下「** Share」（共用），將套件上傳至您公司的內部「Package Share」（套件共用）。

   AEM會顯示狀態並指出封裝完成上傳的時間，之後您可以按一下 **x** （右上角）以退出「 **Share Package** 」（共用封裝）視窗。

1. 上傳完成後，您可以導覽至公司的內部資料夾，以查看您剛共用的套件。

>[!NOTE]
若要修改「封裝共用」上可用的封裝，您必須下載它、重新建立它，然後再將它上傳至「封裝共用」。

### 刪除包 {#deleting-a-package}

您只能刪除由上載的包，如下所述：

1. 在公司樹中，檢查包含該包的包組。
1. 按一下套件。
1. 按一下刪除按鈕。

   ![chlimage_1-18](do-not-localize/chlimage_1-30.png)

1. 按一 **下「刪除** 」，確認您要刪除套件。

### 將包設為半私有 {#making-packages-semi-private}

您可以在組織外部共用套件，但不能公開共用。 這些方案將被視為半私有。 若要共用這些半私用套件，您需要Adobe支援的協助。 若要這麼做，請開啟Adobe支援的票證，要求將套件提供給組織以外的機構使用。 他們會要求您提供您要授與套件存取權的Adobe ID清單。

## 軟體散發（測試版） {#software-distribution-beta}

[Software Distribution](https://downloads.experiencecloud.adobe.com) 是專為簡化AEM套件的搜尋和下載而設計的全新使用者介面。 它目前為測試版狀態，且僅能以雲端服務客戶及Adobe員工身分存取Adobe Managed Services和AEM。

>[!NOTE]
* [Package Share](#package-share) 將一直運作，直到所有客戶都能存取「軟體散發」。
* 所有軟體包都可從「軟體包共用」和「軟體分發」中獲得。


>[!CAUTION]
目前，AEM套件管理程式無法與「軟體散發」搭配使用，您可將套件下載至本機磁碟。

