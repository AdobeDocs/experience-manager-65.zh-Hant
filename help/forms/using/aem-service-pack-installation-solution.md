---
title: 安裝最新6.5.15.0 Service Pack後，CRX/套件組合和開始頁面服務即出現無法使用錯誤
description: 安裝最新6.5.15.0 Service Pack後，CRX/套件組合和開始頁面服務即出現無法使用錯誤
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# 安裝AEM (6.5.15.0) Service Pack後發生服務無法使用錯誤 {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

安裝後 [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，錯誤發生為：
* 錯誤 [felixdispatchqueue] org.apache.sling.scripting.console FrameworkEvent錯誤(org.osgi.framework.BundleException：無法解析org.apache.sling.scripting.console

安裝AEM 6.5.15.0 Service Pack後，CRX/Bundle和起始頁面會顯示服務無法使用錯誤。

## 套用至 {#applies-to}

此解決方案適用於：
* 所有JEE伺服器（在JBoss EAP 7.4.0上執行的除外）上的AEM Forms

## 解決方案 {#solution}

>[!NOTE]
>
>疑難排解步驟適用於除JBoss EAP 7.4以外的所有應用程式伺服器。

安裝之後 [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，如果CRX/套件組合和起始頁面顯示服務無法使用錯誤，請執行以下步驟：

1. 停止應用程式伺服器。
1. 導覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找到 `bundle.info` 檔案。
1. 開啟 `bundle.info` 在ant文字編輯器中的檔案，並搜尋 `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >萬一 `bundle.info` 在 `bundle52` 不包含 `org.apache.felix.http.bridge` 束，檢查 `org.apache.felix.http.bridge`. 然後導覽至 [aem-forms根]\crx-repository\launchpad\felix\bundle[x] 並在此位置執行後續步驟。

1. 導覽至URL： `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 搜尋 `bundle.jar` 並重新命名 `bundle.jar` 至 `bundle.jar.bak`.
1. 複製 `Bundle for AEM 6.5 Forms on JEE Service Pack 15` 在此位置，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. 啟動應用程式伺服器，等待記錄檔穩定並檢查套件組合狀態。
1. 當所有套件組合都處於作用中狀態時，請安裝 [JEE Service Pack 15上AEM 6.5 Forms的片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 從 `system/console/bundles` 並等待應用程式伺服器穩定下來。
1. 停止應用程式伺服器。
1. 瀏覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 並刪除 `bundle.jar`.
1. 重新命名 `bundle.jar.bak` 至 `bundle.jar`.
1. 啟動應用程式伺服器。
