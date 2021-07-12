---
title: 安裝和配置文檔服務
seo-title: 安裝和配置文檔服務
description: 安裝AEM Forms檔案服務，以建立、組合、分發、封存PDF檔案、新增數位簽名以限制檔案存取，以及將條碼式表單解碼。
seo-description: 安裝AEM Forms檔案服務，以建立、組合、分發、封存PDF檔案、新增數位簽名以限制檔案存取，以及將條碼式表單解碼。
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 2%

---

# 安裝和配置文檔服務 {#installing-and-configuring-document-services}

AEM Forms提供一組OSGi服務，以完成不同的檔案層級操作，例如建立、組合、分發和封存PDF檔案、新增數位簽名以限制檔案存取，以及將條碼式表單解碼等服務。 這些服務包含在AEM Forms附加元件套件中。 這些服務統稱為文檔服務。 可用文檔服務及其主要功能的清單如下：

* **組合器服務：** 可讓您組合、重新排列和擴增PDF和XDP檔案，並取得PDF檔案的相關資訊。此外，還可協助將PDF檔案轉換為PDF/A標準，將PDF forms、XML表單和PDF forms轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。 有關詳細資訊，請參閱[組合器服務](/help/forms/using/assembler-service.md)。

* **ConvertPDF服務：** 可讓您將PDF檔案轉換為PostScript或影像檔案（JPEG、JPEG 2000、PNG和TIFF）。如需詳細資訊，請參閱[ConvertPDF Service](/help/forms/using/using-convertpdf-service.md)。

* **條碼式Forms服務：** 可讓您從條碼的電子影像中擷取資料。該服務接受包含一個或多個條形碼的TIFF和PDF檔案作為輸入，並提取條形碼資料。 如需詳細資訊，請參閱[條碼式Forms服務](/help/forms/using/using-barcoded-forms-service.md)。

* **DocAssurance服務：** 可讓您加密和解密檔案、以其他使用權限擴充Adobe Reader的功能，以及將數位簽名新增至檔案。Doc Assurance服務包含三項服務：簽名、加密和讀取器擴展。 有關詳細資訊，請參閱[DocAssurance服務](/help/forms/using/overview-aem-document-services.md)。

* **加密服務：** 可讓您加密及解密檔案。文檔被加密後，其內容將變得不可讀。 授權用戶可以解密該文檔以獲得對其內容的訪問。 有關詳細資訊，請參閱[加密服務](/help/forms/using/overview-aem-document-services.md#encryption-service)。

* **Forms服務：** 可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳送通常在Forms Designer中建立的表單。Forms服務會轉譯您開發為PDF檔案的任何表單設計。 如需詳細資訊，請參閱[Forms服務](/help/forms/using/forms-service.md)。

* **輸出服務：** 可讓您以不同格式建立檔案，包括PDF、雷射打印機格式和標籤打印機格式。雷射打印機格式為PostScript和打印機控制語言(PCL)。 如需詳細資訊，請參閱[輸出服務](/help/forms/using/output-service.md)。

* **PDF產生器服務：** PDF產生器服務提供API，可將原生檔案格式轉換為PDF。它還能將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。 如需詳細資訊，請參閱[PDF產生器服務](aem-document-services-programmatically.md#pdfgeneratorservice)。

* **Reader擴充功能服務：** 透過擴充Adobe Reader的功能與其他使用權限，讓您的組織輕鬆共用互動式PDF檔案。此服務會啟用使用Adobe Reader開啟PDF檔案時無法使用的功能，例如新增註解至檔案、填寫表單及儲存檔案。 如需詳細資訊，請參閱[Reader擴充功能服務](/help/forms/using/overview-aem-document-services.md#reader-extension-service)。

* **簽名服務：** 可讓您在AEM伺服器上使用數位簽名和檔案。例如，簽名服務通常用於以下情況：

   * AEM伺服器會先驗證表單，再傳送給使用者，供使用Acrobat或Adobe Reader開啟。
   * AEM伺服器會使用Acrobat或Adobe Reader驗證已新增至表單的簽名。
   * AEM伺服器代表公證人簽署表格。

   簽名服務訪問儲存在信任儲存中的證書和憑據。 有關詳細資訊，請參閱[簽名服務](/help/forms/using/aem-document-services-programmatically.md)。

AEM Forms是功能強大的企業級平台，而檔案服務只是AEM Forms的其中一項功能。 如需功能的完整清單，請參閱[AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 一般而言，您只需要一個AEM例項（製作或發佈）即可執行AEM Forms檔案服務。 建議運行以下拓撲以運行AEM Forms文檔服務。 有關拓撲的詳細資訊，請參閱[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的架構和部署拓撲。

![適用於AEM Forms的架構和部署拓撲](do-not-localize/document-services.png)

>[!NOTE]
>
>雖然AEM Forms可讓您從單一伺服器設定和執行所有功能，但您應執行容量規劃、負載平衡，以及針對生產環境中的特定功能設定專用伺服器。 例如，針對使用PDF產生器服務每天轉換數千頁和多個最適化表單來擷取資料的環境，為PDF產生器服務和最適化表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並可獨立擴展伺服器。

## 系統需求 {#system-requirements}

開始安裝和設定AEM Forms檔案服務之前，請確定：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見[技術要求](/help/sites-deploying/technical-requirements.md)。

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在製作或發佈模式中，於伺服器上執行的AEM復本。 一般而言，您只需要一個AEM例項（製作或發佈）即可執行AEM Forms檔案服務：

   * **作者**:用於建立、上傳和編輯內容及管理網站的AEM例項。內容準備好上線後，就會複製到發佈執行個體。
   * **發佈**:透過網際網路或內部網路向公眾提供已發佈內容的AEM例項。

* 滿足記憶體要求。 AEM Forms附加元件套件需要：

   * 15 GB的臨時空間，用於基於Microsoft Windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 已安裝PDF產生器在Microsoft Windows和Linux上執行轉換所需的用戶端軟體：

   * **Microsoft Windows**:安 [裝](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Microsoft  [Office或Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**:安 [裝Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* 在Microsoft Windows上，PDF產生器支援WebKit、Acrobat WebCapture和PhantomJS轉換路由，以將HTML檔案轉換為PDF檔案。
>* 在以UNIX為基礎的作業系統上，PDF產生器支援WebKit和PhantomJS轉換路由，以將HTML檔案轉換為PDF檔案。

>



### 基於UNIX的作業系統的額外需求 {#extrarequirements}

如果使用基於UNIX的作業系統，請從相應作業系統的安裝介質安裝以下軟體包：

<table> 
 <tbody> 
  <tr> 
   <td> 
    <ul> 
     <li>expat</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libxcb</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>freetype</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXau</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libSM</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>zlib</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libICE</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libuuid</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>glibc</li> 
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
     <li>fontconfig</li> 
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
     <li>libXinerama</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

* **(僅限PDF產生器**)安裝32位元版本的libcurl、libcrypto和libssl程式庫，並建立下列符號連結。符號連結指向相應庫的最新版本：

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **（僅限PDF產生器）** PDF產生器服務支援WebKit和PhantomJS路由，將HTML檔案轉換為PDF檔案。若要啟用PhantomJS路由的轉換，請安裝下列64位元程式庫。 通常，已安裝這些程式庫。 如果缺少任何程式庫，請手動安裝：

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## 安裝前配置 {#preinstallationconfigurations}

安裝前設定區段中列出的設定僅適用於PDF產生器服務。 如果您未設定PDF產生器服務，可略過安裝前設定區段。

### 安裝Adobe Acrobat和協力廠商應用程式 {#install-adobe-acrobat-and-third-party-applications}

如果您打算使用PDF產生器服務將原生檔案格式(例如Microsoft Word、Microsoft Excel、Microsoft PowerPoint、OpenOffice、WordPerfect X7和Adobe Acrobat)轉換為PDF檔案，請確定這些應用程式已安裝在AEM Forms伺服器上。

>[!NOTE]
>
>* Adobe Acrobat、Microsoft Word、Excel和Powerpoint僅適用於Microsoft Windows。 如果您使用基於UNIX的作業系統，請安裝OpenOffice以將RTF檔案和支援的Microsoft Office檔案轉換為PDF文檔。
>* 為所有設定為使用PDF產生器服務的使用者，關閉安裝Adobe Acrobat和協力廠商軟體後顯示的所有對話方塊。
>* 至少啟動一次所有已安裝的軟體。 關閉所有配置為使用PDF生成器服務的用戶的所有對話框。

>



安裝Acrobat後，開啟Microsoft Word。 在&#x200B;**Acrobat**&#x200B;標籤上，按一下「建立PDF **」 ，並將電腦上可用的.doc或.docx檔案轉換為PDF檔案。**&#x200B;如果轉換成功，AEM Forms已準備好搭配PDF產生器服務使用Acrobat。

### 設定環境變數 {#setup-environment-variables}

為32位元和64位元Java開發套件、協力廠商應用程式和Adobe Acrobat設定環境變數。 環境變數應包含用於啟動相應應用程式的執行檔的絕對路徑，例如，下表列出了一些應用程式的環境變數：

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
   <td><p><strong>JDK（32位）</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Adobe Acrobat</strong></p> </td> 
   <td><p>Acrobat_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td> 
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
>* 所有環境變數和個別路徑都區分大小寫。
>* JAVA_HOME、JAVA_HOME_32和Acrobat_PATH（僅限Windows）是必要的環境變數。
>* 環境變數OpenOffice_PATH設定為安裝資料夾，而不是執行檔的路徑。
>* 請勿為Microsoft Office應用程式（如Word、PowerPoint、Excel和Project）或AutoCAD設定環境變數。 如果這些應用程式安裝在伺服器上，則生成PDF服務會自動啟動這些應用程式。
>* 在基於UNIX的平台上，將OpenOffice安裝為/root。 如果OpenOffice未作為根目錄安裝，PDF生成器服務將無法將OpenOffice文檔轉換為PDF文檔。 如果您需要以非根用戶身份安裝並運行OpenOffice，則為非根用戶提供sudo權限。
>* 如果在基於UNIX的平台上使用OpenOffice，請運行以下命令以設定路徑變數：

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### （僅適用於IBM WebSphere）配置IBM SSL套接字提供程式 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

執行以下步驟來配置IBM SSL套接字提供程式：

1. 建立java.security檔案的副本。 檔案的預設位置為`[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`。
1. 開啟複製的java.security檔案以進行編輯。
1. 更改預設的SSL套接字工廠，使用JSSE2工廠，而不是預設的IBM WebSphere工廠：

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

1. 若要啟用AEM Forms伺服器以使用更新的java.security檔案，請在啟動AEM Forms伺服器時，新增下列java引數：

   `-Djava.security.properties= [path of newly created Java.security file].`

### （僅限Windows）配置安裝油墨和手寫服務 {#configure-install-ink-and-handwriting-service}

如果運行的是Microsoft Windows Server，請配置Ink and Sharttring服務。 需要此服務才能開啟使用Microsoft Office的連結功能的Microsoft PowerPoint檔案：

1. 開啟「伺服器管理器」。 按一下「快速啟動」托盤上的&#x200B;**[!UICONTROL 「伺服器管理器」]**&#x200B;表徵圖。
1. 按一下&#x200B;**[!UICONTROL Features]**&#x200B;功能表中的&#x200B;**[!UICONTROL 新增功能]**。 選中&#x200B;**[!UICONTROL Ink and Shartting Services]**&#x200B;複選框。
1. **[!UICONTROL 選]** 擇「Features」對話框，並選 **[!UICONTROL 擇「Ink and Sharting]** Services」。按一下&#x200B;**[!UICONTROL 安裝]**&#x200B;並安裝該服務。

### （僅限Windows）配置Microsoft Office的檔案塊設定 {#configure-the-file-block-settings-for-microsoft-office}

更改Microsoft Office信任中心設定，使PDF生成器服務能夠轉換使用舊版Microsoft Office建立的檔案。

1. 開啟Microsoft Office應用程式。 例如Microsoft Word。 導覽至&#x200B;**[!UICONTROL 檔案]**> **[!UICONTROL 選項]**。 「選項」對話框隨即出現。

1. 按一下&#x200B;**[!UICONTROL 信任中心]**，然後按一下&#x200B;**[!UICONTROL 信任中心設定]**。
1. 在&#x200B;**[!UICONTROL 信任中心設定]**&#x200B;中，按一下&#x200B;**[!UICONTROL 檔案塊設定]**。
1. 在&#x200B;**[!UICONTROL File Type]**&#x200B;清單中，取消選擇&#x200B;**[!UICONTROL Open]** ，以確定PDF生成器服務應允許轉換為PDF文檔的檔案類型。

### （僅限Windows）授予「替換進程級別令牌」權限 {#grant-the-replace-a-process-level-token-privilege}

用於啟動應用程式伺服器的用戶帳戶需要&#x200B;**替換進程級令牌**&#x200B;權限。 本地系統帳戶預設具有&#x200B;**替換進程級別令牌**&#x200B;權限。 對於與本地管理員組的用戶一起運行的伺服器，必須明確授予該權限。 執行以下步驟授予權限：

1. 開啟Microsoft Windows的組策略編輯器。 要開啟組策略編輯器，請按一下「開始搜索」框中的&#x200B;**[!UICONTROL 開始]**，鍵入&#x200B;**gpedit.msc**，然後按一下&#x200B;**[!UICONTROL 組策略編輯器]**。
1. 導航到&#x200B;**[!UICONTROL 本地電腦策略]** > **[!UICONTROL 電腦配置]** > **[!UICONTROL Windows設定]** > **[!UICONTROL 安全設定]** > **[!UICONTROL 本地策略]** > **[!UICONTROL 用戶權限分配]**&#x200B;並編輯&#x200B;**[!UICONTROL 替換進程級別]**&#x200B;策略，並包括管理員。
1. 將使用者新增至取代處理層級代號項目。

### （僅限Windows）為非管理員啟用PDF產生器服務 {#enable-the-pdf-generator-service-for-non-administrators}

您可以讓非管理員使用者使用PDF產生器服務。 通常，只有具有管理權限的用戶才能使用該服務：

1. 建立環境變數PDFG_NON_ADMIN_ENABLED。
1. 將環境變數的值設為TRUE。
1. 重新啟動AEM Forms執行個體。

### （僅限Windows）禁用用戶帳戶控制(UAC) {#disable-user-account-control-uac}

1. 要訪問系統配置實用程式，請轉至&#x200B;**[!UICONTROL 開始>運行]**，然後輸入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 按一下&#x200B;**[!UICONTROL 工具]**&#x200B;頁簽，向下滾動並選擇&#x200B;**[!UICONTROL 更改UAC設定]**。 按一下&#x200B;**[!UICONTROL Launch]**&#x200B;在新窗口中運行命令。
1. 將滑桿調整到「永不通知」級別。 完成後，關閉命令窗口並關閉「系統配置」窗口。
1. 驗證UAC的註冊表設定是否設定為0（零）。 執行下列步驟以驗證：

   1. Microsoft建議您先備份註冊表，然後再修改它。 有關詳細步驟，請參閱[如何備份和還原Windows](https://support.microsoft.com/en-us/help/322756)中的註冊表。
   1. 開啟Microsoft Windows Registry編輯器。 要開啟註冊表編輯器，請轉至「開始」>「運行」，鍵入regedit，然後按一下「確定」。
   1. 導航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. 確保將EnableLUA的值設定為0（零）。
   1. 確保將&#x200B;**EnableLUA**&#x200B;的值設定為0（零）。 如果值不是0，請將值變更為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

### （僅限Windows）禁用錯誤報告服務 {#disable-error-reporting-service}

在Windows Server上使用PDF生成器服務將文檔轉換為PDF時，Windows Server偶爾會報告執行檔遇到問題，需要關閉。 不過，它不會影響PDF轉換，因為它會在背景繼續進行。

為避免收到錯誤，您可以停用Windows錯誤報告。 有關禁用錯誤報告的詳細資訊，請參閱[https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx)。

### （僅限Windows）配置HTML到PDF的轉換 {#configure-html-to-pdf-conversion}

PDF產生器服務提供WebKit、WebCapture和PhantomJS路由或方法，將HTML檔案轉換為PDF檔案。 在Windows上，要啟用WebKit和Acrobat WebCapture路由的轉換，請將Unicode字型複製到%windir%\fonts目錄。

>[!NOTE]
>
>每當您將新字型安裝至字型資料夾時，請重新啟動AEM Forms執行個體。

### （僅限UNIX平台）將HTML轉換為PDF時需額外設定  {#extra-configurations-for-html-to-pdf-conversion}

在UNIX平台上，PDF產生器服務支援WebKit和PhantomJS路由，將HTML檔案轉換為PDF檔案。 若要啟用HTML轉換為PDF，請執行下列組態，適用於您偏好的轉換路徑：

### （僅基於UNIX的平台）啟用對Unicode字型的支援（僅WebKit） {#enable-support-for-unicode-fonts-webkit-only}

根據您的系統，將Unicode字型複製到以下任何目錄：

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType(Solaris)

>[!NOTE]
>
>* 在RedHat Enterprise Linux 6.x和更新版本上，Courier字型不可用。 要安裝Courier字型，請下載font-ibm-type1-1.0.3.zip存檔。 在/usr/share/fonts解壓存檔。 建立從/usr/share/X11/fonts到/usr/share/fonts的符號連結。
>* 從Html2PdfSvc/bin和/usr/share/fonts目錄中刪除所有.lst字型快取檔案。
>* 確保目錄/usr/lib/X11/fonts和/usr/share/fonts存在。 如果目錄不存在，則使用ln命令建立從/usr/share/X11/fonts到/usr/lib/X11/fonts的符號連結，以及從/usr/share/fonts到/usr/share/X11/fonts的另一個符號連結。 另外，請確保在/usr/lib/X11/fonts上可用Courier字型。
>* 確保/usr/share/fonts或/usr/share/X11/fonts目錄中提供所有字型（Unicode和非Unicode）。
>* 以非根用戶身份運行PDF生成器服務時，請提供對所有字型目錄的非根用戶讀寫權限。
>* 每當您將新字型安裝至字型資料夾時，請重新啟動AEM Forms執行個體。

>



## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms檔案服務和其他AEM Forms功能。 執行下列步驟以安裝套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取套件的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

   您也可以透過[AEM Forms發行](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中列出的直接連結下載套件。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即停止伺服器。** 停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNEGRESTED消息停止顯示在.log檔 `[AEM-Installation-Directory]/crx-quickstart/logs/error`案中，並且日誌穩定。

## 安裝後配置 {#post-installation-configurations}

### 為RSA/BuncyCastle庫配置引導委派  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. 停止AEM例項。 導覽至[AEM安裝目錄]\crx-quickstart\conf\ folder 。 開啟sling.properties檔案以進行編輯。

   如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`啟動AEM例項，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. （僅限AIX）將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 儲存並關閉檔案。

### 配置字型管理器服務  {#configuring-the-font-manager-service}

1. 以管理員身分登入[AEM Configuration Manager](http://localhost:4502/system/console/configMgr)。
1. 找到並開啟&#x200B;**[!UICONTROL CQ-DAM-Handler-Gibson字型管理器]**&#x200B;服務。 指定「系統字型」、「Adobe伺服器字型」和「客戶字型」目錄的路徑。 按一下「**[!UICONTROL 儲存]**」。

   >[!NOTE]
   >
   >非Adobe方提供的字型的使用權受此類方向您提供的這些字型的許可協定管轄，而使用Adobe軟體的許可不涵蓋這些字型。 Adobe建議您在將非Adobe字型與Adobe軟體搭配使用之前，尤其是在伺服器環境中使用字型時，先檢閱並確保符合所有適用的非Adobe授權合約。
   > 在字型資料夾中安裝新字型時，請重新啟動AEM Forms執行個體。

### 設定本機使用者帳戶以執行PDF產生器服務  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

執行PDF產生器服務需要本機使用者帳戶。 有關建立本地用戶的步驟，請參閱在Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account)中建立用戶帳戶或在基於UNIX的平台](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html)中建立用戶帳戶。[[

1. 開啟「[AEM Forms PDF生成器配置](http://localhost:4502/libs/fd/pdfg/config/ui.html)」頁。

1. 在&#x200B;**[!UICONTROL 用戶帳戶]**&#x200B;頁簽中，提供本地用戶帳戶的憑據，然後按一下&#x200B;**[!UICONTROL 提交]**。 如果Microsoft Windows提示，請允許訪問該用戶。 成功新增後，已設定的使用者會顯示在&#x200B;**[!UICONTROL 使用者帳戶]**&#x200B;標籤的&#x200B;**[!UICONTROL 您的使用者帳戶]**&#x200B;區段下。

### 配置超時設定 {#configure-the-time-out-settings}

1. 在[AEM Configuration Manager](http://localhost:4502/system/console/configMgr)中，找到並開啟&#x200B;**[!UICONTROL Jacorb ORB Provider]**&#x200B;服務。

   將以下內容添加到&#x200B;**[!UICONTROL Custom Properties.name]**&#x200B;欄位中，然後按一下&#x200B;**[!UICONTROL Save]**。 它將掛起的答復超時（也稱為CORBA客戶端超時）設定為600秒。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. 登入AEM製作例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 設定PDF產生器]**。 預設URL為http://localhost:4502/libs/fd/pdfg/config/ui.html。

   開啟&#x200B;**[!UICONTROL 一般配置]**&#x200B;頁簽，並修改以下欄位的值以用於您的環境：

<table> 
 <tbody> 
  <tr> 
   <td>欄位</td> 
   <td>說明</td> 
   <td>預設值</td> 
  </tr> 
  <tr> 
   <td>伺服器轉換逾時</td> 
   <td>PDFG轉換在伺服器轉換逾時中定義的秒數內保持作用中</td> 
   <td>270秒<br /> </td> 
  </tr> 
  <tr> 
   <td>PDFG 清理掃描秒數</td> 
   <td>執行轉換後操作所需的秒數。<br /> </td> 
   <td>3600秒</td> 
  </tr> 
  <tr> 
   <td>工作逾期秒數</td> 
   <td>允許PDF產生器服務執行轉換的持續時間。 確保「作業過期秒數」的值大於「PDFG清理掃描秒數」值。</td> 
   <td>7200秒</td> 
  </tr> 
 </tbody> 
</table>

### （僅限Windows）為PDF產生器服務設定Acrobat {#configure-acrobat-for-the-pdf-generator-service}

在Microsoft Windows上，PDF產生器服務使用Adobe Acrobat將支援的檔案格式轉換為PDF檔案。 執行下列步驟來為PDF產生器服務設定Adobe Acrobat:

1. 開啟Acrobat並選取&#x200B;**[!UICONTROL Edit]**> **[!UICONTROL Preferences]**> **[!UICONTROL Updater]**。 在檢查更新中，取消選擇&#x200B;**[!UICONTROL 自動安裝更新]**，然後按一下&#x200B;**[!UICONTROL 確定]**。 關閉Acrobat。
1. 按兩下系統上的PDF文檔。 Acrobat首次啟動時，登入、歡迎畫面和EULA的對話方塊會隨即顯示。 為所有設定為使用PDF產生器的使用者關閉這些對話方塊。
1. 執行PDF產生器公用程式批次檔案，為PDF產生器服務設定Acrobat:

   1. 開啟[AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp)，然後從套件管理器下載`adobe-aemfd-pdfg-common-pkg-[version].zip`檔案。
   1. 將下載的.zip檔案解壓縮。 以管理權限開啟命令提示符。
   1. 導覽至`[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts`目錄。 運行以下批處理檔案：

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat已設定為透過PDF產生器服務執行。

1. 執行系統整備工具(SRT)以驗證Acrobat安裝。 此工具會檢查電腦是否已正確設定以執行PDF產生器轉換，並在指定路徑產生報表：

   1. 開啟命令提示符。 導覽至`[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt`資料夾。 從命令提示符運行以下命令：

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >如果「系統就緒工具」報告acrobat插件資料夾中沒有pdfgen.api檔案，則將pdfgen.api檔案從`[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32`目錄複製到`[Acrobat_root]\Acrobat\plug_ins`目錄。

   1. 導航到 `[Path_of_reports_folder]`. 開啟SystemReadinessTool.html檔案。 驗證報表並修正上述問題。

### （僅限Windows）配置將HTML轉換為PDF的主要路由 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF產生器服務提供多個路由，可將HTML檔案轉換為PDF檔案：Webkit、Acrobat WebCapture（僅限Windows）和PhantomJS。 Adobe建議使用PhantomJS路由，因為它具有處理動態內容的功能，並且對32位庫、32位JDK沒有依賴性，或者不需要額外的字型。 此外，PhantomJS路由不需要sudo或根存取權即可執行轉換。

HTML轉換為PDF的預設主要路由為Webkit。 要更改轉換路線，請執行以下操作：

1. 在AEM製作例項上，導覽至&#x200B;**[!UICONTROL 工具]**> **[!UICONTROL Forms]**> **[!UICONTROL 設定PDF產生器]**。

1. 在&#x200B;**[!UICONTROL 一般配置]**&#x200B;頁簽中，從&#x200B;**[!UICONTROL HTML轉換為PDF的主要路由下拉式清單中選擇首選的轉換路由]**。

### 初始化全局信任儲存 {#intialize-global-trust-store}

使用「信任儲存管理」，您可以導入、編輯和刪除您在伺服器上信任的證書，以驗證數字簽名和證書驗證。 您可以匯入和匯出任何數量的憑證。 匯入憑證後，您可以編輯信任設定和信任存放區類型。 執行以下步驟來初始化信任儲存：

1. 以管理員身分登入AEM Forms執行個體。
1. 前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 信任儲存]**。
1. 按一下&#x200B;**[!UICONTROL 建立TrustStore]**。 設定密碼，然後點選&#x200B;**[!UICONTROL Save]**。

### 為Reader擴展和加密服務設定證書 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance服務可將使用權應用於PDF文檔。 若要對PDF檔案套用使用權限，請設定憑證。

設定憑證之前，請確定您有：

* 證書檔案(.pfx)。

* 憑證隨附的私密金鑰密碼。

* 私人金鑰別名. 您可以執行Java keytool命令來查看私鑰別名：
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 密鑰庫檔案密碼。 如果您使用的是Adobe的Reader擴充功能憑證，金鑰存放區檔案密碼一律與私密金鑰密碼相同。

執行下列步驟來設定憑證：

1. 以管理員身分登入AEM Author例項。 前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。
1. 按一下使用者帳戶的&#x200B;**[!UICONTROL name]**&#x200B;欄位。 將開啟「**[!UICONTROL 編輯用戶設定]**」頁。 在AEM製作例項上，憑證位於KeyStore中。 如果您之前尚未建立KeyStore，請按一下&#x200B;**[!UICONTROL 建立KeyStore]**&#x200B;並為KeyStore設定新密碼。 如果伺服器已包含KeyStore，請跳過此步驟。  如果您使用的是Adobe的Reader擴充功能憑證，金鑰存放區檔案密碼一律與私密金鑰密碼相同。
1. 在&#x200B;**[!UICONTROL 編輯用戶設定]**&#x200B;頁面上，選擇&#x200B;**[!UICONTROL KeyStore]**&#x200B;頁簽。 展開&#x200B;**[!UICONTROL 從密鑰儲存檔案]**&#x200B;添加私鑰選項並提供別名。 別名用於執行Reader擴展操作。
1. 要上載證書檔案，請按一下&#x200B;**[!UICONTROL 選擇密鑰儲存檔案]**&#x200B;並上載&lt;filename>.pfx檔案。

   將與證書關聯的&#x200B;**[!UICONTROL 密鑰儲存密碼]**、**[!UICONTROL 私鑰密碼]**&#x200B;和&#x200B;**[!UICONTROL 私鑰別名]**&#x200B;添加到相應欄位。 按一下&#x200B;**[!UICONTROL Submit]**。

   >[!NOTE]
   >
   >在生產環境中，將評估憑證取代為生產憑證。 在更新過期或評估憑據之前，請確保刪除舊的Reader擴展憑據。

1. 按一下&#x200B;**[!UICONTROL 編輯用戶設定]**&#x200B;頁面上的&#x200B;**[!UICONTROL 保存並關閉]**。

### 啟用AES-256 {#enable-aes}

若要對PDF檔案使用AES 256加密，請取得並安裝Java加密擴充功能(JCE)無限強度管轄權原則檔案。 替換jre/lib/security資料夾中的local_policy.jar和US_export_policy.jar檔案。 例如，如果您使用Sun JDK，請將下載的檔案複製到`[JAVA_HOME]/jre/lib/security`資料夾。

組合器服務依賴於Reader擴展服務、簽名服務、Forms服務和輸出服務。 執行下列步驟以驗證所需的服務是否已啟動並正在運行：

1. 以管理員身分登入URL `https://'[server]:[port]'/system/console/bundles`。
1. 搜索以下服務，並確保服務已啟動並運行：

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
   <td>表單服務</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td> 
  </tr> 
  <tr> 
   <td>輸出服務</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td> 
  </tr> 
 </tbody> 
</table>

## 已知問題和疑難排解 {#known-issues-and-troubleshooting}

* 如果壓縮的輸入檔案包含檔案名稱中包含雙位元組字元的HTML檔案，則HTML轉換為PDF會失敗。 為避免此問題，在命名HTML檔案時，請勿使用雙位元組字元。

* 在基於UNIX的作業系統上，執行以下操作以查找任何缺少的庫：

1. 導航到 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 執行下列命令，列出PhantomJS轉換HTML至PDF所需的所有程式庫。

   `ldd phantomjs`

   運行以下命令以列出缺少的庫。

   `ldd phantomjs | grep not`

1. 手動安裝遺失的程式庫。

## 後續步驟 {#next-steps}

您有正常運作的AEM Forms檔案服務環境。 您可以通過以下方式使用文檔服務：

* [OSGi上以表單為中心的工作流程](/help/forms/using/aem-forms-workflow.md)
* [Watched 資料夾](/help/forms/using/watched-folder-in-aem-forms.md)
* [檔案服務API](/help/forms/using/aem-document-services-programmatically.md)
