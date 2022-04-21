---
title: 安裝和配置文檔服務
seo-title: Installing and configuring document services
description: 安裝AEM Forms文檔服務以建立、匯編、分發、歸檔PDF文檔、添加數字簽名以限制對文檔的訪問，並對BarcodedForms解碼。
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 4b3327ed46024662813bb538f8338c59e508e10e
workflow-type: tm+mt
source-wordcount: '5330'
ht-degree: 1%

---

# 安裝和配置文檔服務 {#installing-and-configuring-document-services}

AEM Forms提供一組OSGi服務，以完成不同的文檔級操作，例如，建立、匯編、分發和歸檔PDF文檔、添加數字簽名以限制對文檔的訪問，以及對Barcoded Bion解碼等服務。 這些服務包含在AEM Forms附加包中。 這些服務統稱為文檔服務。 可用文檔服務及其主要功能清單如下：

* **匯編程式服務：** 使您能夠組合、重新排列和擴展PDF和XDP文檔，並獲取有關PDF文檔的資訊。 它還幫助將PDF文檔轉換為PDF/A標準，將PDF forms、XML表單和PDF forms轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。 有關詳細資訊，請參見 [匯編程式服務](/help/forms/using/assembler-service.md)。

* **ConvertPDF服務：** 使您能夠將PDF文檔轉換為PostScript或影像檔案(JPEG、JPEG2000、PNG和TIFF)。 有關詳細資訊，請參見 [ConvertPDF服務](/help/forms/using/using-convertpdf-service.md)。

* **巴克德Forms社：** 使您能夠從條形碼的電子影像中提取資料。 該服務接受包括一個或多個條形碼的TIFF和PDF檔案作為輸入，並提取條形碼資料。 有關詳細資訊，請參見 [巴克德Forms局](/help/forms/using/using-barcoded-forms-service.md)。

* **DocAssurance服務：** 使您能夠加密和解密文檔，擴展具有其他使用權限的Adobe Reader的功能，並向文檔添加數字簽名。 Doc Assurance服務包含三項服務：簽名、加密和讀取器擴展。 有關詳細資訊，請參見 [DocAssurance服務](/help/forms/using/overview-aem-document-services.md)。

* **加密服務：** 使您能夠加密和解密文檔。 當文檔被加密時，其內容將變得不可讀。 授權用戶可以解密文檔以獲得對其內容的訪問。 有關詳細資訊，請參見 [加密服務](/help/forms/using/overview-aem-document-services.md#encryption-service)。

* **Forms社：** 允許您建立互動式資料捕獲客戶端應用程式，這些應用程式驗證、處理、轉換和傳遞通常在Forms設計器中建立的表單。 Forms服務提供您開發為PDF文檔的任何窗體設計。 有關詳細資訊，請參見 [Forms](/help/forms/using/forms-service.md)。

* **輸出服務：** 使您能夠以不同格式建立文檔，包括PDF、雷射打印機格式和標籤打印機格式。 雷射打印機格式為PostScript和打印機控制語言(PCL)。 有關詳細資訊，請參見 [輸出服務](/help/forms/using/output-service.md)。

* **PDF生成器服務：** PDF生成器服務提供API以將本機檔案格式轉換為PDF。 它還將PDF轉換為其他檔案格式，並優化PDF文檔的大小。 有關詳細資訊，請參見 [PDF生成器服務](aem-document-services-programmatically.md#pdfgeneratorservice)。

* **Reader分機服務：** 通過擴展Adobe Reader的功能並附加使用權限，使您的組織能夠輕鬆共用互動式PDF文檔。 該服務激活在使用Adobe Reader開啟PDF文檔時不可用的功能，例如向文檔添加註釋、填寫表單和保存文檔。 有關詳細資訊，請參見 [Reader分機服務](/help/forms/using/overview-aem-document-services.md#reader-extension-service)。

* **簽名服務：** 允許您在伺服器上使用數字簽名和AEM文檔。 例如，簽名服務通常用於以下情況：

   * 伺服器AEM在將表單發送給用戶以使用Acrobat或Adobe Reader開啟之前對表單進行認證。
   * 服AEM務器驗證已通過使用Acrobat或Adobe Reader添加到表單的簽名。
   * 服AEM務器代表公證員簽署表格。

   簽名服務訪問儲存在信任儲存中的證書和憑據。 有關詳細資訊，請參見 [簽名服務](/help/forms/using/aem-document-services-programmatically.md)。

AEM Forms是強大的企業級平台，文檔服務只是AEM Forms的一項功能。 有關權能的完整清單，請參見 [AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加軟體包是部署到的應AEM用程式 通常，只需一個實AEM例（作者或發佈）即可運行AEM Forms文檔服務。 建議使用以下拓撲來運行AEM Forms文檔服務。 有關拓撲的詳細資訊，請參見 [用於AEM Forms的體系結構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![用於AEM Forms的體系結構和部署拓撲](do-not-localize/document-services.png)

>[!NOTE]
>
>儘管AEM Forms允許您從單個伺服器設定和運行所有功能，但您應該執行容量規劃、負載平衡，並針對生產環境中的特定功能設定專用伺服器。 例如，對於使用PDF生成器服務每天轉換數千頁和多個自適應表單以捕獲資料的環境，請為PDF生成器服務和自適應表單功能設定單獨的AEM Forms伺服器。 它有助於提供最佳效能並獨立擴展伺服器。

## 系統要求 {#system-requirements}

在開始安裝和配置AEM Forms文檔服務之前，請確保：

* 硬體和軟體基礎架構已到位。 有關支援的硬體和軟體的詳細清單，請參見 [技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實例AEM已啟動並正在運行。 在術AEM語中，「實例」是在作者或發AEM布模式下在伺服器上運行的副本。 通常，您只需一個實AEM例（作者或發佈）即可運行AEM Forms文檔服務：

   * **作者**:用於AEM建立、上載和編輯內容以及管理網站的實例。 一旦內容準備好投入使用，就會將其複製到發佈實例。
   * **發佈**:通過AEMInternet或內部網路向公眾提供已發佈內容的實例。

* 滿足記憶體要求。 AEM Forms附加軟體包要求：

   * 15 GB臨時空間，用於基於Microsoft® Windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 安裝了PDF生成器在Microsoft® Windows和Linux®上執行轉換所需的客戶端軟體：

   * **Microsoft® Windows**:安裝 [Microsoft®辦公室](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) 或 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**:安裝 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* 在Microsoft® Windows上，PDF生成器支援WebKit、AcrobatWebCapture和PhantomJS轉換路由，以將HTML檔案轉換為PDF文檔。
>* 在基於UNIX的作業系統上，PDF生成器支援WebKit和PhantomJS轉換路由，以將HTML檔案轉換為PDF文檔。
>


### 基於UNIX的作業系統的額外要求 {#extrarequirements}

如果使用基於UNIX的作業系統，請從相應作業系統的安裝介質安裝以下軟體包：

<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>外</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>自由型</li>
    </ul> </td>
   <td>
    <ul>
     <li>庫</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>茲利布</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>液體</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>格列布</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>方配</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>利布希內拉馬</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(僅PDF生成器)**)安裝32位版本的libcurl、libcrypto和libssl庫，並建立以下符號連結。 符號連結指向各個庫的最新版本：

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(僅限PDF生成器)** PDF生成器服務支援WebKit和PhantomJS路由，以將HTML檔案轉換為PDF文檔。 要啟用PhantomJS路由的轉換，請安裝下面列出的64位庫。 通常，已安裝這些庫。 如果缺少任何庫，請手動安裝：

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc.s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## 預安裝配置 {#preinstallationconfigurations}

安裝前配置部分中列出的配置僅適用於PDF生成器服務。 如果未配置PDF生成器服務，可跳過預安裝配置部分。

### 安裝Adobe Acrobat和第三方應用程式 {#install-adobe-acrobat-and-third-party-applications}

如果您要使用PDF生成器服務將本機檔案格式(如Microsoft® Word、Microsoft® Excel、Microsoft® PowerPoint、OpenOffice、WordPerfect X7和Adobe Acrobat)轉換為PDF文檔，請確保這些應用程式安裝在AEM Forms伺服器上。

>[!NOTE]
>
>* 如果您的AEM Forms伺服器處於離線或安全環境中，且Internet無法激活Adobe Acrobat，請參閱 [離線激活](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) 以便激活這類Adobe Acrobat。
>* Adobe Acrobat、Microsoft® Word、Excel和Powerpoint僅可用於Microsoft® Windows。 如果使用基於UNIX的作業系統，請安裝OpenOffice以將富文本檔案和支援的Microsoft® Office檔案轉換為PDF文檔。
>* 關閉安裝Adobe Acrobat和第三方軟體後顯示的所有對話框，供配置為使用PDF生成器服務的所有用戶使用。
>* 至少啟動一次所有已安裝的軟體。 關閉所有配置為使用PDF生成器服務的用戶的所有對話框。
>* [檢查您的Adobe Acrobat序列號的到期日期](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) 並設定更新許可證或 [遷移序列號](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 根據到期日。


安裝Acrobat後，開啟Microsoft® Word。 在 **Acrobat** 按鈕 **建立PDF** 並將電腦上可用的.doc或.docx檔案轉換為PDF文檔。 如果轉換成功，AEM Forms已準備好將Acrobat與PDF生成器服務配合使用。

### 設定環境變數 {#setup-environment-variables}

為32位和64位Java開發工具包、第三方應用程式和Adobe Acrobat設定環境變數。 環境變數應包含用於啟動相應應用程式的執行檔的絕對路徑，例如，下表列出了幾個應用程式的環境變數：

<table>
 <tbody>
  <tr>
   <td><p><strong>應用程式</strong></p> </td>
   <td><p><strong>環境變數</strong></p> </td>
   <td><p><strong>範例</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK（64位）</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat路徑</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>記事本</strong></p> </td>
   <td><p>記事本路徑</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 所有環境變數和相應的路徑都區分大小寫。
>* JAVA_HOME、JAVA_HOME_32和Acrobat_PATH（僅限Windows）是必需的環境變數。
>* 環境變數OpenOffice_PATH設定為安裝資料夾，而不是執行檔的路徑。
>* 請勿為Microsoft® Office應用程式（如Word、PowerPoint、Excel和Project）或AutoCAD設定環境變數。 如果這些應用程式安裝在伺服器上，則生成PDF服務將自動啟動這些應用程式。
>* 在基於UNIX的平台上，以/root身份安裝OpenOffice。 如果OpenOffice未作為根目錄安裝，則PDF生成器服務將無法將OpenOffice文檔轉換為PDF文檔。 如果需要以非根用戶身份安裝和運行OpenOffice，請為非根用戶提供sudo權限。
>* 如果在基於UNIX的平台上使用OpenOffice，請運行以下命令來設定路徑變數：
>
> `export OpenOffice_PATH=/opt/openoffice.org4`

### (僅適用於IBM® WebSphere®)配置IBM® SSL套接字提供程式 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

執行以下步驟來配置IBM® SSL套接字提供程式：

1. 建立java.security檔案的副本。 檔案的預設位置是 `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`。
1. 開啟複製的java.security檔案進行編輯。
1. 更改預設SSL套接字工廠以使用JSSE2工廠，而不是預設的IBM® WebSphere®工廠：

   **預設內容：**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **修改的內容：**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. 要使AEM Forms伺服器能夠使用更新的java.security檔案，在啟動AEM Forms伺服器時，請添加以下java參數：

   `-Djava.security.properties= [path of newly created Java.security file].`

### （僅限Windows）配置安裝墨跡和手寫服務 {#configure-install-ink-and-handwriting-service}

如果運行的是Microsoft® Windows Server，請配置墨跡和手寫服務。 要開啟使用Microsoft® Office墨跡書寫功能的Microsoft® PowerPoint檔案，需要此服務：

1. 開啟伺服器管理器。 按一下 **[!UICONTROL 伺服器管理器]** 表徵圖。
1. 按一下 **[!UICONTROL 添加功能]** 的 **[!UICONTROL 功能]** 的子菜單。 選擇 **[!UICONTROL 墨跡和手寫服務]** 的子菜單。
1. **[!UICONTROL 選擇功能]** 對話框 **[!UICONTROL 墨跡和手寫服務]** 的下界。 按一下 **[!UICONTROL 安裝]** 並且安裝了服務。

### （僅限Windows）配置Microsoft® Office的檔案塊設定 {#configure-the-file-block-settings-for-microsoft-office}

更改Microsoft® Office信任中心設定，使PDF生成器服務能夠轉換使用舊版Microsoft® Office建立的檔案。

1. 開啟Microsoft® Office應用程式。 例如，Microsoft® Word。 導航到 **[!UICONTROL 檔案]**> **[!UICONTROL 選項]**。 將出現「選項」對話框。

1. 按一下 **[!UICONTROL 信任中心]**，然後按一下 **[!UICONTROL 信任中心設定]**。
1. 在 **[!UICONTROL 信任中心設定]**&#x200B;按一下 **[!UICONTROL 檔案塊設定]**。
1. 在 **[!UICONTROL 檔案類型]** 清單，取消選擇 **[!UICONTROL 開啟]** 檔案類型，允許PDF生成器服務轉換為PDF文檔。

### （僅限Windows）授予「替換進程級別令牌」權限 {#grant-the-replace-a-process-level-token-privilege}

用於啟動應用程式伺服器的用戶帳戶要求 **替換進程級別令牌** 權限。 本地系統帳戶具有 **替換進程級別令牌** 權限。 對於使用「本地管理員」組的用戶運行的伺服器，必須明確授予該權限。 執行以下步驟授予權限：

1. 開啟Microsoft® Windows的組策略編輯器。 要開啟組策略編輯器，請按一下 **[!UICONTROL 開始]**&#x200B;鍵 **gpedit.msc** 在「開始搜索」框中，按一下 **[!UICONTROL 組策略編輯器]**。
1. 導航到 **[!UICONTROL 本地電腦策略]** > **[!UICONTROL 電腦配置]** > **[!UICONTROL Windows設定]** > **[!UICONTROL 安全設定]** > **[!UICONTROL 本地策略]** > **[!UICONTROL 用戶權限分配]** 編輯 **[!UICONTROL 替換進程級別令牌]** 策略並包括「管理員」組。
1. 將用戶添加到「替換進程級別令牌」條目。

### （僅限Windows）為非管理員啟用PDF生成器服務 {#enable-the-pdf-generator-service-for-non-administrators}

您可以啟用非管理員用戶使用PDF生成器服務。 通常，只有具有管理權限的用戶才能使用該服務：

1. 建立環境變數PDFG_NON_ADMIN_ENABLED。
1. 將環境變數的值設定為TRUE。
1. 重新啟動AEM Forms實例。

### （僅限Windows）禁用用戶帳戶控制(UAC) {#disable-user-account-control-uac}

1. 要訪問系統配置實用程式，請轉至 **[!UICONTROL 開始>運行]** 然後輸入 **[!UICONTROL MSCONFIG]**。
1. 按一下 **[!UICONTROL 工具]** 向下滾動，選擇 **[!UICONTROL 更改UAC設定]**。 按一下 **[!UICONTROL 啟動]** 命令。
1. 將滑塊調整到「從不通知」級別。 完成後，關閉命令窗口並關閉「System Configuration（系統配置）」窗口。
1. 驗證UAC的註冊表設定是否設定為0（零）。 執行以下步驟驗證：

   1. Microsoft®建議在修改註冊表之前先備份它。 有關詳細步驟，請參見 [如何在Windows中備份和還原註冊表](https://support.microsoft.com/en-us/help/322756)。
   1. 開啟Microsoft® Windows註冊表編輯器。 要開啟註冊表編輯器，請轉到「開始」>「運行」，鍵入regedit，然後按一下「確定」。
   1. 導航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. 確保EnableLUA的值設定為0（零）。
   1. 確保 **啟用LUA** 設定為0（零）。 如果值不是0，請將值更改為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

### （僅限Windows）禁用錯誤報告服務 {#disable-error-reporting-service}

使用Windows Server上的PDF生成器服務將文檔轉換為PDF時，Windows Server偶爾會報告執行檔遇到問題，必須關閉。 但是，它不影響PDF轉換，因為它在後台繼續。

為避免收到錯誤，可以禁用Windows錯誤報告。 有關禁用錯誤報告的詳細資訊，請參閱 [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx)。

### （僅限Windows）配置HTML到PDF轉換 {#configure-html-to-pdf-conversion}

PDF生成器服務提供WebKit、WebCapture和PhantomJS路由或方法，以將HTML檔案轉換為PDF文檔。 在Windows上，要啟用WebKit和AcrobatWebCapture路由的轉換，請將Unicode字型複製到%windir%\fonts目錄。

>[!NOTE]
>
>無論何時將新字型安裝到字型資料夾，請重新啟動AEM Forms實例。

### （僅基於UNIX的平台）用於HTML到PDF轉換的額外配置  {#extra-configurations-for-html-to-pdf-conversion}

在基於UNIX的平台上，PDF生成器服務支援WebKit和PhantomJS路由，以將HTML檔案轉換為PDF文檔。 要啟用HTML到PDF轉換，請執行以下適用於您首選轉換路由的配置：

### （僅限基於UNIX的平台）啟用對Unicode字型的支援（僅限WebKit） {#enable-support-for-unicode-fonts-webkit-only}

將Unicode字型複製到適合您的系統的以下任意目錄：

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType(Solaris™)

>[!NOTE]
>
>* 在Red Hat® Enterprise Linux® 6.x及更高版本上，Courier字型不可用。 要安裝courier字型，請下載font-ibm-type1-1.0.3.zip存檔檔案。 在/usr/share/fonts處解壓縮存檔檔案。 建立從/usr/share/X11/fonts到/usr/share/fonts的符號連結。
>* 從Html2PdfSvc/bin和/usr/share/fonts目錄中刪除所有.lst字型快取檔案。
>* 確保目錄/usr/lib/X11/fonts和/usr/share/fonts存在。 如果目錄不存在，則使用ln命令建立從/usr/share/X11/fonts到/usr/lib/X11/fonts的符號連結，以及從/usr/share/fonts到/usr/share/X11/fonts的其他符號連結。 另外，請確保信使字型位於/usr/lib/X11/fonts。
>* 確保所有字型（Unicode和非Unicode）都可在/usr/share/fonts或/usr/share/X11/fonts目錄中使用。
>* 以非根用戶身份運行PDF生成器服務時，請提供對所有字型目錄的非根用戶讀寫權限。
>* 無論何時將新字型安裝到字型資料夾，請重新啟動AEM Forms實例。
>


## 安裝AEM Forms載入項軟體包 {#install-aem-forms-add-on-package}

AEM Forms附加軟體包是部署到的應AEM用程式 該軟體包包含AEM Forms文檔服務和其他AEM Forms功能。 執行以下步驟以安裝軟體包：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

   您也可以通過中列出的直接連結下載軟體包 [AEM Forms釋放](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 文章。

1. 安裝軟體包後，系統會提示您重新啟動實AEM例。 **不要立即停止伺服器。** 停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出現在 `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log檔案和日誌穩定。

## 安裝後配置 {#post-installation-configurations}

### 為RSA/BouncyCastle庫配置引導委派  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. 停止實AEM例。 導航到 [AEM安裝目錄]\crx-quickstart\conf\ folder。 開啟sling.properties檔案進行編輯。

   如果您使用 `[AEM installation directory]\crx-quickstart\bin\start.bat` 要啟動實AEM例，請編輯位於 `[AEM_root]\crx-quickstart\`。

1. 將以下屬性添加到sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. （僅限AIX®）將以下屬性添加到sling.properties檔案：

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 保存並關閉檔案。

### 配置字型管理器服務  {#configuring-the-font-manager-service}

1. 登錄到 [配AEM置管理器](http://localhost:4502/system/console/configMgr) 作為管理員。
1. 查找並開啟 **[!UICONTROL CQ-DAM-Handler-Gibson字型管理器]** 服務。 指定「系統字型」、「Adobe伺服器字型」和「客戶字型」目錄的路徑。 按一下「**[!UICONTROL 儲存]**」。

   >[!NOTE]
   >
   >您使用Adobe以外各方提供的字型的權利受此類各方提供的這些字型的許可協定的約束，而使用Adobe軟體的許可不包括在您的許可範圍內。 Adobe建議您在將非Adobe字型與Adobe軟體一起使用之前，先檢查並確保遵守所有適用的非Adobe許可協定，特別是有關在伺服器環境中使用字型的協定。
   > 將新字型安裝到字型資料夾時，請重新啟動AEM Forms實例。

### 配置本地用戶帳戶以運行PDF生成器服務  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

運行PDF生成器服務需要本地用戶帳戶。 有關建立本地用戶的步驟，請參見 [在Windows中建立用戶帳戶](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) 或在基於UNIX的平台中建立用戶帳戶。

1. 開啟 [AEM FormsPDF發電機配置](http://localhost:4502/libs/fd/pdfg/config/ui.html) 的子菜單。

1. 在 **[!UICONTROL 用戶帳戶]** 頁籤，提供本地用戶帳戶的憑據，然後按一下 **[!UICONTROL 提交]**。 如果Microsoft® Windows提示，允許訪問用戶。 成功添加後，配置的用戶將顯示在 **[!UICONTROL 您的用戶帳戶]** 的 **[!UICONTROL 用戶帳戶]** 頁籤。

### 配置超時設定 {#configure-the-time-out-settings}

1. 在 [配置管理器](http://localhost:4502/system/console/configMgr)，定位並開啟 **[!UICONTROL Jacorb ORB提供程式]** 服務。

   將以下內容添加到 **[!UICONTROL 自定義屬性.name]** 按一下 **[!UICONTROL 保存]**。 它將掛起的答復超時（也稱為CORBA客戶端超時）設定為600秒。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. 登錄到作AEM者實例並導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置PDF生成器]**。 預設URL為 <http://localhost:4502/libs/fd/pdfg/config/ui.html>。

   開啟 **[!UICONTROL 常規配置]** 頁籤，並修改環境的以下欄位的值：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
   <td>預設值</td>
  </tr>
  <tr>
   <td>伺服器轉換逾時</td>
   <td>PDFG轉換在伺服器轉換超時中定義的秒數內保持活動狀態</td>
   <td>270秒<br /> </td>
  </tr>
  <tr>
   <td>PDFG 清理掃描秒數</td>
   <td>執行轉換後操作所需的秒數。<br /> </td>
   <td>3600秒</td>
  </tr>
  <tr>
   <td>工作逾期秒數</td>
   <td>允許PDF生成器服務運行轉換的持續時間。 確保「Job Expiration Seconds（作業過期秒）」的值大於「PDFG Cleanup Scan Seconds（PDFG清理掃描秒）」值。</td>
   <td>7200秒</td>
  </tr>
 </tbody>
</table>

### （僅限Windows）為PDF生成器服務配置Acrobat {#configure-acrobat-for-the-pdf-generator-service}

在Microsoft® Windows上，PDF生成器服務使用Adobe Acrobat將支援的檔案格式轉換為PDF文檔。 執行以下步驟為PDF生成器服務配置Adobe Acrobat:

1. 開啟Acrobat並選擇 **[!UICONTROL 編輯]**> **[!UICONTROL 首選項]**> **[!UICONTROL 更新程式]**。 在檢查更新中，取消選擇 **[!UICONTROL 自動安裝更新]**，然後按一下 **[!UICONTROL 確定]**。 關閉Acrobat。
1. 按兩下系統上的PDF文檔。 當Acrobat首次啟動時，將出現「登錄」、「歡迎」螢幕和「EULA」對話框。 為配置為使用PDF生成器的所有用戶關閉這些對話框。
1. 運行PDF生成器實用程式批處理檔案，為PDF生成器服務配置Acrobat:

   1. 開啟 [包管AEM理器](http://localhost:4502/crx/packmgr/index.jsp) 下載 `adobe-aemfd-pdfg-common-pkg-[version].zip` 檔案。
   1. 解壓縮下載的.zip檔案。 以管理權限開啟命令提示符。
   1. 導航到 `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\adobe-aemfd-pdfg-common-pkg-[version]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` 的子菜單。 運行以下批處理檔案：

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat配置為使用PDF生成器服務運行。

1. 運行 [系統就緒性工具(SRT)](#SRT) 驗證Acrobat安裝。

### （僅限Windows）配置主路由以進行HTML到PDF轉換 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF生成器服務提供多條路由，以將HTML檔案轉換為PDF文檔：Webkit、AcrobatWebCapture（僅限Windows）和PhantomJS。 Adobe建議使用PhantomJS路由，因為它能夠處理動態內容，並且不依賴於32位庫、32位JDK，或者不需要額外的字型。 此外，PhantomJS路由不需要sudo或根訪問權來運行轉換。

HTML到PDF轉換的預設主路由是Webkit。 要更改轉換路由：

1. 在作AEM者實例上，導航至 **[!UICONTROL 工具]**> **[!UICONTROL Forms]**> **[!UICONTROL 配置PDF生成器]**。

1. 在 **[!UICONTROL 常規配置]** 頁籤 **[!UICONTROL 用於HTML到PDF轉換的主要路由]** 下拉。

### 初始化全局信任儲存 {#intialize-global-trust-store}

使用信任儲存管理，您可以導入、編輯和刪除在伺服器上信任的證書，以驗證數字簽名和證書身份驗證。 您可以導入和導出任意數量的證書。 導入證書後，可以編輯信任設定和信任儲存類型。 執行以下步驟以初始化信任儲存：

1. 以管理員身份登錄AEM Forms實例。
1. 轉到  **[!UICONTROL 工具]** >  **[!UICONTROL 安全]** >  **[!UICONTROL 信任儲存]**。
1. 按一下  **[!UICONTROL 建立信任儲存]**。 設定密碼並點擊 **[!UICONTROL 保存]**。

### 為Reader擴展和加密服務設定證書 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance服務可以將使用權限應用於PDF文檔。 要對PDF文檔應用使用權限，請配置證書。

在設定證書之前，請確保您有：

* 證書檔案(.pfx)。

* 證書附帶的私鑰密碼。

* 私人金鑰別名. 可以執行Java keytool命令來查看私鑰別名：
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 密鑰庫檔案密碼。 如果使用的是Adobe的Reader擴展證書，則密鑰庫檔案密碼始終與私鑰密碼相同。

執行以下步驟來配置證書：

1. 以管理員身份登錄到AEM Author實例。 轉到 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
1. 按一下 **[!UICONTROL 名稱]** 的子菜單。 的 **[!UICONTROL 編輯用戶設定]** 的上界。 在AEM Author實例上，證書駐留在KeyStore中。 如果您之前未建立KeyStore，請按一下 **[!UICONTROL 建立密鑰儲存]** 並為KeyStore設定新密碼。 如果伺服器已包含KeyStore，請跳過此步驟。  如果使用的是Adobe的Reader擴展證書，則密鑰庫檔案密碼始終與私鑰密碼相同。
1. 在 **[!UICONTROL 編輯用戶設定]** ，選擇 **[!UICONTROL 密鑰儲存]** 頁籤。 展開 **[!UICONTROL 從密鑰儲存檔案添加私鑰]** 選項並提供別名。 別名用於執行Reader擴展操作。
1. 要上載證書檔案，請按一下 **[!UICONTROL 選擇密鑰儲存檔案]** 上傳 &lt;filename>.pfx檔案。

   添加 **[!UICONTROL 密鑰儲存密碼]**。 **[!UICONTROL 私鑰密碼]**, **[!UICONTROL 私鑰別名]** 與證書關聯到相應欄位的。 按一下 **[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >在生產環境中，將評估憑據替換為生產憑據。 在更新過期或評估憑據之前，請確保刪除舊Reader擴展憑據。

1. 按一下 **[!UICONTROL 保存並關閉]** 的 **[!UICONTROL 編輯用戶設定]** 的子菜單。

### 啟用AES-256 {#enable-aes}

要對PDF檔案使用AES 256加密，請獲取並安裝Java加密擴展(JCE)無限強度管轄權策略檔案。 替換jre/lib/security資料夾中的local_policy.jar和US_export_policy.jar檔案。 例如，如果使用Sun JDK，請將下載的檔案複製到 `[JAVA_HOME]/jre/lib/security` 的子菜單。

匯編器服務取決於Reader擴展服務、簽名服務、Forms服務和輸出服務。 執行以下步驟以驗證所需的服務是否已啟動並正在運行：

1. 登錄到URL `https://'[server]:[port]'/system/console/bundles` 作為管理員。
1. 搜索以下服務並確保服務已啟動並正在運行：

<table>
 <tbody>
  <tr>
   <th>服務名稱</th>
   <th>組合包名稱</th>
  </tr>
  <tr>
   <td>簽名服務</td>
   <td>adobe-aemfd簽名</td>
  </tr>
  <tr>
   <td>Reader 延伸模組服務</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Forms 服務</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>輸出服務</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

## 已知問題和故障排除 {#known-issues-and-troubleshooting}

* 如果壓縮的輸入檔案在檔案名中包含雙位元組字元的HTML檔案，則PDF到HTML轉換失敗。 要避免此問題，請在命名HTML檔案時不要使用雙位元組字元。

* 在基於UNIX的作業系統上，執行以下操作以查找任何缺少的庫：

1. 導航到 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 運行以下命令以列出PhantomJSHTML到PDF轉換所需的所有庫。

   `ldd phantomjs`

   運行以下命令以列出缺少的庫。

   `ldd phantomjs | grep not`

1. 手動安裝缺少的庫。

## 系統就緒性工具(SRT) {#SRT}

「系統就緒性」工具檢查機器是否配置正確以運行PDF生成器轉換。 該工具在指定路徑上生成報告。 要運行工具，請執行以下操作：

1. 開啟命令提示符。 導航到 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` 的子菜單。

1. 從命令提示符運行以下命令：

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   該命令生成報告，並建立srt_config.yaml檔案。

   >[!NOTE]
   >
   > * 如果系統就緒工具報告pdfgen.api檔案在Acrobat插件資料夾中不可用，則從 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` 目錄 `[Acrobat_root]\Acrobat\plug_ins` 的子菜單。
   >
   > * 可以使用srt_config.yaml檔案配置的各種設定。 檔案格式為：


   ```
      # =================================================================
      # SRT Configuration
      # =================================================================
      #Note - follow correct format to avoid parsing failures
      #e.g. <param name>:<space><param value> 
      #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
      locale: en
   
      #aemTempDir: AEM Temp direcotry
      aemTempDir:
   
      #users: provide PDFG converting users list
      #users:
      # - user1
      # - user2
      users:
   
      #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
      profile:
   
      #outputDir: directory where output files will be saved
      outputDir:
   ```

1. 導航到 `[Path_of_reports_folder]`. 開啟SystemReadinessTool.html檔案。 驗證報告並修復上述問題。

## 疑難排解

如果即使在修復了SRT工具報告的所有問題後仍面臨問題，請執行以下檢查：

在執行以下檢查之前，請確保 [系統就緒性工具](#SRT) 不報告任何錯誤。

+++ Adobe Acrobat

* 僅確保 [支援的版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 安裝了Microsoft® Office（32位）和Adobe Acrobat，並取消了開啟對話。
* 確保禁用Adobe Acrobat更新服務。
* 確保 [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) 批處理檔案以管理員權限運行。
* 確保在PDF配置UI中添加PDF生成器用戶。
* 確保 [替換進程級別令牌](#grant-the-replace-a-process-level-token-privilege) 為PDF生成器用戶添加權限。
* 確保為AcrobatOffice應用程式啟用MicrosoftPDFMaker Office COM載入項。

+++

+++Open Office

**Microsoft® Windows**

* 確保 [支援的版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 已安裝Microsoft辦公室，並取消所有應用程式的開啟對話。
* 確保在PDF配置UI中添加PDF生成器用戶。
* 確保PDF生成器用戶是管理員組的成員， [替換進程級別令牌](#grant-the-replace-a-process-level-token-privilege) 為用戶設定權限。
* 確保用戶在PDF生成器UI中配置，並執行以下操作：
   1. 使用PDF生成器用戶登錄Microsoft® Windows。
   1. 開啟Microsoft® Office或Open Office應用程式並取消所有對話框。
   1. 將AdobePDF設定為預設打印機。
   1. 將Acrobat設定為PDF檔案的預設程式。
   1. 使用「檔案」>「打印」和「Acrobat功能區」選項在MicrosoftOffice應用程式中手動轉換並取消所有對話框。
   1. 結束與轉換相關的所有進程，如winword.exe、powerpoint.exe和excel.exe。
   1. 重新啟動AEM Forms伺服器。

**Linux®**

* 確保 [支援的版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 已安裝Open Office，所有應用程式的開啟對話框均被取消，Office應用程式已成功啟動。
* 建立環境變數 `OpenOffice_PATH` 並將其設定為指向在 [控制台](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) 或dt（設備樹）配置檔案。
* 如果安裝OpenOffice時出現問題，請確保 [32位庫](#extrarequirements) OpenOffice安裝所需的內容可用。

+++

++HTML到PDF轉換問題

* 確保字型目錄已添加到PDF生成器配置UI中。

**Linux和Solaris（PhantomJS轉換路由）**

* 確保32位庫(libicudata.so.42)可用於基於Webkit的HTMLToPDF轉換，64位(libicudata.so.42 libs可用於基於PhantomJS的HTMLToPDF轉換。

* 運行以下命令以列出phantomjs的缺少庫：

   ```
   ldd phantomjs | grep not
   ```

* 確保JAVA_HOME_32環境變數指向正確的位置。

**Linux®和Solaris™（WebKit轉換路由）**

* 確保目錄 `/usr/lib/X11/fonts` 和 `/usr/share/fonts` 存在。 如果目錄不存在，請從建立符號連結 `/usr/share/X11/fonts` 至 `/usr/lib/X11/fonts` 另一個符號連結 `/usr/share/fonts` 至 `/usr/share/X11/fonts`。

   ```
   ln -s /usr/share/fonts /usr/share/X11/fonts
   
   ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
   ```

* 確保IBM字型在usr/share/fonts下複製。
* 確保電腦上提供ghost漏洞修復glibc。 使用預設包管理器更新到glibc的最新版本。 它包括Ghost漏洞修復。
* 確保系統上安裝了32位lib curl、libcrypto和libssl庫的最新版本。 還建立符號連結 `/usr/lib/libcurl.so` (或libcurl.a（用於AIX®）, `/usr/lib/libcrypto.so` （或libcrypto.a for AIX®）和 `/usr/lib/libssl.so` （或libssl.a for AIX®），指向各個庫的最新版本（32位）。

* 為IBM® SSL套接字提供程式執行以下步驟：
   1. 從中複製java.security檔案 `<WAS_Installed_JAVA>\jre\lib\security` 到你AEM Forms伺服器上的任何位置。 預設位置為「預設位置」為= `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`。

   1. 在複製的位置編輯java.security檔案，並更改JSSE2工廠的預設SSL Socket工廠（使用JSSE2工廠而不是WebSphere®）。

      更改以下預設JSSE套接字工廠：

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      替換為

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ 無法添加PDF生成器(PDFG)用戶

* 確保Windows上已安裝Microsoft® Visual C++ 2012 x86和Microsoft® Visual C++ 2013 x86（32位）可再發行軟體。

+++

+++自動化test故障

* 對於Microsoft® Office和OpenOffice，請手動執行至少一次轉換（作為每個用戶），以確保轉換過程中不會彈出對話框。 如果出現任何對話，則將其取消。 自動轉換過程中不應出現此類對話框。

* 在OSGi環境上的AEM Forms上運行自動化之前，請確保test包已安裝並處於活動狀態。

+++

+++多用戶轉換失敗

* 驗證伺服器日誌以檢查特定用戶的轉換是否失敗。（進程資源管理器可以幫助您檢查不同用戶的運行進程）

* 確保為PDF生成器配置的用戶具有本地管理權限。

* 確保PDF生成器用戶對LC temp和PDFG temp用戶具有讀、寫和執行權限。

* 對於Microsoft® Office和OpenOffice，請手動執行至少一次轉換（作為每個用戶），以確保轉換過程中不會彈出對話框。 如果出現任何對話，則將其取消。 自動轉換過程中不應出現此類對話框。

* 執行示例轉換。

+++

+++安裝在Adobe Acrobat伺服器上的AEM Forms許可證到期

* 如果你有Adobe Acrobat的現有許可證，而且已經過期， [下載最新版本的Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html)，並遷移序列號。 之前 [遷移序列號](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number)。

   * 使用以下命令生成prov.xml並使用prov.xml檔案（而不是中提供的命令）重新序列化現有安裝 [遷移序列號](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 編號文章。

      * 生成prov.xml

         ```
         adobe_prtk --tool=VolumeSerialize --generate --serial=<serialnum> [--leid=<LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=limited list of locales in xx_XX format or ALL>] [--provfile=<Absolute path to prov.xml>]
         ```

      * 卷序列化包（使用prov.xml檔案和新序列重新序列化現有安裝）:以管理員身份從PRTK安裝資料夾中運行以下命令，以序列化和激活客戶端電腦上部署的包：

         ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         ```

* 對於大型安裝，請使用 [AcrobatCustomization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) 刪除以前版本的Reader和Acrobat。 自定義安裝程式並將其部署到您組織的所有電腦。

+++

+++ AEM Forms伺服器處於離線或安全環境中，並且Internet無法激活Acrobat。

* 您可以在Adobe產品首次發佈後7天內聯機完成線上激活和註冊，或使用啟用網際網路的設備和產品序列號完成此過程。 有關詳細說明，請參見 [離線激活](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en)。

+++

## 後續步驟 {#next-steps}

您有一個運行中的AEM Forms文檔服務環境。 您可以通過以下方式使用文檔服務：

* [在OSGi上以表單為中心的工作流](/help/forms/using/aem-forms-workflow.md)
* [Watched 資料夾](/help/forms/using/watched-folder-in-aem-forms.md)
* [文檔服務API](/help/forms/using/aem-document-services-programmatically.md)
