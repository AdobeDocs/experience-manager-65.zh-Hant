---
title: 安裝和設定檔案服務
description: 安裝AEM Forms檔案服務，以建立、彙編、散佈、封存PDF檔案、新增數位簽名以限制對檔案的存取，以及解碼條碼式Forms。
topic-tags: installing
role: Admin, Developer
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: c6d38c682dc45e3dcebef194b3b80510ab10f9e2
workflow-type: tm+mt
source-wordcount: '10086'
ht-degree: 1%

---

# 安裝和設定檔案服務 {#installing-and-configuring-document-services}

AEM Forms提供了一組OSGi服務，用於完成不同的檔案層級作業，例如，建立、彙編、散發和封存PDF檔案、新增數位簽名以限制對檔案的存取，以及解碼條碼Forms的服務。 這些服務包含在AEM Forms附加元件套件中。 這些服務統稱為檔案服務。 可用檔案服務及其主要功能的清單如下：

* **組合器服務：**&#x200B;可讓您組合、重新排列及擴充PDF和XDP檔案，並取得有關PDF檔案的資訊。 它還有助於將PDF檔案轉換和驗證為PDF/A標準，將PDF forms、XML表單和PDF forms轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。 如需詳細資訊，請參閱[組合器服務](/help/forms/using/assembler-service.md)。

* **ConvertPDF服務：**&#x200B;可讓您將PDF檔案轉換為PostScript或影像檔案(JPEG、JPEG 2000、PNG和TIFF)。 如需詳細資訊，請參閱[ConvertPDF服務](/help/forms/using/using-convertpdf-service.md)。

* **條碼式Forms服務：**&#x200B;可讓您從條碼的電子影像擷取資料。 此服務接受包含一或多個條碼作為輸入的TIFF和PDF檔案，並擷取條碼資料。 如需詳細資訊，請參閱[條碼式Forms服務](/help/forms/using/using-barcoded-forms-service.md)。

* **DocAssurance服務：**&#x200B;可讓您加密和解密檔案、透過其他使用許可權擴充Adobe Reader的功能，以及將數位簽章新增至您的檔案。 Doc Assurance服務包含三項服務：簽名、加密和讀者延伸模組。 如需詳細資訊，請參閱[DocAssurance服務](/help/forms/using/overview-aem-document-services.md)。

* **加密服務：**&#x200B;可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 授權的使用者可以解密檔案以取得其內容的存取權。 如需詳細資訊，請參閱[加密服務](/help/forms/using/overview-aem-document-services.md#encryption-service)。

* **Forms服務：**&#x200B;可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Forms Designer中建立的表單。 Forms服務會將您開發的任何表單設計轉譯為PDF檔案。 如需詳細資訊，請參閱[Forms服務](/help/forms/using/forms-service.md)。

* **輸出服務：**&#x200B;可讓您建立不同格式的檔案，包括PDF、雷射印表機格式及標籤印表機格式。 雷射印表機格式為PostScript和印表機控制語言(PCL)。 如需詳細資訊，請參閱[輸出服務](/help/forms/using/output-service.md)。

* **PDF Generator服務：** PDF Generator服務提供可將原生檔案格式轉換為PDF的API。 它也會將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。 如需詳細資訊，請參閱[PDF Generator服務](aem-document-services-programmatically.md#pdfgeneratorservice)。

* **Reader Extension Service：**&#x200B;藉由擴充具有其他使用許可權的Adobe Reader功能，讓您的組織可以輕鬆共用互動式PDF檔案。 此服務會啟動使用Adobe Reader開啟PDF檔案時無法使用的功能，例如新增註釋至檔案、填寫表單及儲存檔案。 如需詳細資訊，請參閱[Reader擴充功能服務](/help/forms/using/overview-aem-document-services.md#reader-extension-service)。

* **簽章服務：**&#x200B;可讓您在AEM伺服器上處理數位簽章和檔案。 例如，簽章服務通常用於以下情況：

   * AEM伺服器會先認證表單，再傳送給使用者使用Acrobat或Adobe Reader開啟。
   * AEM伺服器會使用Acrobat或Adobe Reader驗證已新增至表單的簽名。
   * AEM伺服器代表公證人簽署表格。

  簽章服務會存取儲存在信任存放區中的憑證和認證。 如需詳細資訊，請參閱[簽章服務](/help/forms/using/aem-document-services-programmatically.md)。

AEM Forms是功能強大的企業級平台，檔案服務只是AEM Forms的其中一項功能。 如需完整的功能清單，請參閱[AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 一般而言，您只需要一個AEM例項（製作或發佈）即可執行AEM Forms檔案服務。 建議使用下列拓撲來執行AEM Forms檔案服務。 如需拓撲的詳細資訊，請參閱[AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![AEM Forms的架構和部署拓撲](do-not-localize/document-services.png)

>[!NOTE]
>
>雖然AEM Forms可讓您從單一伺服器設定並執行所有功能，但您應執行容量規劃、負載平衡，並為生產環境中的特定功能設定專用伺服器。 例如，在使用PDF Generator服務每天轉換數千頁頁面及多個調適型表單來擷取資料的環境中，請為PDF Generator服務和調適型表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並獨立擴充伺服器。

## 系統要求 {#system-requirements}

開始安裝及設定AEM Forms檔案服務前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體詳細清單，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且執行中。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM副本。 一般而言，您只需要一個AEM例項（製作或發佈）即可執行AEM Forms檔案服務：

   * **作者**：用來建立、上傳和編輯內容以及管理網站的AEM執行個體。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **發佈**：透過網際網路或內部網路，向公眾提供已發佈內容的AEM執行個體。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * Microsoft® Windows安裝專用的15 GB暫存空間。
   * UNIX安裝需要6 GB的暫存空間。

* 已安裝在Microsoft®Windows和Linux®上執行PDF產生器轉換所需的使用者端軟體：

   * **Microsoft® Windows**：安裝[Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)或[Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**：安裝[Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* 在Microsoft® Windows上，PDF Generator支援WebKit、Acrobat WebCapture和WebToPDF轉換路由，將HTML檔案轉換為PDF檔案。
>* 在UNIX作業系統上，PDF Generator支援WebKit和WebToPDF轉換路徑，可將HTML檔案轉換為PDF檔案。
>

### UNIX作業系統的額外需求 {#extrarequirements}

如果您使用UNIX作業系統，請從個別作業系統的安裝媒體安裝下列32位元套件：
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>外派人員</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>自由文字</li>
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

* **(僅限PDF Generator**)安裝32位元版本的libcurl、libcrypto和libssl程式庫，並建立下列symlink。 符號連結指向個別程式庫的最新版本：

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(僅限PDF Generator)** PDF Generator服務支援WebKit和WebToPDF路由，以便將HTML檔案轉換為PDF檔案。 若要啟用WebToPDF路由的轉換，請安裝下列的64位元程式庫。 一般而言，這些程式庫已經安裝。 如果缺少任何程式庫，請手動安裝：

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
* (僅限PDF Generator)若要在RHEL 8或RHEL 9、SLES15安裝程式上啟用WebKit路由，預設可能無法使用32位元`nspr`資料庫；如果不存在，請安裝。

* (僅限PDF Generator)如果Unix®伺服器上的WebToPDF轉換失敗，並出現下列錯誤：

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
然後設定以下環境變數並重新啟動伺服器：
  `OPENSSL_CONF=/etc/ssl`

>[!NOTE]
>
> WebToPDF也用於互動式通訊中的「圖表」功能。 因此，上述WebToPDF的所有設定步驟都適用於確保「圖表」功能正常運作。

## 安裝前設定 {#preinstallationconfigurations}

「安裝前設定」區段中列出的設定僅適用於PDF Generator服務。 如果您未設定PDF Generator服務，可以略過安裝前設定區段。

### 安裝Adobe Acrobat和協力廠商應用程式 {#install-adobe-acrobat-and-third-party-applications}

如果您要使用PDF Generator服務將原生檔案格式(例如Microsoft®Word、Microsoft®Excel、Microsoft®PowerPoint、OpenOffice和Adobe Acrobat)轉換為PDF檔案，請確定這些應用程式已安裝在AEM Forms伺服器上。

>[!NOTE]
>
><!-- * If your AEM Forms Server is in an offline or secure environment and internet is not available to activate Adobe Acrobat, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) for instructions to activate such instances of Adobe Acrobat. -->
>* Adobe Acrobat、Microsoft®Word、Excel和Powerpoint僅適用於Microsoft®Windows。 如果您使用UNIX作業系統，請安裝OpenOffice，將RTF文字檔和支援的Microsoft® Office檔案轉換成PDF檔案。
>* 關閉在安裝Adobe Acrobat和協力廠商軟體後，針對所有設定為使用PDF Generator服務的使用者顯示的所有對話方塊。
>* 至少啟動一次所有已安裝的軟體。 關閉所有設定要使用PDF Generator服務之使用者的所有對話方塊。
>* [檢查Adobe Acrobat序號的到期日](https://helpx.adobe.com/tw/enterprise/kb/volume-license-expiration-check.html)並設定更新授權的日期，或[根據到期日](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number)移轉您的序號。

### 安裝Adobe Acrobat Pro DC

#### 先決條件

安裝Acrobat之前，請先檢閱這些基本需求。 您應該有：

* 熟悉[Adobe Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html)
* 瞭解您的[AEM Forms部署架構](/help/forms/using/aem-forms-architecture-deployment.md)
* Adobe Admin Console和執行AEM Forms之伺服器的管理許可權。
* 具有Adobe [Admin Console](https://helpx.adobe.com/in/enterprise/using/admin-roles.html)之[管理員存取權](https://adminconsole.adobe.com)的使用者。 一般而言，您組織的管理員已經有具有管理員存取權的使用者。 您可以觀看此[教學影片](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s)，瞭解新增管理員的步驟。
* 在Adobe Admin Console中具有[部署管理員](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html)角色的使用者帳戶。 相同的[教學影片](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s)示範如何新增部署管理員。
* 執行AEM Forms的電腦上的本機系統管理員許可權
* Windows 64位元作業系統
* 穩定的網際網路連線以進行授權啟用
<!-- Backup solution for existing Acrobat settings
 Supported version of Adobe Acrobat (see [Adobe documentation](https://helpx.adobe.com/acrobat/kb/acrobat-dc-compatibility-with-windows-macos.html) for details) -->


#### 實作工作流程和時間表

視您的環境而定，完成程式通常需要1-2小時：

| 步驟 | 估計時間 | 先決條件 |
|------|----------------|---------------|
| 1.在Admin Console中建立FRL套件) | 15-20 分鐘 | [Admin Console存取權](https://helpx.adobe.com/in/enterprise/admin-guide.html) |
| 2.授予下載許可權 | 5-10 分鐘 | [Admin Console存取權](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) |
| 3.解除安裝先前的Acrobat | 10-15 分鐘 | 伺服器管理員存取權 |
| 4.下載並安裝Adobe Acrobat Pro | 10-15 分鐘 | 伺服器管理員存取權 |
| 5.下載及部署FRL套件 | 20-30 分鐘 | 伺服器管理員存取權 |
| 6.確認安裝 | 5-10 分鐘 | 伺服器存取 |

<!-- ![Workflow diagram showing the FRL implementation process](/help/forms/using/assets/frl.svg) -->

**選擇您的安裝路徑**

適用於Microsoft Office安裝的Adobe Acrobat Pro DC安裝程式，會因您的授權型別和部署情況而略有不同。 為確保您遵循特定環境的正確步驟，請選取符合您設定的標籤：

* **授權型別**：零售或大量授權
* **部署型別**：單一使用者或多個使用者

每個標籤都包含針對您的特定設定而最佳化的專屬指示，協助您避免設定問題並確保適當的授權合規性。

>[!VIDEO](https://video.tv.adobe.com/v/3469669)

>[!NOTE]
>
>影片示範「零售業授權 — 單一使用者」設定的安裝程式。 若為其他部署案例（零售 — 多位使用者、大量授權 — 單一使用者或大量授權 — 多位使用者），請參閱以下對應標籤中的特定步驟9指示，以確保針對您的部署型別正確啟動伺服器和啟用授權。

>[!BEGINTABS]

>[!TAB 零售授權 — 單一使用者]

#### 在您的AEM Forms伺服器上為Adobe Acrobat設定功能限制授權(FRL)

這些步驟假設您同時在Adobe Admin Console和執行AEM Forms的伺服器上擁有必要的管理許可權。

##### 準備FRL套件(Adobe Admin Console)

若要執行這些步驟，必須有&#x200B;*系統管理員*&#x200B;的Adobe Admin Console存取權。

###### 步驟1：登入Adobe Admin Console

1. 開啟網頁瀏覽器，並導覽至[Adobe Admin Console](https://adminconsole.adobe.com/)
1. 使用具有&#x200B;*系統管理員*&#x200B;許可權的帳戶登入。
1. （選用）如果您的組織可存取多個IMS組織，請使用Admin Console右上角的組織選擇選項來選擇正確的組織。 在大多數客戶案例中，這已設定為您組織的預設值，因為使用者通常只能存取自己的組織。

###### 步驟2：建立FRL套件

1. 在Admin Console中，導覽至「套件」索引標籤。 這是Adobe Admin Console套件，而非AEM套件。
1. 選取&#x200B;**功能限制授權**&#x200B;卡片，然後按一下&#x200B;**開始使用**&#x200B;按鈕。 請確定您選取正確的授權型別。
1. 在&#x200B;**建立封裝**&#x200B;畫面上，設定封裝設定：

   | 設定 | 建議值 | 備註 |
   |---------|-------------------|-------|
   | 啟用方法 | 離線 | 建議的選項 |
   | 權利 | PDF Generation (PDFG) | AEM Forms PDF Generator功能所需 |
   | 設定平台 | Windows 64位元 | 目前不支援Apple macOS |
   | 啟用本機 | 使用作業系統語言 | 預設設定 |
   | 語言 | 您的偏好語言 | 適用於Acrobat介面 |
   | 選擇應用程式 — 可用的應用程式 | 將Adobe Acrobat保留在可用的應用程式中。 不要移至選取的應用程式 | 您會在步驟6中從Adobe Experience League頁面[下載Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro)。 |
   | 選擇應用程式 — 選取的應用程式 | 僅保留選定應用程式中的授權檔案 | FRL部署的預設設定 |
   | 外掛程式 | 不要在此畫面上進行任何變更 | |
   | 選項 | 不要在此畫面上進行任何變更 | |
   | 完成 | 套件名稱： 「Acrobat FRL AEM Forms」 | 使用描述性名稱 |

1. 按一下&#x200B;**建立**&#x200B;以建立封裝。

###### 步驟3：提供下載許可權給使用者

建議您建立專用服務帳戶來管理FRL套件。 如果您還沒有專用帳戶，可以觀看[此教學影片](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s)以瞭解如何新增使用者至您的Adobe組織。

取得適當的帳戶後，請依照下列步驟授與下載許可權：

1. 在Admin Console中，導覽至&#x200B;**使用者**&#x200B;索引標籤。
2. 尋找或建立使用者帳戶以授予下載許可權。
3. 按一下使用者的名稱以開啟其設定檔。
4. 按一下使用者&#x200B;**編輯管理許可權**&#x200B;旁的圖示。
5. 將&#x200B;**部署管理員**&#x200B;角色指派給使用者。 其他管理員角色也可以運作，但部署管理員是建議的角色。 按一下&#x200B;**儲存**。


##### 部署FRL套件(AEM Forms伺服器)

下列步驟會在AEM Forms伺服器上執行，並擁有該電腦的&#x200B;*本機系統管理員*&#x200B;許可權。

###### 步驟4：以管理員身分登入執行AEM Forms的伺服器

使用適當的方法存取執行AEM Forms的伺服器。 請確定您使用具有本機系統管理員許可權的帳戶來存取伺服器。

###### 步驟5：解除安裝舊版Acrobat （如有）

**重要：**&#x200B;在解除安裝之前，請備份任何自訂Acrobat設定、設定檔或設定。

1. 開啟Windows控制檯。
2. 瀏覽至&#x200B;**設定**&#x200B;並開啟&#x200B;**應用程式**。
3. 在已安裝程式清單中找到&#x200B;**Adobe Acrobat**
4. 選取&#x200B;**解除安裝**，然後依照提示移除應用程式。 如果出現提示，請重新啟動伺服器
5. 請確定已解除安裝程式的所有Classic版本。 如需完全移除，請使用[Adobe Acrobat清潔工具](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html)。

###### 步驟6：下載並安裝Adobe Acrobat Pro

解除安裝先前版本後，您需要下載並安裝相容的Adobe Acrobat Pro版本：

1. 移至[Adobe Acrobat DC下載頁面](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html)。
2. 瀏覽至&#x200B;**Acrobat Pro安裝程式**&#x200B;區段。
3. 若要搭配AEM Forms PDF Generator使用，請下載「適用於Windows （32位元）」安裝程式，因為這是AEM Forms PDF Generator支援的版本。
4. 請依照頁面上的安裝指示操作：
   * 將下載的zip檔案解壓縮至您電腦上的資料夾
   * 瀏覽至Setup.exe檔案（請勿從zip檔案內執行Setup.exe檔案）
   * 連按兩下Setup.exe以開始安裝
   * 請依照熒幕上的指示完成安裝
5. 安裝後，請開啟Adobe Acrobat Pro並關閉任何歡迎對話方塊，以完成初始設定。
6. 建立簡單的PDF以驗證安裝。

###### 步驟7：下載FRL套件

1. 使用您在步驟3中提供的[使用者帳戶](https://adminconsole.adobe.com/)登入&#x200B;*Adobe Admin Console*。
1. 瀏覽至&#x200B;**封裝**&#x200B;標籤。
1. 找到您在步驟2建立的FRL套件(命名為「Acrobat FRL AEM Forms」或您的自訂套件名稱)。
1. 按一下&#x200B;**下載**&#x200B;將封裝下載至伺服器。

###### 步驟8：部署套件

1. **解壓縮封裝：**&#x200B;將下載的ZIP檔案內容解壓縮至伺服器上的目錄（例如`C:\AcrobatFRL`）。 確定可輕鬆存取擷取目錄。

2. **以系統管理員身分開啟命令提示字元(Windows)：**&#x200B;在[開始]按鈕上按一下滑鼠右鍵，然後選取[命令提示字元(Admin)]或[Windows PowerShell (Admin)]

3. **瀏覽至擷取目錄：**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **執行啟動命令：**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **重要：**
   > * 將`<JSON_FILE_NAME>.json`取代為擷取之封裝中JSON檔案的&#x200B;*確切*&#x200B;檔案名稱。
   > * JSON檔案名稱區分大小寫。
   > * 仔細檢查錯字的檔案名稱。

   **預期輸出：**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **注意：**&#x200B;啟動程式可能需要約30秒。

5. **瞭解命令引數：**

   | 參數 | 說明 |
   |-----------|-------------|
   | `-p` | 指定平台（自動偵測作業系統） |
   | `-i` | 指示工具安裝及啟動授權 |
   | `-f` | 指定JSON授權檔案的路徑 |

###### 步驟9：測試PDF Generator服務

完成所有程式後，請執行快速動作測試以確認安裝有效：

1. 開啟AEM Forms管理介面
2. 導覽至PDF Generator服務
3. 嘗試將簡單的Microsoft Office檔案轉換為PDF
4. 驗證轉換是否成功完成

#### 在FRL啟用後驗證Acrobat版本

1. 在伺服器上開啟Adobe Acrobat Pro DC
2. 請前往→關於Adobe Acrobat Pro DC的說明」
3. 驗證版本編號是否符合預期的版本
4. 確認授權狀態顯示為「已啟用」

>[!TAB 零售授權 — 多位使用者]

#### 在您的AEM Forms伺服器上為Adobe Acrobat設定功能限制授權(FRL)

這些步驟假設您同時在Adobe Admin Console和執行AEM Forms的伺服器上擁有必要的管理許可權。

##### 準備FRL套件(Adobe Admin Console)

若要執行這些步驟，必須有&#x200B;*系統管理員*&#x200B;的Adobe Admin Console存取權。

###### 步驟1：登入Adobe Admin Console

1. 開啟網頁瀏覽器，並導覽至[Adobe Admin Console](https://adminconsole.adobe.com/)
1. 使用具有&#x200B;*系統管理員*&#x200B;許可權的帳戶登入。
1. （選用）如果您的組織可存取多個IMS組織，請使用Admin Console右上角的組織選擇選項來選擇正確的組織。 在大多數客戶案例中，這已設定為您組織的預設值，因為使用者通常只能存取自己的組織。

###### 步驟2：建立FRL套件

1. 在Admin Console中，導覽至「套件」索引標籤。 這是Adobe Admin Console套件，而非AEM套件。
1. 選取&#x200B;**功能限制授權**&#x200B;卡片，然後按一下&#x200B;**開始使用**&#x200B;按鈕。 請確定您選取正確的授權型別。
1. 在&#x200B;**建立封裝**&#x200B;畫面上，設定封裝設定：

   | 設定 | 建議值 | 備註 |
   |---------|-------------------|-------|
   | 啟用方法 | 離線 | 建議的選項 |
   | 權利 | PDF Generation (PDFG) | AEM Forms PDF Generator功能所需 |
   | 設定平台 | Windows 64位元 | 目前不支援Apple macOS |
   | 啟用本機 | 使用作業系統語言 | 預設設定 |
   | 語言 | 您的偏好語言 | 適用於Acrobat介面 |
   | 選擇應用程式 — 可用的應用程式 | 將Adobe Acrobat保留在可用的應用程式中。 不要移至選取的應用程式 | 您會在步驟6中從Adobe Experience League頁面[下載Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro)。 |
   | 選擇應用程式 — 選取的應用程式 | 僅保留選定應用程式中的授權檔案 | FRL部署的預設設定 |
   | 外掛程式 | 不要在此畫面上進行任何變更 | |
   | 選項 | 不要在此畫面上進行任何變更 | |
   | 完成 | 套件名稱： 「Acrobat FRL AEM Forms」 | 使用描述性名稱 |

1. 按一下&#x200B;**建立**&#x200B;以建立封裝。

###### 步驟3：提供下載許可權給使用者

建議您建立專用服務帳戶來管理FRL套件。 如果您還沒有專用帳戶，可以觀看[此教學影片](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s)以瞭解如何新增使用者至您的Adobe組織。

取得適當的帳戶後，請依照下列步驟授與下載許可權：

1. 在Admin Console中，導覽至&#x200B;**使用者**&#x200B;索引標籤。
2. 尋找或建立使用者帳戶以授予下載許可權。
3. 按一下使用者的名稱以開啟其設定檔。
4. 按一下使用者&#x200B;**編輯管理許可權**&#x200B;旁的圖示。
5. 將&#x200B;**部署管理員**&#x200B;角色指派給使用者。 其他管理員角色也可以運作，但部署管理員是建議的角色。 按一下&#x200B;**儲存**。


##### 部署FRL套件(AEM Forms伺服器)

下列步驟會在AEM Forms伺服器上執行，並擁有該電腦的&#x200B;*本機系統管理員*&#x200B;許可權。

###### 步驟4：以管理員身分登入執行AEM Forms的伺服器

使用適當的方法存取執行AEM Forms的伺服器。 請確定您使用具有本機系統管理員許可權的帳戶來存取伺服器。

###### 步驟5：解除安裝舊版Acrobat （如有）

**重要：**&#x200B;在解除安裝之前，請備份任何自訂Acrobat設定、設定檔或設定。

1. 開啟Windows控制檯。
2. 瀏覽至&#x200B;**設定**&#x200B;並開啟&#x200B;**應用程式**。
3. 在已安裝程式清單中找到&#x200B;**Adobe Acrobat**
4. 選取&#x200B;**解除安裝**，然後依照提示移除應用程式。 如果出現提示，請重新啟動伺服器
5. 請確定已解除安裝程式的所有Classic版本。 如需完全移除，請使用[Adobe Acrobat清潔工具](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html)。

###### 步驟6：下載並安裝Adobe Acrobat Pro

解除安裝先前版本後，您需要下載並安裝相容的Adobe Acrobat Pro版本：

1. 移至[Adobe Acrobat DC下載頁面](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html)。
2. 瀏覽至&#x200B;**Acrobat Pro安裝程式**&#x200B;區段。
3. 若要搭配AEM Forms PDF Generator使用，請下載「適用於Windows （32位元）」安裝程式，因為這是AEM Forms PDF Generator支援的版本。
4. 請依照頁面上的安裝指示操作：
   * 將下載的zip檔案解壓縮至您電腦上的資料夾
   * 瀏覽至Setup.exe檔案（請勿從zip檔案內執行Setup.exe檔案）
   * 連按兩下Setup.exe以開始安裝
   * 請依照熒幕上的指示完成安裝
5. 安裝後，請開啟Adobe Acrobat Pro並關閉任何歡迎對話方塊，以完成初始設定。
6. 建立簡單的PDF以驗證安裝。

###### 步驟7：下載FRL套件

1. 使用您在步驟3中提供的[使用者帳戶](https://adminconsole.adobe.com/)登入&#x200B;*Adobe Admin Console*。
1. 瀏覽至&#x200B;**封裝**&#x200B;標籤。
1. 找到您在步驟2建立的FRL套件(命名為「Acrobat FRL AEM Forms」或您的自訂套件名稱)。
1. 按一下&#x200B;**下載**&#x200B;將封裝下載至伺服器。

###### 步驟8：部署套件

1. **解壓縮封裝：**&#x200B;將下載的ZIP檔案內容解壓縮至伺服器上的目錄（例如`C:\AcrobatFRL`）。 確定可輕鬆存取擷取目錄。

2. **以系統管理員身分開啟命令提示字元(Windows)：**&#x200B;在[開始]按鈕上按一下滑鼠右鍵，然後選取[命令提示字元(Admin)]或[Windows PowerShell (Admin)]

3. **瀏覽至擷取目錄：**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **執行啟動命令：**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **重要：**
   > * 將`<JSON_FILE_NAME>.json`取代為擷取之封裝中JSON檔案的&#x200B;*確切*&#x200B;檔案名稱。
   > * JSON檔案名稱區分大小寫。
   > * 仔細檢查錯字的檔案名稱。

   **預期輸出：**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **注意：**&#x200B;啟動程式可能需要約30秒。

5. **瞭解命令引數：**

   | 參數 | 說明 |
   |-----------|-------------|
   | `-p` | 指定平台（自動偵測作業系統） |
   | `-i` | 指示工具安裝及啟動授權 |
   | `-f` | 指定JSON授權檔案的路徑 |

###### 步驟9：啟動AEM Forms伺服器

完成所有程式後，請執行快速動作測試以確認安裝有效：

1. 從互動式使用者工作階段中的命令列主控台啟動AEM Forms伺服器。 (登入伺服器並從命令列手動啟動AEM Forms。)
2. 啟動伺服器後，讓使用者工作階段保持作用中。 請勿登出電腦，因為這會終止伺服器程式。 您可以安全地關閉遠端案頭(RDP)視窗而不登出；只要工作階段保持作用中狀態，伺服器就會繼續執行。
3. 為了提高可靠性，請設定啟動工作或排程工作，以在使用者登入時自動啟動AEM Forms伺服器。

###### 步驟10測試PDF Generator服務

1. 開啟AEM Forms管理介面
2. 導覽至PDF Generator服務
3. 嘗試將簡單的Microsoft Office檔案轉換為PDF
4. 驗證轉換是否成功完成

#### 在FRL啟用後驗證Acrobat版本

1. 在伺服器上開啟Adobe Acrobat Pro DC
2. 請前往→關於Adobe Acrobat Pro DC的說明」
3. 驗證版本編號是否符合預期的版本
4. 確認授權狀態顯示為「已啟用」

>[!TAB 大量授權 — 單一使用者]

#### 在您的AEM Forms伺服器上為Adobe Acrobat設定功能限制授權(FRL)

這些步驟假設您同時在Adobe Admin Console和執行AEM Forms的伺服器上擁有必要的管理許可權。

##### 準備FRL套件(Adobe Admin Console)

若要執行這些步驟，必須有&#x200B;*系統管理員*&#x200B;的Adobe Admin Console存取權。

###### 步驟1：登入Adobe Admin Console

1. 開啟網頁瀏覽器，並導覽至[Adobe Admin Console](https://adminconsole.adobe.com/)
1. 使用具有&#x200B;*系統管理員*&#x200B;許可權的帳戶登入。
1. （選用）如果您的組織可存取多個IMS組織，請使用Admin Console右上角的組織選擇選項來選擇正確的組織。 在大多數客戶案例中，這已設定為您組織的預設值，因為使用者通常只能存取自己的組織。

###### 步驟2：建立FRL套件

1. 在Admin Console中，導覽至「套件」索引標籤。 這是Adobe Admin Console套件，而非AEM套件。
1. 選取&#x200B;**功能限制授權**&#x200B;卡片，然後按一下&#x200B;**開始使用**&#x200B;按鈕。 請確定您選取正確的授權型別。
1. 在&#x200B;**建立封裝**&#x200B;畫面上，設定封裝設定：

   | 設定 | 建議值 | 備註 |
   |---------|-------------------|-------|
   | 啟用方法 | 離線 | 建議的選項 |
   | 權利 | PDF Generation (PDFG) | AEM Forms PDF Generator功能所需 |
   | 設定平台 | Windows 64位元 | 目前不支援Apple macOS |
   | 啟用本機 | 使用作業系統語言 | 預設設定 |
   | 語言 | 您的偏好語言 | 適用於Acrobat介面 |
   | 選擇應用程式 — 可用的應用程式 | 將Adobe Acrobat保留在可用的應用程式中。 不要移至選取的應用程式 | 您會在步驟6中從Adobe Experience League頁面[下載Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro)。 |
   | 選擇應用程式 — 選取的應用程式 | 僅保留選定應用程式中的授權檔案 | FRL部署的預設設定 |
   | 外掛程式 | 不要在此畫面上進行任何變更 | |
   | 選項 | 不要在此畫面上進行任何變更 | |
   | 完成 | 套件名稱： 「Acrobat FRL AEM Forms」 | 使用描述性名稱 |

1. 按一下&#x200B;**建立**&#x200B;以建立封裝。

###### 步驟3：提供下載許可權給使用者

建議您建立專用服務帳戶來管理FRL套件。 如果您還沒有專用帳戶，可以觀看[此教學影片](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s)以瞭解如何新增使用者至您的Adobe組織。

取得適當的帳戶後，請依照下列步驟授與下載許可權：

1. 在Admin Console中，導覽至&#x200B;**使用者**&#x200B;索引標籤。
2. 尋找或建立使用者帳戶以授予下載許可權。
3. 按一下使用者的名稱以開啟其設定檔。
4. 按一下使用者&#x200B;**編輯管理許可權**&#x200B;旁的圖示。
5. 將&#x200B;**部署管理員**&#x200B;角色指派給使用者。 其他管理員角色也可以運作，但部署管理員是建議的角色。 按一下&#x200B;**儲存**。


##### 部署FRL套件(AEM Forms伺服器)

下列步驟會在AEM Forms伺服器上執行，並擁有該電腦的&#x200B;*本機系統管理員*&#x200B;許可權。

###### 步驟4：以管理員身分登入執行AEM Forms的伺服器

使用適當的方法存取執行AEM Forms的伺服器。 請確定您使用具有本機系統管理員許可權的帳戶來存取伺服器。

###### 步驟5：解除安裝舊版Acrobat （如有）

**重要：**&#x200B;在解除安裝之前，請備份任何自訂Acrobat設定、設定檔或設定。

1. 開啟Windows控制檯。
2. 瀏覽至&#x200B;**設定**&#x200B;並開啟&#x200B;**應用程式**。
3. 在已安裝程式清單中找到&#x200B;**Adobe Acrobat**
4. 選取&#x200B;**解除安裝**，然後依照提示移除應用程式。 如果出現提示，請重新啟動伺服器
5. 請確定已解除安裝程式的所有Classic版本。 如需完全移除，請使用[Adobe Acrobat清潔工具](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html)。

###### 步驟6：下載並安裝Adobe Acrobat Pro

解除安裝先前版本後，您需要下載並安裝相容的Adobe Acrobat Pro版本：

1. 移至[Adobe Acrobat DC下載頁面](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html)。
2. 瀏覽至&#x200B;**Acrobat Pro安裝程式**&#x200B;區段。
3. 若要搭配AEM Forms PDF Generator使用，請下載「適用於Windows （32位元）」安裝程式，因為這是AEM Forms PDF Generator支援的版本。
4. 請依照頁面上的安裝指示操作：
   * 將下載的zip檔案解壓縮至您電腦上的資料夾
   * 瀏覽至Setup.exe檔案（請勿從zip檔案內執行Setup.exe檔案）
   * 連按兩下Setup.exe以開始安裝
   * 請依照熒幕上的指示完成安裝
5. 安裝後，請開啟Adobe Acrobat Pro並關閉任何歡迎對話方塊，以完成初始設定。
6. 建立簡單的PDF以驗證安裝。

###### 步驟7：下載FRL套件

1. 使用您在步驟3中提供的[使用者帳戶](https://adminconsole.adobe.com/)登入&#x200B;*Adobe Admin Console*。
1. 瀏覽至&#x200B;**封裝**&#x200B;標籤。
1. 找到您在步驟2建立的FRL套件(命名為「Acrobat FRL AEM Forms」或您的自訂套件名稱)。
1. 按一下&#x200B;**下載**&#x200B;將封裝下載至伺服器。

###### 步驟8：部署套件

1. **解壓縮封裝：**&#x200B;將下載的ZIP檔案內容解壓縮至伺服器上的目錄（例如`C:\AcrobatFRL`）。 確定可輕鬆存取擷取目錄。

2. **以系統管理員身分開啟命令提示字元(Windows)：**&#x200B;在[開始]按鈕上按一下滑鼠右鍵，然後選取[命令提示字元(Admin)]或[Windows PowerShell (Admin)]

3. **瀏覽至擷取目錄：**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **執行啟動命令：**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **重要：**
   > * 將`<JSON_FILE_NAME>.json`取代為擷取之封裝中JSON檔案的&#x200B;*確切*&#x200B;檔案名稱。
   > * JSON檔案名稱區分大小寫。
   > * 仔細檢查錯字的檔案名稱。

   **預期輸出：**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **注意：**&#x200B;啟動程式可能需要約30秒。

5. **瞭解命令引數：**

   | 參數 | 說明 |
   |-----------|-------------|
   | `-p` | 指定平台（自動偵測作業系統） |
   | `-i` | 指示工具安裝及啟動授權 |
   | `-f` | 指定JSON授權檔案的路徑 |

###### 步驟9：啟動AEM Forms伺服器

完成所有程式後，請執行快速動作測試以確認安裝有效：

1. 使用遠端案頭(RDP)登入伺服器，並使用服務啟動AEM Forms伺服器。
2. 伺服器執行後，不要簡單地關閉RDP視窗。 相反地，登出使用者即可順利登出 — 這可確保工作階段順利結束，而服務會繼續於背景執行。

###### 步驟10：測試PDF Generator服務

完成所有程式後，請執行快速動作測試以確認安裝有效：

1. 開啟AEM Forms管理介面
2. 導覽至PDF Generator服務
3. 嘗試將簡單的Microsoft Office檔案轉換為PDF
4. 驗證轉換是否成功完成

###### 步驟11：在FRL啟用後驗證Acrobat版本

1. 在伺服器上開啟Adobe Acrobat Pro DC
2. 請前往→關於Adobe Acrobat Pro DC的說明」
3. 驗證版本編號是否符合預期的版本
4. 確認授權狀態顯示為「已啟用」

>[!TAB 大量授權 — 多位使用者]

#### 在您的AEM Forms伺服器上為Adobe Acrobat設定功能限制授權(FRL)

這些步驟假設您同時在Adobe Admin Console和執行AEM Forms的伺服器上擁有必要的管理許可權。

##### 準備FRL套件(Adobe Admin Console)

若要執行這些步驟，必須有&#x200B;*系統管理員*&#x200B;的Adobe Admin Console存取權。

###### 步驟1：登入Adobe Admin Console

1. 開啟網頁瀏覽器，並導覽至[Adobe Admin Console](https://adminconsole.adobe.com/)
1. 使用具有&#x200B;*系統管理員*&#x200B;許可權的帳戶登入。
1. （選用）如果您的組織可存取多個IMS組織，請使用Admin Console右上角的組織選擇選項來選擇正確的組織。 在大多數客戶案例中，這已設定為您組織的預設值，因為使用者通常只能存取自己的組織。

###### 步驟2：建立FRL套件

1. 在Admin Console中，導覽至「套件」索引標籤。 這是Adobe Admin Console套件，而非AEM套件。
1. 選取&#x200B;**功能限制授權**&#x200B;卡片，然後按一下&#x200B;**開始使用**&#x200B;按鈕。 請確定您選取正確的授權型別。
1. 在&#x200B;**建立封裝**&#x200B;畫面上，設定封裝設定：

   | 設定 | 建議值 | 備註 |
   |---------|-------------------|-------|
   | 啟用方法 | 離線 | 建議的選項 |
   | 權利 | PDF Generation (PDFG) | AEM Forms PDF Generator功能所需 |
   | 設定平台 | Windows 64位元 | 目前不支援Apple macOS |
   | 啟用本機 | 使用作業系統語言 | 預設設定 |
   | 語言 | 您的偏好語言 | 適用於Acrobat介面 |
   | 選擇應用程式 — 可用的應用程式 | 將Adobe Acrobat保留在可用的應用程式中。 不要移至選取的應用程式 | 您會在步驟6中從Adobe Experience League頁面[下載Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro)。 |
   | 選擇應用程式 — 選取的應用程式 | 僅保留選定應用程式中的授權檔案 | FRL部署的預設設定 |
   | 外掛程式 | 不要在此畫面上進行任何變更 | |
   | 選項 | 不要在此畫面上進行任何變更 | |
   | 完成 | 套件名稱： 「Acrobat FRL AEM Forms」 | 使用描述性名稱 |

1. 按一下&#x200B;**建立**&#x200B;以建立封裝。

###### 步驟3：提供下載許可權給使用者

建議您建立專用服務帳戶來管理FRL套件。 如果您還沒有專用帳戶，可以觀看[此教學影片](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s)以瞭解如何新增使用者至您的Adobe組織。

取得適當的帳戶後，請依照下列步驟授與下載許可權：

1. 在Admin Console中，導覽至&#x200B;**使用者**&#x200B;索引標籤。
2. 尋找或建立使用者帳戶以授予下載許可權。
3. 按一下使用者的名稱以開啟其設定檔。
4. 按一下使用者&#x200B;**編輯管理許可權**&#x200B;旁的圖示。
5. 將&#x200B;**部署管理員**&#x200B;角色指派給使用者。 其他管理員角色也可以運作，但部署管理員是建議的角色。 按一下&#x200B;**儲存**。


##### 部署FRL套件(AEM Forms伺服器)

下列步驟會在AEM Forms伺服器上執行，並擁有該電腦的&#x200B;*本機系統管理員*&#x200B;許可權。

###### 步驟4：以管理員身分登入執行AEM Forms的伺服器

使用適當的方法存取執行AEM Forms的伺服器。 請確定您使用具有本機系統管理員許可權的帳戶來存取伺服器。

###### 步驟5：解除安裝舊版Acrobat （如有）

**重要：**&#x200B;在解除安裝之前，請備份任何自訂Acrobat設定、設定檔或設定。

1. 開啟Windows控制檯。
2. 瀏覽至&#x200B;**設定**&#x200B;並開啟&#x200B;**應用程式**。
3. 在已安裝程式清單中找到&#x200B;**Adobe Acrobat**
4. 選取&#x200B;**解除安裝**，然後依照提示移除應用程式。 如果出現提示，請重新啟動伺服器
5. 請確定已解除安裝程式的所有Classic版本。 如需完全移除，請使用[Adobe Acrobat清潔工具](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html)。

###### 步驟6：下載並安裝Adobe Acrobat Pro

解除安裝先前版本後，您需要下載並安裝相容的Adobe Acrobat Pro版本：

1. 移至[Adobe Acrobat DC下載頁面](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html)。
2. 瀏覽至&#x200B;**Acrobat Pro安裝程式**&#x200B;區段。
3. 若要搭配AEM Forms PDF Generator使用，請下載「適用於Windows （32位元）」安裝程式，因為這是AEM Forms PDF Generator支援的版本。
4. 請依照頁面上的安裝指示操作：
   * 將下載的zip檔案解壓縮至您電腦上的資料夾
   * 瀏覽至Setup.exe檔案（請勿從zip檔案內執行Setup.exe檔案）
   * 連按兩下Setup.exe以開始安裝
   * 請依照熒幕上的指示完成安裝
5. 安裝後，請開啟Adobe Acrobat Pro並關閉任何歡迎對話方塊，以完成初始設定。
6. 建立簡單的PDF以驗證安裝。

###### 步驟7：下載FRL套件

1. 使用您在步驟3中提供的[使用者帳戶](https://adminconsole.adobe.com/)登入&#x200B;*Adobe Admin Console*。
1. 瀏覽至&#x200B;**封裝**&#x200B;標籤。
1. 找到您在步驟2建立的FRL套件(命名為「Acrobat FRL AEM Forms」或您的自訂套件名稱)。
1. 按一下&#x200B;**下載**&#x200B;將封裝下載至伺服器。

###### 步驟8：部署套件

1. **解壓縮封裝：**&#x200B;將下載的ZIP檔案內容解壓縮至伺服器上的目錄（例如`C:\AcrobatFRL`）。 確定可輕鬆存取擷取目錄。

2. **以系統管理員身分開啟命令提示字元(Windows)：**&#x200B;在[開始]按鈕上按一下滑鼠右鍵，然後選取[命令提示字元(Admin)]或[Windows PowerShell (Admin)]

3. **瀏覽至擷取目錄：**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **執行啟動命令：**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **重要：**
   > * 將`<JSON_FILE_NAME>.json`取代為擷取之封裝中JSON檔案的&#x200B;*確切*&#x200B;檔案名稱。
   > * JSON檔案名稱區分大小寫。
   > * 仔細檢查錯字的檔案名稱。

   **預期輸出：**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **注意：**&#x200B;啟動程式可能需要約30秒。

5. **瞭解命令引數：**

   | 參數 | 說明 |
   |-----------|-------------|
   | `-p` | 指定平台（自動偵測作業系統） |
   | `-i` | 指示工具安裝及啟動授權 |
   | `-f` | 指定JSON授權檔案的路徑 |

###### 步驟9：啟動AEM Forms伺服器

完成所有程式後，請執行快速動作測試以確認安裝有效：

1. 從互動式使用者工作階段中的命令列主控台啟動AEM Forms伺服器。 (登入伺服器並從命令列手動啟動AEM Forms。)
2. 啟動伺服器後，讓使用者工作階段保持作用中。 請勿登出電腦，因為這會終止伺服器程式。 您可以安全地關閉遠端案頭(RDP)視窗而不登出；只要工作階段保持作用中狀態，伺服器就會繼續執行。
3. 為了提高可靠性，請設定啟動工作或排程工作，以在使用者登入時自動啟動AEM Forms伺服器。

###### 步驟10：測試PDF Generator服務

完成所有程式後，請執行快速動作測試以確認安裝有效：

1. 開啟AEM Forms管理介面
2. 導覽至PDF Generator服務
3. 嘗試將簡單的Microsoft Office檔案轉換為PDF
4. 驗證轉換是否成功完成

#### 在FRL啟用後驗證Acrobat版本

1. 在伺服器上開啟Adobe Acrobat Pro DC
2. 請前往→關於Adobe Acrobat Pro DC的說明」
3. 驗證版本編號是否符合預期的版本
4. 確認授權狀態顯示為「已啟用」

>[!ENDTABS]



### 在Acrobat中啟動時停用保護模式

在啟用功能限制授權(FRL)並驗證Acrobat啟用後，建議您在Adobe Acrobat中停用「啟動時保護模式」，以確保與AEM Forms PDF Generator相容。

請依照下列步驟操作：

1. 在伺服器上開啟&#x200B;**Adobe Acrobat Pro DC**。
2. 移至&#x200B;**功能表** > **偏好設定**。
3. 在「偏好設定」視窗中，從左窗格選取&#x200B;**安全性（增強功能）**。
4. 在&#x200B;**沙箱保護**&#x200B;區段下，**取消勾選**&#x200B;選項&#x200B;**「啟動時啟用保護模式」**。
5. 如果提示確認，請按一下&#x200B;**是**。
6. 按一下&#x200B;**確定**&#x200B;儲存變更並關閉[偏好設定]視窗。
7. 重新啟動Adobe Acrobat Pro DC，變更才會生效。

>[!NOTE]
>
>伺服器端自動化情況(例如AEM Forms PDF Generator)需要停用保護模式。 此設定只能在專用伺服器環境中變更，不能在使用者案頭上變更。

如需詳細資訊，請參閱受保護模式上的[Adobe檔案](https://helpx.adobe.com/tw/acrobat/kb/protected-mode-troubleshooting-reader.html)。



### 設定環境變數 {#setup-environment-variables}

為64位元Java Development Kit、協力廠商應用程式和Adobe Acrobat設定環境變數。 環境變數應包含用來啟動對應應用程式之執行檔的絕對路徑，例如，下表列出一些應用程式的環境變數：

<table>
 <tbody>
  <tr>
   <td><p><strong>應用程式</strong></p> </td>
   <td><p><strong>環境變數</strong></p> </td>
   <td><p><strong>範例</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK （64位元）</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk11</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat路徑</p> </td>
   <td><p>C:\Program檔案(x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>記事本</strong></p> </td>
   <td><p>記事本_路徑</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program檔案(x86)\OpenOffice 4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 所有環境變數和各自的路徑都區分大小寫。
>* JAVA_HOME和Acrobat_PATH （僅限Windows）是強制的環境變數。
>* 環境變數OpenOffice_PATH設定為安裝資料夾，而非可執行檔的路徑。
>* 請勿為Microsoft® Office應用程式（例如Word、PowerPoint、Excel和Project）或AutoCAD設定環境變數。 如果這些應用程式已安裝在伺服器上，則產生PDF服務會自動啟動這些應用程式。
>* 在UNIX平台上，以/root格式安裝OpenOffice。 如果OpenOffice未安裝為root，則PDF Generator服務無法將OpenOffice檔案轉換為PDF檔案。 如果您需要以非根使用者身分安裝及執行OpenOffice，請向非根使用者提供sudo許可權。
>* 如果您在UNIX平台使用OpenOffice，請執行以下命令來設定路徑變數：\
> `export OpenOffice_PATH=/opt/openoffice.org4`
>* 在SUSE® Linux® （SLES 15 SP6或更新版本）平台上，請遵循下列步驟設定OpenOffice：
>     * 將最新可用的32位元變體`OpenOffice 4.1.x`安裝至目錄，例如`/opt/openoffice4`。
>     * 將`OpenOffice_PATH`環境變數設定為指向此位置。 例如：`OpenOffice_PATH=/opt/openoffice4`。
>     * 請確定已將`OpenOffice_PATH`變數設定為全域（例如，使用`/etc/profile`或系統專屬的對等變數），以便在登入時可供所有使用者使用。

### (僅適用於IBM® WebSphere®)設定IBM® SSL通訊端提供者 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

執行以下步驟來設定IBM® SSL通訊端提供者：

1. 建立java.security檔案的復本。 檔案的預設位置為`[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`。
1. 開啟複製的java.security檔案進行編輯。
1. 變更預設的SSL通訊端工廠以使用JSSE2工廠，而非預設的IBM® WebSphere®工廠：

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

1. 若要讓AEM Forms伺服器使用更新的java.security檔案，請在啟動AEM Forms伺服器時新增下列java引數：

   `-Djava.security.properties= [path of newly created Java.security file].`

### （僅限Windows）設定Microsoft® Office的檔案封鎖設定 {#configure-the-file-block-settings-for-microsoft-office}

變更Microsoft® Office信任中心設定，讓PDF Generator服務能夠轉換使用舊版Microsoft® Office建立的檔案。

1. 開啟Microsoft® Office應用程式。 例如，Microsoft® Word。 瀏覽至&#x200B;**[!UICONTROL 檔案]**> **[!UICONTROL 選項]**。 「選項」對話方塊隨即顯示。

1. 按一下[信任中心]&#x200B;**&#x200B;**，然後按一下[信任中心設定]&#x200B;**&#x200B;**。
1. 在&#x200B;**[!UICONTROL 信任中心設定]**&#x200B;中，按一下&#x200B;**[!UICONTROL 檔案封鎖設定]**。
1. 在&#x200B;**[!UICONTROL 檔案型別]**&#x200B;清單中，取消選取&#x200B;**[!UICONTROL 開啟]**，該檔案型別應該允許PDF Generator服務轉換成PDF檔案。

### （僅限Windows）授予Replace a process level token許可權 {#grant-the-replace-a-process-level-token-privilege}

用來啟動應用程式伺服器的使用者帳戶需要&#x200B;**取代處理序層級權杖**&#x200B;許可權。 本機系統帳戶預設具有&#x200B;**取代處理序層級權杖**&#x200B;許可權。 對於以Local Administrators群組的使用者執行的伺服器，必須明確授與許可權。 執行以下步驟來授與許可權：

1. 開啟Microsoft® Windows的群組原則編輯器。 若要開啟群組原則編輯器，請按一下[開始] **&#x200B;**，在[開始搜尋]方塊中輸入&#x200B;**gpedit.msc**，然後按一下[群組原則編輯器] **[!UICONTROL 。]**
1. 瀏覽至&#x200B;**[!UICONTROL 本機電腦原則]** > **[!UICONTROL 電腦組態]** > **[!UICONTROL Windows設定]** > **[!UICONTROL 安全性設定]** > **[!UICONTROL 本機原則]** > **[!UICONTROL 使用者許可權指派]**，並編輯&#x200B;**[!UICONTROL 取代處理序層級權杖]**&#x200B;原則並包含Administrators群組。
1. 將使用者新增至「取代程式層級權杖」專案。

>[!NOTE]
>
> 如上所示，如果AEM伺服器是以LocalSystem帳戶(LSA)下的服務方式執行，則不需要明確指派此許可權給使用者。

### （僅限Windows）為非管理員啟用PDF Generator服務 {#enable-the-pdf-generator-service-for-non-administrators}

您可以讓非管理員使用者使用PDF Generator服務。 通常只有具有管理許可權的使用者才能使用服務：

1. 建立環境變數PDFG_NON_ADMIN_ENABLED。
1. 將環境變數的值設定為TRUE。
1. 重新啟動AEM Forms執行個體。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

### （僅限Windows）停用使用者帳戶控制(UAC) {#disable-user-account-control-uac}

1. 若要存取系統組態公用程式，請移至&#x200B;**[!UICONTROL 開始>執行]**，然後輸入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 按一下&#x200B;**[!UICONTROL 工具]**&#x200B;標籤，然後向下捲動並選取&#x200B;**[!UICONTROL 變更UAC設定]**。 按一下&#x200B;**[!UICONTROL 啟動]**，在新視窗中執行命令。
1. 將滑桿調整為「永不通知」等級。 完成後，關閉命令視窗並關閉「系統組態」視窗。
1. 確認UAC的登入設定設為0 （零）。 執行以下步驟以進行驗證：

   1. Microsoft®建議您在修改登入之前先備份登入。 如需詳細步驟，請參閱[如何在Windows](https://support.microsoft.com/en-us/help/322756)中備份及還原登入。
   1. 開啟Microsoft® Windows登入編輯器。 若要開啟登入編輯程式，請前往[開始] > [執行]，輸入regedit，然後按一下[確定]。
   1. 瀏覽至`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。 請確定EnableLUA的值設為0 （零）。
   1. 請確定&#x200B;**EnableLUA**&#x200B;的值設為0 （零）。 如果值不是0，請將值變更為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

### （僅限Windows）停用錯誤報告服務 {#disable-error-reporting-service}

在Windows Server上使用PDF Generator服務將檔案轉換為PDF時，Windows Server偶爾會報告可執行檔發生問題，必須關閉。 但是，這不會影響PDF轉換，因為轉換會在背景中繼續。

若要避免收到錯誤，您可以停用Windows錯誤報告。 如需停用錯誤報告的詳細資訊，請參閱[https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx)。

### （僅限Windows）設定HTML至PDF的轉換 {#configure-html-to-pdf-conversion}

PDF Generator服務提供將HTML檔案轉換為PDF檔案的WebKit、WebCapture和WebToPDF路徑或方法。 在Windows上，若要啟用WebKit和Acrobat WebCapture路由的轉換，請將Unicode字型複製到%windir%\fonts目錄。

>[!NOTE]
>
>每當您將新字型安裝至字型資料夾時，請重新啟動AEM Forms例項。

### （僅限UNIX平台） HTML轉換為PDF的額外設定  {#extra-configurations-for-html-to-pdf-conversion}

在UNIX平台上，PDF Generator服務支援WebKit和WebToPDF路由，將HTML檔案轉換為PDF檔案。 若要啟用HTML到PDF的轉換，請依照您偏好的轉換路線，執行下列設定：

### （僅限UNIX平台）啟用Unicode字型支援（僅限WebKit） {#enable-support-for-unicode-fonts-webkit-only}

視您的系統需要，將Unicode字型複製到下列任何目錄：

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* 在Red Hat® Enterprise Linux® 6.x和更新版本上，Courier字型無法使用。 若要安裝Courier字型，請下載font-ibm-type1-1.0.3.zip封存。 在/usr/share/fonts解壓縮封存。 從/usr/share/X11/fonts建立符號連結至/usr/share/fonts。
>* 刪除Html2PdfSvc/bin和/usr/share/fonts目錄中的所有.lst字型快取檔案。
>* 確定目錄/usr/lib/X11/fonts和/usr/share/fonts存在。 如果目錄不存在，請使用ln指令建立從/usr/share/X11/fonts到/usr/lib/X11/fonts的符號連結，以及從/usr/share/fonts到/usr/share/X11/fonts的另一個符號連結。 同時請確定在/usr/lib/X11/fonts中可以使用快遞。
>* 請確定/usr/share/fonts或/usr/share/X11/fonts目錄中的所有字型（Unicode和非Unicode）都可用。
>* 當您以非root使用者的身分執行PDF Generator服務時，請為非root使用者提供所有字型目錄的讀寫存取權。
>* 每當您將新字型安裝至字型資料夾時，請重新啟動AEM Forms例項。
>

## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms Document Services和其他AEM Forms功能。 執行以下步驟來安裝套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

   您也可以透過[AEM Forms發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)文章中列出的直接連結來下載套件。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即停止伺服器。**&#x200B;在停止AEM Forms伺服器之前，請等候直到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在`[AEM-Installation-Directory]/crx-quickstart/logs/error`.log檔案中，而且記錄檔穩定。

## 安裝後設定 {#post-installation-configurations}

### 設定RSA/BouncyCastle程式庫的開機委派  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. 停止AEM執行個體。 導覽至[AEM安裝目錄]\crx-quickstart\conf\資料夾。 開啟sling.properties檔案進行編輯。

   如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`啟動AEM執行個體，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。

1. 將以下屬性新增到sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (僅限AIX®)將以下屬性新增到sling.properties檔案：

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 儲存並關閉檔案。

### 設定字型管理員服務  {#configuring-the-font-manager-service}

1. 以系統管理員身分登入[AEM Configuration Manager](http://localhost:4502/system/console/configMgr)。
1. 找到並開啟&#x200B;**[!UICONTROL CQ-DAM-Handler-Gibson字型管理員]**&#x200B;服務。 指定System Fonts、Adobe Server Fonts和Customer Fonts目錄的路徑。 按一下&#x200B;**[!UICONTROL 儲存]**。

   >[!NOTE]
   >
   >您使用Adobe以外各方所提供字型的權利，受這些各方所提供且具備這些字型的授權合約所規範，且不在您使用Adobe軟體的授權範圍內。 Adobe建議您在搭配Adobe軟體使用非Adobe字型之前，檢閱並確保符合所有適用的非Adobe授權合約，尤其是在伺服器環境中使用字型的相關事項。
   >將新字型安裝至字型資料夾時，請重新啟動AEM Forms例項。
   >

### 設定本機使用者帳戶以執行PDF Generator服務  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

執行PDF Generator服務需要本機使用者帳戶。 如需建立本機使用者的步驟，請參閱[在Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account)中建立使用者帳戶，或在UNIX平台中建立使用者帳戶。

1. 開啟[AEM Forms PDF Generator設定](http://localhost:4502/libs/fd/pdfg/config/ui.html)頁面。

1. 在&#x200B;**[!UICONTROL 使用者帳戶]**&#x200B;索引標籤中，提供本機使用者帳戶的認證，然後按一下&#x200B;**[!UICONTROL 提交]**。 如果Microsoft®Windows提示，請允許使用者存取。 成功新增後，設定的使用者會顯示在&#x200B;**[!UICONTROL 使用者帳戶]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 您的使用者帳戶]**&#x200B;區段下。

### 設定逾時設定 {#configure-the-time-out-settings}

1. 在[AEM組態管理員](http://localhost:4502/system/console/configMgr)中，找到並開啟&#x200B;**[!UICONTROL Jacorb ORB提供者]**&#x200B;服務。

   將下列專案新增至&#x200B;**[!UICONTROL 自訂屬性。名稱]**&#x200B;欄位，然後按一下&#x200B;**[!UICONTROL 儲存]**。 它會將擱置中的回覆逾時（也稱為CORBA使用者端逾時）設定為600秒。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. 登入AEM作者執行個體並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 設定PDF Generator]**。 預設URL為<http://localhost:4502/libs/fd/pdfg/config/ui.html>。

   開啟&#x200B;**[!UICONTROL 一般組態]**&#x200B;標籤，並修改您環境的下列欄位值：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
   <td>預設值</td>
  </tr>
  <tr>
   <td>伺服器轉換逾時</td>
   <td>PDFG轉換會在伺服器轉換逾時中定義的秒數內保持作用中</td>
   <td>270秒<br /> </td>
  </tr>
  <tr>
   <td>PDFG 清理掃描秒數</td>
   <td>執行轉換後作業所需的秒數。<br /> </td>
   <td>3600秒</td>
  </tr>
  <tr>
   <td>工作逾期秒數</td>
   <td>允許PDF Generator服務執行轉換的持續時間。 請確定作業過期秒數的值大於PDFG清理掃描秒數的值。</td>
   <td>7200秒</td>
  </tr>
 </tbody>
</table>

### （僅限Windows）為PDF Generator服務設定Acrobat {#configure-acrobat-for-the-pdf-generator-service}

在Microsoft® Windows上，PDF Generator服務會使用Adobe Acrobat將支援的檔案格式轉換為PDF檔案。 執行以下步驟，為PDF Generator服務設定Adobe Acrobat：

1. 開啟Acrobat並選取&#x200B;**[!UICONTROL 編輯]**> **[!UICONTROL 偏好設定]**> **[!UICONTROL 更新程式]**。 在[檢查更新]中，取消選取[自動安裝更新]&#x200B;**&#x200B;**，然後按一下[確定]&#x200B;**&#x200B;**。 關閉Acrobat。
1. 連按兩下您系統上的PDF檔案。 當Acrobat首次啟動時，會顯示登入、歡迎畫面和EULA的對話方塊。 為所有設定要使用PDF Generator的使用者關閉這些對話方塊。
1. 執行PDF Generator公用程式批次檔案，為PDF Generator服務設定Acrobat：

   1. 開啟[AEM封裝管理員](http://localhost:4502/crx/packmgr/index.jsp)，並從封裝管理員下載`adobe-aemfd-pdfg-common-pkg-[version].zip`檔案。
   1. 將下載的.zip檔案解壓縮。 以管理許可權開啟命令提示字元。
   1. 瀏覽至`[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. 解壓縮`adobe-aemfd-pdfg-common-pkg-[version]`。
   1. 導覽至`[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]`目錄。 執行以下批次檔案：

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat已設定為搭配PDF Generator服務執行。

1. 執行[系統整備工具(SRT)](#SRT)以驗證Acrobat安裝。


### （僅限Windows）設定HTML轉換為PDF的主要路由 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF Generator服務提供將HTML檔案轉換為PDF檔案的多種途徑：Webkit、Acrobat WebCapture （僅限Windows）和WebToPDF。 Adobe建議使用WebToPDF路由，因為它具有處理動態內容的功能，並且不依賴32位元程式庫或不需要額外字型。 此外，WebToPDF路由不需要sudo或root存取權即可執行轉換。

HTML至PDF轉換的預設主要路徑為Webkit。 若要變更轉換路線：

1. 在AEM作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]**> **[!UICONTROL Forms]**> **[!UICONTROL 設定PDF Generator]**。

1. 在&#x200B;**[!UICONTROL 一般組態]**&#x200B;標籤中，從&#x200B;**[!UICONTROL HTML到PDF轉換的主要路線]**&#x200B;下拉式清單中選取偏好的轉換路線。

### 初始化全域信任存放區 {#intialize-global-trust-store}

使用「信任存放區管理」，您可以匯入、編輯和刪除信任在伺服器上的憑證，以驗證數位簽章和憑證驗證。 您可以匯入和匯出任意數量的憑證。 匯入憑證後，您可以編輯信任設定和信任存放區型別。 執行以下步驟來初始化信任存放區：

1. 以管理員身分登入AEM Forms執行個體。
1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 信任存放區]**。
1. 按一下&#x200B;**[!UICONTROL 建立TrustStore]**。 設定密碼並選取&#x200B;**[!UICONTROL 儲存]**。

### 設定Reader擴充功能和加密服務的憑證 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance服務可套用使用許可權至PDF檔案。 若要套用使用許可權至PDF檔案，請設定憑證。

在設定憑證之前，請確定您擁有：

* 憑證檔案(.pfx)。

* 憑證提供的私密金鑰密碼。

* 私密金鑰別名。 您可以執行Java keytool指令來檢視「私密金鑰別名」：
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 金鑰庫檔案密碼。 如果您使用Adobe的Reader擴充功能憑證，Keystore檔案密碼一律與私密金鑰密碼相同。

執行以下步驟來設定憑證：

1. 以管理員身分登入AEM作者執行個體。 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。
1. 按一下使用者帳戶的&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位。 **[!UICONTROL 編輯使用者設定]**&#x200B;頁面隨即開啟。 在AEM編寫執行個體上，憑證位於KeyStore中。 如果您先前尚未建立KeyStore，請按一下[建立KeyStore] **&#x200B;**，並設定KeyStore的新密碼。 如果伺服器已包含KeyStore，請略過此步驟。  如果您使用Adobe的Reader擴充功能憑證，Keystore檔案密碼一律與私密金鑰密碼相同。
1. 在&#x200B;**[!UICONTROL 編輯使用者設定]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL KeyStore]**&#x200B;索引標籤。 展開&#x200B;**[!UICONTROL 從金鑰庫檔案新增私密金鑰]**&#x200B;選項並提供別名。 別名可用來執行Reader擴充功能作業。
1. 若要上傳憑證檔案，請按一下&#x200B;**[!UICONTROL 選取金鑰存放區檔案]**，然後上傳&lt;filename>.pfx檔案。

   將與憑證相關聯的&#x200B;**[!UICONTROL 金鑰存放區密碼]**、**[!UICONTROL 私密金鑰密碼]**&#x200B;和&#x200B;**[!UICONTROL 私密金鑰別名]**&#x200B;新增至個別欄位。 按一下「**[!UICONTROL 提交]**」。

   >[!NOTE]
   >
   >在生產環境中，將評估認證取代為生產認證。 在更新過期的認證或評估認證之前，請務必刪除舊的Reader擴充功能認證。

1. 在&#x200B;**[!UICONTROL 編輯使用者設定]**&#x200B;頁面上按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

### 啟用AES-256 {#enable-aes}

若要對PDF檔案使用AES 256加密，請取得並安裝Java Cryptography Extension (JCE) Unlimited Strength管轄原則檔案。 取代jre/lib/security資料夾中的local_policy.jar和US_export_policy.jar檔案。 例如，如果您使用Sun JDK，請將下載的檔案複製到`[JAVA_HOME]/jre/lib/security`資料夾。

組合器服務取決於Reader擴充功能服務、簽名服務、Forms服務和輸出服務。 執行以下步驟，確認必要的服務已啟動且執行中：

1. 以系統管理員身分登入URL `https://'[server]:[port]'/system/console/bundles`。
1. 搜尋下列服務，並確定服務已啟動且執行中：

<table>
 <tbody>
  <tr>
   <th>服務名稱</th>
   <th>組合包名稱</th>
  </tr>
  <tr>
   <td>簽名服務</td>
   <td>adobe-aemfd-signatures</td>
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

### （僅限Windows）設定Microsoft®專案的登入專案 {#configure-registry-entry-for-microsoft-project}

在電腦上安裝AEM Forms附加元件和Microsoft® Project後，請在64位元位置註冊Microsoft® Project的專案。 它有助於執行Project到PDFG的轉換測試。 下列是列出登入輸入程式的步驟：

1. 開啟Microsoft® Windows登入編輯器(regedit)，若要開啟登入編輯器，請前往[開始] > [執行]，輸入regedit，然後按一下[確定]。
1. 導覽至`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Adobe\Acrobat PDFMaker\<version>\Office\SupportedApp`，並建立新的&#x200B;**二進位值**&#x200B;登入並將它重新命名為&#x200B;**專案**。
1. 將已建立之二進位登入的資料值修改成01，然後按一下確定。
1. 關閉登入專案。


## 已知問題和疑難排解 {#known-issues-and-troubleshooting}

* 如果壓縮的輸入檔案包含檔案名稱中含有雙位元組字元的HTML檔案，PDFHTML轉換便會失敗。 為了避免此問題，命名HTML檔案時請勿使用雙位元組字元。

* 在基於UNIX的作業系統上，執行下列操作以尋找任何遺漏的程式庫：

1. 導覽至 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`。

1. HTML執行以下命令，列出WebToPDF轉換為PDF所需的所有程式庫。

   `ldd phantomjs`

   執行以下命令以列出遺失的程式庫。

   `ldd phantomjs | grep not`

1. 手動安裝遺失的程式庫。

## 系統整備工具(SRT) {#SRT}

[系統整備工具](#srt-configuration)會檢查電腦是否已正確設定為執行PDF Generator轉換。 工具會在指定的路徑產生報表。 若要執行工具：

1. 開啟命令提示。 導覽至 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` 檔案夾。

1. 從命令提示字元執行下列命令：

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   該指令會產生報告，也會建立srt_config.yaml檔案。 您可以使用它來設定SRT工具的選項。 可選擇性設定SRT工具的選項。

   >[!NOTE]
   >
   >* 如果系統整備工具報告pdfgen.api檔案在Acrobat外掛程式資料夾中無法使用，則將pdfgen.api檔案從`[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32`目錄複製到`[Acrobat_root]\Acrobat\plug_ins`目錄。

1. 瀏覽至`[Path_of_reports_folder]`。 開啟SystemReadinessTool.html檔案。 驗證報告並修正上述問題。

### 設定SRT工具的選項 {#srt-configuration}

您可以使用srt_config.yaml檔案來設定SRT工具的各種設定。 檔案格式為：

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
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

* **地區設定：**&#x200B;它是必要引數。 它支援英文(en)、德文(de)、法文(fr)和日文(ja)。 預設值為en。 這對OSGi上在AEM Forms上執行的PDF Generator服務沒有影響。
* **aemTempDir：**&#x200B;它是選用引數。 它會指定Adobe Experience Manager的暫存位置。
* **使用者：**&#x200B;它是選用引數。 您可以指定使用者來檢查使用者是否擁有執行PDF Generator所需的許可權和目錄的讀取/寫入存取權。 如果未指定使用者，則會略過使用者特定檢查，並在報表中顯示為失敗。
* **outputDir：**&#x200B;指定儲存SRT報告的位置。 預設位置是SRT工具的目前工作目錄。

## 疑難排解

如果在修復SRT工具所報告的所有問題後仍遇到問題，請執行以下檢查：

在執行以下檢查之前，請確定[系統整備工具](#SRT)未報告任何錯誤。

+++ Adobe Acrobat

* 確保只安裝[支援的Microsoft® Office （32位元）和Adobe Acrobat版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)，並取消開啟對話方塊。
<!-- (Acrobat 2020 only) Ensure that Adobe Acrobat Update Service is disabled. -->
* 確定[Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service)批次檔案是以管理員許可權執行。
* 確認已在PDF Generator設定UI中新增PDF使用者。
* 確定已為PDF Generator使用者新增[取代處理序層級權杖](#grant-the-replace-a-process-level-token-privilege)許可權。
* 確認已針對Microsoft Office應用程式啟用Acrobat PDFMaker Office COM增益集。

+++

+++OpenOffice

**Microsoft® Windows**

* 請確認已安裝32位元[支援的Microsoft Office版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)，並取消所有應用程式的開啟對話方塊。
* 確認已在PDF Generator設定UI中新增PDF使用者。
* 請確定PDF Generator使用者是系統管理員群組的成員，並且已為該使用者設定了[取代處理序層級權杖](#grant-the-replace-a-process-level-token-privilege)許可權。
* 請確認已在PDF Generator UI中設定使用者，並執行下列動作：
   1. 使用PDF Generator使用者登入Microsoft® Windows。
   1. 開啟Microsoft® Office或OpenOffice應用程式並取消所有對話方塊。
   1. 將AdobePDF設為預設印表機。
   1. 將Acrobat設為PDF檔案的預設程式。
   1. 在Microsoft Office應用程式中使用選項「檔案>列印和Acrobat功能區」來執行手動轉換，並取消所有對話方塊。
   1. 結束所有與轉換相關的程式，例如winword.exe、powerpoint.exe和excel.exe。
   1. 重新啟動AEM Forms伺服器。

**Linux®**

* 安裝[支援的OpenOffice版本](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)。 AEM Forms支援32位元和64位元版本。 安裝之後，請開啟所有OpenOffice應用程式、取消所有對話視窗，然後關閉應用程式。 重新開啟應用程式，並確保開啟OpenOffice應用程式時不會顯示任何對話方塊。

* 建立環境變數`OpenOffice_PATH`，並將其設定為指向設定在[主控台](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/)或dt （裝置樹狀結構）設定檔中的OpenOffice安裝。
* 如果安裝OpenOffice時發生問題，請確定OpenOffice安裝所需的[32位元程式庫](#extrarequirements)可供使用。

+++

+++HTML到PDF的轉換問題

* 確保在PDF Generator設定UI中新增字型目錄。

**Linux與Solaris （WebToPDF轉換路由）**

* 確保可用於基於Webkit的HTMLToPDF轉換的32位元資料庫(libicudata.so.42)和64位元(libicudata.so.42資料庫可用於基於WebToPDF的HTMLToPDF轉換。

* 執行以下命令以列出WebToPDF的遺失程式庫：

  ```
  ldd phantomjs | grep not
  ```

**Linux®和Solaris™ （WebKit轉換路由）**

* 確定目錄`/usr/lib/X11/fonts`和`/usr/share/fonts`存在。 如果目錄不存在，請建立從`/usr/share/X11/fonts`到`/usr/lib/X11/fonts`的符號連結，以及從`/usr/share/fonts`到`/usr/share/X11/fonts`的另一個符號連結。

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* 請確定IBM字型複製於usr/share/fonts之下。
* 確定電腦上有Ghost弱點修正Glibc。 使用您的預設封裝管理員來更新至最新版本的glibc。 其中包括Ghost弱點修正。
* 確保系統上已安裝32位元lib curl、libcrypto和libssl程式庫的最新版本。 同時建立指向個別程式庫最新版本（32位元）的符號連結`/usr/lib/libcurl.so` (或libcurl.a (AIX®))、`/usr/lib/libcrypto.so` (或libcrypto.a (AIX®)和`/usr/lib/libssl.so` (或libssl.a (AIX®))。

* 對IBM® SSL通訊端提供者執行以下步驟：
   1. 將java.security檔案從`<WAS_Installed_JAVA>\jre\lib\security`複製到AEM Forms伺服器上的任何位置。 預設位置為「預設位置」= `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`。

   1. 編輯複製位置的java.security檔案，並變更預設的SSL通訊端工廠與JSSE2工廠(使用JSSE2工廠而非WebSphere®)。

      變更下列預設JSSE通訊端處理站：

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

<!-- +++ Unable to add a PDF Generator (PDFG) user

* (Acrobat 2020 only) Ensure Microsoft&reg; Visual C++ 2012 x86 and Microsoft&reg; Visual C++ 2013 x86 (32-bit) redistributable are installed on Windows.

+++
-->
+++自動化測試失敗

* 對於Microsoft® Office和OpenOffice，請手動執行至少一個轉換（以每位使用者的身分），以確保轉換期間不會彈出任何對話方塊。 如果出現任何對話方塊，則將其關閉。 自動轉換期間不應出現這類對話方塊。

* 在OSGi環境的AEM Forms上執行自動化之前，請確定測試套件已安裝且作用中。

+++

<!-- +++ (Acrobat 2020 only) Multiple user conversion failures 

* Verify the server logs to check if the conversion is failing for a particular user.(Process Explorer can help you check running process for different users)

* Ensure that the user configured for PDF Generator has local admin rights.

* Ensure that PDF Generator user has read, write, and execute permissions on LC temp and PDFG temp users.

* For Microsoft&reg; Office and OpenOffice, perform at least one conversion manually (as each user) to ensure that no dialogue pops up during conversion. If any dialogue appears, dismissed it. No such dialogue should appear during automated conversion.

* Perform a sample conversion.

+++ -->

<!-- (Acrobat 2020 only) License of Adobe Acrobat installed on AEM Forms Server expires

* If you have an existing license of Adobe Acrobat and it has expired, [Download the latest version of Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html), and migrating your serial number. Before [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Use the following commands to generate prov.xml and reserialize the existing install using the prov.xml file instead of commands provided in [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) number article.

      ```

         adobe_prtk --tool=VolumeSerialize --generate --serial=<serialnum> [--leid=<LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=limited list of locales in xx_XX format or ALL>] [--provfile=<Absolute path to prov.xml>]

      ```

   * Volume serialize the package (Re-serialize the existing install using the prov.xml file and the new serial): Run the following command from the PRTK installation folder as an administrator to serialize and activate the deployed packages on client machines:

      ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         
      ```

* For large-scale installations, use the [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) to remove previous versions of Reader and Acrobat. Customize the installer and deploy it to all the machines of your organization.

(Acrobat 2020 only) AEM Forms Server is in an offline or secure environment and internet is not available to activate Acrobat.

* You can go online within 7 days of the first launch of your Adobe product to complete an online activation and registration or use an internet-enabled device and your product's serial number to complete this process. For detailed instructions, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++ -->

+++ 無法在Windows Server上將Word或Excel檔案轉換為PDF

當使用者嘗試在Microsoft Windows Server上將Word或Excel檔案轉換成PDF時，會發生下列錯誤：

*來自主要轉換器的錯誤訊息：
ALC-PDG-015-003 — 系統無法開啟輸入檔案。 再次提交您的檔案或連絡您的系統管理員。*

若要解決此問題，請參閱[無法在Windows Server](/help/forms/using/disable-uac-for-pdfgconfiguration.md)上將Word或Excel檔案轉換成PDF。

+++

+++ 無法在Windows Server 2019上將Excel檔案轉換為PDF

當您在Microsoft Windows Server 2019上將Microsoft Excel 2019轉換為PDF時，必須確定以下事項：

* 使用PDF Generator服務時，您的Windows電腦不應與AEM伺服器（Windows RDP工作階段）有任何作用中的遠端連線。
* 預設印表機必須設定為Adobe PDF。

  >[!NOTE]
  >* 若為Apple macOS和Ubuntu作業系統，您不需要設定上述設定。

+++

+++ 無法將XPS檔案轉換為PDF

若要解決此問題，[在Windows](https://helpx.adobe.com/in/acrobat/kb/unable-convert-xps-to-pdfs.html)上建立功能特定的登入機碼。

+++


## 後續步驟 {#next-steps}

您有一個運作中的AEM Forms檔案服務環境。 您可以透過以下方式使用檔案服務：

* [OSGi上的表單中心工作流程](/help/forms/using/aem-forms-workflow.md)
* [Watched 資料夾](/help/forms/using/watched-folder-in-aem-forms.md)
* [檔案服務API](/help/forms/using/aem-document-services-programmatically.md)
