---
title: 安全核對表
seo-title: Security Checklist
description: 瞭解配置和部署時的各種安全注意事項AEM。
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: 41752e40f2bceae98d4a9ff8bf130476339fe324
workflow-type: tm+mt
source-wordcount: '3025'
ht-degree: 1%

---

# 安全核對表 {#security-checklist}

本節介紹您應採取的各種步驟，以確保在部署時AEM安全安裝。 清單應從上到下應用。

>[!NOTE]
>
>此外，還提供了有關發佈的最危險安全威脅的詳細資訊 [開啟Web應用程式安全項目(OWASP)](https://owasp.org/www-project-top-ten/)。

>[!NOTE]
>
>還有一些 [安全考慮](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 之金額。

## 主要安全措施 {#main-security-measures}

### 在生AEM產就緒模式下運行 {#run-aem-in-production-ready-mode}

有關詳細資訊，請參見 [在生AEM產就緒模式下運行](/help/sites-administering/production-ready.md)。

### 啟用 HTTPS 以提供傳輸層安全性 {#enable-https-for-transport-layer-security}

在作者實例和發佈實例上啟用HTTPS傳輸層對於具有安全實例是必需的。

>[!NOTE]
>
>查看 [啟用HTTP Over SSL](/help/sites-administering/ssl-by-default.md) 的子菜單。

### 安裝安全修補程式 {#install-security-hotfixes}

確保已安裝最新 [安全修補程式由Adobe提供](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hant)。

### 更改和OSGi控制台管AEM理帳戶的預設密碼 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe建議在安裝後更改特權的密碼 [**AEM** `admin` 帳戶](#changing-the-aem-admin-password) （在所有實例上）。

這些帳戶包括：

* AEM `admin` 帳戶

   更改管理員帳戶的密AEM碼後，在訪問CRX時使用新密碼。

* 的 `admin` OSGi Web控制台的密碼

   此更改還應用於用於訪問Web控制台的管理員帳戶，因此在訪問該帳戶時使用相同的密碼。

這兩個帳戶使用單獨的憑據，並且每個帳戶都使用不同的強密碼對安全部署至關重要。

#### 更改管AEM理員密碼 {#changing-the-aem-admin-password}

管理員帳AEM戶的密碼可通過 [花崗岩操作 — 用戶](/help/sites-administering/granite-user-group-admin.md) 控制台。

在此可編輯 `admin` 帳戶和 [更改密碼](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。

>[!NOTE]
>
>更改管理員帳戶還會更改OSGi Web控制台帳戶。 更改管理員帳戶後，應將OSGi帳戶更改為其他帳戶。

#### 更改OSGi Web控制台密碼的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了AEM `admin` 帳戶，如果更改OSGi web控制台密碼的預設密碼失敗，則可能導致：

* 伺服器在啟動和關閉期間使用預設密碼（對於大型伺服器而言可能需要幾分鐘）的暴露；
* 當儲存庫關閉/重新啟動捆綁包 — 並且OSGI正在運行時，伺服器的暴露。

有關更改Web控制台密碼的詳細資訊，請參見 [更改OSGi Web控制台管理員密碼](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下。

#### 更改OSGi Web控制台管理員密碼 {#changing-the-osgi-web-console-admin-password}

更改用於訪問Web控制台的密碼。 使用 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 更新以下屬性 **Apache Felix OSGi管理控制台**:

* **用戶名** 和 **密碼**，用於訪問Apache Felix Web管理控制台本身的憑據。
必須更改密碼 *後* 初始安裝以確保實例的安全。

>[!NOTE]
>
>請參閱 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 以獲取配置OSGi設定的完整詳細資訊。

**更改OSGi Web控制台管理員密碼**:

1. 使用 **工具**。 **操作** 菜單開啟它 **Web控制台** 導航到 **配置** 的子菜單。
例如，在 `<server>:<port>/system/console/configMgr`。
1. 導航到並開啟 **Apache Felix OSGi管理控制台**。
1. 更改 **用戶名** 和 **密碼**。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 選取&#x200B;**儲存**。

### 實現自定義錯誤處理程式 {#implement-custom-error-handler}

Adobe建議定義自定義錯誤處理程式頁，尤其是404和500 HTTP響應代碼，以防止資訊洩漏。

>[!NOTE]
>
>請參閱 [如何建立自定義指令碼或錯誤處理程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) 的子菜單。

### 完成Dispatcher安全檢查表 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您基礎架構的關鍵部分。 Adobe建議您完成 [調度程式安全核對表](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en)。

>[!CAUTION]
>
>使用Dispatcher，必須禁用「.form」選擇器。

## 驗證步驟 {#verification-steps}

### 配置複製和傳輸用戶 {#configure-replication-and-transport-users}

指定的標準安AEM裝 `admin` 作為預設傳輸憑據的用戶 [複製代理](/help/sites-deploying/replication.md)。 此外，管理員用戶還用於在作者系統上源化複製。

出於安全考慮，應更改這兩項，以反映手頭的特定使用情形，同時考慮以下兩個方面：

* 的 **傳輸用戶** 不得是admin用戶。 相反，在發佈系統上設定只對發佈系統相關部分具有訪問權限的用戶，並使用該用戶的憑據進行傳輸。

   您可以從捆綁的複製接收方用戶開始，並配置此用戶的訪問權限以匹配您的情況

* 的 **複製用戶** 或 **代理用戶ID** 也不得是admin用戶，而是只能查看已複製內容的用戶。 複製用戶用於收集要在作者系統上複製的內容，然後再將其發送到發佈者。

### 檢查操作儀表板安全運行狀況檢查 {#check-the-operations-dashboard-security-health-checks}

6AEM介紹了新的操作儀表板，旨在幫助系統操作員解決問題並監控實例的運行狀況。

儀表板還附帶了安全運行狀況檢查的集合。 建議您先檢查所有安全運行狀況檢查的狀態，然後再與生產實例一起使用。 有關詳細資訊，請參閱 [操作儀表板文檔](/help/sites-administering/operations-dashboard.md)。

### 檢查示例內容是否存在 {#check-if-example-content-is-present}

所有示例內容和用戶(例如，Geometrixx項目及其元件)都應在生產系統上完全卸載和刪除，然後才能公開訪問。

>[!NOTE]
>
>示例 `We.Retail` 如果此實例正在運行，則應用程式將被刪除 [生產就緒模式](/help/sites-administering/production-ready.md)。 如果此情況不是這樣，則可以通過轉到「包管理器」，然後搜索和卸載所有示例內容來卸載示例內容 `We.Retail` 包。

請參閱 [使用包](package-manager.md)。

### 檢查CRX開發包是否存在 {#check-if-the-crx-development-bundles-are-present}

應先卸載這些開發OSGi捆綁包，然後發佈生產系統，然後才能訪問。

* AdobeCRXDE支援（com.adobe.granite.crxde支援）
* Adobe花崗岩CRX瀏覽器(com.adobe.granite.crx-explorer)
* Adobe花崗岩CRXDE Lite(com.adobe.granite.crxde-lite)

### 檢查Sling開發包是否存在 {#check-if-the-sling-development-bundle-is-present}

的 [開發AEM人員工具](/help/sites-developing/aem-eclipse.md) 部署Apache Sling工具支援安裝(org.apache.sling.tooling.support.install)。

應先卸載此OSGi捆綁包，然後才能發佈生產系統，然後才能訪問它們。

### Protect反跨站點請求偽造 {#protect-against-cross-site-request-forgery}

#### CSRF保護框架 {#the-csrf-protection-framework}

AEM6.1船隻，其機制有助於防止跨站點請求偽造攻擊，稱為 **CSRF保護框架**。 有關如何使用它的詳細資訊，請參閱 [文檔](/help/sites-developing/csrf-protection.md)。

#### 吊具參考過濾器 {#the-sling-referrer-filter}

要解決CRX WebDAV和Apache Sling中跨站點請求偽造(CSRF)的已知安全問題，請為引用過濾器添加配置以使用它。

引用篩選器服務是OSGi服務，用於配置以下內容：

* 應過濾哪些http方法
* 是否允許空的引用器標頭
* 以及除伺服器主機外允許的伺服器清單。

   預設情況下，localhost和伺服器綁定到的當前主機名的所有變體都在清單中。

要配置引用程式篩選器服務，請執行以下操作：

1. 開啟Apache Felix控制台(**配置**):

   `https://<server>:<port_number>/system/console/configMgr`

1. 登錄身份 `admin`。
1. 在 **配置** ，選擇

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 欄位，輸入允許作為引用者的所有主機。 每個條目必須為

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允許來自此伺服器的所有請求以及給定埠。
   * 如果還要允許https請求，則必須輸入第二行。
   * 如果允許該伺服器的所有埠，則可以 `0` 作為埠號。

1. 檢查 `Allow Empty` 欄位。

   >[!CAUTION]
   >
   >Adobe建議在使用命令行工具(如 `cURL` 而不是允許空值，因為它可能會使您的系統遭受CSRF攻擊。

1. 編輯此篩選器用於檢查的方法 `Filter Methods` 的子菜單。

1. 按一下 **保存** 的子菜單。

### OSGI設定 {#osgi-settings}

預設情況下，某些OSGI設定會設定為允許更輕鬆地調試應用程式。 更改發佈和建立生產性實例上的此類設定，以避免內部資訊洩露給公眾。

>[!NOTE]
>
>下面的所有設定，除 **第CQ WCM日調試篩選器**，由 [生產就緒模式](/help/sites-administering/production-ready.md)。 因此，Adobe建議您在生產環境中部署實例之前先檢查所有設定。

對於以下每種服務，必須更改指定的設定：

* [Adobe花崗岩HTML庫經理](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 啟用 **微型** （刪除CRLF和空格字元）。
   * 啟用 **吉普** （允許使用一個請求對檔案進行壓縮和訪問）。
   * 禁用 **調試**
   * 禁用 **計時**

* [第CQ WCM日調試篩選器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * 取消 **啟用**

* [第CQ WCM篩選器](/help/sites-deploying/osgi-configuration-settings.md):

   * 僅發佈，設定 **WCM模式** &quot;已禁用&quot;

* [Apache Sling JavaScript處理程式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 禁用 **生成調試資訊**

* [Apache Sling JSP指令碼處理程式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * 禁用 **生成調試資訊**
   * 禁用 **映射內容**

請參閱 [OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md)。

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

## 進一步閱讀 {#further-readings}

### 緩解拒絕服務(DoS)攻擊 {#mitigate-denial-of-service-dos-attacks}

阻斷服務 (DoS) 攻擊指的是嘗試讓電腦資源無法提供給其目標使用者使用。此攻擊通常通過超載資源來完成；例如：

* 來自外部源的大量請求。
* 請求的資訊超過系統可以成功傳遞的資訊。

   例如，整個儲存庫的JSON表示法。

* 通過請求具有無限數量URL的內容頁面，URL可以包括句柄、某些選擇器、擴展和尾碼 — 其中任何一個都可以修改。

   比如說， `.../en.html` 也可以請求為：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   所有有效變體(例如，返回 `200` 響應並配置為快取)由Dispatcher進行快取，最終導致完整檔案系統，並且沒有服務用於進一步的請求。

在防止此類攻擊時有許多配置點，但此處僅討論與這些AEM相關的點。

**配置Sling以防止DoS**

吊帶 *以內容為中心*。 當每個(HTTP)請求以JCR資源（儲存庫節點）的形式映射到內容時，處理將集中於內容：

* 第一個目標是保存內容的資源（JCR節點）。
* 其次，呈現器或指令碼從資源屬性中與請求的某些部分（例如，選擇器和/或擴展）一起定位。

請參閱 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing) 的子菜單。

這種方法使吊具功能強大且靈活，但與往常一樣，必須謹慎管理靈活性。

為幫助防止DoS誤用，您可以執行以下操作：

1. 在應用程式級別合併控制項。 由於可能的變體數，預設配置不可行。

   在您的應用程式中，您應：

   * 控制應用程式中的選擇器，以便 *僅* 提供所需的顯式選擇器並返回 `404` 為其他人服務。
   * 防止輸出無限數量的內容節點。

1. 檢查預設投遞器的配置，這可能是問題區域。

   * 特別是，JSON呈現器跨多個級別跨樹結構。

      例如，請求：

      `http://localhost:4502/.json`

      可以將整個儲存庫轉儲到JSON表示法中，這可能導致伺服器出現嚴重問題。 因此，Sling對最大結果數設定了限制。 要限制JSON呈現的深度，請設定以下值：

      **JSON最大結果** ( `json.maximumresults`)

      的 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)。 超過此限制時，呈現將折疊。 Sling中的預設值AEM為 `1000`。

   * 作為預防措施，您應禁用其它預設投遞程式(HTML、純文字檔案、XML)。 同樣，通過配置 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)。
   >[!CAUTION]
   >
   >請勿禁用JSON呈現器，因為它是JSON的正常操作所必需AEM的。

1. 使用防火牆篩選對實例的訪問。

   * 必須使用作業系統級防火牆來過濾對實例中可能導致拒絕服務攻擊的點的訪問，如果這些點處於未保護狀態。

**緩解使用表單選擇器導致的DO**

>[!NOTE]
>
>此緩解應僅在未使AEM用Forms的環境中執行。

因AEM為沒有為 `FormChooserServlet`，在查詢中使用表單選擇器可觸發代價高昂的儲存庫遍歷，通AEM常會使實例陷入停頓。 表單選擇器可通過 **&amp;ast;.form。&amp;ast;** 字串。

要緩解此問題，可以執行以下步驟：

1. 通過將瀏覽器指向 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. 搜索 **第CQ WCM表單選擇器Servlet**
1. 按一下條目後，禁用 **高級搜索要求** 的上界。

1. 按一下「**儲存**」。

**緩解由資產下載Servlet引起的DO**

預設資產下載servlet允許經過驗證的用戶發出任意大的併發下載請求以建立資產的ZIP檔案。 建立大型ZIP存檔會使伺服器和網路過載。 要降低此行為可能導致的拒絕服務(DoS)風險， `AssetDownloadServlet` OSGi元件在上預設禁用 [!DNL Experience Manager] 發佈實例。 已啟用 [!DNL Experience Manager] 預設情況下，作者實例。

如果不需要下載功能，請在作者和發佈部署上禁用servlet。 如果安裝程式要求啟用資產下載功能，請參閱 [這篇文章](/help/assets/download-assets-from-aem.md) 的子菜單。 此外，您可以定義部署可支援的最大下載限制。

### 禁用WebDAV {#disable-webdav}

通過停止適當的OSGi捆綁包，在作者和發佈環境上禁用WebDAV。

1. 連接到 **Felix管理控制台** 運行於：

   `https://<*host*>:<*port*>/system/console`

   比如說， `http://localhost:4503/system/console/bundles`。

1. 在束清單中，查找名為：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 要停止此捆綁包，請在「操作」(Actions)列中按一下「停止」(Stop)按鈕。

1. 同樣，在包清單中，查找名為：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 要停止此捆綁包，請按一下「停止」按鈕。

   >[!NOTE]
   >
   >不需要AEM重新啟動。

### 驗證您沒有在用戶主路徑中透露個人身份資訊 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

通過確保不洩露儲存庫用戶主路徑中的任何個人身份資訊，保護您的用戶非常重要。

自AEM6.1以來，用戶（也稱為可授權）ID節點名稱的儲存方式隨著新的實現而改變 `AuthorizableNodeName` 。 新介面不再公開節點名稱中的用戶ID，而是生成隨機名稱。

不必執行任何配置來啟用它，因為它現在是在中生成可授權ID的預設方AEM式。

雖然不建議使用，但您可以禁用它，以備需要舊實現時，與現有應用程式向後相容。 要執行此操作，必須執行以下操作：

1. 轉到Web控制台，從屬性中刪除** org.apache.jackrabbit.oak.security.user.RandomAuthorizedNodeName**條目 **requiredServicePid** 在 **Apache Jackrabbit Oak安全提供程式**。

   您還可以通過查找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** OSGi配置中的PID。

1. 刪除 **Apache Jackrabbit Oak隨機可授權節點名** 從Web控制台配置OSGi。

   為便於查找，此配置的PID為 **org.apache.jackrabbit.oak.security.user.RandomAuthorizedNodeName**。

>[!NOTE]
>
>有關詳細資訊，請參閱 [可授權的節點名稱生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)。

### 匿名權限強化包 {#anonymous-permission-hardening-package}

預設情況下，AEM儲存系統元資料，如 `jcr:createdBy` 或 `jcr:lastModifiedBy` 作為節點屬性，在儲存庫中常規內容旁邊。 根據配置和訪問控制設定，在某些情況下，這可能導致暴露個人識別資訊(PII)，例如，當此類節點呈現為原始JSON或XML時。

與所有儲存庫資料一樣，這些屬性由Oak授權棧介導。 應根據最少特權原則限制對其的訪問。

為了支援此功能，Adobe提供了一個權限強化包，作為客戶構建的基礎。 它通過在儲存庫根目錄安裝「拒絕」訪問控制項來工作，限制對常用系統屬性的匿名訪問。 包可供下載 [這裡](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) 並且可以安裝在所有支援的版本AEM上。

為了說明更改，我們可以比較在安裝軟體包之前可以匿名查看的節點屬性：

![安裝軟體包之前](/help/sites-administering/assets/before_resized.png)

與安裝軟體包後可查看的軟體， `jcr:createdBy` 和 `jcr:lastModifiedBy` 不可見：

![安裝包後](/help/sites-administering/assets/after_resized.png)

有關詳細資訊，請參閱軟體包發行說明。

### 避免點擊劫持 {#prevent-clickjacking}

為防止點擊劫持，Adobe建議您配置Web伺服器以 `X-FRAME-OPTIONS` HTTP標頭設定為 `SAMEORIGIN`。

有關點擊劫持的詳細資訊，請參閱 [OWASP網站](https://www.owasp.org/index.php/Clickjacking)。

### 確保在需要時正確複製加密密鑰 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和身份驗證方案要求您跨所有實例複製加密AEM密鑰。

在執行此操作之前，密鑰複製在不同版本之間的操作方式不同，因為6.3版和舊版本之間的密鑰儲存方式不同。

有關詳細資訊，請參閱下文。

#### 複製6AEM.3的密鑰 {#replicating-keys-for-aem}

而在較舊版本中，複製密鑰儲存在儲存庫中，從AEM6.3開始，它們儲存在檔案系統中。

因此，要跨實例複製密鑰，請將它們從源實例複製到檔案系統上目標實例的位置。

具體來說，您必須執行以下操作：

1. 訪問包AEM含要複製的關鍵材料的實例（通常為作者實例）;
1. 在本地檔案系統中找到com.adobe.granite.crypto.file包。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   的 `bundle.info` 每個資料夾中的檔案標識包名稱。

1. 導航到資料資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 複製HMAC和主檔案。
1. 然後，轉到要將HMAC密鑰複製到的目標實例，然後導航到資料資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 貼上以前複製的兩個檔案。
1. [刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 目標實例已在運行。
1. 對要將密鑰複製到的所有實例重複上述步驟。

>[!NOTE]
>
>在首次安裝時添加以下參數，可以恢復到6.3之前的儲存密鑰方AEM法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 複製6.AEM2和舊版本的密鑰 {#replicating-keys-for-aem-and-older-versions}

在AEM6.2和更舊版本中，密鑰儲存在 `/etc/key` 的下界。

建議在實例中安全地複製密鑰的方法是僅複製此節點。 您可以通過CRXDE Lite有選擇地複製節點：

1. 通過轉到開啟CRXDE Lite *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. 選擇 `/etc/key` 的下界。
1. 轉到 **複製** 頁籤。
1. 按 **複製** 按鈕

### 執行滲透測試 {#perform-a-penetration-test}

Adobe建議您在開始生產之前AEM對基礎架構執行滲透test。

### 開發最佳做法 {#development-best-practices}

新的發展必須遵循 [安全最佳做法](/help/sites-developing/security.md) 確保您的AEM環境安全。
