---
title: 導入和管理應用程式
seo-title: Import and manage applications
description: 瞭解如何導入和管理應用程式。
seo-description: Learn how to import and manage applications.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 導入和管理應用程式{#import-and-manage-applications}

在形AEM式中， *應用* 是用於儲存實施表單解決方案所需的AEM資產的容器。 資產示例包括表單設計、表單片段、影像、進程、DDX檔案、表單指南、HTML頁和SWF檔案。 在項目開發階段，Workbench用戶可以直接從Workbench中的「應用程式」視圖部署應用程式。 部署後，這些應用程式將出現在管理控制台的「應用程式管理」頁的「應用程式」頁籤中。

當應用程式完成並準備部署到生產伺服器時，Workbench用戶會將應用程式打包到 *AEMforms應用程式檔案* (.lca)。 然後，管理員使用「應用程式管理」頁上的「應用程式」頁籤，使用管理控制台導入和部署應用程式檔案。

您還可以使用「應用程式管理」頁上的存檔標籤來導入使用workbench 8.x建立的LCA。

>[!NOTE]
>
>已知的問題是，未來版本的LCA檔案不一定向後相容。 雖然可以從將來的表單版本AEM（例如預覽版本）中查看和導入LCA檔案，但不支援這樣做，並且可能導致異常行為。

使用「應用程式」標籤可導入和管理在Workbench中建立的應用程式。 應用程式管理員還可以導出應用程式的運行時配置。 導出運行時配置消除了在啟動已部署的應用程式之前在生產環境中手動重新配置設定的需要。 運行時配置檔案包含：

* 服務配置設定
* 池配置設定
* 端點配置設定
* 安全配置檔案

## 導入應用程式或存檔 {#import-an-application-or-archive}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 按一下「導入」。
1. 按一下「瀏覽」(Browse)，選擇要導入的.lca檔案，然後按一下「預覽」(Preview)。 「預覽應用程式」頁顯示有關該應用程式的資訊。
1. （可選）要查看應用程式中包含的資產清單，請按一下查看資產。
1. （可選）要將資產部署到運行時，請選擇「導入完成時將資產部署到運行時」。 如果未選擇此選項，則可以稍後部署資產。
1. 按一下「導入」。 應用程式將顯示在「應用程式」頁籤上。
1. 使用管理員憑據登錄CRX儲存庫。
1. 導航到內容/檔案庫/lcapplications

   >[!NOTE]
   >
   >導入的應用程式顯示在lcapplications節點中。

1. 按一下其中一個導入的應用程式。

   右側的「屬性」(Properties)頁籤顯示選定CRX節點的屬性。

   的 **同步狀態** 屬性指示Forms伺服器和CRX儲存庫AEM之間資料同步的狀態。 一旦導入進程開始，此狀態即設定為0（零）。 此狀態表示資料當前未同步。 當資料同步時，狀態設定為1。

## 部署應用程式 {#deploy-an-application}

您可以部署已導入或從Workbench導入的Workbench用戶的應用程式。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 選中要部署的應用程式旁邊的複選框，然後按一下部署。
1. 在出現的確認對話框中按一下確定。

## 取消部署應用程式 {#undeploy-an-application}

可以從運行時取消部署應用程式。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 選中要取消部署的應用程式旁邊的複選框，然後按一下取消部署。
1. 在出現的確認對話框中按一下確定。

## 從伺服器中刪除應用程式 {#remove-an-application-from-the-server}

在從伺服器中刪除應用程式之前取消部署該應用程式。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 選中要刪除的應用程式旁邊的複選框，然後按一下刪除。
1. 在出現的確認對話框中按一下確定。

## 導入應用程式的運行時配置 {#import-an-application-s-runtime-configuration}

如果應用程式管理員導出了應用程式的運行時配置，則可以將其導入到已部署的應用程式中。 您可以使用管理控制台或通過指令碼式LCA部署導入它。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「導入運行時配置」。
1. 按一下瀏覽並選擇包含運行時配置的XML檔案。
1. 按一下「導入」。

## 導出應用程式的運行時配置 {#export-an-application-s-runtime-configuration}

您可以導出已部署應用程式的運行時配置資訊。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「導出運行時配置」(Export Runtime Config)並保存所生成的配置檔案(XML)。

## 表單應用程式AEM的指令碼部署 {#scripted-deployment-of-aem-forms-applications}

您還可以使用指令碼部署工具來部署應用程式檔案，包括指定以下設定的settings.xml檔案：

* 服務配置設定
* 池配置設定
* 端點配置設定
* 安全配置檔案

指令碼式部署消除了在啟動部署的應用程式之前在生產環境中手動重新配置設定的需要。

1. 從命令提示符導航到 *[根]*/sdk/misc/Foundation/ArchiveManagement。
1. 查看ReadMe.txt檔案以瞭解更詳細的說明。
1. 手動修改scriptedDeploy.bat和sample-files/sample.xml檔案，如readme.txt檔案中所述。
1. 運行scriptedDeploy.bat檔案。 此操作將使用AEM覆蓋設定部署表單存檔檔案。
