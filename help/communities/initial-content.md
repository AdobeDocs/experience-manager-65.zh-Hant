---
title: 初始沙盒內容
seo-title: 初始沙盒內容
description: 建立內容
seo-description: 建立內容
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: 65e2b98cfd980f17302b4751127e25827decec22
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 2%

---


# 初始沙盒內容 {#initial-sandbox-content}

在本節中，您會建立下列所有使用頁面範本 [的頁面](initial-app.md#createthepagetemplate):

* SCF沙盒網站，此網站會重新導向至首頁的英文版。

   * SCF沙盒——網站英文版的首頁面。

   * SCF播放——要播放的首頁的子頁。

雖然本教學課程不深入探究 [語言副本](../../help/sites-administering/tc-prep.md)，但是其設計目的在於讓根頁面透過HTML標題實作使用者偏好語言的偵測，並重新導向至該語言的適當首頁。 慣例是使用雙字母國家／地區代碼作為頁面的節點名稱，例如英文為&quot;en&quot;、法文為&quot;fr&quot;等。

## 建立第一頁 {#create-first-pages}

現在有了頁面范 [本](initial-app.md#createthepagetemplate)，我們可以在/content目錄中建立網站的根頁面。

1. 標準UI目前提供建立網站的藍圖。 由於本教學課程是建立簡單網站，因此傳統的UI十分實用。

   若要切換至傳統UI，請選取全域導覽，並將滑鼠指標暫留在「專案」圖示的右側。 選擇「 *切換至傳統UI* 」表徵圖，該表徵圖顯示：

   ![classic-ui](assets/classic-ui.png)

   必須由管理員啟用切換至傳統 [UI的功能](../../help/sites-administering/enable-classic-ui.md)。

1. 從傳統 [UI歡迎頁面中](http://localhost:4502/welcome.html)，選擇 **[!UICONTROL 網站]**。

   ![classic-ui-website](assets/classic-ui-website.png)

   或者，瀏覽至 [/網站管理員，直接存取網站的經典UI。](http://localhost:4502/siteadmin)

1. 在瀏覽器窗格中，選擇「 **[!UICONTROL 網站]** 」，然後在工具列中選擇「新 **[!UICONTROL 增]** >新 **[!UICONTROL 增頁面」]**。

   在「建 **[!UICONTROL 立頁面]** 」對話方塊中，輸入下列：

   * 標題: `SCF Sandbox Site`
   * 名稱: `an-scf-sandbox`
   * 選取 **[!UICONTROL SCF沙盒播放範本]**
   * Click **[!UICONTROL Create]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 在瀏覽器窗格中，選擇您剛建立的頁面，然 `/Websites/SCF Sandbox Site`後按一下「 **[!UICONTROL 新建]** 」>「 **[!UICONTROL 新建頁面]**」:

   * 標題: `SCF Sandbox`
   * 名稱: `en`
   * 選取 **[!UICONTROL SCF沙盒播放範本]**
   * Click **[!UICONTROL Create]**

1. 在瀏覽器窗格中，選擇剛建立的頁面，然 `/Websites/SCF Sandbox Site/SCF Sandbox`後按一下「 **[!UICONTROL 新建]** 」 > 「新建頁 **[!UICONTROL 面」]**

   * 標題: `SCF Play`
   * 名稱: `play`
   * 選取 **[!UICONTROL SCF沙盒播放範本]**
   * Click **[!UICONTROL Create]**

1. 網站現在會以此方式出現在網站主控台中。 請注意，在瀏覽器窗格中選擇的項目的子頁面會顯示在右窗格中，供管理。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   這是使用網站工具和模板建立內容的儲存庫視圖：

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 新增設計路徑 {#add-the-design-path}

當使 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` 用「工具」(Tools)控制台的設計部分建立時，屬性「

* `cq:template="/libs/wcm/core/templates/designpage"`

定義，提供使用來參考指令碼中設計資產的選用功能 `currentDesign.getPath()`。 例如

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名稱: `cq:designPath`
   * 類型: `String`
   * 值: `/etc/designs/an-scf-sandbox`

* 按一下綠色 `[+] Add`

儲存庫應如下所示：

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 按一下「 **[!UICONTROL 全部儲存」]**

如果保存配置時遇到問題，請重新登錄並再次配置。

>[!NOTE]
>
>使用是可 `cq:designPath` 選的，與使用clientlibs無關 [，這是SCF元件使用clientlibs來管理其JS和CSS時的必](develop-app.md#includeclientlibsintemplate)[](client-customize.md#clientlibs-for-scf) 要條件。


