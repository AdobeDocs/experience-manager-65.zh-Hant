---
title: 安裝最新的6.5.15.0 Service Pack後，CRX/套件組合和啟動頁面服務無法使用的錯誤
description: 安裝最新的6.5.15.0 Service Pack後，CRX/套件組合和啟動頁面服務無法使用的錯誤
source-git-commit: f5bf33e0a2ff73b8884a55bbe77e87ee991aeef9
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 2%

---


# 安裝AEM(6.5.15.0)Service Pack後，服務無法使用錯誤 {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

安裝 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，錯誤發生為：
* 錯誤 [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR(org.osgi.framework.BundleException:無法解析org.apache.sling.scripting.console

安裝AEM 6.5.15.0 Service Pack後，CRX/套件組合和開始頁面會顯示服務無法使用錯誤。

## 解決方案 {#solution}

>[!NOTE]
>
>故障排除步驟適用於除JBoss EAP 7.4之外的所有應用程式伺服器。

安裝後 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，如果CRX/套件組合和開始頁面顯示服務無法使用錯誤，請執行下列步驟：

1. 停止應用程式伺服器。
1. 導覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找出 `bundle.info` 檔案。
1. 開啟 `bundle.info` 在ant文本編輯器中搜索檔案，並將包名搜索為 `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >若 `bundle.info` 在 `bundle52` 不包含 `org.apache.felix.http.bridge` 捆綁，檢查緊鄰的方括弧中的捆綁編號 `org.apache.felix.http.bridge`. 然後導覽至 [aem-forms根]\crx-repository\launchpad\felix\bundle[x] 並在此位置執行後續步驟。

1. 導航到網址: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 搜尋 `bundle.jar` 並重新命名 `bundle.jar` to `bundle.jar.bak`.
1. 複製 `bundle.jar` 從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. 啟動應用程式伺服器，等待日誌穩定並檢查捆綁狀態。
1. 所有套件組合都處於啟動狀態後，請安裝 `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` 來自的servlet片段 `system/console/bundles` 從 [軟體分發。](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 等待應用伺服器穩定。
1. 停止應用程式伺服器。
1. 導覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 和刪除 `bundle.jar`.
1. 重新命名 `bundle.jar.bak` 到 `bundle.jar`.
1. 啟動應用程式伺服器。

## 套用至 {#applies-to}

此解決方案適用於：
* AEM Forms（所有JEE伺服器上），但運行JBoss EAP 7.4.0的伺服器除外
