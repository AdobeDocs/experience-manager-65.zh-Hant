---
title: 安全性檢查清單
seo-title: 安全性檢查清單
description: 瞭解設定和部署時的各種安全性考量AEM。
seo-description: 瞭解設定和部署時的各種安全性考量AEM。
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: 安全性
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2842'
ht-degree: 0%

---

# 安全檢查清單{#security-checklist}

本節說明您應採取的各種步驟，以確保在部署時AEM的安裝安全。 清單應從上到下套用。

>[!NOTE]
>
>[還有關Open Web Application Security Project(OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)發佈的最危險安全威脅的詳細資訊。

>[!NOTE]
>
>在開發階段，還有一些額外的[安全性考量](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)。

## 主要安全措施{#main-security-measures}

### 在生AEM產就緒模式下運行{#run-aem-in-production-ready-mode}

如需詳細資訊，請參閱[在生產就AEM緒模式中執行](/help/sites-administering/production-ready.md)。

### 啟用HTTPS以確保傳輸層安全{#enable-https-for-transport-layer-security}

在作者和發佈例項上啟用HTTPS傳輸層對於擁有安全例項是必備的。

>[!NOTE]
>
>如需詳細資訊，請參閱[啟用HTTP Over SSL](/help/sites-administering/ssl-by-default.md)一節。

### 安裝安全性修補程式{#install-security-hotfixes}

請確定您已安裝了Adobe](https://helpx.adobe.com/tw/experience-manager/kb/aem63-available-hotfixes.html)提供的最新[安全性修補程式。

### 更改和OSGi控制台管AEM理帳戶的預設密碼{#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe強烈建議在安裝後更改特權&#x200B;[**AEM** `admin`帳戶](#changing-the-aem-admin-password)（在所有實例上）的口令。

這些帳戶包括：

* &lt;AEMa0/>帳戶`admin`

   在您變更管理員帳戶的密AEM碼後，在存取CRX時，就需要使用新密碼。

* OSGi Web控制台的`admin`口令

   此變更也會套用至用於存取Web主控台的管理員帳戶，因此在存取Web主控台時，您必須使用相同的密碼。

這兩個帳戶使用不同的憑證，並且對每個帳戶使用不同的強式密碼，對於安全部署至關重要。

#### 更改AEM管理員密碼{#changing-the-aem-admin-password}

管理員帳AEM戶的密碼可以透過[Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md)主控台進行變更。

您可以在這裡編輯`admin`帳戶並變更密碼](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。[

>[!NOTE]
>
>變更管理員帳戶也會變更OSGi網頁主控台帳戶。 變更管理員帳戶後，您應將OSGi帳戶變更為其他項目。

#### 更改OSGi Web控制台密碼{#importance-of-changing-the-osgi-web-console-password}的重要性

除了AEM`admin`帳戶，如果無法更改OSGi Web控制台密碼的預設密碼，則可能導致：

* 在啟動和關閉期間使用預設密碼的伺服器曝光（大型伺服器可能需要幾分鐘的時間）;
* 當儲存庫關閉／重新啟動綁定——且OSGI正在運行時，伺服器的暴露。

有關更改Web控制台密碼的詳細資訊，請參閱下面的[更改OSGi Web控制台管理密碼](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)。

#### 更改OSGi Web控制台管理員密碼{#changing-the-osgi-web-console-admin-password}

您還必須更改用於訪問Web控制台的口令。 這是通過配置[Apache Felix OSGi管理控制台](/help/sites-deploying/osgi-configuration-settings.md)的以下屬性來完成的：

**User** Name and  **Password**，用於訪問Apache Felix Web Management Console本身的認證。在初始安裝後必須更改密碼，以確保實例的安全性。

要執行此操作：

1. 導覽至位於`<server>:<port>/system/console/configMgr`的Web主控台。
1. 導覽至&#x200B;**Apache Felix OSGi Management Console**&#x200B;並變更&#x200B;**使用者名稱**&#x200B;和&#x200B;**密碼**。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 按一下「**儲存**」。

### 實作自訂錯誤處理常式{#implement-custom-error-handler}

Adobe建議定義自訂錯誤處理常式頁面，尤其是404和500個HTTP回應代碼，以防止資訊洩漏。

>[!NOTE]
>
>如需詳細資訊，請參閱[如何建立自訂指令碼或錯誤處理常式](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html)知識庫文章。

### 完整的Dispatcher Security Checklist {#complete-dispatcher-security-checklist}

DispatcherAEM是您基礎架構中的關鍵部分。 Adobe強烈建議您完成[dispatcher安全檢查清單](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/security-checklist.html)。

>[!CAUTION]
>
>使用Dispatcher ，您必須禁用&quot;。form&quot;選擇器。

## 驗證步驟{#verification-steps}

### 配置複製和傳輸用戶{#configure-replication-and-transport-users}

標準安裝AEM將`admin`指定為預設[複製代理](/help/sites-deploying/replication.md)內傳輸憑據的用戶。 此外，管理員用戶還用於在作者系統上查找複製源。

出於安全考慮，應對兩者做出更改，以反映手邊的特定使用案例，同時考慮到以下兩個方面：

* **transport user**&#x200B;不應是admin用戶。 相反地，在發佈系統上設定僅對發佈系統的相關部分具有訪問權限的用戶，並使用該用戶的憑據進行傳輸。

   您可以從捆綁的複製接收器用戶開始，並配置此用戶的訪問權限以匹配您的情況

* **複製用戶**&#x200B;或&#x200B;**代理用戶Id**&#x200B;也不應是管理員用戶，而應是只能看到應複製內容的用戶。 複製用戶用於收集要在作者系統上複製的內容，然後再將其發送到發佈者。

### 檢查Operations Dashboard Security Health Checks {#check-the-operations-dashboard-security-health-checks}

AEM6推出全新的Operations Dashboard，旨在協助系統營運商疑難排解問題並監控執行個體的健全狀況。

控制面板也隨附一組安全性健康狀況檢查。 建議您先檢查所有安全性健康狀況檢查的狀態，再與生產實例一起上線。 如需詳細資訊，請參閱[ Operations Dashboard檔案](/help/sites-administering/operations-dashboard.md)。

### 檢查範例內容是否存在{#check-if-example-content-is-present}

所有範例內容和使用者(例如，Geometrixx專案及其元件)應先在生產系統上完全解除安裝並刪除，再公開存取。

>[!NOTE]
>
>如果此實例在[生產就緒模式](/help/sites-administering/production-ready.md)中運行，則We.Retail應用程式示例將被刪除。 如果由於任何原因，不是這樣，您可以通過轉到「包管理器」，然後搜索和卸載所有We.Retail包來卸載示例內容。 有關詳細資訊，請參閱[使用包](package-manager.md)。

### 檢查CRX開發包是否存在{#check-if-the-crx-development-bundles-are-present}

這些開發OSGi套件應先在作者和發佈生產系統上解除安裝，然後再加以存取。

* AdobeCRXDE支援(com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer(com.adobe.granite.crx-explorer)
* Adobe花崗岩CRXDE Lite(com.adobe.granite.crxde-lite)

### 檢查Sling開發套件是否存在{#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md)部署Apache Sling Tooling Support Install(org.apache.sling.tooling.support.install)。

此OSGi套件應先解除安裝在作者和發佈生產系統上，再加以存取。

### Protect反對跨網站偽造要求{#protect-against-cross-site-request-forgery}

#### CSRF保護框架{#the-csrf-protection-framework}

AEM 6.1船舶提供一種機制，可協助保護您免受跨網站偽造要求攻擊，稱為&#x200B;**CSRF Protection Framework**。 有關如何使用它的詳細資訊，請參閱[文檔](/help/sites-developing/csrf-protection.md)。

#### The Sling Referrer Filter {#the-sling-referrer-filter}

若要解決CRX WebDAV和Apache Sling中跨網站要求偽造(CSRF)的已知安全性問題，您必須新增反向連結篩選器的設定，才能使用它。

反向連結篩選服務是一項OSGi服務，可讓您設定：

* 哪些http方法應加以篩選
* 是否允許空的反向連結標題
* 以及除伺服器主機外允許的伺服器清單。

   預設情況下，綁定伺服器的localhost和當前主機名的所有變化都在清單中。

若要設定反向連結篩選服務：

1. 在以下位置開啟Apache Felix控制台(**Configurations**):

   `https://<server>:<port_number>/system/console/configMgr`

1. 以`admin`的身分登入。
1. 在&#x200B;**配置**&#x200B;菜單中，選擇：

   `Apache Sling Referrer Filter`

1. 在`Allow Hosts`欄位中，輸入允許做為反向連結的所有主機。 每個項目都必須是表單

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允許來自該伺服器的所有請求和給定埠。
   * 如果您也想要允許https要求，您必須輸入第二行。
   * 如果允許該伺服器的所有埠，可以使用`0`作為埠號。

1. 如果您要允許空白／遺失反向連結標題，請勾選`Allow Empty`欄位。

   >[!CAUTION]
   >
   >建議在使用命令列工具（例如`cURL`）時提供反向連結，而不要允許空值，因為它可能會使您的系統受到CSRF攻擊。

1. 編輯此篩選器應用於`Filter Methods`欄位檢查的方法。

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### OSGI設定{#osgi-settings}

有些OSGI設定預設會設定，讓應用程式的除錯更輕鬆。 您必須在發佈和製作生產性執行個體時變更這些項目，以避免內部資訊洩露給公眾。

>[!NOTE]
>
>除&#x200B;**The Day CQ WCM Debug Filter**&#x200B;之外，以下所有設定都由[Production Ready Mode](/help/sites-administering/production-ready.md)自動覆蓋。 因此，我們建議您先檢閱所有設定，再將執行個體部署至生產環境。

對於下列每項服務，需要更改指定的設定：

* [AdobeGranite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 啟用&#x200B;**Minify**（以移除CRLF和空白字元）。
   * 啟用&#x200B;**Gzip**（允許使用一個請求對檔案進行壓縮和訪問）。
   * 停用&#x200B;**除錯**
   * 停用&#x200B;**計時**

* [日CQ WCM除錯篩選](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * 取消選中&#x200B;**啟用**

* [日CQ WCM篩選](/help/sites-deploying/osgi-configuration-settings.md):

   * 在僅發佈時，將&#x200B;**WCM模式**&#x200B;設為「已停用」

* [Apache Sling Java指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 停用&#x200B;**產生除錯資訊**

* [Apache Sling JSP指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * 停用&#x200B;**產生除錯資訊**
   * 禁用&#x200B;**映射內容**

有關詳細資訊，請參閱[OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md)。

使用時，有AEM幾種管理此類服務配置設定的方法；如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

## 進一步閱讀{#further-readings}

### 緩解拒絕服務(DoS)攻擊{#mitigate-denial-of-service-dos-attacks}

拒絕服務(DoS)攻擊是企圖使電腦資源對其預定用戶不可用。 這通常是通過超載資源實現的；例如：

* 來自外部來源的大量請求。
* 系統無法成功傳遞更多資訊。

   例如，整個儲存庫的JSON表示法。

* 透過請求不限數量URL的內容頁面，URL可包含控制代碼、部分選擇器、擴充功能和字尾——其中任何一個都可加以修改。

   例如，`.../en.html`也可以被請求為：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   所有有效變化（例如返回`200`響應並配置為快取）都將由調度程式進行快取，最終導致完整檔案系統，並且沒有服務用於進一步請求。

防止此類攻擊的配置點有很多，這裡我們只討論與之直接相關的AEM。

**設定Sling以防止DoS**

Sling為&#x200B;*content-centric*。 這表示處理會以JCR資源（儲存庫節點）的形式，將每個(HTTP)請求映射至內容時，將重點放在內容上：

* 第一個目標是保存內容的資源（JCR節點）。
* 其次，轉換器（或指令碼）與請求的某些部分（例如選擇器和／或擴充功能）結合，從資源屬性中找到。

>[!NOTE]
>
>這在[Sling Request Processing](/help/sites-developing/the-basics.md#sling-request-processing)下有更詳細的說明。

這種方式讓Sling功能強大，而且有彈性，但是和以往一樣，需要謹慎管理的彈性。

為協助防止誤用DoS，您可以：

1. 在應用程式層級整合控制項；由於可能的變化數量，預設配置不可行。

   在您的應用程式中，您應：

   * 控制應用程式中的選擇器，讓您&#x200B;*僅*&#x200B;提供所需的明確選擇器，並傳回其他所有選擇器的`404`。
   * 防止輸出不限數量的內容節點。

1. 檢查預設轉譯器的配置，該配置可能是問題區域。

   * 尤其是JSON轉譯器，它可將樹狀結構橫跨多個層級。

      例如，請求：

      `http://localhost:4502/.json`

      可以將整個儲存庫轉儲為JSON表示法。 這會導致伺服器出現嚴重問題。 因此，Sling會設定最大結果數的限制。 若要限制JSON轉換的深度，您可以設定值：

      **JSON最大結果** ( `json.maximumresults`)

      在[Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)的組態中。 超過此限制時，演算將會收合。 Sling within的預設值AEM為`200`。

   * 作為預防措施，可禁用其他預設渲染器（HTML、純文字檔案、XML）。 再次，請設定[Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)。
   >[!CAUTION]
   >
   >請勿停用JSON轉譯器，這是正常作業的必要項AEM目。

1. 使用防火牆來篩選對您實例的存取。

   * 必須使用作業系統層級防火牆，才能篩選對例項的存取，若未受保護，可能會導致拒絕服務攻擊。

**減輕因使用表單選擇器而造成的DoS影響**

>[!NOTE]
>
>此緩解措施僅應在未使AEM用Forms的環境中執行。

由AEM於`FormChooserServlet`不提供現成可用的索引，因此在查詢中使用表單選擇器將觸發代價高昂的儲存庫遍歷，通常會使實例AEM停止。 表單選擇器可通過&#x200B;**&amp;ast;.form的存在來檢測。查詢中的&amp;ast;**&#x200B;字串。

為減輕此問題，請遵循下列步驟：

1. 將瀏覽器指向&#x200B;*https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*，移至「Web控制台」

1. 搜索&#x200B;**Day CQ WCM表單選擇器Servlet**
1. 按一下條目後，請在以下窗口中禁用&#x200B;**高級搜索要求**。

1. 按一下「**儲存**」。

**減輕資產下載Servlet造成的DoS影響**

中的預設資產下載ServletAEM允許通過身份驗證的用戶發出任意大型的併發下載請求，以建立可見資產的ZIP檔案，該檔案可能會使伺服器和／或網路過載。

為了降低此功能造成的潛在DoS風險，`AssetDownloadServlet` OSGi元件預設會停用於最新版本的發AEM布例項。

如果您的設定要求啟用資產下載伺服器，請參閱[本文章](/help/assets/download-assets-from-aem.md)以取得詳細資訊。

### 禁用WebDAV {#disable-webdav}

WebDAV應在作者和發佈環境中都停用。 這可以通過停止適當的OSGi捆綁包來完成。

1. 連線至&#x200B;**Felix Management Console**，執行於：

   `https://<*host*>:<*port*>/system/console`

   例如`http://localhost:4503/system/console/bundles`。

1. 在綁定清單中，查找名為：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 按一下「停止」按鈕（在「動作」欄中）以停止此搭售。

1. 再次在綁定清單中，查找名為：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 按一下停止按鈕以停止此包。

   >[!NOTE]
   >
   >不需要AEM重新啟動。

### 確認您未在使用者首頁路徑{#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}中透露個人識別資訊

請務必確保不會在儲存庫用戶主路徑中洩露任何個人身份識別資訊，以保護您的用戶。

自AEM6.1以來，使用`AuthorizableNodeName`介面的新實作來變更使用者（也稱為可授權）ID節點名稱的儲存方式。 新介面將不再公開節點名稱中的使用者ID，而是產生隨機名稱。

不需要執行任何設定才能啟用，因為這是在中產生可授權ID的預設方式AEM。

雖然不建議使用，但您可以停用它，以備需要舊實作時，以便與現有應用程式回溯相容。 若要這麼做，您必須：

1. 前往Web主控台，從&#x200B;**Apache Jackrabbit Oak SecurityProvider**&#x200B;中的屬性&#x200B;**requiredServicePids**&#x200B;移除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**項目。

   您也可以在OSGi組態中尋找&#x200B;**org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID，以找到Oak安全性提供者。

1. 從Web主控台刪除&#x200B;**Apache Jackrabbit Oak Random Authorized Node Name** OSGi組態。

   若要更容易查閱，請注意，此組態的PID是&#x200B;**org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**。

>[!NOTE]
>
>如需詳細資訊，請參閱[可授權節點名稱產生](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)上的Oak檔案。

### 防止點按劫持{#prevent-clickjacking}

為避免點按劫持，建議您設定您的網站伺服器，以提供設為`SAMEORIGIN`的`X-FRAME-OPTIONS` HTTP標題。

有關點按劫持的更多[資訊，請參閱OWASP站點](https://www.owasp.org/index.php/Clickjacking)。

### 確保在需要時正確複製加密密鑰{#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和驗證方案要求您在所有實例中複製加密AEM密鑰。

在執行此操作之前，請注意，密鑰複製在不同版本之間的操作方式不同，因為6.3和更舊版本之間密鑰的儲存方式不同。

請參閱下方以取得詳細資訊。

#### 複製6.AEM3 {#replicating-keys-for-aem}的密鑰

而在舊版中，複製密鑰儲存在儲存庫中，從6.AEM3開始，它們儲存在檔案系統中。

因此，為了跨實例複製密鑰，您需要將它們從源實例複製到檔案系統上的目標實例的位置。

更具體地說，您需要：

1. 存取包AEM含要複製之關鍵材料的例項，通常為作者例項；
1. 在本機檔案系統中找到com.adobe.granite.crypto.file套件。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   每個資料夾內的`bundle.info`檔案將標識包名稱。

1. 導覽至資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 複製HMAC和主檔案。
1. 然後，前往您要複製HMAC金鑰的目標執行個體，並導覽至資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 貼上您先前複製的兩個檔案。
1. [如果目標實](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 例已在運行，請刷新Crypto Bundle。
1. 對要將密鑰複製到的所有實例重複上述步驟。

>[!NOTE]
>
>首次安裝時，您可以新增下列參數，回復至6.3之前的儲存金鑰方法AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 複製6.AEM2和舊版{#replicating-keys-for-aem-and-older-versions}的密鑰

在AEM6.2和更舊版本中，密鑰儲存在`/etc/key`節點下的儲存庫中。

建議在實例間安全地複製密鑰的方法是僅複製此節點。 您可以通過CRXDE Lite有選擇地複製節點：

1. 前往&#x200B;*https://&lt;serveraddress>:4502/crx/de/index.jsp*&#x200B;開啟CRXDE Lite
1. 選擇`/etc/key`節點。
1. 轉到&#x200B;**Replication**&#x200B;頁籤。
1. 按&#x200B;**複製**&#x200B;按鈕。

### 執行滲透測試{#perform-a-penetration-test}

Adobe強烈建議您在開始生產之前，先AEM對基礎架構執行滲透測試。

### 開發最佳實踐{#development-best-practices}

新的開發必須遵循[安全性最佳實務](/help/sites-developing/security.md)，以確保您的環境AEM安全無虞。
