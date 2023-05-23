---
title: 疑難排解整合問題
seo-title: Troubleshooting Integration Issues
description: 瞭解如何解決整合問題。
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

## 一般故障排除提示 {#general-troubleshooting-tips}

### 確保沒有JavaScript錯誤 {#ensure-there-are-no-javascript-errors}

檢查瀏覽器的JavaScript控制台是否顯示任何錯誤。 未處理的錯誤可能會阻止後續代碼正確執行。 如果出現錯誤，請檢查導致錯誤的指令碼以及在哪個區域。 指令碼的路徑可能會指示指令碼屬於哪些功能。

### 登錄元件級別 {#logging-on-component-level}

在某些情況下，在元件級別添加其他語句可能會有所幫助。 由於呈現了元件，因此可以添加臨時標籤以顯示可能有助於識別潛在問題的變數值。 例如：

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

有關日誌記錄的其他詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md) 和 [使用審計記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 頁。

## 分析整合問題 {#analytics-integration-issues}

### 報告導入程式導致CPU/記憶體使用率較高 {#the-report-importer-causes-high-cpu-memory-usage}

報告導入程式導致CPU/記憶體使用率高或導致 `OutOfMemoryError` 例。

#### 解決方案 {#solution}

要解決此問題，可嘗試以下操作：

* 確保未註冊大量PollingImporter（請參閱下面的「Shutdown taime a four PollingImporter」一節）。
* 使用CRON表達式在一天中的某個時間運行報表導入程式 `ManagedPollingImporter` 配置 [OSGi控制台](/help/sites-deploying/configuring-osgi.md)。

有關在中建立自定義資料導入程式服務的其AEM他詳細資訊，請閱讀以下文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)。

### 由於PollingImporter，關閉需要很長時間 {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

分析設計時考慮了繼承機制。 通常，通過在頁面屬性中添加對分析配置的引用來為站點啟用分析 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 頁籤。 然後，該配置將自動繼承到所有子頁，而無需再次引用它，除非某頁需要其他配置。 添加對站點的引用還會自動建立該類型的多個節點(AEM6.3和6.3的節點12或6的節AEM點6.4和更高版本) `cq;PollConfig` 實例化用於將分析資料導入到的PollingImporterAEM。 因此：

* 引用Analytics的大量頁面會導致大量PollingImporter。
* 此外，複製和貼上引用分析配置的頁面會導致其PollingImporter的重複。

#### 解決方案 {#solution-1}

首先，分析 [錯誤.log](/help/sites-deploying/configure-logging.md) 可能會讓您瞭解活動或註冊的PollingImporter的數量。 例如：

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

其次，確保只有頂層頁面（層次結構中的上層）引用了分析配置。

有關在中建立自定義資料導入程式服務的其AEM他詳細資訊，請閱讀以下文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)。

## DTM（舊版）問題 {#dtm-legacy-issues}

### DTM指令碼標籤未在頁源中呈現 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

的 [DTM](/help/sites-administering/dtm.md) 即使在頁屬性中引用了配置，也未正確將指令碼標籤包括在頁中 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 頁籤。

#### 解決方案 {#solution-2}

要解決此問題，可嘗試以下操作：

* 確保加密的屬性可以解密(請注意，加密可能在每個實例上使用不同的自動生AEM成密鑰)。 有關其他詳細資訊，另請閱讀 [配置屬性的加密支援](/help/sites-administering/encryption-support-for-configuration-properties.md)。
* 重新發佈中找到的配置 `/etc/cloudservices/dynamictagmanagement`
* 檢查ACL `/etc/cloudservices`。 ACL應為：

   * 允許；jcr：讀取；WebService SupportServiceFinder
   * 允許；jcr：讀取；大家；代表:glob:&amp;ast;/defaults/&amp;ast
   * 允許；jcr：讀取；大家；代表:glob:&amp;ast;/預設值
   * 允許；jcr：讀取；大家；代表:glob:&amp;ast;/public/&amp;ast;
   * 允許；jcr：讀取；大家；代表:glob:&amp;ast;/public

有關管理ACL的詳細資訊，請閱讀 [用戶管理和安全](/help/sites-administering/security.md#permissions-in-aem) 的子菜單。

## 目標整合問題 {#target-integration-issues}

### 使用自定義頁面元件時，在預覽模式下不可見目標內容 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

此問題之所以出現，是因為自定義頁面元件不包含處理目標DTM整合的正確JSP或客戶端庫。

#### 解決方案 {#solution-3}

您可以嘗試以下解決方案：

* 確保自定義 `headlibs.jsp` (如果 `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`)包括：

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 確保自定義 `head.html` (如果 `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **不** 選擇性地包括特定的整合頭，如下例：

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

的 `servicelibs.jsp` 添加所需的分析JavaScript對象並載入與網站關聯的雲服務庫。 對於目標服務，通過 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

載入的庫集取決於目標客戶端庫的類型( `mbox.js` 或 `at.js`)。

使用DTM交付時 `mbox.js` 或 `at.js` 確保在呈現內容之前載入了庫。 使用非同步載入這些庫的Tag Management系統可能會導致執行目標特定JavaScript代碼時出現問題。

有關其他資訊，請閱讀 [為目標內容開發](/help/sites-developing/target.md#understanding-the-target-component) 的子菜單。

### 瀏覽器控制台中顯示錯誤「AppMeasurement初始化中缺少報表套件ID」 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

當使用DTM在網站上實現Adobe Analytics並使用自定義代碼時，可能會出現此問題。 原因是 `s = new AppMeasurement()` 實例化 `s` 的雙曲餘切值。

#### 解決方案 {#solution-4}

使用 `s_gi` 而不是 `new AppMeasurement` 實例化方法。 例如：

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 預設優惠會隨機顯示，而不是正確的優惠 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

此問題可能有多種原因：

* 正在載入目標客戶端庫( `mbox.js` 或 `at.js`)非同步使用第三方Tag Management系統可能會隨機打破目標。 目標庫應同步載入到頁面頭中。 當從中傳送庫時，始終如AEM此。

* 正在載入兩個目標客戶端庫( `at.js`)，例如，使用DTM的和使用中的Target配置的AEM。 這可能導致 `adobe.target` 定義 `at.js` 版本不同。

#### 解決方案 {#solution-5}

您可以嘗試以下解決方案：

* 確保在中同步執行載入DTM類庫的客戶代碼（後者又載入目標庫） [頁首](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages)。
* 如果站點配置為使用DTM來傳遞目標庫，請確保 **由DTM提供的客戶端庫** 選項 [目標配置](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) 地址欄。

### 使用AT.js 1.3+時，始終顯示預設優惠，而不是正確的優惠 {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

現成6AEM.2和6.3與AT.js版本1.3.0+不相容。 通過AT.js 1.3.0版介紹其API的參數驗證， `adobe.target.applyOffer()` 需要「mbox」參數，但 `atjs-itegration.js` 代碼。

#### 解決方案 {#solution-6}

要解決此問題，請編輯 `atjs-itegration.js` 並添加 `"mbox": mboxName` 的參數對象中的欄位 `adobe.target.applyOffer()` 如下：

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

### 「目標和設定」頁不顯示「報告源」部分 {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

此問題很可能 [A4TAnalytics Cloud配置](/help/sites-administering/target-configuring.md) 設定問題。

#### 解決方案 {#solution-7}

您需要通過向以下對象發出驗證請求來驗證A4T是否已正確啟AEM用：

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

如果響應包含行 `a4tEnabled:false`，連接 [Adobe客戶關懷](https://helpx.adobe.com/contact.html) 正確設定帳戶。

### 有用的目標API {#helpful-target-apis}

下面介紹了兩個目標API，在對目標問題進行故障排除時，這些API可能會很有用：

* 檢索給定客戶端代碼的目標終結點

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 檢索客戶端的配置檔案

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
