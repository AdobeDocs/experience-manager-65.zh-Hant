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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 初始沙盒內容 {#initial-sandbox-content}

在本節中，您會建立下列所有使用頁面範本 [的頁面](initial-app.md#createthepagetemplate):

* SCF沙盒網站，此網站會重新導向至首頁的英文版

   * SCF沙盒——網站英文版的首頁

      * SCF播放——要播放的首頁的子項

雖然本教學課程不深入探究 [語言副本](../../help/sites-administering/tc-prep.md)，但是其設計目的在於讓根頁面透過HTML標題實作使用者偏好語言的偵測，並重新導向至該語言的適當首頁。 慣例是使用雙字母國家／地區代碼作為頁面的節點名稱，例如英文為&quot;en&quot;、法文為&quot;fr&quot;等。

## 建立第一頁 {#create-first-pages}

現在有了頁面 [範本](initial-app.md#createthepagetemplate)，我們可以在/content目錄中建立網站的根頁面。

1. 標準UI目前提供建立網站的藍圖。 由於本教學課程是建立簡單網站，因此傳統的UI十分實用。

   若要切換至傳統UI，請選取全域導覽，並將滑鼠指標暫留在「專案」圖示的右側。 選擇「 *切換至傳統UI* 」表徵圖，該表徵圖顯示：

   ![chlimage_1-36](assets/chlimage_1-36.png)

   必須由管理員啟用切換至傳統 [UI的功能](../../help/sites-administering/enable-classic-ui.md)。

1. 從傳統 [UI歡迎頁面中](http://localhost:4502/welcome.html)，選擇 **[!UICONTROL 網站]**。

   ![chlimage_1-37](assets/chlimage_1-37.png)

   或者，瀏覽至 [/網站管理員，直接存取網站的經典UI。](http://localhost:4502/siteadmin)

1. 在檔案總管窗格中，選取「 **[!UICONTROL 網站]** 」，然後在工具列中選取「 **[!UICONTROL 新增>新頁面」]**。

   在「建 **[!UICONTROL 立頁面]** 」對話方塊中，輸入下列：

   * 標題: `SCF Sandbox Site`
   * 名稱: `an-scf-sandbox`
   * 選取 **[!UICONTROL SCF沙盒播放範本]**
   * Click **[!UICONTROL Create]**
   ![chlimage_1-38](assets/chlimage_1-38.png)

1. 在瀏覽器窗格中，選擇您剛建立的頁面，然 `/Websites/SCF Sandbox Site`後按一下「 **[!UICONTROL 新建」>「新建頁面]**:

   * 標題: `SCF Sandbox`
   * 名稱: `en`
   * 選取 **SCF沙盒播放範本&#x200B;**
   * Click **Create **

1. 在瀏覽器窗格中，選擇您剛建立的頁面，然 `/Websites/SCF Sandbox Site/SCF Sandbox`後按一下「 **[!UICONTROL 新建」>「新建頁面」]**

   * 標題: `SCF Play`
   * 名稱: `play`
   * 選取 **[!UICONTROL SCF沙盒播放範本]**
   * Click **[!UICONTROL Create]**

1. 網站現在會以此方式出現在網站主控台中。 請注意，在瀏覽器窗格中選擇的項目的子頁面會顯示在右窗格中，供管理。

   ![chlimage_1-39](assets/chlimage_1-39.png)

   這是使用網站工具和模板建立內容的儲存庫視圖：

   ![chlimage_1-40](assets/chlimage_1-40.png)

## 新增設計路徑 {#add-the-design-path}

當使 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` 用「工具」(Tools)控制台的設計部分建立時，屬性「

* `cq:template="/libs/wcm/core/templates/designpage"`

定義，提供使用來參考指令碼中設計資產的選用功能 `currentDesign.getPath()`。 例如

* &lt;%字串favIcon = currentDesign.getPath()+ &quot;/favicon.ico&quot;;%>


   * 名稱: `cq:designPath`
   * 類型: `String`
   * 值: `/etc/designs/an-scf-sandbox`

* 按一下綠色 `[+] Add`

儲存庫應如下所示：

![chlimage_1-41](assets/chlimage_1-41.png)

* 按一下「 **[!UICONTROL 全部儲存」]**

[ 難以拯救？ 重新登入！ ]

>[!NOTE]
>
>cq:designPath的使用是選擇性的，與clientlibs的使 [用無關](develop-app.md#includeclientlibsintemplate)，這是SCF元件使用clientlibs來管理其JS和CSS時的必 [](client-customize.md#clientlibs-for-scf) 要條件。

