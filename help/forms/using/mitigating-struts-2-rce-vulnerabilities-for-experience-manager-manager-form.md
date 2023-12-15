---
title: 緩解Experience Manager Forms的Struts 2 RCE漏洞
description: 緩解Experience Manager Forms的Struts 2 RCE漏洞
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
source-git-commit: 61a2fe04805478f7eaf0484edd6a1874e8e96404
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---


# 緩解Experience Manager Forms的Struts 2 RCE漏洞 {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## 問題

已報告Struts 2 RCE的重大安全性漏洞，這是一個用於開發Java EE Web應用程式的常用且開放原始碼的Web應用程式架構。 已分析下列漏洞：

| 漏洞 | 受影響的專案？ | 哪些專案未受影響？ |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | 在JEE上Experience Manager6.5 Forms （從6.5 GA到6.5.19.0的所有版本） | <ul><li> Experience Manager Forms Workbench （所有版本）</li> <li> OSGi上的Experience Manager Forms （所有版本） </li> <li> Experience Manager Formsas a Cloud Service </li> <ul> |

## 解決方法

下表列出所有受影響版本的解決方案：

| 發行 | 目前版本 | 使用者動作 |
|---|---|---|
| 在JEE上Experience Manager6.5 Forms | 6.5.19.0 | [安裝最新Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en) |
| 在JEE上Experience Manager6.5 Forms | 6.5.13.0 - 6.5.18.0 | 使用下列其中一種方法： <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en"> 安裝最新Service Pack </a> </li> <li> <a href ="#use-manual-mitigation-steps"> 使用手動緩解步驟 </a> |
| 在JEE上Experience Manager6.5 Forms | 6.5 - 6.5.12.0 | [安裝最新Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en)  </br> </br> **注意：** AEM Forms目前支援6.5.13.0版到6.5.19.0版。如果您使用舊版，建議升級至6.5.13.0或更新版本。 如需安裝AEM 6.5.13.0或更新版本的指示，請參閱發行說明。 |

### 使用手動緩解步驟 {#use-manual-mitigation-steps}

您可以使用手動緩解步驟來解決執行Service Pack 13的AEM 6.5表單伺服器到執行Service Pack 18 (6.5.13.0 - 6.5.18.0)的AEM 6.5表單伺服器上的問題：

1. 關閉所有伺服器執行個體和定位器。
1. 下載 [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar).
1. 從下載AEM Forms on JEE手動修補工具 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. 解壓縮手動修補工具封存。 它會擷取下列檔案：
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh
1. 開啟終端機視窗，並導覽至包含解壓縮檔案的資料夾。
1. 使用手動修補工具來搜尋、列出及取代所有struts2 jar檔案。 搜尋和取代struts2-core-2.5.30 jar檔案和struts2-core.jar：


>[!BEGINTABS]

>[!TAB Windows]

1. 執行以下命令以列出所有struts2 jar檔案。 在執行命令之前，請將上述命令中的路徑取代為AEM Form伺服器的路徑：

   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
   ```

1. 以列出的順序執行下列命令，以遞回就地取代。 執行命令之前。 將以上命令中的路徑取代為AEM Form伺服器的路徑，並且 `struts2-core-2.5.33.jar` 檔案。


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace C:\temp\struts2-core-2.5.33.jar
   
   
   patch-archive.bat -root=C:\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace C:\Users\labuser\Desktop\struts2-core.jar -action=replace C:\Users\labuser\Desktop\struts2-core.jar
   ```

1. 啟動您的AEM Forms伺服器。


>[!TAB Linux]

1. 執行以下命令以列出所有struts2 jar檔案。 在執行命令之前，請將上述命令中的路徑取代為AEM Form伺服器的路徑：

   ```
   patch-archive.sh -root=\Users\labuser\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
   ```

1. 以列出的順序執行下列命令，以遞回就地取代。 執行命令之前將以上命令中的路徑替換為AEM Form伺服器的路徑和 `struts2-core-2.5.33.jar` 檔案。

   ```
   patch-archive.sh -root=\Users\labuser\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace \temp\struts2-core-2.5.33.jar
   
   
   patch-archive.sh -root=\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace \Users\labuser\Desktop\struts2-core.jar -action=replace \Users\labuser\Desktop\struts2-core.jar
   ```

1. 啟動您的AEM Forms伺服器。

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->