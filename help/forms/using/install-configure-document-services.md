---
title: 安裝和設定檔案服務
seo-title: 安裝和設定檔案服務
description: 安裝AEM Forms檔案服務以建立、組合、分發、封存PDF檔案、新增數位簽章以限制檔案存取，以及解碼條形碼表單。
seo-description: 安裝AEM Forms檔案服務以建立、組合、分發、封存PDF檔案、新增數位簽章以限制檔案存取，以及解碼條形碼表單。
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 0%

---


# 安裝和配置文檔服務{#installing-and-configuring-document-services}

AEM Forms提供一組OSGi服務，以完成不同的檔案層級作業，例如建立、組合、分發和封存PDF檔案、新增數位簽章以限制檔案存取，以及解碼條形碼表單等服務。 這些服務包含在AEM Forms附加套件中。 這些服務統稱為檔案服務。 可用的檔案服務及其主要功能清單如下：

* **匯編服務：** 可讓您合併、重新排列和增強PDF和XDP檔案，並取得PDF檔案的相關資訊。此外，它還可協助將PDF檔案轉換並驗證為PDF/A標準、將PDF表格、XML表格和PDF表格轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。 有關詳細資訊，請參見[Assembler Service](/help/forms/using/assembler-service.md)。

* **ConvertPDF服務：** 可讓您將PDF檔案轉換為PostScript或影像檔案（JPEG、JPEG 2000、PNG和TIFF）。如需詳細資訊，請參閱[ConvertPDF Service](/help/forms/using/using-convertpdf-service.md)。

* **條碼表單服務：** 可讓您從條碼的電子影像擷取資料。該服務接受包含一個或多個條形碼的TIFF和PDF檔案作為輸入，並提取條形碼資料。 如需詳細資訊，請參閱[Barcoded Forms Service](/help/forms/using/using-barcoded-forms-service.md)。

* **DocAssurance服務：** 可讓您加密和解密檔案、以額外的使用權限擴充Adobe Reader的功能，以及在檔案中新增數位簽章。Doc Assurance服務包含三項服務：簽名、加密和Reader擴充功能。 有關詳細資訊，請參閱[DocAssurance Service](/help/forms/using/overview-aem-document-services.md)。

* **加密服務：** 可讓您加密和解密檔案。當文檔加密時，其內容將變得不可讀。 授權用戶可以解密文檔以獲得對其內容的訪問。 如需詳細資訊，請參閱[加密服務](/help/forms/using/overview-aem-document-services.md#encryption-service)。

* **表單服務：可** 讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳遞通常在表單設計工具中建立的表單。Forms服務會轉譯您開發為PDF檔案的任何表格設計。 如需詳細資訊，請參閱[Forms Service](/help/forms/using/forms-service.md)。

* **輸出服務：** 可讓您建立不同格式的檔案，包括PDF、雷射印表機格式和標籤印表機格式。雷射打印機格式為PostScript和打印機控制語言(PCL)。 如需詳細資訊，請參閱[輸出服務](/help/forms/using/output-service.md)。

* **PDF Generator服務：PDF** Generator服務提供API，可將原生檔案格式轉換為PDF。此外，它還可將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。 如需詳細資訊，請參閱[PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice)。

* **Reader Extension服務：讓** 貴組織透過擴充Adobe Reader的功能及額外的使用權限，輕鬆分享互動式PDF檔案。此服務會啟動在使用Adobe Reader開啟PDF檔案時無法使用的功能，例如在檔案中新增註解、填寫表單以及儲存檔案。 如需詳細資訊，請參閱[Reader Extension Service](/help/forms/using/overview-aem-document-services.md#reader-extension-service)。

* **簽名服務：** 可讓您在AEM伺服器上使用數位簽名和檔案。例如，簽名服務通常用於下列情況：

   * AEM伺服器會在將表單傳送至使用者以使用Acrobat或Adobe Reader開啟之前，先進行認證。
   * AEM伺服器會驗證已使用Acrobat或Adobe Reader新增至表單的簽名。
   * AEM伺服器代表公證員簽署表格。

   簽名服務訪問儲存在信任儲存中的證書和證書。 如需詳細資訊，請參閱[簽名服務](/help/forms/using/aem-document-services-programmatically.md)。

AEM Forms是功能強大的企業級平台，而檔案服務只是AEM Forms的功能之一。 如需完整的功能清單，請參閱[AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲{#deployment-topology}

AEM Forms附加元件套件是部署在AEM上的應用程式。 通常，您只需要一個AEM例項（作者或發佈）即可執行AEM Forms檔案服務。 建議使用下列拓撲來執行AEM Forms檔案服務。 如需拓撲的詳細資訊，請參閱[AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![AEM Forms的架構和部署拓撲](do-not-localize/document-services.png)

>[!NOTE]
>
>雖然AEM Forms可讓您從單一伺服器設定並執行所有功能，但您應進行容量規劃、負載平衡，並針對生產環境中的特定功能設定專屬伺服器。 例如，對於使用PDF Generator服務每天轉換數千頁的環境，以及擷取資料的多個調適性表單，請針對PDF Generator服務和最適化表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並可獨立擴展伺服器。

## 系統要求{#system-requirements}

開始安裝和設定AEM Forms檔案服務之前，請確定：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見[技術要求](/help/sites-deploying/technical-requirements.md)。

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在作者或發佈模式下伺服器上執行的AEM復本。 通常，您只需要一個AEM例項（作者或發佈）即可執行AEM Forms檔案服務：

   * **作者**:用於建立、上傳和編輯內容以及管理網站的AEM例項。內容一旦準備好上線，就會複製到發佈實例。
   * **發佈**:透過網際網路或內部網路為大眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的臨時空間，用於基於Microsoft Windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* PDF產生器在Microsoft Windows和Linux上執行轉換所需的用戶端軟體已安裝：

   * **Microsoft Windows**:安裝 [Microsoft ](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office或 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**:安裝 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* 在Microsoft Windows上，PDF產生器支援WebKit、Acrobat WebCapture和PhantomJS轉換路由，以將HTML檔案轉換為PDF檔案。
>* 在以UNIX為基礎的作業系統上，PDF產生器支援WebKit和PhantomJS轉換路由，以將HTML檔案轉換為PDF檔案。

>



### 基於UNIX的作業系統的額外要求{#extrarequirements}

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

* **(僅限PDF產生器**)安裝32位元版本的libcurl、libcrypto和libssl程式庫，並建立下列symlinks。symlinks指向各個庫的最新版本：

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **（僅限PDF Generator）** PDF Generator服務支援WebKit和PhantomJS路由，將HTML檔案轉換為PDF檔案。若要啟用PhantomJS路由轉換，請安裝下列64位元程式庫。 通常，這些庫已安裝。 如果缺少任何庫，請手動安裝：

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

## 預安裝配置{#preinstallationconfigurations}

安裝前設定區段中所列的設定僅適用於PDF Generator服務。 如果您未設定PDF Generator服務，則可略過安裝前設定區段。

### 安裝Adobe Acrobat和協力廠商應用程式{#install-adobe-acrobat-and-third-party-applications}

如果您要使用PDF Generator服務將Microsoft Word、Microsoft Excel、Microsoft PowerPoint、OpenOffice、WordPerfect X7和Adobe Acrobat等原生檔案格式轉換為PDF檔案，請確定這些應用程式已安裝在AEM Forms伺服器上。

>[!NOTE]
>
>* Adobe Acrobat、Microsoft Word、Excel和Powerpoint僅適用於Microsoft Windows。 如果您使用UNIX作業系統，請安裝OpenOffice，將豐富型文字檔案和支援的Microsoft Office檔案轉換為PDF檔案。
>* 為所有已設定使用PDF產生器服務的使用者，關閉安裝Adobe Acrobat和協力廠商軟體後顯示的所有對話方塊。
>* 至少啟動一次所有已安裝的軟體。 關閉所有已設定為使用PDF產生器服務之使用者的對話方塊。

>



安裝Acrobat後，開啟Microsoft Word。 在&#x200B;**Acrobat**&#x200B;標籤上，按一下「建立PDF」，並將電腦上的。doc或。docx檔案轉換為PDF檔案。 ****&#x200B;如果轉換成功，AEM Forms已準備好將Acrobat與PDF Generator服務搭配使用。

### 設定環境變數{#setup-environment-variables}

為32位元和64位元Java開發套件、協力廠商應用程式和Adobe Acrobat設定環境變數。 環境變數應包含用於啟動相應應用程式的執行檔的絕對路徑，例如，下表列出了一些應用程式的環境變數：

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>應用程式</strong></p> </td> 
   <td><p><strong>環境變數</strong></p> </td> 
   <td><p><strong>範例</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK（64位元）</strong></p> </td> 
   <td><p>JAVA_HOME</p> </td> 
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK（32位元）</strong></p> </td> 
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
>* 所有環境變數和各自的路徑均區分大小寫。
>* JAVA_HOME、JAVA_HOME_32和Acrobat_PATH（僅限Windows）是必備的環境變數。
>* 環境變數OpenOffice_PATH設定為安裝資料夾，而不是執行檔的路徑。
>* 請勿為Microsoft Office應用程式（例如Word、PowerPoint、Excel和Project）或AutoCAD設定環境變數。 如果這些應用程式已安裝在伺服器上，「產生PDF」服務會自動啟動這些應用程式。
>* 在基於UNIX的平台上，以/root身份安裝OpenOffice。 如果OpenOffice未以根目錄安裝，PDF產生器服務將無法將OpenOffice檔案轉換為PDF檔案。 如果您需要以非根用戶身份安裝並運行OpenOffice，則為非根用戶提供sudo權限。
>* 如果您在基於UNIX的平台上使用OpenOffice，請運行以下命令以設定路徑變數：

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### （僅適用於IBM WebSphere）配置IBM SSL套接字提供程式{#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

執行以下步驟以配置IBM SSL套接字提供程式：

1. 建立java.security檔案的副本。 檔案的預設位置為`[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`。
1. 開啟複製的java.security檔案以進行編輯。
1. 變更預設的SSL通訊端工廠，使用JSSE2工廠，而非預設的IBM WebSphere工廠：

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

1. 若要啟用AEM Forms伺服器以使用更新的java.security檔案，在啟動AEM Forms伺服器時，請新增下列java引數：

   `-Djava.security.properties= [path of newly created Java.security file].`

### （僅限Windows）配置安裝墨水和手寫服務{#configure-install-ink-and-handwriting-service}

如果您正在運行Microsoft Windows Server，請配置Ink and Shartting服務。 需要該服務才能開啟使用Microsoft Office的輸墨功能的Microsoft PowerPoint檔案：

1. 開啟「伺服器管理器」。 按一下「Quick Launch（快速啟動）」托盤上的「Server Manager（伺服器管理器）」**[!UICONTROL 表徵圖。]**
1. 按一下&#x200B;**[!UICONTROL 功能]**&#x200B;菜單中的&#x200B;**[!UICONTROL 添加功能]**。 選中「**[!UICONTROL 墨水和手寫服務]**」複選框。
1. **[!UICONTROL 選擇「]** 功能」對話框，並 **[!UICONTROL 選擇「油墨和筆跡]** 服務」。按一下&#x200B;**[!UICONTROL 安裝]**&#x200B;並安裝服務。

### （僅限Windows）配置Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}的檔案塊設定

變更Microsoft Office信任中心設定，讓PDF Generator服務可轉換使用舊版Microsoft Office建立的檔案。

1. 開啟Microsoft Office應用程式。 例如，Microsoft Word。 導覽至&#x200B;**[!UICONTROL File]**> **[!UICONTROL Options]**。 將出現選項對話框。

1. 按一下&#x200B;**[!UICONTROL 信任中心]** ，然後按一下&#x200B;**[!UICONTROL 信任中心設定]**。
1. 在&#x200B;**[!UICONTROL 信任中心設定]**&#x200B;中，按一下&#x200B;**[!UICONTROL 檔案塊設定]**。
1. 在&#x200B;**[!UICONTROL 檔案類型]**&#x200B;清單中，針對PDF產生器服務應允許轉換為PDF檔案的檔案類型，取消選取&#x200B;**[!UICONTROL Open]**。

### （僅限Windows）授予「取代進程級別令牌」權限{#grant-the-replace-a-process-level-token-privilege}

用於啟動應用程式伺服器的用戶帳戶要求&#x200B;**替換進程級別Token**&#x200B;權限。 本地系統帳戶預設具有&#x200B;**替換進程級別Token**&#x200B;權限。 對於與「本地管理員」組用戶一起運行的伺服器，必須明確授予該權限。 執行以下步驟授予權限：

1. 開啟Microsoft Windows的群組原則編輯器。 要開啟組策略編輯器，請按一下「開始搜索」框中的&#x200B;**[!UICONTROL 「開始」]**，鍵入&#x200B;**gpedit.msc** ，然後按一下「組策略編輯器」]**。**[!UICONTROL 
1. 導覽至「**[!UICONTROL 本機電腦政策]** > **[!UICONTROL 電腦設定]** > **[!UICONTROL Windows設定]** > **[!UICONTROL 安全設定]** > **[!UICONTROL 本機政策]** > **[!UICONTROL 使用者權限分配]**&#x200B;並編輯&#x200B;**[!UICONTROL 取代處理層級Token]**&#x200B;原則並包含「管理員」群組。
1. 將使用者新增至「取代處理層級Token」項目。

### （僅限Windows）為非管理員啟用PDF產生器服務{#enable-the-pdf-generator-service-for-non-administrators}

您可以讓非管理員使用者使用PDF產生器服務。 通常，只有具有管理權限的用戶才能使用服務：

1. 建立環境變數PDFG_NON_ADMIN_ENABLED。
1. 將環境變數的值設定為TRUE。
1. 重新啟動AEM Forms例項。

### （僅限Windows）禁用用戶帳戶控制(UAC){#disable-user-account-control-uac}

1. 要訪問系統配置實用程式，請轉至&#x200B;**[!UICONTROL 開始>運行]**，然後輸入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 按一下「**[!UICONTROL 工具]**」頁籤並向下滾動並選擇「更改UAC設定&#x200B;]**」。**[!UICONTROL &#x200B;按一下&#x200B;**[!UICONTROL Launch]**&#x200B;在新窗口中運行命令。
1. 將滑桿調整至「永不通知」層級。 完成後，關閉命令窗口並關閉「System Configuration（系統配置）」窗口。
1. 驗證UAC的註冊表設定是否設定為0（零）。 請執行下列步驟來驗證：

   1. Microsoft建議您在修改註冊表之前備份該註冊表。 有關詳細步驟，請參見[如何備份和恢復Windows](https://support.microsoft.com/en-us/help/322756)中的註冊表。
   1. 開啟Microsoft Windows註冊表編輯器。 要開啟註冊表編輯器，請轉至「開始」>「運行」，鍵入regedit，然後按一下「確定」。
   1. 導航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. 確保EnableLUA的值設定為0（零）。
   1. 確保&#x200B;**EnableLUA**&#x200B;的值設定為0（零）。 如果值不是0，請將值變更為0。 關閉註冊表編輯器。

1. 重新啟動電腦。

### （僅限Windows）禁用錯誤報告服務{#disable-error-reporting-service}

在Windows Server上使用PDF Generator服務將檔案轉換為PDF時，Windows Server偶爾會報告執行檔遇到問題，需要關閉。 但是，當PDF繼續在背景時，它不會影響其轉換。

為避免收到錯誤，您可以禁用Windows錯誤報告。 有關禁用錯誤報告的詳細資訊，請參閱[https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx)。

### （僅限Windows）設定HTML至PDF轉換{#configure-html-to-pdf-conversion}

PDF產生器服務提供WebKit、WebCapture和PhantomJS路由或方法，將HTML檔案轉換為PDF檔案。 在Windows上，若要啟用WebKit和Acrobat WebCapture路由轉換，請將Unicode字型複製至%windir%\fonts目錄。

>[!NOTE]
>
>每當您將新字型安裝至字型檔案夾時，請重新啟動AEM Forms例項。

### （僅限UNIX平台）HTML至PDF轉換的額外設定{#extra-configurations-for-html-to-pdf-conversion}

在UNIX平台上，PDF產生器服務支援WebKit和PhantomJS路由，將HTML檔案轉換為PDF檔案。 若要啟用HTML至PDF轉換，請執行下列適用於您偏好轉換路由的設定：

### （僅限UNIX平台）啟用對Unicode字型的支援（僅限WebKit）{#enable-support-for-unicode-fonts-webkit-only}

將Unicode字型複製至下列適合您系統的任何目錄：

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType(Solaris)

>[!NOTE]
>
>* 在RedHat Enterprise Linux 6.x及更新版本中，無法使用courier字型。 若要安裝Courier字型，請下載font-ibm-type1-1.0.3.zip封存。 在/usr/share/fonts擷取封存。 從/usr/share/X11/fonts建立符號連結至/usr/share/fonts。
>* 從Html2PdfSvc/bin和/usr/share/fonts目錄刪除所有。lst字型快取檔案。
>* 請確定目錄/usr/lib/X11/fonts和/usr/share/fonts存在。 如果目錄不存在，則使用ln命令建立從/usr/share/X11/fonts到/usr/lib/X11/fonts的符號連結，以及從/usr/share/fonts到/usr/share/X11/fonts的另一個符號連結。 此外，請確定courier字型可在/usr/lib/X11/fonts取得。
>* 請確定所有字型（Unicode和非Unicode）都可在/usr/share/fonts或/usr/share/X11/fonts目錄中使用。
>* 當您以非root使用者身分執行PDF Generator服務時，請提供非root使用者對所有字型目錄的讀取和寫入存取權。
>* 每當您將新字型安裝至字型檔案夾時，請重新啟動AEM Forms例項。

>



## 安裝AEM Forms附加元件套件{#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署在AEM上的應用程式。 此套件包含AEM Forms Document Services和其他AEM Forms功能。 執行以下步驟以安裝軟體包：

1. 開啟[軟體分發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
1. 點選頁首功能表中的「Adobe Experience Manager ]**」。**[!UICONTROL 
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然後按一下&#x200B;**[!UICONTROL 上載包]**&#x200B;來上載包。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

   您也可以透過[AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中所列的直接連結下載套件。

1. 安裝套件後，系統會提示您重新啟動AEM例項。 **不要立即停止伺服器。** 在停止AEM Forms伺服器之前，請等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log檔案中，且記錄檔穩定。

## 安裝後配置{#post-installation-configurations}

### 為RSA/BuncyCastle庫配置引導委派{#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. 停止AEM例項。 導覽至[AEM安裝目錄]\crx-quickstart\conf\ folder。 開啟sling.properties檔案以進行編輯。

   如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`來啟動AEM例項，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. （僅限AIX）將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 儲存並關閉檔案。

### 配置字型管理器服務{#configuring-the-font-manager-service}

1. 以管理員身分登入[AEM Configuration Manager](http://localhost:4502/system/console/configMgr)。
1. 找到並開啟&#x200B;**[!UICONTROL CQ-DAM-Handler-Gibson字型管理器]**&#x200B;服務。 指定「系統字型」、「Adobe伺服器字型」和「客戶字型」目錄的路徑。 按一下&#x200B;**[!UICONTROL 「儲存」]**。

   >[!NOTE]
   >
   >您使用非Adobe方提供之字型的權利受該等方提供予您的授權合約約束，且您使用Adobe軟體的授權不涵蓋該權利。 Adobe建議您在搭配Adobe軟體使用非Adobe字型之前，先檢閱並確保您符合所有適用的非Adobe授權合約，尤其是在伺服器環境中使用字型。
   > 當您將新字型安裝至字型檔案夾時，請重新啟動AEM Forms例項。

### 設定本機使用者帳戶以執行PDF Generator服務{#configure-a-local-user-account-to-run-the-pdf-generator-service}

執行PDF產生器服務需要本機使用者帳戶。 有關建立本地用戶的步驟，請參閱[在Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account)或[在基於UNIX的平台](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html)中建立用戶帳戶。

1. 開啟「[AEM Forms PDF Generator Configuration](http://localhost:4502/libs/fd/pdfg/config/ui.html)」頁面。

1. 在&#x200B;**[!UICONTROL User Accounts]**&#x200B;標籤中，提供本地用戶帳戶的憑據，然後按一下&#x200B;**[!UICONTROL Submit]**。 如果Microsoft Windows出現提示，請允許用戶訪問。 成功添加後，配置的用戶將顯示在&#x200B;**[!UICONTROL 「用戶帳戶」頁籤的**[!UICONTROL 「您的用戶帳戶」]**部分下。]**

### 配置超時設定{#configure-the-time-out-settings}

1. 在[AEM配置管理器](http://localhost:4502/system/console/configMgr)中，找到並開啟&#x200B;**[!UICONTROL Jacorb ORB Provider]**&#x200B;服務。

   將下列內容新增至&#x200B;**[!UICONTROL 自訂屬性名稱]**&#x200B;欄位，然後按一下「儲存&#x200B;]**」。**[!UICONTROL &#x200B;它將待處理的回復超時（也稱為CORBA客戶端超時）設定為600秒。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. 登入AEM作者例項並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL 設定PDF產生器]**。 預設URL為http://localhost:4502/libs/fd/pdfg/config/ui.html。

   開啟&#x200B;**[!UICONTROL General Configuration]**&#x200B;頁籤，並修改以下欄位的值以用於您的環境：

<table> 
 <tbody> 
  <tr> 
   <td>欄位</td> 
   <td>說明</td> 
   <td>預設值</td> 
  </tr> 
  <tr> 
   <td>伺服器轉換逾時</td> 
   <td>PDFG轉換在「伺服器轉換」逾時中定義的秒數內保持作用中</td> 
   <td>270秒<br /> </td> 
  </tr> 
  <tr> 
   <td>PDFG 清理掃描秒數</td> 
   <td>執行轉換後操作所需的秒數。<br /> </td> 
   <td>3600秒</td> 
  </tr> 
  <tr> 
   <td>工作逾期秒數</td> 
   <td>允許PDF Generator服務執行轉換的期間。 確保「作業過期秒數」的值大於「PDFG清除掃描秒數」值。</td> 
   <td>7200秒</td> 
  </tr> 
 </tbody> 
</table>

### （僅限Windows）為PDF Generator服務設定Acrobat {#configure-acrobat-for-the-pdf-generator-service}

在Microsoft Windows上，PDF Generator服務使用Adobe Acrobat將支援的檔案格式轉換為PDF檔案。 執行下列步驟，為PDF Generator服務設定Adobe Acrobat:

1. 開啟Acrobat並選取「編輯&#x200B;****>**[!UICONTROL 偏好設定]**>**[!UICONTROL 更新程式]**」。 在檢查更新中，取消選擇「自動安裝更新&#x200B;**[!UICONTROL 」，然後按一下「確定」。]******&#x200B;關閉Acrobat。
1. 連按兩下系統上的PDF檔案。 當Acrobat首次啟動時，會出現登入、歡迎畫面和EULA的對話方塊。 針對所有已設定為使用PDF產生器的使用者，關閉這些對話方塊。
1. 執行PDF Generator公用程式批次檔案，為PDF Generator服務設定Acrobat:

   1. 開啟[AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp)，並從套件管理器下載`adobe-aemfd-pdfg-common-pkg-[version].zip`檔案。
   1. 解壓縮下載的。zip檔案。 開啟具有管理權限的命令提示符。
   1. 導覽至`[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts`目錄。 運行以下批處理檔案：

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat已設定為隨PDF Generator服務一起執行。

1. 執行系統準備工具(SRT)以驗證Acrobat安裝。 此工具會檢查機器是否已正確設定為執行PDF產生器轉換，並在指定路徑產生報表：

   1. 開啟命令提示符。 導覽至`[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt`資料夾。 從命令提示符運行以下命令：

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >如果「系統準備工具」報告acrobat外掛程式檔案夾中沒有pdfgen.api檔案，請將pdfgen.api檔案從`[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32`目錄複製到`[Acrobat_root]\Acrobat\plug_ins`目錄。

   1. 導航到 `[Path_of_reports_folder]`. 開啟SystemReadinessTool.html檔案。 驗證報告並修正上述問題。

### （僅限Windows）設定HTML至PDF轉換的主要路由{#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF產生器服務提供多種路由，以將HTML檔案轉換為PDF檔案：Webkit、Acrobat WebCapture（僅限Windows）和PhantomJS。 Adobe建議使用PhantomJS路由，因為它可處理動態內容，而且不需要依賴32位元程式庫、32位元JDK，或不需要額外的字型。 此外，PhantomJS路由不需要sudo或root存取權來執行轉換。

HTML轉換至PDF的預設主要路由是Webkit。 要更改轉換路由，請執行以下操作：

1. 在AEM作者例項上，導覽至「**[!UICONTROL 工具]**>**[!UICONTROL Forms]**> **[!UICONTROL 設定PDF產生器]**」。

1. 在&#x200B;**[!UICONTROL 一般設定]**&#x200B;標籤中，從&#x200B;**[!UICONTROL HTML的主要轉換路由]**&#x200B;下拉式清單中選取偏好的轉換路由。

### 初始化全局信任儲存{#intialize-global-trust-store}

使用信任商店管理，您可以匯入、編輯和刪除您信任伺服器的憑證，以驗證數位簽章和憑證驗證。 您可以匯入和匯出任意數量的憑證。 在匯入憑證後，您可以編輯信任設定和信任商店類型。 執行以下步驟以初始化信任儲存：

1. 以管理員身分登入AEM Forms例項。
1. 前往&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**。
1. 按一下&#x200B;**[!UICONTROL 建立TrustStore]**。 設定密碼並點選&#x200B;**[!UICONTROL Save]**。

### 為Reader擴充功能和加密服務設定憑證{#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance服務可以對PDF檔案套用使用權。 若要套用PDF檔案的使用權，請設定憑證。

設定憑證之前，請確定您有：

* 憑證檔案(.pfx)。

* 憑證隨附的私密金鑰密碼。

* 私人金鑰別名. 您可以執行Java keytool命令來查看私鑰別名：
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 密鑰庫檔案密碼。 如果您使用Adobe的Reader Extensions憑證，Keystore檔案密碼一律與私密金鑰密碼相同。

請執行下列步驟來設定憑證：

1. 以管理員身分登入AEM Author例項。 前往「**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**」。
1. 按一下使用者帳戶的&#x200B;**[!UICONTROL name]**&#x200B;欄位。 將開啟&#x200B;**[!UICONTROL 編輯用戶設定]**&#x200B;頁。 在AEM Author例項中，憑證位於KeyStore中。 如果您尚未以前建立KeyStore，請按一下「建立KeyStore」]**，並為KeyStore設定新密碼。**[!UICONTROL &#x200B;如果伺服器已包含KeyStore，請略過此步驟。  如果您使用Adobe的Reader Extensions憑證，Keystore檔案密碼一律與私密金鑰密碼相同。
1. 在&#x200B;**[!UICONTROL 編輯用戶設定]**&#x200B;頁面上，選擇&#x200B;**[!UICONTROL KeyStore]**&#x200B;頁籤。 展開&#x200B;**[!UICONTROL 從密鑰儲存檔案]**&#x200B;添加私密密鑰選項並提供別名。 別名用於執行Reader Extensions操作。
1. 若要上傳憑證檔案，請按一下「選取金鑰存放區檔案&#x200B;]**」，然後上傳&lt;filename>.pfx檔案。**[!UICONTROL 

   將與證書相關聯的&#x200B;**[!UICONTROL 密鑰儲存密碼]**、**[!UICONTROL 私鑰密碼]**&#x200B;和&#x200B;**[!UICONTROL 私鑰別名]**&#x200B;添加到相應欄位。 按一下&#x200B;**[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >在生產環境中，以生產認證取代您的評估認證。 在更新過期或評估憑證之前，請確定您已刪除舊的Reader Extensions憑證。

1. 按一下&#x200B;**[!UICONTROL 編輯用戶設定]**&#x200B;頁面上的&#x200B;**[!UICONTROL 保存並關閉]**。

### 啟用AES-256 {#enable-aes}

若要針對PDF檔案使用AES 256加密，請取得並安裝Java加密擴充功能(JCE)「無限制強度管轄區」原則檔案。 在jre/lib/security資料夾中取代local_policy.jar和US_export_policy.jar檔案。 例如，如果您使用Sun JDK，請將下載的檔案複製到`[JAVA_HOME]/jre/lib/security`資料夾。

Assembler服務依賴於Reader Extensions服務、Signature服務、Forms服務和Output服務。 執行以下步驟以驗證所需的服務是否已啟動並正在運行：

1. 以管理員身分登入URL `https://'[server]:[port]'/system/console/bundles`。
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
   <td>Reader Extensions服務</td> 
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

## 已知問題和{#known-issues-and-troubleshooting}疑難排解

* 如果壓縮的輸入檔案包含檔案名稱中具有雙位元組字元的HTML檔案，則HTML轉換為PDF會失敗。 為避免此問題，命名HTML檔案時請勿使用雙位元組字元。

* 在基於UNIX的作業系統上，請執行以下操作以查找任何缺少的庫：

1. 導航到 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 執行下列命令，列出PhantomJS轉換HTML至PDF所需的所有程式庫。

   `ldd phantomjs`

   運行以下命令以列出缺少的庫。

   `ldd phantomjs | grep not`

1. 手動安裝缺少的庫。

## 後續步驟{#next-steps}

您有可運作的AEM Forms檔案服務環境。 您可透過下列方式使用檔案服務：

* [OSGi表單導向工作流程](/help/forms/using/aem-forms-workflow.md)
* [Watched 資料夾](/help/forms/using/watched-folder-in-aem-forms.md)
* [檔案服務API](/help/forms/using/aem-document-services-programmatically.md)

