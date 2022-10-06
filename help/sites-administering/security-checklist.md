---
title: 安全性檢查清單
seo-title: Security Checklist
description: 了解設定和部署AEM時的各種安全性考量事項。
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
source-git-commit: f60d3049b10a8ec500dd0cd4b1b5d4efbe415d84
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 3%

---

# 安全性檢查清單 {#security-checklist}

本節說明您應採取的各種步驟，以確保部署時AEM安裝安全無虞。 核對表應從上到下應用。

>[!NOTE]
>
>此外，還提供了關於以下方面的最危險安全威脅的進一步資訊： [開放Web應用程式安全項目(OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>還有其他的 [安全考量](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 之任何定義。

## 主要安全措施 {#main-security-measures}

### 在生產就緒模式下運行AEM {#run-aem-in-production-ready-mode}

如需詳細資訊，請參閱 [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md).

### 啟用 HTTPS 以提供傳輸層安全性 {#enable-https-for-transport-layer-security}

若要有安全例項，必須在製作和發佈例項上啟用HTTPS傳輸層。

>[!NOTE]
>
>請參閱 [透過SSL啟用HTTP](/help/sites-administering/ssl-by-default.md) 一節以取得詳細資訊。

### 安裝安全Hotfix {#install-security-hotfixes}

請確定您已安裝最新的 [由Adobe提供的安全性Hotfix](https://helpx.adobe.com/tw/experience-manager/kb/aem63-available-hotfixes.html).

### 變更AEM和OSGi Console管理帳戶的預設密碼 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe強烈建議您在安裝後，變更有權限之 [**AEM** `admin` 帳戶](#changing-the-aem-admin-password) （在所有例項上）。

這些帳戶包括：

* AEM `admin` 帳戶

   變更AEM管理員帳戶的密碼後，您在存取CRX時就需要使用新密碼。

* 此 `admin` OSGi Web控制台的密碼

   此變更也會套用至用於存取Web主控台的管理員帳戶，因此您在存取該主控台時需要使用相同的密碼。

這兩個帳戶使用不同的憑證，且每個帳戶都有不同的強式密碼，這對於安全部署至關重要。

#### 變更AEM管理員密碼 {#changing-the-aem-admin-password}

AEM管理員帳戶的密碼可透過 [Granite操作 — 使用者](/help/sites-administering/granite-user-group-admin.md) 控制台。

您可以在此編輯 `admin` 帳戶與 [更改密碼](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>變更管理員帳戶也會變更OSGi Web主控台帳戶。 變更管理員帳戶後，您應將OSGi帳戶變更為其他不同帳戶。

#### 更改OSGi Web控制台密碼的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了AEM `admin` 帳戶，若未能變更OSGi Web主控台密碼的預設密碼，可能會導致：

* 在啟動和關閉期間使用預設密碼暴露伺服器（對於大型伺服器可能需要幾分鐘時間）;
* 儲存庫關閉/重新啟動套件組合時，且OSGI執行時，出現伺服器。

有關更改Web控制台密碼的詳細資訊，請參見 [變更OSGi Web主控台管理密碼](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下方。

#### 變更OSGi Web主控台管理密碼 {#changing-the-osgi-web-console-admin-password}

您還必須更改用於訪問Web控制台的密碼。 這是透過設定 [Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md):

**使用者名稱** 和 **密碼**，此為存取Apache Felix Web Management Console本身的憑證。
初始安裝後，必須變更密碼，以確保執行個體的安全性。

要執行此操作：

1. 導覽至Web主控台，位置為 `<server>:<port>/system/console/configMgr`.
1. 導覽至 **Apache Felix OSGi Management Console** 並改變 **使用者名稱** 和 **密碼**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 按一下「**儲存**」。

### 實作自訂錯誤處理常式 {#implement-custom-error-handler}

Adobe建議定義自訂錯誤處理程式頁面，尤其是404和500 HTTP回應代碼，以防止資訊洩漏。

>[!NOTE]
>
>請參閱 [如何建立自訂指令碼或錯誤處理常式](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) 知識庫文章，以取得詳細資訊。

### 完成Dispatcher安全性檢查清單 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您基礎架構的重要一環。 Adobe強烈建議您完成 [dispatcher安全性檢查清單](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/security-checklist.html).

>[!CAUTION]
>
>使用Dispatcher時，您必須停用「.form」選取器。

## 驗證步驟 {#verification-steps}

### 配置複製和傳輸用戶 {#configure-replication-and-transport-users}

AEM的標準安裝會指定 `admin` 預設情況下作為傳輸憑據的用戶 [複製代理](/help/sites-deploying/replication.md). 此外，管理員使用者也可用來在製作系統上來源復寫。

出於安全考慮，應更改兩者以反映當前的特定使用案例，同時考慮以下兩個方面：

* 此 **傳輸使用者** 不應是管理員使用者。 相反地，在發佈系統上設定只具有對發佈系統相關部分的訪問權限的用戶，並使用該用戶的憑據進行傳輸。

   您可以從捆綁的複製接收者用戶開始，並配置此用戶的訪問權限以匹配您的情況

* 此 **復寫使用者** 或 **代理用戶Id** 也不應是管理員使用者，而應是只能看見應複製內容的使用者。 復寫使用者用來收集要在製作系統上複製的內容，再傳送給發佈者。

### 檢查Operations Dashboard Security Health Checks {#check-the-operations-dashboard-security-health-checks}

AEM 6推出新的Operations Dashboard，旨在協助系統運算子疑難排解問題，並監控執行個體的健全狀態。

控制面板也隨附安全性狀況檢查的集合。 建議您先檢查所有安全性健康狀況檢查的狀態，再與生產執行個體一起上線。 如需詳細資訊，請參閱 [Operations Dashboard檔案](/help/sites-administering/operations-dashboard.md).

### 檢查範例內容是否存在 {#check-if-example-content-is-present}

所有示例內容和用戶(例如Geometrixx項目及其元件)應在生產系統上完全卸載和刪除，然後才可公開訪問。

>[!NOTE]
>
>如果此執行個體在 [生產就緒模式](/help/sites-administering/production-ready.md). 如果由於任何原因，情況並非如此，您可以前往「套件管理器」，然後搜尋並解除安裝所有We.Retail套件，以解除安裝範例內容。 如需詳細資訊，請參閱 [使用套件](package-manager.md).

### 檢查CRX開發套件組合是否存在 {#check-if-the-crx-development-bundles-are-present}

應先在製作和發佈生產系統上卸載這些開發OSGi套件組合，才能使其可訪問。

* AdobeCRXDE支援(com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer(com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### 檢查Sling開發套件組合是否存在 {#check-if-the-sling-development-bundle-is-present}

此 [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) 部署Apache Sling工具支援安裝(org.apache.sling.tooling.support.install)。

應先在製作和發佈生產系統上卸載此OSGi套件，然後才能使其可訪問。

### Protect反對跨網站請求偽造 {#protect-against-cross-site-request-forgery}

#### CSRF保護框架 {#the-csrf-protection-framework}

AEM 6.1隨附有助於防止跨網站請求偽造攻擊的機制，稱為 **CSRF保護框架**. 如需如何使用的詳細資訊，請參閱 [檔案](/help/sites-developing/csrf-protection.md).

#### Sling反向連結篩選器 {#the-sling-referrer-filter}

若要解決CRX WebDAV和Apache Sling中跨網站請求偽造(CSRF)的已知安全性問題，您需要為反向連結篩選器新增設定，才能使用它。

反向連結篩選服務是OSGi服務，可讓您設定：

* 應篩選哪些http方法
* 是否允許空的反向連結標題
* 以及除伺服器主機外允許的伺服器清單。

   預設情況下，該伺服器綁定到的本地主機和當前主機名的所有變數都在清單中。

若要設定反向連結篩選服務：

1. 開啟Apache Felix主控台(**配置**):

   `https://<server>:<port_number>/system/console/configMgr`

1. 登入方式 `admin`.
1. 在 **配置** 菜單，選擇

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 欄位中，輸入允許作為反向連結的所有主機。 每個條目都必須是

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允許來自此伺服器的所有請求和給定埠。
   * 如果您也想允許https要求，則必須輸入第二行。
   * 如果允許來自該伺服器的所有埠，則可以使用 `0` 作為埠號。

1. 檢查 `Allow Empty` 欄位，以允許空白/遺失反向連結標題。

   >[!CAUTION]
   >
   >建議使用命令列工具(例如 `cURL` 而不允許空值，因為它可能會讓您的系統受到CSRF攻擊。

1. 編輯此篩選器用於檢查的方法 `Filter Methods` 欄位。

1. 按一下 **儲存** 來儲存變更。

### OSGI設定 {#osgi-settings}

某些OSGI設定預設為允許更輕鬆地對應用程式進行除錯。 您必須在發佈和編寫生產執行個體時變更這些項目，以避免內部資訊洩露給公眾。

>[!NOTE]
>
>下列所有設定，但 **Day CQ WCM除錯篩選器** 會自動由 [生產就緒模式](/help/sites-administering/production-ready.md). 因此，建議您先檢閱所有設定，然後再將執行個體部署至生產環境中。

對於下列每項服務，需要更改指定的設定：

* [AdobeGraniteHTML程式庫管理員](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 啟用 **Minify** （移除CRLF和空格字元）。
   * 啟用 **Gzip** （允許使用一個請求對檔案進行gzippe和訪問）。
   * disable **除錯**
   * disable **計時**

* [Day CQ WCM除錯篩選器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * 取消勾選 **啟用**

* [Day CQ WCM篩選器](/help/sites-deploying/osgi-configuration-settings.md):

   * 僅在發佈時設定 **WCM模式** 設為「已停用」

* [Apache Sling Java指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **產生除錯資訊**

* [Apache Sling JSP指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **產生除錯資訊**
   * disable **對應內容**

如需詳細資訊，請參閱 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md).

使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

## 進一步讀數 {#further-readings}

### 緩解拒絕服務(DoS)攻擊 {#mitigate-denial-of-service-dos-attacks}

阻斷服務 (DoS) 攻擊指的是嘗試讓電腦資源無法提供給其目標使用者使用。這通常是通過超負荷資源實現的；例如：

* 來自外部來源的大量請求。
* 請求系統無法成功傳送的更多資訊。

   例如，整個存放庫的JSON表示法。

* 借由請求含有不限數量URL的內容頁面，URL可以包含控點、某些選取器、擴充功能和尾碼 — 任何可修改的尾碼。

   例如， `.../en.html` 也可請求為：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   所有有效變數(例如傳回 `200` 回應（且已設定為快取）會由dispatcher進行快取，最終導致完整的檔案系統，且沒有服務可供進一步請求使用。

防止此類攻擊的設定點有很多，這裡我們只討論與AEM直接相關的點。

**設定Sling以防止DoS**

Sling是 *以內容為中心*. 這表示處理作業會聚焦在內容上，因為每個(HTTP)請求會以JCR資源（存放庫節點）的形式對應至內容：

* 第一個目標是保存內容的資源（JCR節點）。
* 其次，轉譯器（或指令碼）是結合請求的特定部分（例如選取器和/或擴充功能）從資源屬性中找到。

>[!NOTE]
>
>有關詳情，請參閱 [Sling要求處理](/help/sites-developing/the-basics.md#sling-request-processing).

此方法讓Sling功能強大且極具彈性，但一如既往，需謹慎管理的彈性。

為幫助防止濫用DoS，您可以：

1. 在應用程式級別納入控制項；由於可能的變數數量，預設配置不可行。

   在您的應用程式中，您應：

   * 控制應用程式中的選取器，以便您 *僅限* 提供所需的明確選取器並傳回 `404` 對其他人。
   * 防止輸出不限數量的內容節點。

1. 檢查預設轉譯器的配置，這可能是問題區域。

   * 尤其是JSON轉譯器，可將樹狀結構橫移至多個層級。

      例如，請求：

      `http://localhost:4502/.json`

      可將整個存放庫傾印為JSON表示法。 這會造成嚴重的伺服器問題。 因此，Sling會設定最大結果數量限制。 若要限制JSON呈現的深度，您可以為設定值：

      **JSON最大結果** ( `json.maximumresults`)

      在 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). 超過此限制時，呈現會收合。 AEM內Sling的預設值為 `1000`.

   * 作為預防措施，可禁用其他預設渲染器(HTML、純文字檔案、XML)。 再次，借由設定 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >請勿停用JSON轉譯器，這是正常操作AEM所需的項目。

1. 使用防火牆來篩選對您執行個體的存取。

   * 必須使用作業系統級別防火牆，才能過濾對實例的點的訪問，如果執行個體未受保護，則可能導致拒絕服務攻擊。

**避免因使用表單選取器而造成的問題**

>[!NOTE]
>
>此緩解措施只應在未使用Forms的AEM環境上執行。

由於AEM不提供的現成索引 `FormChooserServlet`，在查詢中使用表單選取器會觸發代價高昂的存放庫周遊，通常會使AEM例項無法執行。 表單選取器可由 **&amp;ast;.form。&amp;ast;** 查詢中的字串。

請依照下列步驟，減少此問題：

1. 前往Web主控台，將瀏覽器指向 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. 搜尋 **Day CQ WCM表單選擇器Servlet**
1. 按一下項目後，停用 **高級搜索需要** 中。

1. 按一下「**儲存**」。

**減少資產下載Servlet所造成的DoS影響**

預設的資產下載servlet可讓已驗證的使用者發出任意大型、同時下載的請求，以建立資產的ZIP檔案。 建立大型ZIP封存檔可能會使伺服器和網路過載。 為降低由此行為導致的潛在拒絕服務(DoS)風險， `AssetDownloadServlet` OSGi元件預設在 [!DNL Experience Manager] 發佈例項。 已啟用 [!DNL Experience Manager] 依預設為製作例項。

如果您不需要下載功能，請在製作和發佈部署上停用servlet。 如果您的設定需要啟用資產下載功能，請參閱 [這篇文章](/help/assets/download-assets-from-aem.md) 以取得更多資訊。 此外，您也可以定義部署可支援的下載上限。

### 禁用WebDAV {#disable-webdav}

WebDAV應在製作和發佈環境中皆停用。 您可以停止適當的OSGi套件組合來完成此作業。

1. 連線至 **Felix Management Console** 執行時間：

   `https://<*host*>:<*port*>/system/console`

   例如 `http://localhost:4503/system/console/bundles`.

1. 在套件組合清單中，找到名為的套件組合：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 按一下停止按鈕（在「操作」列中）以停止此捆綁。

1. 在套件組合清單中，再找名為：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 按一下停止按鈕以停止此捆綁。

   >[!NOTE]
   >
   >不需要重新啟動AEM。

### 確認您未在使用者首頁路徑中披露個人識別資訊 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

您必須確保不會在存放庫使用者首頁路徑中公開任何個人識別資訊，以保護您的使用者。

自AEM 6.1起，使用者（亦稱為可授權）ID節點名稱的儲存方式，會隨著 `AuthorizableNodeName` 介面。 新介面將不再公開節點名稱中的使用者ID，而會改為產生隨機名稱。

您不需要執行任何設定即可啟用，因為這現在是在AEM中產生可授權ID的預設方式。

雖然不建議使用，但您可以停用它，以備您需要舊實作時，以便與現有應用程式回溯相容。 為了執行此操作，您需要：

1. 前往Web主控台，並從屬性中移除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**項目 **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   您也可以尋找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** OSGi設定中的PID。

1. 刪除 **Apache Jackrabbit Oak隨機可授權節點名稱** 從Web控制台進行OSGi配置。

   為了便於查閱，請注意此設定的PID為 **org.apache.jackrabbit.oak.security.user.RandomAuthorizabledNodeName**.

>[!NOTE]
>
>如需詳細資訊，請參閱Oak檔案，位於 [可授權節點名稱生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### 避免點擊劫持 {#prevent-clickjacking}

若要避免點擊劫持，建議您設定網頁伺服器，以提供設為 `SAMEORIGIN` 的 `X-FRAME-OPTIONS` HTTP 標頭。

如需[點擊劫持的詳細資訊，請查看 OWASP 網站](https://www.owasp.org/index.php/Clickjacking)。

### 確保在需要時正確複製加密密鑰 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和驗證配置要求您在所有AEM執行個體間複製加密金鑰。

在執行此操作之前，請注意，密鑰複製在不同版本之間的操作方式不同，因為6.3和較舊版本之間密鑰的儲存方式不同。

如需詳細資訊，請參閱下方。

#### 復寫AEM 6.3的金鑰 {#replicating-keys-for-aem}

而在舊版中，復寫密鑰儲存在儲存庫中，從AEM 6.3開始，它們儲存在檔案系統中。

因此，為了跨實例複製密鑰，您需要將它們從源實例複製到檔案系統上的目標實例位置。

更具體來說，您需要：

1. 存取AEM例項，通常為製作例項，其中包含要複製的重要資料；
1. 在本機檔案系統中找到com.adobe.granite.crypto.file套件組合。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   此 `bundle.info` 每個資料夾內的檔案會識別套件組合名稱。

1. 導覽至資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 複製HMAC和主檔案。
1. 接著，前往您要複製HMAC金鑰的目標執行個體，並導覽至資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 貼上您先前複製的兩個檔案。
1. [刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目標實例已在運行。
1. 對於要將密鑰複製到的所有實例，重複上述步驟。

>[!NOTE]
>
>首次安裝AEM時，您可以新增下列參數，回復到6.3之前的儲存金鑰方法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 復寫AEM 6.2及舊版的金鑰 {#replicating-keys-for-aem-and-older-versions}

在AEM 6.2及舊版中，金鑰會儲存在 `/etc/key` 節點。

安全地在您的實例中複製密鑰的建議方法是僅複製此節點。 您可以透過CRXDE Lite選擇性地複製節點：

1. 開啟CRXDE Lite，前往 *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. 選取 `/etc/key` 節點。
1. 前往 **復寫** 標籤。
1. 按下 **復寫** 按鈕。

### 執行滲透測試 {#perform-a-penetration-test}

Adobe 極力建議您在進入生產階段前執行 AEM 基礎結構的滲透測試。

### 開發最佳實務 {#development-best-practices}

新發展必須遵循 [安全性最佳實務](/help/sites-developing/security.md) 以確保AEM環境安全無虞。
