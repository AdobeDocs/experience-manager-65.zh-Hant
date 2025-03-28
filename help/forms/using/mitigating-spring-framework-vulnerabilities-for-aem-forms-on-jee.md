---
title: 緩解JEE上AEM Forms的Spring Framework漏洞
description: 緩解JEE上AEM Forms的Spring Framework漏洞
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# 緩解JEE上AEM Forms的Spring Framework漏洞

本檔案針對影響JEE上AEM Forms的兩個重大Spring Framework漏洞，提供相關指引：

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**：功能性Web架構中的路徑周遊漏洞
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**： Spring Framework DataBinder區分大小寫比對例外狀況

## 受影響的版本

- JEE上的Adobe Experience Manager 6.5 Forms
- AEM 6.5 Forms GA版本至6.5.22.0

## 解決方法

### 特定版本的解決方案

| AEM Forms版本 | 必要的動作 |
|-------------------|-----------------|
| 6.5.22.0 | 1. [下載您環境的Hotfix](/help/release-notes/aem-forms-hotfix.md)。 </br> 2. 若要安裝此修正程式，請依照指示[在JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)上的AEM表單上安裝Service Pack。 |
| 6.5.17.0 - 6.5.21.0 | [套用手動緩解步驟](#manual-mitigation-steps)。 |
| 6.5 - 6.5.16.0 | 1. [安裝最新的Service Pack](/help/release-notes/release-notes.md)<br>2。 [根據您更新的版本，實作適當的解決方案](#version-specific-solutions)。 |

> **注意**： AEM Forms僅正式支援最近的6個Service Pack。 舊版的使用者應先升級至最新的Service Pack，然後安裝必要的Hotfix。

## 部署考量

### 針對叢集環境

使用叢集部署時：

- 在叢集中的&#x200B;**所有節點**&#x200B;上套用JAR檔案取代(步驟#4)
- 在所有伺服器上使用相同的JAR版本，以維持一致性
- 在初始化任何服務重新啟動之前，完成所有節點的更新
- 實施協調的重新啟動策略，將系統停機時間降至最低

### 適用於單一節點環境

使用獨立部署時：

- 由於沒有要管理的定位器伺服器，因此請遵循簡化的流程
- 省略任何與定位器伺服器設定或啟動相關的步驟
- 依照指示完成所有其他步驟，尤其是JAR取代和資訊清單更新
- 執行所有變更後，請重新啟動應用程式伺服器

## 手動緩解步驟

1. 停止應用程式伺服器。
1. 停止和定位器伺服器。
1. 從核心EAR移除Spring JAR：
   1. 導覽至 `[Adobe_Experience_Manager_Forms installation directory]/deploy`。
   1. 使用封存管理員工具開啟`adobe-core-<appserver>.ear`檔案。 其中`<appserver>`可以是JBoss、WebLogic或WebSphere，視您的環境而定：
   - **對於JBoss：**&#x200B;瀏覽至`ear/lib`資料夾並刪除下列JAR檔案：
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **對於WebLogic或WebSphere：**從EAR的根目錄刪除下列JAR檔案：
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **針對所有應用程式伺服器：**&#x200B;在`adobe-core-<appserver>.ear`的根層級，開啟`adobe-dscf.jar`檔案並編輯`META-INF/MANIFEST.MF`檔案以移除對下列JAR檔案的任何參考：
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. 從Geode分佈取代JAR檔案：
   1. 瀏覽至`<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. 以更新的版本取代現有的JAR檔案：
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   若要取得較新的JAR檔案，請從[Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip)下載spring-6.1.14-jars.zip檔案，並解壓縮ZIP檔案以存取更新的Spring Framework JAR檔案。

   1. 更新下列JAR檔案中的MANIFEST.MF檔案：
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   對於每個JAR：
   - 使用封存管理員工具開啟JAR
   - 尋找並解壓縮`META-INF/MANIFEST.MF`檔案
   - 在文字編輯器中編輯MANIFEST.MF檔案
   - 尋找「Class-Path」區段並更新所有Spring框架參考：
      - `spring-core-<version>.jar`至`spring-core-6.1.14.jar`
      - `spring-web-<version>.jar`至`spring-web-6.1.14.jar`
      - `spring-context-<version>.jar`至`spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar`至`spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar`至`spring-jcl-6.1.14.jar`
   - 儲存修改過的MANIFEST.MF檔案
   - 將JAR中的原始MANIFEST.MF取代為您更新的版本
   - 儲存JAR檔案

   1. 需留意的常見問題：
      - 確保資訊清單中沒有重複的專案
      - 維護正確的行尾
      - 確認所有參照的JAR都存在於指定的位置

   1. 驗證步驟：
      - 檢查資訊清單是否已正確更新
      - 確認所有彈簧相依性均已正確參照
      - 確保沒有舊的版本參考
      - 測試應用程式以確認沒有類別載入問題

1. 執行Configuration Manager。

1. 重新啟動伺服器：
   - 使用JDK 17啟動定位器伺服器
   - 使用先前使用的相同JDK版本（JDK 8或JDK 11）啟動應用程式伺服器。
