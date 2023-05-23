---
title: 將表AEM單工作區與MicrosoftOfficeSharePoint伺服器整合
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: 您可以將表AEM單工作區與MicrosoftOfficeSharePoint伺服器整合。
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

# 將表AEM單工作區與MicrosoftOfficeSharePoint伺服器整合{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- 要求**

**先決知識**
在將AEM Forms工作區添加到SharePoint伺服器之前，必須具有相應權限訪問SharePoint伺服器，並且必須知道訪問工作區的URL。 以下步驟假定您對SharePoint伺服器有豐富的知識。 有關SharePoint伺服器中Web部件的詳細資訊，請參閱WindowsSharePoint服務中的Web部件。

**用戶級別**
開始

可以將AEM Forms工作區用作MicrosoftOfficeSharePoint伺服器(例如，MicrosoftOfficeSharePointServer 2007)中的Web部件。 用戶可以通過使用Web瀏覽器連接到您的AEM Forms伺服器來訪問SharePoint工作區，以提供統一的體驗。 在本文中，您將瞭解將AEM Forms工作區作為Web部件在MicrosoftOfficeSharePoint伺服器中顯示的基本步驟。 您可以執行本文中描述的步驟，以提供統一的體驗，以便連接到SharePoint伺服器的用戶可以從同一埠訪問AEM Forms工作區。

>[!NOTE]
>
>本文中列出的步驟是特定的MicrosoftSharePoint伺服器2007。 您還可以使用其他支援的MicrosoftSharePoint版本配置HTML工作區。

## 將AEM Forms工作區與MicrosoftOfficeSharePoint伺服器2007整合 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

執行以下步驟將AEM Forms工作區整合到Web部件中：

1. 在Web瀏覽器中，導航到SharePoint網站， `https://[myMOSSserver]:44299/default.aspx` 何處 `[myMOSSserver]` 是Sharepoint伺服器的名稱或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint伺服器的預設埠號。 埠號取決於您安裝的SharePoint伺服器。

1. 在網頁的右上側，按一下 **站點操作** 選擇 **編輯頁**。
1. 按一下 **添加Web部件** 按鈕
1. 在「添加Web部件 — 網頁」對話框的「雜項」下，選擇 **頁面查看器Web部件** 然後按一下 **添加**。
1. 在「頁面查看器Web部件」框中，按一下 **編輯** 選擇 **修改共用Web部件**。

   >[!NOTE]
   >
   >「頁面查看器Web部件」(Page Viewer Web Part)框出現在 **添加Web部件** 按鈕（如下圖1所示）:

   ![「頁面查看器Web部件」框(位於MicrosoftOfficeSharePoint伺服器中)。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   圖1 -MicrosoftOfficeSharePoint伺服器中的「頁面查看器Web部件」框。

1. 在「頁面查看器」頁上，執行以下任務：

   1. 在「連結」框中，鍵入AEM Forms工作區的URL，如 `https://[AEM_forms_Server]:8080/lc/ws` 何處 `[AEM_forms_Server]` 表示表單伺服器的IPAEM或名稱。
   1. 按一下 **外觀** 並修改高度、寬度和標題，以便您可以查看整個Workspace用戶介面。 例如，可將高度和寬度分別設定為6英吋和11英吋。
   1. 按一下 **Test連結**。 此時將出現一個新的Web瀏覽器窗口，其中顯示了Workspace。
   1. （可選）按一下 **佈局** 修改Web部件中Workspace的佈局。
   1. （可選）按一下 **高級** 並修改其他設定，如說明以及Web部件中的「工作區」是否可以最小化或關閉。

      按一下 **應用**。

1. 按一下 **退出編輯模式** 並驗證您是否可以訪問Workspace。

完成上述步驟後，您的SharePoint站點看起來與下圖類似（圖2）:

![AEM Forms工作區與MicrosoftOfficeSharePoint伺服器整合](assets/aem-forms-workspace.jpg)

圖2 — 與AEM FormsOfficeSharePoint伺服器整合的MicrosoftWorkspace
