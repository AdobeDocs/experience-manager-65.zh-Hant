---
title: 安裝最新的6.5.15.0 Service Pack後， CRX/bundle和Start page Service不可用錯誤
description: 安裝最新的6.5.15.0 Service Pack後， CRX/bundle和Start page Service不可用錯誤
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
source-git-commit: e961f0c7107b4eacb0d5e50565cb64f5fa30e265
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---

# 安裝(6.5.15.0)Service Pack後AEM出現服務不可用錯誤 {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

安裝後 [AEM 6.5.15.0服務包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，錯誤發生為：
* 錯誤 [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR(org.osgi.framework.BundleException:無法解析org.apache.sling.scripting.console

安裝AEM6.5.15.0 servicePack後， CRX/bundle和起始頁顯示服務不可用錯誤。

## 套用至 {#applies-to}

此解決方案適用於：
* AEM Forms在所有JEE伺服器上，但JBoss EAP 7.4.0上運行的伺服器除外

## 解決方案 {#solution}

>[!NOTE]
>
>排除故障步驟適用於除JBoss EAP 7.4之外的所有應用程式伺服器。

安裝後 [AEM 6.5.15.0服務包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，如果CRX/bundle和起始頁顯示服務不可用錯誤，請執行以下步驟：

1. 停止應用程式伺服器。
1. 導覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 查找 `bundle.info` 的子菜單。
1. 開啟 `bundle.info` 在ant文本編輯器中查找檔案，並將包名稱搜索為 `org.apache.felix.http.bridge`。

   >[!NOTE]
   >
   >以防 `bundle.info` 在 `bundle52` 不包含 `org.apache.felix.http.bridge` 束，檢查位於 `org.apache.felix.http.bridge`。 然後導航到 [根]\crx-repository\launchpad\felix\bundle[x] 並在此位置執行後續步驟。

1. 導航到網址: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 搜索 `bundle.jar` 並更名 `bundle.jar` 至 `bundle.jar.bak`。
1. 複製 `Bundle for AEM 6.5 Forms on JEE Service Pack 15` 在這個地方 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar)。
1. 啟動應用程式伺服器，等待日誌穩定並檢查捆綁狀態。
1. 一旦所有捆綁包都處於活動狀態，請安裝 [JEE Service Pack AEM 15上6.5Forms的片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 從 `system/console/bundles` 等待應用伺服器穩定。
1. 停止應用程式伺服器。
1. 導航到 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 刪除 `bundle.jar`。
1. 更名 `bundle.jar.bak` 到 `bundle.jar`。
1. 啟動應用程式伺服器。
