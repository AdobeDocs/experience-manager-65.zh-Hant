---
title: AEM FormsJEE 6.5.15.0 Service Pack在JBoss® Linux®環境上安裝問題
description: AEM FormsJEE 6.5.15.0 Service Pack未正確安裝在JBoss® Linux®環境中，任何修補程式更改都不會應用於應用程式伺服器。 將「RUP_BOM.xml」檔案添加到XML目錄。
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
source-git-commit: b8c9e5cd3192b51954091b677d700c51617c9460
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---

# AEM Forms6.5.15.0 JEE Service Pack在JBoss®環境上安裝問題 {#aem-forms-installation-issue-environment}

## 問題 {#issue}

AEM FormsJEE 6.5.15.0 Service Pack未正確安裝在JBoss® Linux®環境中。 在 `PatchInstallerProcessing[1-9*].log` 記錄條目， `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`，則記錄。 此條目表示安裝AEM FormsJEE 6.5.15.0 Service Pack失敗。

## 套用至 {#applies-to}

此解決方案適用於：
* JBoss® Linux®環境

>[!NOTE]
>
> 在執行以下步驟之前，請至少將AEM FormsJEE 6.5.15.0 Service Pack安裝在應用程式伺服器上 [將RUP_BOM.xml檔案添加到XML目錄](#solution-solution)。

## 解決方案 {#solution}

要解決安裝問題，請添加「AEM FormsJEE 6.5.15.0」服務包 `RUP_BOM.xml` 檔案到XML目錄：
1. 導航到解壓修補程式的資料夾 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`。
1. 導航到 `/CDROM_Installers/Linux/Disk1/InstData` 定位 `Resource1.zip` 的子菜單。
1. 複製 `Resource1.zip` 檔案位於提取的資料夾之外的某個不同位置，然後解壓縮 `Resource1.zip` 的子菜單。
1. 導航到 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` 複製 `RUP_BOM.xml` 的子菜單。
1. 將RUP_BOM.xml檔案貼上到 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`。
1. 重新安裝 [AEM FormsJEE 6.5.15.0服務包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
