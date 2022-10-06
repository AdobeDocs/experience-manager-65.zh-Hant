---
title: 將AEM表單工作區與Microsoft Office SharePoint Server整合
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: 您可以將AEM Forms工作區與Microsoft Office SharePoint Server整合。
seo-description: You can integrate AEM forms workspace with Microsoft Office SharePoint Server.
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 將AEM表單工作區與Microsoft Office SharePoint Server整合{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**— 需求**

**必備知識**
您必須具備SharePoint伺服器的存取權限，才能將AEM Forms Workspace新增至SharePoint伺服器，而且您必須知道存取Workspace的URL。 下列步驟假設您對SharePoint伺服器有豐富的知識。 有關SharePoint Server中Web部件的詳細資訊，請參閱Windows SharePoint服務中的Web部件。

**使用者層級**
開始

您可以在Microsoft Office SharePoint伺服器(例如，Microsoft Office SharePoint Server 2007)中將AEM Forms Workspace作為Web部件使用。 使用者可使用網頁瀏覽器連線至您的AEM Forms伺服器，以提供統一的體驗，進而存取SharePoint Workspace。 在本文中，您將了解在AEM Forms Office SharePoint Server中將Microsoft Workspace顯示為Web部件的基本步驟。 您可以執行本文所述步驟來提供統一的體驗，讓連線至您的SharePoint伺服器的使用者可以從相同埠存取AEM Forms Workspace。

>[!NOTE]
>
>本文列出的步驟是特定的Microsoft SharePoint Server 2007。 您也可以使用其他支援的Microsoft SharePoint版本來設定HTML工作區。

## 將AEM Forms工作區與Microsoft Office SharePoint Server 2007整合 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

執行下列步驟將AEM Forms Workspace整合至Web部件：

1. 在網頁瀏覽器中，導覽至SharePoint網站，例如 `https://[myMOSSserver]:44299/default.aspx` where `[myMOSSserver]` 是Sharepoint伺服器的名稱或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint伺服器的預設埠號。 埠號取決於您安裝的SharePoint Server。

1. 在網頁的右上方，按一下 **網站動作** 選取 **編輯頁面**.
1. 按一下 **添加Web部件** 按鈕。
1. 在「添加Web部件 — 網頁」對話框的「其他」下，選擇 **頁面查看器Web部件** 然後按一下 **新增**.
1. 在「Page Viewer Web Part（頁面查看器Web部件）」框中，按一下 **編輯** 選取 **修改共用Web部件**.

   >[!NOTE]
   >
   >「頁面查看器Web部件」(Page Viewer Web Part)框顯示在 **添加Web部件** 按鈕（如下圖1所示）:

   ![Microsoft Office SharePoint伺服器中的「頁面查看器Web部件」框。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   圖1. -Microsoft Office SharePoint伺服器中的「頁面查看器Web部件」框。

1. 在「頁面檢視器」頁面上，執行下列工作：

   1. 在「連結」方塊中，輸入AEM Forms Workspace的URL，例如 `https://[AEM_forms_Server]:8080/lc/ws` where `[AEM_forms_Server]` 代表AEM表單伺服器的IP或名稱。
   1. 按一下 **外觀** 並修改高度、寬度和標題，以便查看整個Workspace使用者介面。 例如，您可以將高度和寬度分別設定為6英吋和11英吋。
   1. 按一下 **測試連結**. 隨即出現新的網頁瀏覽器視窗，其中會顯示「工作區」。
   1. （選用）按一下 **版面** 和修改Web部件中工作區的佈局。
   1. （選用）按一下 **進階** 並修改其他設定，例如說明，以及Web部件中的Workspace是否可最小化或關閉。

      按一下 **套用**.

1. 按一下 **退出編輯模式** 並確認您可以存取工作區。

完成上述步驟後，您的SharePoint網站外觀如下圖所示（圖2）:

![AEM Forms Workspace與Microsoft Office SharePoint Server整合](assets/aem-forms-workspace.jpg)

圖2 — 與AEM Forms Office SharePoint伺服器整合的Microsoft Workspace
