---
title: 安裝最新6.5.15.0 Service Pack後，CRX/套件組合和開始頁面服務發生無法使用的錯誤
description: 安裝最新6.5.15.0 Service Pack後，CRX/套件組合和開始頁面服務發生無法使用的錯誤
SEO Description: Trouble shooting steps to resolve the errors after installing latest 6.5.15.0 service pack
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: 8c4fb903-572c-5473-ad45-8ebb0d5d8134
    internal-label: AEM Forms on OSGi
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%
---
# 安裝AEM (6.5.15.0) Service Pack後發生服務無法使用錯誤 {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

安裝[AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)後，錯誤發生如下：
* 錯誤[FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent錯誤(org.osgi.framework.BundleException：無法解析org.apache.sling.scripting.console

安裝AEM 6.5.15.0 Service Pack後，CRX/套件組合和起始頁面顯示服務無法使用錯誤。

## 套用至 {#applies-to}

此解決方案適用於：
* 所有JEE伺服器（在JBoss EAP 7.4.0上執行的除外）上的AEM Forms

## 解決方案 {#solution}

>[!NOTE]
>
>疑難排解步驟適用於除JBoss EAP 7.4以外的所有應用程式伺服器。

安裝[AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)後，如果CRX/套件組合和起始頁面顯示服務無法使用錯誤，請執行下列步驟：

1. 停止應用程式伺服器。
1. 導覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找到`bundle.info`檔案。
1. 在Ant文字編輯器中開啟`bundle.info`檔案，並以`org.apache.felix.http.bridge`搜尋套件組合名稱。

   >[!NOTE]
   >
   >如果`bundle52`底下的`bundle.info`不包含`org.apache.felix.http.bridge`組合，請檢查`org.apache.felix.http.bridge`旁方括弧中的組合編號。 然後導覽至[aem-forms根目錄]\crx-repository\launchpad\felix\bundle[x]，並在此位置執行後續步驟。

1. 導覽至URL： `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`。
1. 搜尋`bundle.jar`並將`bundle.jar`重新命名為`bundle.jar.bak`。
1. 從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar)複製此位置的`Bundle for AEM 6.5 Forms on JEE Service Pack 15`。
1. 啟動應用程式伺服器，等待記錄檔穩定並檢查套件組合狀態。
1. 當所有套件組合都處於作用中狀態時，請從`system/console/bundles`在JEE Service Pack 15[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)上安裝AEM 6.5 Forms的片段，並等待應用程式伺服器穩定下來。
1. 停止應用程式伺服器。
1. 導覽至`[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1`並刪除`bundle.jar`。
1. 將`bundle.jar.bak`重新命名為`bundle.jar`。
1. 啟動應用程式伺服器。
