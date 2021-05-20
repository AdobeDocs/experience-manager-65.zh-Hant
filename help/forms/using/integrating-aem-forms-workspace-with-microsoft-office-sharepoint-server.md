---
title: 將AEM表單工作區與Microsoft Office SharePoint Server整合
seo-title: 將AEM表單工作區與Microsoft Office SharePoint Server整合
description: '您可以將AEM Forms工作區與Microsoft Office SharePoint Server整合。 '
seo-description: '您可以將AEM Forms工作區與Microsoft Office SharePoint Server整合。 '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 將AEM表單工作區與Microsoft Office SharePoint Server整合{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**— 需求**

**必**
備知識在將AEM Forms Workspace添加到SharePoint伺服器之前，您必須具有對SharePoint Server的訪問權限，並且必須知道要訪問Workspace的URL。以下步驟假定您對SharePoint Server有知識。 有關SharePoint Server中的Web部件的詳細資訊，請參閱Windows SharePoint Services中的Web部件。

**用戶**
levelBeing

您可以在Microsoft Office SharePoint Server（如Microsoft Office SharePoint Server 2007）中將AEM Forms Workspace用作Web部件。 使用者可使用網頁瀏覽器連線至您的SharePoint伺服器，以存取AEM Forms Workspace，提供統一的體驗。 在本文中，您將了解在Microsoft Office SharePoint Server中將AEM Forms Workspace顯示為Web部件的基本步驟。 您可以執行本文所述的步驟，提供統一的體驗，讓連接到SharePoint伺服器的用戶可以從同一埠訪問AEM Forms Workspace。

>[!NOTE]
>
>本文中列出的步驟是特定的Microsoft SharePoint Server 2007。 您也可以使用其他支援的Microsoft SharePoint版本來設定HTML工作區。

## 將AEM Forms工作區與Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}整合

執行下列步驟將AEM Forms Workspace整合至Web部件：

1. 在Web瀏覽器中，導航到SharePoint站點，如`https://[myMOSSserver]:44299/default.aspx`，其中`[myMOSSserver]`是Sharepoint伺服器的名稱或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint伺服器的預設埠號。 埠號取決於您安裝的SharePoint Server。

1. 在網頁的右上方，按一下「**站點操作**」並選擇「**編輯頁面**」。
1. 按一下&#x200B;**添加Web部件**&#x200B;按鈕。
1. 在「添加Web部件 — 網頁」對話框的「其他」下，選擇「**頁面查看器Web部件**」，然後按一下「**添加**」。
1. 在「頁面查看器Web部件」框中，按一下&#x200B;**edit**&#x200B;並選擇&#x200B;**修改共用Web部件**。

   >[!NOTE]
   >
   >「Page Viewer Web Part（頁面查看器Web部件）」框顯示在&#x200B;**「Add a Web Part**」按鈕下，按一下了步驟3，如下圖所示（圖1）:

   ![Microsoft Office SharePoint伺服器中的「頁面查看器Web部件」框。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   圖1. - Microsoft Office SharePoint伺服器中的「頁面查看器Web部件」框。

1. 在「頁面檢視器」頁面上，執行下列工作：

   1. 在「連結」方塊中，輸入AEM Forms Workspace的URL，例如`https://[AEM_forms_Server]:8080/lc/ws`，其中`[AEM_forms_Server]`代表AEM表單伺服器的IP或名稱。
   1. 按一下「**外觀**」並修改高度、寬度和標題，以便查看整個Workspace用戶介面。 例如，您可以將高度和寬度分別設定為6英吋和11英吋。
   1. 按一下「**測試連結**」。 隨即出現新的網頁瀏覽器視窗，其中會顯示「工作區」。
   1. （可選）按一下&#x200B;**Layout**&#x200B;並修改Web部件中Workspace的佈局。
   1. （可選）按一下&#x200B;**Advanced**&#x200B;並修改其他設定，如說明，以及Web部件中Workspace是否可以最小化或關閉。

      按一下&#x200B;**Apply**。

1. 按一下「**退出編輯模式**」 ，確認您可以存取工作區。

完成上述步驟後，您的SharePoint站點外觀類似於下圖（圖2）:

![AEM Forms Workspace與Microsoft Office SharePoint Server整合](assets/aem-forms-workspace.jpg)

圖2 — 與Microsoft Office SharePoint Server整合的AEM Forms Workspace
