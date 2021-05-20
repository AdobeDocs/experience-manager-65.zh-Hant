---
title: 初始沙箱內容
seo-title: 初始沙箱內容
description: 建立內容
seo-description: 建立內容
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 2%

---

# 初始沙箱內容{#initial-sandbox-content}

在本節中，您將建立以下頁面，這些頁面均使用[頁面範本](initial-app.md#createthepagetemplate):

* SCF沙箱網站，此網站會重新導向至主要頁面的英文版本。

   * SCF沙箱 — 網站英文版的主要頁面。

   * SCF播放 — 要播放的主要頁面的子項。

雖然本教學課程不深入[language copies](../../help/sites-administering/tc-prep.md)，但其設計是讓根頁面可透過HTML標題實作使用者偏好語言的偵測，並重新導向至該語言的適當首頁面。 慣例是使用雙字母國家/地區代碼作為頁面的節點名稱，例如英文為&quot;en&quot;，法文為&quot;fr&quot;等。

## 建立首頁{#create-first-pages}

現在有[頁面範本](initial-app.md#createthepagetemplate)，我們可以在/content目錄中建立網站的根頁面。

1. 標準UI目前提供建立網站的藍圖。 由於本教學課程是建立簡單網站，傳統UI很實用。

   若要切換至傳統UI，請選取全域導覽，並將游標暫留在「專案」圖示的右側。 選取顯示的&#x200B;*切換至傳統UI*&#x200B;圖示：

   ![classic-ui](assets/classic-ui.png)

   管理員](../../help/sites-administering/enable-classic-ui.md)必須啟用切換至傳統UI的功能。[

1. 從[傳統UI歡迎頁面](http://localhost:4502/welcome.html)中，選擇&#x200B;**[!UICONTROL 網站]**。

   ![classic-ui-website](assets/classic-ui-website.png)

   或者，瀏覽至[/siteadmin，直接存取傳統網站UI。](http://localhost:4502/siteadmin)

1. 在瀏覽器窗格中，選擇&#x200B;**[!UICONTROL 網站]**，然後在工具欄中選擇&#x200B;**[!UICONTROL 新建]** > **[!UICONTROL 新建頁]**。

   在&#x200B;**[!UICONTROL 建立頁面]**&#x200B;對話方塊中，輸入以下內容：

   * 標題: `SCF Sandbox Site`
   * 名稱: `an-scf-sandbox`
   * 選擇&#x200B;**[!UICONTROL SCF沙箱播放模板]**
   * 按一下&#x200B;**[!UICONTROL 建立]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 在瀏覽器窗格中，選擇您剛建立的頁面`/Websites/SCF Sandbox Site`，然後按一下&#x200B;**[!UICONTROL New]** > **[!UICONTROL New Page]**:

   * 標題: `SCF Sandbox`
   * 名稱: `en`
   * 選擇&#x200B;**[!UICONTROL SCF沙箱播放模板]**
   * 按一下&#x200B;**[!UICONTROL 建立]**

1. 在瀏覽器窗格中，選擇您剛建立的頁面`/Websites/SCF Sandbox Site/SCF Sandbox`，然後按一下&#x200B;**[!UICONTROL 新建]** > **[!UICONTROL 新建頁面]**

   * 標題: `SCF Play`
   * 名稱: `play`
   * 選擇&#x200B;**[!UICONTROL SCF沙箱播放模板]**
   * 按一下&#x200B;**[!UICONTROL 建立]**

1. 網站現在會以這種方式顯示在「網站主控台」中。 請注意，瀏覽器窗格中所選項目的子頁將顯示在可以管理這些項目的右窗格中。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   以下是使用「網站」工具和範本建立內容的存放庫檢視：

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 添加設計路徑{#add-the-design-path}

使用工具控制台的設計部分建立` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`時，屬性為&quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

已定義，可提供使用`currentDesign.getPath()`參考指令碼中設計資產的選用功能。 例如

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名稱: `cq:designPath`
   * 類型: `String`
   * 值: `/etc/designs/an-scf-sandbox`

* 按一下綠色`[+] Add`

存放庫應如下所示：

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 按一下「**[!UICONTROL 全部保存]**」

如果在儲存設定時遇到任何問題，請重新登入並再次設定。

>[!NOTE]
>
>使用`cq:designPath`是可選的，並且與使用clientlibs](develop-app.md#includeclientlibsintemplate)無關，因為SCF元件使用[clientlibs](client-customize.md#clientlibs-for-scf)來管理其JS和CSS，所以這些基本上是必要的。[
