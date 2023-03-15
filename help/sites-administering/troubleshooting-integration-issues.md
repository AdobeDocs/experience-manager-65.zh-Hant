---
title: 疑難排解整合問題
seo-title: Troubleshooting Integration Issues
description: 了解如何疑難排解整合問題。
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 2%

---

# 疑難排解整合問題{#troubleshooting-integration-issues}

## 一般疑難排解提示 {#general-troubleshooting-tips}

### 確認沒有JavaScript錯誤 {#ensure-there-are-no-javascript-errors}

檢查瀏覽器的JavaScript主控台是否顯示任何錯誤。 未處理的錯誤可能會導致後續代碼無法正確執行。 如果有錯誤，請檢查導致錯誤的指令碼，以及在哪個區域。 指令碼的路徑可能會指出指令碼屬於哪些功能。

### 登入元件層級 {#logging-on-component-level}

在某些情況下，在元件層級新增其他陳述式可能會很實用。 由於已呈現元件，因此您可以新增臨時標籤來顯示可能有助於識別潛在問題的變數值。 例如：

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

如需記錄的其他詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md) 和 [使用審核記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 頁面。

## Analytics整合問題 {#analytics-integration-issues}

### 報表匯入工具造成CPU/記憶體使用率較高 {#the-report-importer-causes-high-cpu-memory-usage}

Report Importer導致CPU/記憶體使用率高或導致 `OutOfMemoryError` 例外。

#### 解決方案 {#solution}

若要修正此問題，您可以嘗試下列項目：

* 確保未註冊大量PollingImporter（請參閱下面的「由於PollingImporter而導致關機需要很長時間」一節）。
* 對使用CRON運算式執行 `ManagedPollingImporter` 組態 [OSGi主控台](/help/sites-deploying/configuring-osgi.md).

如需在AEM中建立自訂資料匯入工具服務的其他詳細資訊，請參閱下列文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### 由於PollingImporter，關閉需要很長時間 {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics的設計考量到繼承機制。 通常，您會在頁面屬性內新增對Analytics設定的參考，以啟用網站的Analytics [Cloud Services](/help/sites-developing/extending-cloud-config.md) 標籤。 然後，除非頁面需要不同的設定，否則設定會自動繼承至所有子頁面，而不需要再次參照。 新增網站的參考也會自動建立數個節點(AEM 6.3的12個及舊版，AEM 6.4的6個及更新版本) `cq;PollConfig` 可將用來匯入Analytics資料的PollingImporter實例化至AEM。 因此：

* 有許多頁面參考Analytics會導致大量的PollingImporter。
* 此外，參照Analytics設定來複製和貼上頁面會導致其PollingImporter重複。

#### 解決方案 {#solution-1}

首先，分析 [error.log](/help/sites-deploying/configure-logging.md) 可能會讓您深入了解使用中或已註冊的輪詢匯入工具的數量。 例如：

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

其次，請確定只有最上層的頁面（階層中的上層）會參照Analytics設定。

如需在AEM中建立自訂資料匯入工具服務的其他詳細資訊，請參閱下列文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## DTM（舊版）問題 {#dtm-legacy-issues}

### DTM指令碼標籤不會轉譯於頁面來源中 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

此 [DTM](/help/sites-administering/dtm.md) 指令碼標籤未正確納入頁面中，即使頁面屬性中已參考設定亦然 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 標籤。

#### 解決方案 {#solution-2}

若要修正問題，您可以嘗試下列步驟：

* 請確定加密的屬性可以解密(請注意，加密可能會在每個AEM例項上使用不同的自動產生金鑰)。 如需其他詳細資訊，請一併閱讀 [配置屬性的加密支援](/help/sites-administering/encryption-support-for-configuration-properties.md).
* 重新發佈 `/etc/cloudservices/dynamictagmanagement`
* 檢查ACL `/etc/cloudservices`. ACL應為：

   * 允許；jcr:read;webservice-support-servicelibfinder
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/defaults/&amp;ast;
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/defaults
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/public/&amp;ast;
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/public

有關管理ACL的詳細資訊，請閱讀 [使用者管理與安全性](/help/sites-administering/security.md#permissions-in-aem) 頁面。

## Target整合問題 {#target-integration-issues}

### 使用自訂頁面元件時，預覽模式中看不到目標內容 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

發生此問題是因為自訂頁面元件不包含處理Target DTM整合的正確JSP或用戶端程式庫。

#### 解決方案 {#solution-3}

您可以嘗試下列解決方案：

* 確認自訂 `headlibs.jsp` （若有） `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`)包含下列項目：

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 確認自訂 `head.html` （若有） `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **不** 選擇性地包含特定整合標題，如下例：

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

此 `servicelibs.jsp` 新增所需的analytics JavaScript物件並載入與網站相關聯的雲端服務程式庫。 若為Target服務，程式庫會透過 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

載入的程式庫集取決於目標用戶端程式庫的類型( `mbox.js` 或 `at.js`)。

使用DTM來傳送時 `mbox.js` 或 `at.js` 請確定在轉譯內容之前已載入程式庫。 使用Tag Management系統以非同步方式載入這些程式庫，可能會在執行目標特定JavaScript程式碼時造成問題。

如需詳細資訊，請閱讀 [針對目標內容開發](/help/sites-developing/target.md#understanding-the-target-component) 頁面。

### 瀏覽器主控台中會顯示「AppMeasurement初始化中缺少報表套裝ID」錯誤 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

使用DTM在網站上實作Adobe Analytics且使用自訂程式碼時，可能會出現此問題。 原因是使用 `s = new AppMeasurement()` 將 `s` 物件。

#### 解決方案 {#solution-4}

使用 `s_gi` 而非 `new AppMeasurement` 實例化方法。 例如：

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 預設選件會隨機顯示，而非正確的選件 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

此問題可能有多個原因：

* 載入Target用戶端程式庫( `mbox.js` 或 `at.js`)非同步使用第三方Tag Management系統可能會隨機中斷鎖定目標。 Target程式庫應在頁面標題中同步載入。 從AEM傳送程式庫時，一律會如此。

* 載入兩個Target用戶端程式庫( `at.js`)，例如使用DTM和使用AEM中的Target設定。 這可能會導致 `adobe.target` 定義(若 `at.js` 版本不同。

#### 解決方案 {#solution-5}

您可以嘗試下列解決方案：

* 請確定載入類似DTM的程式庫（接著載入Target程式庫）的客戶程式碼會在 [頁首](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* 如果網站設定為使用DTM來傳送Target資料庫，請確定 **由DTM傳遞的Clientlib** 選項 [Target設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) 的URL區段。

### 使用AT.js 1.3+時，一律會顯示預設選件，而非正確的選件 {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

現成的AEM 6.2和6.3與AT.js 1.3.0+版不相容。 隨著AT.js 1.3.0版推出其API的參數驗證， `adobe.target.applyOffer()` 需要「mbox」參數， `atjs-itegration.js` 程式碼。

#### 解決方案 {#solution-6}

要解決此問題，請編輯 `atjs-itegration.js` 並新增 `"mbox": mboxName` 的參數對象中的欄位 `adobe.target.applyOffer()` 如下所示：

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 「目標與設定」頁面不會顯示「報表來源」區段 {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

此問題很可能是 [A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md) 布建問題。

#### 解決方案 {#solution-7}

您必須向AEM發出下列驗證請求，以確認A4T已正確啟用您的Target帳戶：

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

如果回應包含行 `a4tEnabled:false`，連結 [Adobe客戶服務](https://helpx.adobe.com/contact.html) 才能正確布建您的帳戶。

### 實用的Target API {#helpful-target-apis}

以下顯示兩個在疑難排解Target問題時可能很實用的Target API:

* 擷取指定clientcode的Target端點

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 擷取用戶端的設定檔

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
