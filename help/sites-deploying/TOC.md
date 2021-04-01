---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: AEM 6.5 Deploying 指南
breadcrumb-title: Deploying 指南
user-guide-description: 進一步了解 Adobe Experience Manager 6.5 的安裝、部署和架構，包括我們的 Adobe Managed Services 雲端部署。
feature-set: Experience Manager Sites
feature: 部署
role: 架構師
translation-type: tm+mt
source-git-commit: d7b0803385aaa451a1ec7ec280ff51c3e96e36e7
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 10%

---


# AEM 6.5部署使用手冊{#deploying}

+ [部署使用指南](home.md)
+ 平台AEM{#introduction}簡介
   + [平台簡AEM介](platform.md)
   + [技術需求](technical-requirements.md)
   + [6.AEM5中的儲存元素](storage-elements-in-aem-6.md)
   + [使AEM用MongoDB](aem-with-mongodb.md)
+ 部AEM署{#deploying}
   + [部署和維護](deploy.md)
   + [建議的部署](recommended-deploys.md)
   + [應用程式伺服器安裝](application-server-install.md)
   + [自訂獨立安裝](custom-standalone-install.md)
   + [命令行啟動和停止](command-line-start-and-stop.md)
   + [在6中配置節點儲存和資料存AEM儲](data-store-config.md)
   + [修訂清除](revision-cleanup.md)
   + [Oak查詢和索引](queries-and-indexing.md)
   + [如何使用AEMTarMK冷備用](tarmk-cold-standby.md)
   + [6.5中的AEMRDBMS支援](rdbms-support-in-aem.md)
   + [透過Oak-run Jar建立索引](indexing-via-the-oak-run-jar.md)
   + [Oak-run.jar索引使用案例](oak-run-indexing-usecases.md)
   + [疑難排解Oak索引](troubleshooting-oak-indexes.md)
   + [選擇匯總使用統計資訊收集](opt-in-aggregated-usage-statistics.md)
   + [疑難排解](troubleshooting.md)
+ 配AEM置{#configuring}
   + [基本配置概念](configuring.md)
   + [記錄](configure-logging.md)
   + [配置OSGi](configuring-osgi.md)
   + [OSGi配置設定](osgi-configuration-settings.md)
   + [執行模式](configure-runmodes.md)
   + [Web 主控台](web-console.md)
   + [複寫](replication.md)
   + [使用互相SSL進行複製](mssl-replication.md)
   + [複製故障排除](troubleshoot-rep.md)
   + [靜態對象的過期](expiration-static-objects.md)
   + [版本清除](version-purging.md)
   + [監控和維護您的實AEM例](monitoring-and-maintaining.md)
   + [卸載作業](offloading.md)
   + [單一登入](single-sign-on.md)
   + [資源映射](resource-mapping.md)
   + [透過SSL啟用HTTP](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [一致性和遍歷檢查](consistency-check.md)
   + [效能准則](performance-guidelines.md)
   + [效能最佳化](configuring-performance.md)
   + [資產效能指南](assets-performance-sizing.md)
   + [設定操作說明文章](ht-deploy.md)
   + [配置Web控制台](configuring-web-console.md)
+ 升級AEM至6.5 {#upgrading}
   + [升級AEM至6.5](upgrade.md)
   + [規劃升級](upgrade-planning.md)
   + [用模式檢測器評估升級複雜度](pattern-detector.md)
   + [6.5中的AEM向後相容性](backward-compatibility.md)
   + [升級程式](upgrade-procedure.md)
   + [執行就地升級](in-place-upgrade.md)
   + [使用離線重新索引以減少升級期間的停機時間](upgrade-offline-reindexing.md)
   + [延遲內容移轉](lazy-content-migration.md)
   + [使用CRX2Oak移轉工具](using-crx2oak.md)
   + [升級前維護任務](pre-upgrade-maintenance-tasks.md)
   + [升級後檢查和疑難排解](post-upgrade-checks-and-troubleshooting.md)
   + [升級自訂搜尋Forms](upgrading-custom-search-forms.md)
   + [可持續升級](sustainable-upgrades.md)
   + [升級程式碼和自訂](upgrading-code-and-customizations.md)
   + [應用程式伺服器安裝的升級步驟](app-server-upgrade.md)
   + [升級後卸載的過時捆綁包清單](obsolete-bundles.md)
+ 資料庫重組{#restructuring}
   + [6.5中的AEM儲存庫重組](repository-restructuring.md)
   + [6.5中的常AEM見儲存庫重組](all-repository-restructuring-in-aem-6-5.md)
   + [6.5版中的站點AEM儲存庫重組](sites-repository-restructuring-in-aem-6-5.md)
   + [6.5中的資產AEM儲存庫重組](assets-repository-restructuring-in-aem-6-5.md)
   + [Dynamic Media6.AEM5版資料庫重組](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Forms6.AEM5版資料庫重組](forms-repository-restructuring-in-aem-6-5.md)
   + [6.5版中的電子商AEM務儲存庫重組](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [6.5中的AEM Communities資源庫重組](communities-repository-restructuring-in-aem-6-5.md)
+ 電子商務 {#ecommerce}
   + [電子商務概觀](ecommerce.md)
   + [SAPCommerce Cloud](sap-commerce-cloud.md)
   + [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ 最佳作法 {#practices}
   + [部署最佳實務](best-practices.md)
   + [效能樹](performance-tree.md)
   + [效能測試的最佳實務](best-practices-for-performance-testing.md)
   + [查詢和索引的最佳做法](best-practices-for-queries-and-indexing.md)
   + [面向客戶的用戶介面Recommendations](ui-recommendations.md)
   + [效能與可擴充性](performance.md)
