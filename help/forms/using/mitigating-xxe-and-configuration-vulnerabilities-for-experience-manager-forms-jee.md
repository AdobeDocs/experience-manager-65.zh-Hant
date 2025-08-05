---
title: 緩解JEE上AEM Forms的XXE、Struts開發模式設定和遠端程式碼執行弱點
description: 緩解JEE上AEM Forms的XXE、設定和遠端程式碼執行弱點
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: cacad43c2c32a1a14de0ea5f845818018ba8b2ec
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 5%

---

# 緩解JEE上AEM Forms的RCE (CVE-2025-49533)、Struts開發模式設定(CVE-2025-54253)、XXE (CVE-2025-54254)和漏洞 {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## 快速參考

| **影響層級** | **受影響的版本** | **建議的動作** |
|---|---|---|
| **關鍵** | JEE Service Pack 23 (6.5.23.0)上的AEM 6.5 Forms | [安裝最新的Hotfix](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **關鍵** | JEE Service Pack 18至22 (6.5.18.0 - 6.5.22.0)上的AEM 6.5 Forms | [手動安裝修正](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **關鍵** | JEE Service Pack 17 (6.5.17.0)或更舊版本上的AEM 6.5 Forms | 升級至支援的Service Pack版本，然後為您的新版本套用建議的緩解步驟 |
| **不受影響** | OSGi、Workbench、Cloud Service上的AEM Forms | 不需要採取任何動作 |

**已處理的漏洞：**

- 遠端程式碼執行(CVE-2025-49533)
- 設定安全問題(CVE-2025-54253)
- XML外部實體(XXE)處理(CVE-2025-54254)

## 概觀

### 受影響的內容

| 漏洞 | 影響 | 受影響的元件 |
|---|---|---|
| **CVE-2025-49533**：遠端程式碼執行 | GetDocumentServlet中未驗證的程式碼執行 | JEE Service Pack 23 (6.5.23.0)及舊版上的AEM 6.5 Forms |
| **CVE-2025-54253**：設定問題 | 在管理UI中啟用Struts開發模式 | JEE Service Pack 23 (6.5.23.0)及舊版上的AEM 6.5 Forms |
| **CVE-2025-54254**： XXE處理中 | Document Security模組允許未經授權的檔案存取 | JEE Service Pack 23 (6.5.23.0)及舊版上的AEM 6.5 Forms |


### 未受影響的專案

- Experience Manager Forms Workbench （所有版本）
- OSGi上的Experience Manager Forms （所有版本）
- Experience Manager Forms as a Cloud Service

## 解析度選項


### 開始之前

在進行任何變更之前，請備份您要修改或更新的EAR檔案或DSC檔案：

- 在您的部署目錄中找出原始的EAR或DSC檔案。
- 將檔案複製到部署目錄外部的安全備份位置。
- 繼續進行任何更新之前，請確定備份完整且可存取。

此預防措施可讓您還原原始狀態，以防您在更新過程中遇到任何問題。

### 選項1： （適用於版本6.5.23.0的使用者）安裝最新的Hotfix

1. [下載6.5.23.0](/help/release-notes/aem-forms-hotfix.md)的Hotfix。
1. 遵循標準[Hotfix/修補程式安裝指示](/help/release-notes/jee-patch-installer-65.md)
1. 如果您在IBM WebSphere或Oracle WebLogic上使用Document Security (前身為Rights Management)，請在啟動AEM Forms伺服器前設定下列Java系統屬性（JVM引數）：

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. 重新啟動應用程式伺服器

### 選項2： （適用於6.5.18.0 - 6.5.22.0的使用者）手動Hotfix安裝

+++手動安裝6.5.18.0 - 6.5.22.0的Hotfix

**步驟1：下載並解壓縮Hotfix套件**

- 從Adobe軟體發佈入口網站下載[ - 6.5.22.6.5.18.0的](/help/release-notes/aem-forms-hotfix.md)Hotfix
- 在本機擷取

**步驟2：瀏覽至正確的版本資料夾**

- 根據環境中安裝的Service Pack版本，前往相符的資料夾。

  例如，Service Pack 20的資料夾為：

  ```
  <extracted-hotfix>/SP20/
  ```

**步驟3：找到部署目錄**

- 在JEE伺服器上的AEM Forms上，前往：

  ```
  [AEM installation directory]/deploy
  ```

  範例：`adobe/adobe-experience-manager-forms/deploy`



**步驟4：更新並取代EAR檔案**

>[!BEGINTABS]

>[!TAB JBoss]

1. 開啟`adobe-core-jboss.ear`並將`adminui.war`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

1. 在`adobe-core-jboss.ear`內，移至`lib/`資料夾並將`adobe-uisupport.jar`取代為：

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 儲存EAR。 確保變更已正確儲存。


1. 將`adobe-edcserver-jboss.ear`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

1. 將`adobe-forms-jboss.ear`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. 開啟`adobe-core-weblogic.ear`並將`adminui.war`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

1. 在`adobe-core-weblogic.ear`內，將`adobe-uisupport.jar`取代為：

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 儲存EAR。 確保變更已正確儲存。


1. 將`adobe-edcserver-weblogic.ear`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

1. 將`adobe-forms-weblogic.ear`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. 開啟`adobe-core-websphere.ear`並將`adminui.war`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

1. 在`adobe-core-websphere.ear`內，將`adobe-uisupport.jar`取代為：

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 儲存EAR。 確保變更已正確儲存。


1. 將`adobe-edcserver-websphere.ear`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

1. 將`adobe-forms-websphere.ear`取代為

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   例如 `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**步驟5：使用`adobe-rightsmanagement-<appserver>-dsc.jar`更新**&#x200B;檔案

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

例如 `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**步驟6： WebSphere和WebLogic上Document Security的其他設定**：

如果您使用Document Security (前身為Rights Management)，請在啟動AEM Forms伺服器前設定下列Java系統屬性（JVM引數）：

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**步驟7：重新執行組態管理員**

- 啟動Configuration Manager以重新部署更新的EAR並套用Hotfix

+++

### 選項3： （適用於6.5.17.0和更早版本的使用者）升級路徑

1. [升級至支援的Service Pack版本](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. 根據您的新版本，遵循以上選項1或選項2

## 參照

- [CWE-611： XML外部實體參考的限制不正確](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16：組態](https://cwe.mitre.org/data/definitions/16.html)
- [OWASP XXE預防速查表](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Adobe Experience Manager Forms安全性最佳實務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=zh-Hant)
