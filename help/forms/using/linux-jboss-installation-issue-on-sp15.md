---
title: AEM Forms JEE 6.5.15.0 Service Pack在JBoss® Linux®環境上安裝問題
description: AEM Forms JEE 6.5.15.0 Service Pack未正確安裝在JBoss® Linux®環境中，任何修補程式變更都不會套用至應用程式伺服器。 將「RUP_BOM.xml」檔案添加到XML目錄。
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# AEM Forms 6.5.15.0 JEE Service Pack在JBoss®環境上安裝問題 {#aem-forms-installation-issue-environment}

## 問題 {#issue}

AEM Forms JEE 6.5.15.0 Service Pack未正確安裝在JBoss® Linux®環境中。 在 `PatchInstallerProcessing[1-9*].log` 檔案記錄項目， `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`，則會記錄。 此項目表示安裝AEM Forms JEE 6.5.15.0 Service Pack失敗。

## 套用至 {#applies-to}

此解決方案適用於：
* JBoss® Linux®環境

>[!NOTE]
>
> 在執行以下步驟之前，請至少在應用程式伺服器上安裝一次AEM Forms JEE 6.5.15.0 Service Pack: [將RUP_BOM.xml檔案添加到XML目錄](#solution-solution).

## 解決方案 {#solution}

若要修正安裝問題AEM Forms JEE 6.5.15.0 Service Pack，請新增 `RUP_BOM.xml` 檔案到XML目錄：
1. 導覽至您擷取修補程式的資料夾 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. 導覽至 `/CDROM_Installers/Linux/Disk1/InstData` 位置，並找出 `Resource1.zip` 檔案。
1. 複製 `Resource1.zip` 檔案在擷取的資料夾外部的不同位置，然後解壓縮 `Resource1.zip` 檔案。
1. 導覽至 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` 並複製 `RUP_BOM.xml` 檔案。
1. 貼上RUP_BOM.xml檔案，位置為 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. 重新安裝 [AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).