---
title: JBoss® Linux®環境中的AEM Forms JEE 6.5.15.0 Service Pack安裝問題
description: JBoss® Linux®環境未正確安裝AEM Forms JEE 6.5.15.0 Service Pack，應用程式伺服器不會套用任何修補程式變更。 將'RUP_BOM.xml'檔案新增至XML目錄。
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 1%

---

# JBoss®環境中的AEM Forms 6.5.15.0 JEE Service Pack安裝問題 {#aem-forms-installation-issue-environment}

## 問題 {#issue}

AEM Forms JEE 6.5.15.0 Service Pack未正確安裝在JBoss® Linux®環境中。 在 `PatchInstallerProcessing[1-9*].log` 將記錄專案存檔， `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`，即會記錄。 此專案表示AEM Forms JEE 6.5.15.0 Service Pack的安裝不成功。

## 套用至 {#applies-to}

此解決方案適用於：
* JBoss® Linux®環境

>[!NOTE]
>
> 執行以下步驟之前，請確定應用程式伺服器上已安裝AEM Forms JEE 6.5.15.0 Service Pack至少一次： [將RUP_BOM.xml檔案新增至XML目錄](#solution-solution).

## 解決方案 {#solution}

AEM Forms若要修正安裝問題，請新增 `RUP_BOM.xml` 檔案至XML目錄：
1. 導覽至您擷取修補程式的資料夾 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. 瀏覽至 `/CDROM_Installers/Linux/Disk1/InstData` 定位並找到 `Resource1.zip` 檔案。
1. 複製 `Resource1.zip` 解壓縮資料夾外部某個不同位置的檔案並解壓縮 `Resource1.zip` 檔案。
1. 瀏覽至 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` 並複製 `RUP_BOM.xml` 檔案。
1. 將RUP_BOM.xml檔案貼到 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. 重新安裝 [AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
