---
title: 疑難排解整合問題
seo-title: 疑難排解整合問題
description: 了解如何疑難排解整合問題。
seo-description: 了解如何疑難排解整合問題。
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 1%

---

# 疑難排解整合問題{#troubleshooting-integration-issues}

## 一般疑難排解提示{#general-troubleshooting-tips}

### 確保沒有JavaScript錯誤{#ensure-there-are-no-javascript-errors}

檢查瀏覽器的JavaScript主控台是否顯示任何錯誤。 未處理的錯誤可能會導致後續代碼無法正確執行。 如果有錯誤，請檢查導致錯誤的指令碼，以及在哪個區域。 指令碼的路徑可能會指出指令碼屬於哪些功能。

### 在元件級別{#logging-on-component-level}上登錄

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

有關日誌記錄的其他詳細資訊，請參閱[Logging](/help/sites-deploying/configure-logging.md)和[Working with Audit Records and Log Files](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)頁。

## Analytics整合問題{#analytics-integration-issues}

### 報告導入程式導致CPU/記憶體使用率高{#the-report-importer-causes-high-cpu-memory-usage}

Report Importer導致CPU/記憶體使用率較高，或導致`OutOfMemoryError`異常。

#### 解決方案 {#solution}

若要修正此問題，您可以嘗試下列項目：

* 確保未註冊大量PollingImporter（請參閱下面的「由於PollingImporter而導致關機需要很長時間」一節）。
* 在[OSGi主控台](/help/sites-deploying/configuring-osgi.md)中，使用`ManagedPollingImporter`設定的CRON運算式，在一天的特定時間執行報表匯入工具。

如需在AEM中建立自訂資料匯入工具服務的其他詳細資訊，請參閱下列文章[https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)。

### 由於PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}，關閉需要很長時間

Analytics的設計考量到繼承機制。 通常，您會在頁面屬性[Cloud Services](/help/sites-developing/extending-cloud-config.md)標籤內新增對Analytics設定的參考，以啟用網站的Analytics。 然後，除非頁面需要不同的設定，否則設定會自動繼承至所有子頁面，而不需要再次參照。 將參考新增至網站也會自動建立數個節點(AEM 6.3為12,AEM 6.4為6,   和更新版本)，將用來將Analytics資料匯入AEM的PollingImporter實例化。 `cq;PollConfig`因此：

* 有許多頁面參考Analytics會導致大量的PollingImporter。
* 此外，參照Analytics設定來複製和貼上頁面會導致其PollingImporter重複。

#### 解決方案{#solution-1}

首先，分析[error.log](/help/sites-deploying/configure-logging.md)可讓您深入了解使用中或已註冊的PollingImporter的數量。 例如：

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

如需在AEM中建立自訂資料匯入工具服務的其他詳細資訊，請參閱下列文章[https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)。

## DTM（舊版）問題{#dtm-legacy-issues}

### DTM指令碼標籤不會呈現在頁面來源{#the-dtm-script-tag-is-not-rendered-in-the-page-source}中

即使頁面屬性[Cloud Services](/help/sites-developing/extending-cloud-config.md)索引標籤中已參考設定，頁面中仍未正確包含[DTM](/help/sites-administering/dtm.md)指令碼標籤。

#### 解決方案{#solution-2}

若要修正問題，您可以嘗試下列步驟：

* 請確定加密的屬性可以解密(請注意，加密可能會在每個AEM例項上使用不同的自動產生金鑰)。 有關其他詳細資訊，請閱讀[配置屬性的加密支援](/help/sites-administering/encryption-support-for-configuration-properties.md)。
* 重新發佈`/etc/cloudservices/dynamictagmanagement`中的配置
* 檢查`/etc/cloudservices`上的ACL。 ACL應為：

   * 允許；jcr:read;webservice-support-servicelibfinder
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/defaults/&amp;ast;
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/defaults
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/public/&amp;ast;
   * 允許；jcr:read;大家；rep:glob:&amp;ast;/public

有關管理ACL的詳細資訊，請閱讀[用戶管理和安全性](/help/sites-administering/security.md#permissions-in-aem)頁。

## Target整合問題{#target-integration-issues}

### 使用自訂頁面元件{#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}時，在預覽模式中看不到目標內容

發生此問題是因為自訂頁面元件不包含處理Target DTM整合的正確JSP或用戶端程式庫。

#### 解決方案{#solution-3}

您可以嘗試下列解決方案：

* 確認自訂`headlibs.jsp`（如果有`/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`）包含下列項目：

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 確認自訂`head.html`（如果有`/apps/<CUSTOM-COMPONENTS-PATH>/head.html`）**不**&#x200B;選擇性地包含特定的整合標題，如下列範例所示：

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

`servicelibs.jsp`會新增必要的分析JavaScript物件並載入與網站相關聯的雲端服務程式庫。 若為Target服務，會透過`/libs/cq/analytics/components/testandtarget/headlibs.jsp`載入程式庫

載入的程式庫集取決於Target設定上使用的目標用戶端程式庫類型（`mbox.js`或`at.js`）。

使用DTM來傳送`mbox.js`或`at.js`時，請務必在轉譯內容之前載入程式庫。 使用非同步載入這些程式庫的標籤管理系統，可能會在執行目標特定JavaScript程式碼時造成問題。

如需詳細資訊，請參閱[針對目標內容開發](/help/sites-developing/target.md#understanding-the-target-component)頁面。

### 瀏覽器主控台{#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}中會顯示「AppMeasurement初始化中缺少報表套裝ID」錯誤

使用DTM在網站上實作Adobe Analytics且使用自訂程式碼時，可能會出現此問題。 原因是使用`s = new AppMeasurement()`實例化`s`對象。

#### 解決方案{#solution-4}

使用`s_gi`取代`new AppMeasurement`實例化方法。 例如：

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 預設選件會隨機顯示，而非正確的選件{#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

此問題可能有多個原因：

* 使用第三方標籤管理系統非同步載入Target用戶端程式庫（`mbox.js`或`at.js`）可能會隨機中斷鎖定目標。 Target程式庫應在頁面標題中同步載入。 從AEM傳送程式庫時，一律會如此。

* 同時載入兩個Target用戶端程式庫(`at.js`)，例如一個使用DTM，另一個使用AEM中的Target設定。 如果`at.js`版本不同，這可能會導致`adobe.target`定義衝突。

#### 解決方案{#solution-5}

您可以嘗試下列解決方案：

* 請確定載入DTM類型程式庫的客戶程式碼（進而載入Target程式庫）會在[頁面標題](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages)中同步執行。
* 如果網站設定為使用DTM來傳送Target資料庫，請確定已在網站的[Target設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html)中勾選DTM **傳遞的** Clientlib選項。

### 使用AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}時，一律會顯示預設選件，而非正確的選件

現成的AEM 6.2和6.3與AT.js 1.3.0+版不相容。 隨著AT.js 1.3.0版推出API的參數驗證，`adobe.target.applyOffer()`需要「mbox」參數，而`atjs-itegration.js`程式碼未提供此參數。

#### 解決方案{#solution-6}

要解決此問題，請編輯`atjs-itegration.js`並按如下方式在`adobe.target.applyOffer()`的參數對象中添加`"mbox": mboxName`欄位：

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

### 「目標與設定」頁面未顯示「報表來源」區段{#the-goals-settings-page-does-not-show-the-reporting-sources-section}

此問題很可能是[A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md)布建問題。

#### 解決方案{#solution-7}

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

如果回應包含行`a4tEnabled:false`，請連絡Adobe客戶服務](https://helpx.adobe.com/contact.html)以正確布建您的帳戶。[

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
