---
title: 將AEM表單工作區與Microsoft Office SharePoint Server整合
seo-title: 將AEM表單工作區與Microsoft Office SharePoint Server整合
description: '您可以將AEM表單工作區與Microsoft Office SharePoint Server整合。 '
seo-description: '您可以將AEM表單工作區與Microsoft Office SharePoint Server整合。 '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---


# 將AEM表單工作區與Microsoft Office SharePoint Server整合{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**-需求**

**先決**
知識您必須先具備適當權限才能將AEM Forms Workspace新增至SharePoint Server，而且您必須知道存取Workspace的URL。以下步驟假設您對SharePoint Server了如指掌。 有關SharePoint Server中Web部件的詳細資訊，請參閱Windows SharePoint Services中的Web部件。

**用戶級**
開始

您可以在Microsoft Office SharePoint Server（例如Microsoft Office SharePoint Server 2007）中將AEM Forms Workspace當做Web Part。 使用者可以使用網頁瀏覽器連線至您的SharePoint伺服器，以存取AEM Forms Workspace，提供統一的體驗。 在本文中，您將學習在Microsoft Office SharePoint Server中將AEM Forms Workspace顯示為Web Part的基本步驟。 您可以執行本文所述的步驟，以提供統一的體驗，讓連線至SharePoint伺服器的使用者可以從相同的連接埠存取AEM Forms Workspace。

>[!NOTE]
>
>本文中列出的步驟是特定的Microsoft SharePoint Server 2007。 您也可以使用其他支援版本的Microsoft SharePoint來設定HTML工作區。

## 將AEM Forms Workspace與Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}整合

執行下列步驟，將AEM Forms Workspace整合至Web Part:

1. 在Web瀏覽器中，導航到SharePoint站點，例如`https://[myMOSSserver]:44299/default.aspx` ，其中`[myMOSSserver]`是Sharepoint伺服器的名稱或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint伺服器的預設埠號。 埠號取決於您安裝的SharePoint伺服器。

1. 在網頁的右上側，按一下「網站動作」**，然後選取「編輯頁面」**。****
1. 按一下&#x200B;**添加Web部件**&#x200B;按鈕。
1. 在「添加Web部件- Web頁對話框」的「其他」下，選擇「**頁面查看器Web部件**」，然後按一下「添加&#x200B;**a3/>」。**
1. 在「頁面檢視器Web部件」方塊中，按一下「編輯&#x200B;**編輯**」並選取「修改共用Web部件&#x200B;**」。**

   >[!NOTE]
   >
   >「Page Viewer Web Part（頁面檢視器網頁部件）」方塊會出現在您在步驟3中按一下的&#x200B;**「Add a Web Part（新增網頁部件**）」按鈕下方，如下圖所示（圖1）:

   ![Microsoft Office SharePoint伺服器中的「頁面檢視器網頁部件」方塊。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   圖1. - Microsoft Office SharePoint伺服器中的「頁面檢視器網頁部件」方塊。

1. 在「頁面檢視器」頁面上，執行下列工作：

   1. 在「連結」方塊中，輸入AEM Forms Workspace的URL，例如`https://[AEM_forms_Server]:8080/lc/ws`，其中`[AEM_forms_Server]`代表AEM Forms伺服器的IP或名稱。
   1. 按一下「外觀」(**Appearance)**&#x200B;並修改高度、寬度和標題，讓您看到整個Workspace使用者介面。 例如，您可以分別將高度和寬度設定為6英吋和11英吋。
   1. 按一下&#x200B;**測試連結**。 隨即出現新的網頁瀏覽器視窗，其中會顯示「工作區」。
   1. （可選）按一下「Layout ****」，並修改「Web Part」（網頁部件）中「Workspace」（工作區）的版面。
   1. （可選）按一下「**進階**」並修改其他設定，例如說明，以及「Web部件」中的「工作區」是否可最小化或關閉。

      按一下&#x200B;**Apply**。

1. 按一下「**退出編輯模式**」並驗證您可以訪問工作區。

完成上述步驟後，您的SharePoint網站看起來類似下圖（圖2）:

![AEM Forms Workspace與Microsoft Office SharePoint Server整合](assets/aem-forms-workspace.jpg)

圖2 —— 與Microsoft Office SharePoint Server整合的AEM Forms工作區

