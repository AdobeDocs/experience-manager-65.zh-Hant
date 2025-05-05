---
title: 整合AEM表單工作區與Microsoft Office SharePoint Server
description: 您可以整合AEM表單工作區與Microsoft Office SharePoint Server。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 整合AEM表單工作區與Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**— 需求**

**必備知識**
在您可以將AEM Forms Workspace新增到SharePoint伺服器之前，您必須擁有具有適當許可權的存取SharePoint伺服器的許可權，並且必須知道存取Workspace的URL。 以下步驟假設您熟悉SharePoint Server。 如需SharePoint伺服器中網頁元件的詳細資訊，請參閱Windows SharePoint服務中的網頁元件。

**使用者層級**
開始

您可以使用AEM Forms Workspace作為Microsoft Office SharePoint伺服器(例如Microsoft Office SharePoint Server 2007)中的網頁元件。 使用者可使用網頁瀏覽器連線至您的AEM Forms伺服器，以提供統一的體驗來存取SharePoint Workspace。 閱讀本文，您將瞭解在AEM Forms Office SharePoint Server中將Microsoft Workspace顯示為Web元件的基本步驟。 您可以執行本文中所述的步驟，以提供統一的體驗，讓連線至您SharePoint伺服器的使用者可以從相同連線埠存取AEM Forms Workspace。

>[!NOTE]
>
>本文列出的步驟是特定的Microsoft SharePoint Server 2007。 您也可以將HTML Workspace與其他支援的Microsoft SharePoint版本一起設定。

## 將AEM Forms Workspace與Microsoft Office SharePoint Server 2007整合 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

執行以下步驟，將AEM Forms Workspace整合至網頁元件：

1. 在網頁瀏覽器中，導覽至SharePoint網站，例如`https://[myMOSSserver]:44299/default.aspx`，其中`[myMOSSserver]`是Sharepoint伺服器的名稱或IP位址。

   >[!NOTE]
   >
   >44299是SharePoint伺服器的預設連線埠號碼。 連線埠號碼取決於您安裝的SharePoint Server。

1. 在網頁的右上角，按一下&#x200B;**網站動作**&#x200B;並選取&#x200B;**編輯頁面**。
1. 按一下&#x200B;**新增網頁元件**&#x200B;按鈕。
1. 在[新增網頁元件 — 網頁元件]對話方塊的[其他]下，選取&#x200B;**頁面檢視器網頁元件**，然後按一下[新增]。**&#x200B;**
1. 在「頁面檢視器網頁元件」方塊中，按一下&#x200B;**編輯**&#x200B;並選取&#x200B;**修改共用網頁元件**。

   >[!NOTE]
   >
   >「頁面檢視器網頁元件」方塊會顯示在您在步驟3中按一下的「新增網頁元件」**按鈕下方，如下圖所示（圖1）：**

   ![Microsoft Office SharePoint Server中的Page Viewer Web元件方塊。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   圖1. - Microsoft Office SharePoint伺服器中的「頁面檢視器」網頁元件方塊。

1. 在「頁面檢視器」頁面上，執行下列工作：

   1. 在「連結」方塊中，輸入AEM Forms Workspace的URL，例如`https://[AEM_forms_Server]:8080/lc/ws`，其中`[AEM_forms_Server]`代表AEM Forms伺服器的IP或名稱。
   1. 按一下「**外觀**」並修改高度、寬度和標題，以便您可以看到整個Workspace使用者介面。 例如，您可以將高度和寬度分別設定為6英吋和11英吋。
   1. 按一下&#x200B;**測試連結**。 隨後會出現一個新的Web瀏覽器視窗，其中會顯示Workspace。
   1. （選用）按一下「**配置**」並修改網頁元件中Workspace的配置。
   1. （選擇性）按一下「**進階**」並修改其他設定，例如說明以及網頁元件中的Workspace是否可以最小化或關閉。

      按一下「**套用**」。

1. 按一下&#x200B;**結束編輯模式**，然後確認您可以存取Workspace。

完成上述步驟後，您的SharePoint網站外觀會類似於下圖（圖2）：

![AEM Forms Workspace與Microsoft Office SharePoint Server整合](assets/aem-forms-workspace.jpg)

圖2 - AEM Forms Workspace與Microsoft Office SharePoint Server整合
