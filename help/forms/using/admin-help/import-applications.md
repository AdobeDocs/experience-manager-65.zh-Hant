---
title: 導入和管理應用程式
seo-title: Import and manage applications
description: 了解如何匯入和管理應用程式。
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

在AEM表單中， *應用程式* 是儲存實作AEM表單解決方案所需資產的容器。 資產的範例包括表單設計、表單片段、影像、程式、DDX檔案、表單指南、HTML頁面和SWF檔案。 在專案的開發階段期間，Workbench使用者可以直接從Workbench的「應用程式」檢視部署應用程式。 部署後，這些應用程式將顯示在管理控制台中的「應用程式管理」頁的「應用程式」頁簽上。

當應用程式完成並準備好部署至生產伺服器時，Workbench使用者會將應用程式封裝至 *AEM forms應用程式檔案* (.lca)。 然後，管理員使用管理控制台，使用「應用程式管理」頁上的「應用程式」頁簽導入和部署應用程式檔案。

您也可以使用「應用程式管理」頁面上的封存標籤，匯入使用Workbench 8.x建立的LCA。

>[!NOTE]
>
>有一個已知問題，即將來版本的LCA檔案不一定向後相容。 雖然您可以從未來的AEM表單版本（例如預覽版本）檢視和匯入LCA檔案，但不支援，且可能導致異常行為。

使用「應用程式」標籤可匯入和管理在Workbench中建立的應用程式。 應用程式管理員也可以導出應用程式的運行時配置。 導出運行時配置無需在啟動部署的應用程式之前手動重新配置生產環境中的設定。 運行時配置檔案包含：

* 服務配置設定
* 池配置設定
* 端點配置設定
* 安全設定檔

## 匯入應用程式或封存 {#import-an-application-or-archive}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 按一下「匯入」。
1. 按一下「瀏覽」(Browse)，選擇要導入的.lca檔案，然後按一下「預覽」(Preview)。 「預覽應用程式」頁顯示有關應用程式的資訊。
1. （可選）若要查看應用程式中包含的資產清單，請按一下「檢視資產」。
1. （選用）若要將資產部署至執行階段，請選取匯入完成時將資產部署至執行階段。 如果您未選取此選項，稍後可以部署資產。
1. 按一下「匯入」。 應用程式會出現在「應用程式」標籤上。
1. 使用管理員憑證登入CRX存放庫。
1. 導覽至內容/dam/lcapplications

   >[!NOTE]
   >
   >匯入的應用程式會顯示在lcapplications節點中。

1. 按一下其中一個匯入的應用程式。

   右側的「屬性」頁簽顯示所選CRX節點的屬性。

   此 **syncState** 屬性會指出AEM表單伺服器與CRX存放庫之間資料的同步狀態。 匯入程式一開始，此狀態就會設為0（零）。 此狀態表示資料當前未同步。 資料同步時，狀態會設為1。

## 部署應用程式 {#deploy-an-application}

您可以部署已匯入的應用程式，或從Workbench匯入的Workbench使用者。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 選中要部署的應用程式旁的複選框，然後按一下「部署」。
1. 在顯示的確認對話方塊中，按一下確定。

## 取消部署應用程式 {#undeploy-an-application}

您可以從執行階段取消部署應用程式。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 選中要取消部署的應用程式旁邊的複選框，然後按一下取消部署。
1. 在顯示的確認對話方塊中，按一下確定。

## 從伺服器中刪除應用程式 {#remove-an-application-from-the-server}

先取消部署應用程式，然後再從伺服器中刪除它。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 選取您要移除之應用程式旁的核取方塊，然後按一下「移除」 。
1. 在顯示的確認對話方塊中，按一下確定。

## 匯入應用程式的執行階段設定 {#import-an-application-s-runtime-configuration}

如果應用程式管理員導出了應用程式的運行時配置，則可以將其導入已部署的應用程式。 您可以使用管理控制台或通過指令碼式LCA部署導入它。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「導入運行時配置」(Import Runtime Config)。
1. 按一下「瀏覽」，然後選擇包含運行時配置的XML檔案。
1. 按一下「匯入」。

## 導出應用程式的運行時配置 {#export-an-application-s-runtime-configuration}

您可以導出已部署應用程式的運行時配置資訊。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「導出運行時配置」(Export Runtime Config)，並保存生成的配置檔案(XML)。

## AEM表單應用程式的指令碼部署 {#scripted-deployment-of-aem-forms-applications}

您也可以使用指令碼部署工具來部署應用程式檔案，包括指定以下設定的settings.xml檔案：

* 服務配置設定
* 池配置設定
* 端點配置設定
* 安全設定檔

指令碼部署無需在啟動部署的應用程式之前手動重新配置生產環境中的設定。

1. 從命令提示字元導覽至 *[aem-forms根]*/sdk/misc/Foundation/ArchiveManagement。
1. 查看ReadMe.txt檔案，以獲取更詳細的說明。
1. 如readme.txt檔案所述，手動修改scriptedDeploy.bat和sample-files/sample.xml檔案。
1. 運行scriptedDeploy.bat檔案。 此動作會部署AEM表單封存檔案及覆寫設定。
