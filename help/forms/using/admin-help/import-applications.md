---
title: 匯入和管理應用程式
seo-title: 匯入和管理應用程式
description: 瞭解如何匯入及管理應用程式。
seo-description: 瞭解如何匯入及管理應用程式。
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 匯入和管理應用程式{#import-and-manage-applications}

在AEM表單中，應 ** 用程式是儲存實作AEM表單解決方案所需資產的容器。 資產的範例包括表單設計、表單片段、影像、程式、DDX檔案、表單參考線、HTML頁面和SWF檔案。 在專案開發階段，Workbench使用者可直接從Workbench的「應用程式」檢視來部署應用程式。 部署後，這些應用程式會顯示在「應用程式管理」頁面的「應用程式」索引標籤上的管理控制台中。

當應用程式完成並可部署至生產伺服器時，Workbench使用者會將應用程式封裝至 *AEM表單應用程式檔案* (.lca)。 然後，管理員使用「應用程式管理」頁面上的「應用程式」標籤，使用管理控制台匯入和部署應用程式檔案。

您也可以使用「應用程式管理」頁面上的封存標籤，匯入使用workbench 8.x建立的LCA。

>[!NOTE]
>
>已知的問題是，未來版本的LCA檔案不一定向後相容。 雖然您可從未來的AEM表單版本（例如預覽版本）檢視和匯入LCA檔案，但不支援這樣做，並可能導致異常行為。

使用「應用程式」標籤，匯入並管理在Workbench中建立的應用程式。 應用程式管理員也可以匯出應用程式的執行時期設定。 匯出執行時期設定後，您就不需要在開始部署應用程式之前，在生產環境中手動重新設定設定。 運行時配置檔案包含：

* 服務配置設定
* 池配置設定
* 端點配置設定
* 安全性設定檔

## 匯入應用程式或封存 {#import-an-application-or-archive}

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」。
1. 按一下「匯入」。
1. 按一下「瀏覽」並選取要匯入的。lca檔案，然後按一下「預覽」。 「預覽應用程式」頁面會顯示應用程式的相關資訊。
1. （可選）若要查看應用程式中包含的資產清單，請按一下「檢視資產」。
1. （可選）若要將資產部署至執行階段，請選取「匯入完成時將資產部署至執行階段」。 如果您未選取此選項，則可稍後部署資產。
1. 按一下「匯入」。 應用程式會出現在「應用程式」索引標籤上。
1. 使用管理員憑據登錄到CRX儲存庫。
1. 導覽至內容/dam/lcapplications

   >[!NOTE]
   >
   >匯入的應用程式會顯示在lcapplications節點中。

1. 按一下其中一個導入的應用程式。

   右邊的「屬性」頁籤顯示所選CRX節點的屬性。

   syncState **屬性指出** AEM Forms伺服器與CRX存放庫之間資料同步的狀態。 匯入程式一開始，此狀態就會設為0（零）。 此狀態表示資料當前未同步。 當資料同步時，狀態設定為1。

## 部署應用程式 {#deploy-an-application}

您可以部署已匯入或已從Workbench匯入Workbench的Workbench使用者。

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」。
1. 選取您要部署之應用程式旁的核取方塊，然後按一下「部署」。
1. 在出現的確認對話框中按一下確定。

## 取消部署應用程式 {#undeploy-an-application}

您可以從執行時期解除部署應用程式。

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」。
1. 選取您要取消部署之應用程式旁的核取方塊，然後按一下「取消部署」。
1. 在出現的確認對話框中按一下確定。

## 從伺服器中刪除應用程式 {#remove-an-application-from-the-server}

將應用程式從伺服器移除之前，請先解除部署它。

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」。
1. 選取您要移除之應用程式旁的核取方塊，然後按一下「移除」。
1. 在出現的確認對話框中按一下確定。

## 匯入應用程式的執行時期設定 {#import-an-application-s-runtime-configuration}

如果應用程式管理員導出了應用程式的運行時配置，則可以將其導入到部署的應用程式中。 您可以使用管理控制台或透過指令碼LCA部署來匯入它。

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「匯入執行階段設定」。
1. 按一下「瀏覽」，並選取包含執行階段設定的XML檔案。
1. 按一下「匯入」。

## 匯出應用程式的執行時期設定 {#export-an-application-s-runtime-configuration}

您可以匯出已部署應用程式的執行時期設定資訊。

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「匯出執行階段設定」，並儲存產生的設定檔案(XML)。

## AEM表單應用程式的原稿部署 {#scripted-deployment-of-aem-forms-applications}

您也可以使用指令碼部署工具來部署應用程式檔案，包括指定下列設定的settings.xml檔案：

* 服務配置設定
* 池配置設定
* 端點配置設定
* 安全性設定檔

指令碼式部署不需要在開始部署應用程式之前在生產環境中手動重新配置設定。

1. 在命令提示符下，導 *[覽至aem-forms root]*/sdk/misc/Foundation/ArchiveManagement。
1. 請參閱ReadMe.txt檔案，以取得更詳細的指示。
1. 手動修改scriptedDeploy.bat和sample-files/sample.xml檔案，如readme.txt檔案中所述。
1. 執行scriptedDeploy.bat檔案。 此動作會以覆寫設定來部署AEM表單封存檔案。

