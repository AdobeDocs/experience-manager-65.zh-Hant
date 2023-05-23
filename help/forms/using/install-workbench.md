---
title: 安裝工作台
seo-title: Install workbench
description: 安裝工作台。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# 安裝工作台 {#install-workbench}

本文檔提供了安裝和配置AEM FormsWorkbench的說明。 安裝程式還安裝Forms設計器。

## 誰應該閱讀此文檔？ {#who-should-read-this-doc}

本文檔適用於負責安裝、配置、管理或部署Workbench的管理員或開發人員。 此外還包括配置系統以支援升級的AEM Forms進程的資訊。 提供的資訊基於以下假設：任何閱讀本文檔的人都熟悉Microsoft® Windows®作業系統。

## 其他資訊 {#additional-information}

此表中的資源可以幫助您瞭解更多資訊並開始使用AEM Forms。
<table>
 <tbody>
  <tr>
   <td><p><strong>關於後述資訊：</strong></p> </td>
   <td><p><strong>請參閱</strong></p> </td>
  </tr>
  <tr>
   <td><p>Workbench的過程資訊</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">工作台幫助</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>有關AEM Forms及其如何與其他Adobe產品整合的一般資訊</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms概述</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>所有可供AEM Forms使用的檔案</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms文檔</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>有關此產品版本的補丁程式更新、技術說明和其他資訊</p> </td>
   <td><p>聯繫Adobe企業支援</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex工作區不建議用於AEM Forms。 它可供AEM Forms發行。

## 安裝前 {#before-you-install}

### Workbench安裝概述 {#workbench-installation-overview}

Workbench是一個整合開發環境(IDE)，開發人員和表單作者使用它來建立自動化的業務流程和表單。 它還用於管理流程和表單使用的資源和服務。

下圖描述了Workbench安裝，包括：
* 使用Workbench的流程設計
* 使用設計器進行窗體設計

>[!NOTE]
>
>AEM Forms伺服器需要單獨的安裝程式。 有關詳細資訊，請參閱AEM Forms的JEE安裝文檔。

![預設呈現形式](assets/installing-workbench.png)

## 系統先決條件 {#system-prerequisites}

本節概述硬體和軟體要求以及支援的平台。

### 最低硬體和軟體要求 {#minimum-hardware-software-requirements}

**工作台**
建議最低要求為：安裝的磁碟空間：
* 僅Workbench為680 MB。
* 在單個驅動器上安裝2.15 GB，以完全安裝Workbench、Designer和示例元件。
* 400 MB用於臨時安裝目錄 — 200 MB（用戶\temp目錄）和200 MB（Windows臨時目錄）。

>[!NOTE]
>
>如果所有這些位置都位於單個驅動器上，則安裝期間必須有1.5 GB的可用空間。 安裝完成後，將刪除複製到臨時目錄的檔案。

* 硬體要求：英特爾®奔騰® 4或AMD®等效處理器，1 GHz。
* Java™ Runtime Environment(JRE)7.0更新51或更高版本到7.0。
* 16位或更高顏色的顯示器解析度為1024 X 768像素或更高。
* 到AEM Forms伺服器的TCP/IPv4或TCP/IPv6網路連接。
* 安裝Visual C++可再發行運行時程式包2012 32位。
* 安裝Visual C++可再發行運行時程式包2013 32位。

>[!NOTE]
>
>您必須具有「管理」權限才能安裝Workbench。 如果您使用非管理員帳戶進行安裝，安裝程式會提示您輸入相應帳戶的憑據。

### 支援的平台 {#supported-platforms}

請參閱以下位置的Workbench支援平台的完整清單 [AEM Forms支援的平台](https://www.adobe.com/go/learn_aemforms_supportedplatforms_65)。

## 設計器安裝注意事項 {#designer-installation-considerations}

預設情況下，Workbench安裝包含相應的僅英文版本的Designer。 如果Workbench安裝應用程式在您的電腦上檢測到現有版本的Designer，則安裝可能會終止，您必須先刪除當前版本的Designer，然後才能繼續。
下表列出了在安裝Workbench時可能遇到的設計器安裝方案以及必須執行的任何操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>當前安裝的設計器版本</strong></p> </td>
   <td><p><strong>所需操作</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro或Acrobat Pro擴展（包括設計師）</p> </td>
   <td><p>無。<br /> 
Workbench安裝會檢測您的電腦上安裝了Acrobat Pro或Acrobat Pro擴展的設計器實例。<br />
不同版本的Designer可以共存於同一系統中，例如Workbench 6.4的Designer 6.4.x和Workbench 6.5的Designer 6.5.0.x。無需卸載隨Acrobat10 Pro或Acrobat10 Pro Extended或更高版本安裝的Designer版本。
<br /></p> </td>
  </tr>
  <tr>
   <td><p>設計器（獨立）</p> </td>
   <td><p>無。<br />Workbench附帶的Designer版本僅為英文。 <br />Workbench安裝程式不會重新安裝新版本的Designer。 將為Workbench安裝程式捆綁的更新版本打補丁。 這還允許您在Workbench中使用Designer的本地化版本。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 在Windows 10上卸載設計器（獨立） {#uninstall-designer-standalone-windows10}

1. 轉到 **控制面板>程式>程式和功能**
1. 在當前安裝的程式清單中，選擇 **Adobe設計器**。
1. 按一下 **卸載** 然後按一下 **是**。

## 安裝Workbench {#installing-workbench}

本章介紹如何安裝Workbench。

### 安裝並運行Workbench {#installing-and-running-workbench}

在安裝Workbench之前，必須確保您的環境包括運行Workbench所需的軟體和硬體(請參閱「」部分： **安裝前**)。

**要安裝和運行Workbench，請執行以下操作：**

1. 執行以下任務之一：
   * 導航到安裝介質上的\workbench目錄，然後按兩下run_windows_installer.bat檔案。
   * 將Workbench下載並解壓縮到檔案系統。 下載後，導航到\workbench目錄，然後按兩下run_windows_installer.bat檔案。

   >[!IMPORTANT]
   >
   >Workbench安裝程式僅從本地驅動器運行。 無法從遠程站點運行。

   >[!NOTE]
   >
   >如果遇到錯誤「無法建立Java™虛擬機」，則建立名為_JAVA_OPTIONS且值為 — Xmx512M的環境變數並運行安裝程式。

1. 在「簡介」螢幕上，按一下「下一步」。
1. 閱讀產品許可協定，選擇「I accept the terms of the License Agreement（我接受許可協定的條款）」 ，然後按一下「Next（下一步）」。
1. （可選）如果需要此工具來建立和修改表單，請選擇「安裝Adobe設計器」。

   >[!NOTE]
   通過取消選擇此選項，您可以繼續使用隨Acrobat10一起安裝的設計器。

1. 接受列出的預設目錄，或按一下「選擇」並導航到要安裝Workbench的目錄，然後按一下「下一步」。

   >[!NOTE]
   安裝目錄路徑不應包含#（磅）和$（美元）字元。

1. 查看預安裝摘要，然後按一下「安裝」。 安裝程式顯示安裝進度。
1. 查看安裝摘要。 選擇「啟動AEM Forms工作台」以啟動工作台，然後按一下「下一步」。
1. 查看發行說明，然後按一下「完成」。
1. 您的電腦上現在安裝了以下項目：
   * **工作台**:要從「開始」菜單運行Workbench，請選擇「所有程式」>「AEM Forms」>「工作台」(Workbench)，如果您選擇將快捷資料夾儲存在其中。 有關資訊，請參見 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">使用Workbench</a> 文檔。
   * **設計師**:您可以從Workbench內部訪問Designer。 有關資訊，請參閱中的入門主題 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">設計器幫助</a>。
   * **AEM FormsSDK**:有關使用SDK的詳細資訊，請參見 <a href="https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf">與AEM Forms</a>。

## 升級進程 {#upgrading-processes}

AEM Forms的JEE進程可以使用升級嚮導升級到AEM Forms應用程式。 有關詳細資訊，請參閱Workbench幫助中的升級舊對象文檔。

### 配置並登錄到伺服器 {#configuring-and-logging-server}

要使用Workbench，您必須運行一個AEM Forms實例，通常在單獨的電腦上。 您必須具有用戶名和密碼才能登錄到AEM Forms，以及有關伺服器位置的詳細資訊。

>[!NOTE]
如果您將AEM Forms配置為使用EMC Documentum®或IBM® FileNet儲存庫提供程式，並且要登錄到除在表單管理控制台中配置為預設值的儲存庫之外的儲存庫AEM，請將用戶名提供為username@Repository。

### 配置超時設定 {#configuring-timeout-settings}

預設情況下，Workbench在兩小時後超時，而不考慮活動或不活動。 要編輯超時設定，請參閱中的「配置用戶管理>配置高級系統屬性」 <a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">管理控制台幫助</a>。

### 配置Workbench以通過HTTPS連接 {#configuring-workbench-to-connect-over-HTTPS}

要通過HTTPS將Workbench連接到AEM Forms伺服器，必須確保頒發公鑰的證書頒發機構(CA)被Workbench認為受信任。 如果證書未被識別為來自受信任源，則必須更新 [工作台_首頁]/workbench/jre/lib/security目錄。

>[!NOTE]
[工作台_首頁] 表示Workbench的安裝目錄。 預設位置為C:\Program Files (x86)\Adobe Experience Manager表單Workbench。

確保使用證書中指定的名稱連接到HTTPS。 此名稱通常是完全限定的主機名。

**更新cacert檔案**:
1. 確保您有安全套接字層(SSL)證書的副本。 請與配置SSL伺服器的管理員聯繫，或使用Web瀏覽器導出證書。

   >[!NOTE]
   要導出證書，請開啟Web瀏覽器並登錄到管理控制台，在瀏覽器中安裝證書，然後將證書從瀏覽器導出到臨時儲存位置(或直接導出到 [工作台_首頁]/workbench/jre/lib/security目錄)。

1. 將證書複製到 [工作台_首頁]/workbench/jre/lib/security目錄。

1. 開啟命令提示符窗口，導航到 [工作台_首頁]/workbench/jre/bin，然後鍵入以下命令：
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`其中：
   * `changeit` 是cacerts密鑰庫的預設口令。
   * certname是您在步驟1中選擇的證書。
   * 示例是您為證書選擇的別名。 此值可以更改。

1. 當提示信任證書時，鍵入Yes並按Enter鍵。 keytool將繼續將cacerts檔案導入到 [工作台_首頁]/workbench/jre/lib/security目錄。

1. 關閉並重新啟動Workbench以應用更改。

### 為動態生成的模板配置快取設定 {#configuring-cache-settings-for-dynamically-generated-templates}

如果您的應用程式通過自動更新XFA內容來即時生成唯一模板，則應考慮快取操作的以下方面。 實際上，每個事務都使用一個新的唯一模板。

當表單生成器或輸出在快取中搜索或更新特定表單模板的條目時，它使用幾個鍵值來定位要訪問的特定快取條目。

* **模板檔案名**:用作快取表單的主要唯一標識符的模板的位置和檔案名。
* **時間戳**:模板檔案包含用於確定表單上次更新時間的時間戳。
* **模板UUID**:設計器在每個模板中插入表單及其版本的唯一標識符(UUID)。 每次更新表單時，都會更新嵌入的UUID。 例如，XDP模板可能顯示以下內容：

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **呈現選項**:在所呈現的表單快取中，快取內容被分別儲存用於每組唯一呈現選項。


Forms服務通過引用檔案名或儲存庫位置或作為記憶體中的XML對象的值來接收模板。
* **參考傳遞的模板**:使用內容根和表單名稱。 如果使用此方法在每個請求中傳遞具有不同檔案名的唯一模板，則磁碟快取會不斷增長，並且永遠不會重複使用。 為防止出現這種情況，應使用相同的檔案名傳遞唯一模板，以確保對所有請求更新相同的快取。
* **按值傳遞的模板**:使用theinDataDoc參數使用與資料一起傳遞的模板位元組。 如果使用此方法傳遞具有不同UUID的唯一模板，則磁碟快取將不斷增長，並且永遠不會被重用。 為防止出現此情況，應從所有模板中刪除UUID屬性，以確保未為模板建立快取。 或者，傳遞相同的非空UUID允許建立快取對象，但確保使用每個請求更新相同的快取。

要防止快取不斷增長，請考慮以下因素，以便使用新的AEM FormsAPI、正在renderHTMLForm2和renderPDFForm2來呈現動態生成的模板。

當使用新API時，模板將作為文檔對象傳遞，該文檔對象在Forms服務中根據模板是否被鈍化處理。

對於UUID和內容根作為快取鍵的被鈍化文檔，請考慮以下方面：
* 未為沒有UUID的被動式輸入模板建立快取。
* 如果傳遞了多個具有相同UUID和內容根的被鈍化的輸入模板，則會覆蓋同一快取。

對於檔案名和內容根作為快取鍵的非鈍化文檔，請考慮以下方面：
* 對於非鈍化的輸入模板，快取取決於生成文檔的內容根和檔案名。
同一快取僅用於具有相同內容根和模板檔案名的請求。
以下最佳做法確保在動態生成的模板傳遞到Forms服務時快取不會無休止地增長：
   * 刪除UUID或在所有動態生成的模板中傳遞相同的UUID。
   * 從模板位元組或磁碟上相同檔案名生成文檔。

### 正在卸載Workbench {#uninstalling-workbench}

使用「控制面板」中的「添加或刪除程式」功能啟動卸載程式。 Workbench和Designer應用程式有單獨的卸載程式。

## 配置AEM FormsXDC編輯器 {#configuring-aem-forms-xdc-editor}

使用XDC編輯器，網路打印機管理員可以建立和修改XMLForms體系結構設備配置(XDC)檔案。 XDC檔案描述打印機的功能，如打印機語言或紙張大小與托盤位置之間的關聯。

在網路打印機管理員使用XDC編輯器之前，請重新定位示例XDC檔案，並參閱使用XDC編輯器建立設備配置檔案。

**獲取示例XDC檔案**:
1. 在AEM Forms伺服器上，在 [AEM Forms根]\sdk\samples\Output\IVS。
1. 將此資料夾的內容複製到可從Workbench或Eclipse系統訪問的目錄中。

**獲取XDC編輯器幫助**:
1. 轉到AEM Forms文檔網站。
1. 按一下 **開發** 頁籤，然後導航至使用XDC編輯器建立設備配置檔案。 按照自述檔案中提供的說明下載xdc_editor_help_web.zip檔案並安裝幫助檔案。
