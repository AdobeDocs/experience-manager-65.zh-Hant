---
title: 初始沙箱內容
description: 瞭解如何在沙箱中使用頁面範本來建立英文版網站的首頁面，以及首頁面的子頁面。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 2%

---

# 初始沙箱內容 {#initial-sandbox-content}

在此區段中，您建立以下所有使用[頁面範本](initial-app.md#createthepagetemplate)的頁面：

* SCF沙箱網站，這會重新導向至首頁面的英文版。

   * SCF沙箱 — 英文版網站的首頁面。

   * SCF播放 — 要播放之首頁面的子頁面。

本教學課程未深入探討[語言副本](../../help/sites-administering/tc-prep.md)。 相反地，它的設計讓根頁面可透過HTML標題為使用者實施偏好語言偵測，並重新導向至該語言的適當首頁面。 慣例是將兩個字母的國家代碼用於頁面的節點名稱，例如，「en」用於英文，「fr」用於法文。

## 建立第一頁 {#create-first-pages}

現在已有[頁面範本](initial-app.md#createthepagetemplate)，您可以在/content目錄中建立網站的根頁面。

1. 標準UI目前提供用於建立網站的藍圖。 由於本教學課程會建立簡單的網站，傳統UI會很實用。

   若要切換至傳統UI，請選取全域導覽，並將滑鼠游標停留在「專案」圖示的右側。 選取&#x200B;*切換到傳統UI*&#x200B;圖示，其會出現：

   ![傳統ui](assets/classic-ui.png)

   切換到傳統UI的能力必須由管理員[啟用](../../help/sites-administering/enable-classic-ui.md)。

1. 從[傳統UI歡迎頁面](http://localhost:4502/welcome.html)，選取&#x200B;**[!UICONTROL 網站]**。

   ![classic-ui-website](assets/classic-ui-website.png)

   或者，您可以瀏覽至[/siteadmin，直接存取網站的傳統UI。](http://localhost:4502/siteadmin)

1. 在總管窗格中，選取&#x200B;**[!UICONTROL 網站]**，然後在工具列中選取&#x200B;**[!UICONTROL 新增]** > **[!UICONTROL 新增頁面]**。

   在&#x200B;**[!UICONTROL 建立頁面]**&#x200B;對話方塊中，輸入下列內容：

   * 標題： `SCF Sandbox Site`
   * 名稱：`an-scf-sandbox`
   * 選取&#x200B;**[!UICONTROL SCF沙箱播放範本]**
   * 按一下「**[!UICONTROL 建立]**」。

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 在總管窗格中，選取您建立的頁面`/Websites/SCF Sandbox Site`，然後按一下&#x200B;**[!UICONTROL 新增]** > **[!UICONTROL 新增頁面]**：

   * 標題： `SCF Sandbox`
   * 名稱：`en`
   * 選取&#x200B;**[!UICONTROL SCF沙箱播放範本]**
   * 按一下「**[!UICONTROL 建立]**」。

1. 在總管窗格中，選取您建立的頁面`/Websites/SCF Sandbox Site/SCF Sandbox`，然後按一下&#x200B;**[!UICONTROL 新增]** > **[!UICONTROL 新增頁面]**

   * 標題： `SCF Play`
   * 名稱：`play`
   * 選取&#x200B;**[!UICONTROL SCF沙箱播放範本]**
   * 按一下「**[!UICONTROL 建立]**」。

1. 這就是網站現在在「網站」主控台中的顯示方式。 請注意，在總管窗格中選取之專案的子頁面會顯示在可管理專案的右窗格中。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   這是使用網站工具和範本建立的存放庫檢視：

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 新增設計路徑 {#add-the-design-path}

當使用「工具」主控台的「設計」區段建立` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`時，屬性&#39;&#39;

* `cq:template="/libs/wcm/core/templates/designpage"`

已定義，提供使用`currentDesign.getPath()`在指令碼中參考設計資產的選擇性功能。 例如

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名稱：`cq:designPath`
   * 類型：`String`
   * 值： `/etc/designs/an-scf-sandbox`

* 按一下綠色`[+] Add`

存放庫應如下所示：

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 按一下&#x200B;**[!UICONTROL 全部儲存]**

如果儲存設定時發生任何問題，請重新登入並再次設定。

>[!NOTE]
>
>使用`cq:designPath`是選擇性的，且與[使用clientlibs](develop-app.md#includeclientlibsintemplate)無關，因為SCF元件使用[clientlibs](client-customize.md#clientlibs-for-scf)管理其JS和CSS時需要使用。
