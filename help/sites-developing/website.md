---
title: 建立功能齊全的網站(JSP)
seo-title: 建立功能齊全的網站(JSP)
description: 本教學課程可讓您使用AEM建立功能完整的網站
seo-description: 本教學課程可讓您使用AEM建立功能完整的網站
uuid: ec76ad5e-af6c-43ad-ae57-a4ae4ac7029f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 90bc05c9-e971-4e75-bc07-5e137c6c913e
docset: aem65
exl-id: d7cf843c-c837-4b97-b6c5-0fbd6793bdd4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4952'
ht-degree: 2%

---

# 建立功能齊全的網站(JSP){#create-a-fully-featured-website-jsp}

>[!NOTE]
>
>本文說明如何使用JSP和基於傳統UI建立網站。 Adobe建議如[開發AEM Sites快速入門](/help/sites-developing/getting-started.md)一文所述，為您的網站運用最新的AEM技術。

本教學課程可讓您使用Adobe Experience Manager(AEM)建立功能完整的網站。 該網站將以通用網站為基礎，主要針對網頁開發人員。 所有開發工作都會在製作環境中進行。

本教學課程說明如何：

1. 安裝AEM。
1. 存取CRXDE Lite（開發環境）。
1. 在CRXDE Lite中設定專案結構。
1. 建立範本、元件和指令碼，作為建立內容頁面的基礎。
1. 建立網站的根頁面，然後建立內容頁面。
1. 建立下列元件以用於您的頁面：

   * 上層導覽
   * 列出子項
   * 標誌
   * 影像
   * 文字影像
   * 搜尋

1. 包括各種基礎元件。

執行所有步驟後，您的頁面會如下所示：

![chlimage_1-24](assets/chlimage_1-24.png)

**下載最終結果**

若要遵循教學課程而非執行練習，請下載website-1.0.zip。 此檔案是AEM內容套件，包含本教學課程的結果。 使用[套件管理器](/help/sites-administering/package-manager.md)將套件安裝至您的製作執行個體。

**注意：** 安裝此套件會覆寫您使用本教學課程建立之製作執行個體上的任何資源。

網站內容套件

[取得檔案](assets/website-1_0.zip)

## 安裝Adobe Experience Manager {#installing-adobe-experience-manager}

若要安裝AEM執行個體以開發您的網站，請依照指示使用作者和發佈執行個體](/help/sites-deploying/deploy.md#author-and-publish-installs)來設定[部署環境，或執行[一般安裝](/help/sites-deploying/deploy.md#default-local-install)。 一般安裝包括下載AEM Quickstart JAR檔案、將license.properties檔案放置在與JAR檔案相同的目錄中，然後按兩下JAR檔案。

安裝AEM後，按一下歡迎頁面上的CRXDE Lite連結以存取CRXDE Lite開發環境：

![chlimage_1-25](assets/chlimage_1-25.png)

>[!NOTE]
>
>使用預設埠在本機安裝的AEM製作執行個體的CRXDE LiteURL為[https://localhost:4502/crx/de/](https://localhost:4502/crx/de/)。

### 在{#setting-up-the-project-structure-in-crxde-lite}CRXDE Lite中設定項目結構

使用CRXDE Lite在儲存庫中建立mywebsite應用程式結構：

1. 在CRXDE Lite左側的樹狀結構中，按一下右鍵&#x200B;**`/apps`**&#x200B;資料夾，然後按一下&#x200B;**Create** > **Create** **Folder**。 在&#x200B;**建立資料夾**&#x200B;對話框中，鍵入`mywebsite`作為資料夾名稱，然後按一下&#x200B;**確定**。
1. 按一下右鍵&#x200B;**`/apps/mywebsite`**&#x200B;資料夾，然後按一下&#x200B;**Create** > **Create Folder**。 在&#x200B;**建立資料夾**&#x200B;對話框中，鍵入`components`作為資料夾名稱，然後按一下&#x200B;**確定**。
1. 按一下右鍵&#x200B;**`/apps/mywebsite`**&#x200B;資料夾，然後按一下&#x200B;**Create** > **Create Folder**。 在&#x200B;**建立資料夾**&#x200B;對話框中，鍵入`templates`作為資料夾名稱，然後按一下&#x200B;**確定**。

   樹狀結構現在看起來應該像這樣：

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 按一下「**全部保存**」。

### 設定設計{#setting-up-the-design}

在本節中，您使用設計工具建立應用程式的設計。 設計會提供您網站的CSS和影像資源。

>[!NOTE]
>
>按一下以下連結即可下載mywebsite.zip。 封存包含您設計的static.css和影像檔案。

static.css檔案和影像範例

[取得檔案](assets/mywebsite.zip)

1. 在AEM歡迎頁面上，按一下&#x200B;**工具**。 ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))

   ![chlimage_1-27](assets/chlimage_1-27.png)

1. 在資料夾樹中，選擇&#x200B;**Designs**&#x200B;資料夾，然後按一下&#x200B;**New** > **New Page**。 鍵入`mywebsite`作為標題，然後按一下&#x200B;**Create**。

1. 如果表中未顯示mywebsite項，請刷新樹或表。

1. [使](/help/sites-administering/webdav-access.md) 用https://localhost:4502上的WebDAV存取URL，將下載的mywebsite.zip `static.css` 檔 `images` 案中的範例檔案和資料夾複製到資料 `/etc/designs/mywebsite` 夾中。

   ![chlimage_1-28](assets/chlimage_1-28.png)

### 建立Contentpage模板、元件和指令碼{#creating-the-contentpage-template-component-and-script}

在本節中，您會建立下列項目：

* 用於建立範例網站中內容頁面的內容頁面範本
* 用於呈現內容頁面的內容頁面元件
* contentpage指令碼

#### 建立Contentpage模板{#creating-the-contentpage-template}

建立範本以作為網站網頁的基礎。

範本定義新頁面的預設內容。 複雜的網站可能會使用數個範本來建立網站中不同類型的頁面。 在本練習中，所有頁面都以一個簡單範本為基礎。

1. 在CRXDE Lite的資料夾樹中，按一下右鍵`/apps/mywebsite/templates`，然後按一下&#x200B;**Create** > **Create Template**。

1. 在「建立模板」對話框中，鍵入以下值，然後按一下&#x200B;**Next**:

   * **標籤**:contentpage
   * **標題**:我的網站內容頁面範本
   * **說明**:這是我的網站內容頁面範本
   * **資源類型：** mywebsite/components/contentpage

   使用「排名」屬性的預設值。

   ![chlimage_1-21](assets/chlimage_1-29.png)

   資源類型標識呈現頁面的元件。 在這種情況下，使用contentpage模板建立的所有頁面都由`mywebsite/components/contentpage`元件呈現。

1. 要指定可使用此模板的頁面的路徑，請按一下加號按鈕，然後在出現的文本框中鍵入`/content(/.*)?`。 然後，按一下&#x200B;**Next**。

   ![chlimage_1-30](assets/chlimage_1-30.png)

   允許的路徑屬性的值為&#x200B;*規則運算式。* 路徑符合運算式的頁面可使用範本。在這種情況下，規則運算式會符合&#x200B;**/content**&#x200B;資料夾和所有子頁面的路徑。

   當作者在/content下建立頁面時，**contentpage**&#x200B;範本會顯示在可使用範本清單中。

1. 按一下&#x200B;**允許的父項**&#x200B;和&#x200B;**允許的子項**&#x200B;面板中的&#x200B;**下一步**，然後按一下&#x200B;**確定**。 在CRXDE Lite中，按一下&#x200B;**全部保存**。

   ![chlimage_1-31](assets/chlimage_1-31.png)

#### 建立Contentpage元件{#creating-the-contentpage-component}

建立&#x200B;*元件*，用於定義內容並呈現使用contentpage模板的頁面。 元件的位置必須與contentpage模板的Resource Type屬性的值對應。

1. 在CRXDE Lite中，按一下右鍵`/apps/mywebsite/components`，然後按一下&#x200B;**Create** > **Component**。
1. 在&#x200B;**建立元件**&#x200B;對話方塊中，輸入下列屬性值：

   * **標籤**:contentpage
   * **標題**:我的網站內容頁面元件
   * **說明**:這是我的網站內容頁面元件

   ![chlimage_1-32](assets/chlimage_1-32.png)

   新元件的位置為`/apps/mywebsite/components/contentpage`。 此路徑與內容頁面範本的資源類型（減去路徑的初始&#x200B;**`/apps/`**&#x200B;部分）對應。

   此通信會將範本連結至元件，且對網站的正確運作至關重要。

1. 按一下&#x200B;**Next**&#x200B;直到對話框的「允許的子項」面板出現，然後按一下&#x200B;**OK**。 在CRXDE Lite中，按一下&#x200B;**全部保存**。

   現在的結構如下：

   ![chlimage_1-33](assets/chlimage_1-33.png)

#### 開發Contentpage元件指令碼{#developing-the-contentpage-component-script}

將程式碼新增至contentpage.jsp指令碼以定義頁面內容。

1. 在CRXDE Lite中，開啟`/apps/mywebsite/components/contentpage`中的`contentpage.jsp`檔案。 依預設，檔案包含下列程式碼：

   ```java
   <%--
   
     My Website Content Page Component component.
   
     This is My Website Content Page Component.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
       /* TODO add you code here */
   %>
   ```

1. 複製下列程式碼，並將其貼到預設程式碼之後的contentpage.jsp中：

   ```java
   <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
       pageEncoding="ISO-8859-1"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "https://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
   <title>My title</title>
   </head>
   <body>
   <div>My body</div>
   </body>
   </html>
   ```

1. 按一下「**儲存全部**」以儲存變更。

### 建立網站頁面和內容頁面{#creating-your-website-page-and-content-pages}

在本節中，您將建立以下所有頁面均使用內容頁面範本：我的網站，英文、產品、服務和客戶。

1. 在AEM歡迎頁面([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))上，按一下「網站」。

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. 在資料夾樹中，選擇&#x200B;**Websites**&#x200B;資料夾，然後按一下&#x200B;**New** > **New Page**。
1. 在&#x200B;**建立頁面**&#x200B;視窗中，輸入以下內容：

   * 標題: `My Website`
   * 名稱: `mywebsite`
   * 選擇`My Website Content Page Template`

   ![chlimage_1-35](assets/chlimage_1-35.png)

1. 按一下&#x200B;**建立**。在資料夾樹中，選擇&#x200B;**/Websites/My Website**&#x200B;頁，然後按一下&#x200B;**New** > **New Page**。
1. 在「建立頁面」對話方塊中，輸入下列屬性值，然後按一下「建立」：

   * 標題：英文
   * 名稱：en
   * 選擇「我的網站內容」頁面模板

1. 在資料夾樹中，選擇&#x200B;**/Websites/My Website/English**&#x200B;頁，然後按一下&#x200B;**New**> **New Page**。
1. 在&#x200B;**建立頁面**&#x200B;對話方塊中，輸入以下屬性值，然後按一下&#x200B;**建立**:

   * 標題：產品
   * 選擇「我的網站內容」頁面模板

1. 在資料夾樹中，選擇&#x200B;**/Websites/My Website/English**&#x200B;頁，然後按一下&#x200B;**New** > **New Page**。
1. 在&#x200B;**建立頁面**&#x200B;對話方塊中，輸入以下屬性值，然後按一下&#x200B;**建立**:

   * 標題：服務
   * 選擇「我的網站內容」頁面模板

1. 在資料夾樹中，選擇&#x200B;**/Websites/My Website/English**&#x200B;頁，然後按一下&#x200B;**New** > **New Page**。
1. 在&#x200B;**建立頁面**&#x200B;對話方塊中，輸入以下屬性值，然後按一下&#x200B;**建立**:

   * 標題：客戶
   * 選擇「我的網站內容」頁面模板

   您的結構如下所示：

   ![chlimage_1-36](assets/chlimage_1-36.png)

1. 若要將您的頁面連結至mywebsite設計，請在CRXDE Lite中選取`/content/mywebsite/en/jcr:content`節點。 在「屬性」索引標籤中，為新屬性鍵入以下值，然後按一下「添加」：

   * 名稱：cq:designPath
   * 類型：字串
   * 值：/etc/designs/mywebsite

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 在新的Web瀏覽器頁簽或窗口中，開啟[https://localhost:4502/content/mywebsite/en/products.html](https://localhost:4502/content/mywebsite/en/products.html)以查看「產品」頁：

   ![chlimage_1-38](assets/chlimage_1-38.png)

### 增強Contentpage指令碼{#enhancing-the-contentpage-script}

本節說明如何使用AEM Foundation元件指令碼以及撰寫您自己的指令碼來增強contentpage指令碼。

**Products**&#x200B;頁面如下所示：

![chlimage_1](assets/chlimage_1.jpeg)

#### 使用Foundation頁面指令碼{#using-the-foundation-page-scripts}

在本練習中，您可以設定頁面元件，使其超類型為AEM頁面元件。 由於元件會繼承其超類型的功能，因此您的pagecontent會繼承Page元件的指令碼和屬性。

例如，在元件JSP代碼中，可以參照超類型元件提供的指令碼，就像它們包含在元件中一樣。

1. 在CRXDE Lite中，將屬性新增至`/apps/mywebsite/components/contentpage`節點。

   1. 選擇`/apps/mywebsite/components/contentpage`節點。
   1. 在「屬性」頁簽的底部，鍵入以下屬性值，然後按一下「添加」：

      * **名稱：** sling:resourceSuperType
      * **類型：** 字串
      * **值：** foundation/components/page
   1. 按一下「全部儲存」 。


1. 開啟`/apps/mywebsite/components/contentpage`下的`contentpage.jsp`檔案，並使用下列程式碼取代現有程式碼：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" contentType="text/html; charset=utf-8" %><%
   %><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
   <html>
   <cq:include script="head.jsp"/>
   <cq:include script="body.jsp"/>
   </html>
   ```

1. 儲存您的變更。
1. 在瀏覽器中，重新載入產品頁面。 如下所示：

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

   開啟頁面來源，查看head.jsp和body.jsp指令碼產生的javascript和HTML元素。 當您開啟頁面時，下列指令碼片段會開啟Sidekick:

   ```java
   CQ.WCM.launchSidekick("/content/mywebsite/en/products",
               {propsDialog: "/libs/foundation/components/page/dialog",
                  locked: false locked: false
                });
   ```

#### 使用您自己的指令碼{#using-your-own-scripts}

在本節中，您可以建立數個指令碼，每個指令碼都會產生頁面內文的一部分。 然後，在pagecontent元件中建立body.jsp檔案，以覆寫AEM Page元件的body.jsp。 在body.jsp檔案中，您包含的指令碼會產生頁面內文的不同部分。

**提示：** 如果元件包含的檔案與元件超類型中的檔案具有相同名稱和相對位置，則稱為覆蓋 **。

1. 在CRXDE Lite中，在`/apps/mywebsite/components/contentpage`下建立檔案`left.jsp`:

   1. 按一下右鍵節點`/apps/mywebsite/components/contentpage`，然後選擇**Create **，然後選擇&#x200B;**Create File**。

   1. 在視窗中，輸入`left.jsp`作為&#x200B;**名稱**，然後按一下&#x200B;**確定**。

1. 編輯檔案`left.jsp`以移除現有內容，並以下列程式碼取代：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="left">
   <div>logo</div>
   <div>newslist</div>
   <div>search</div>
   </div>
   ```

1. 儲存變更。
1. 在CRXDE Lite中，在`/apps/mywebsite/components/contentpage`下建立檔案`center.jsp`:

   1. 按一下右鍵節點`/apps/mywebsite/components/contentpage`，選擇&#x200B;**建立**，然後選擇&#x200B;**建立檔案**。

   1. 在對話框中，鍵入`center.jsp`作為&#x200B;**名稱**，然後按一下&#x200B;**確定**。

1. 編輯檔案`center.jsp`以移除現有內容，並使用下列程式碼加以取代：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="center">
   <div>trail</div>
   <div>title</div>
   <div>parsys</div>
   </div>
   ```

1. 儲存變更。
1. 在CRXDE Lite中，在`/apps/mywebsite/components/contentpage`下建立檔案`right.jsp`:

   1. 按一下右鍵節點`/apps/mywebsite/components/contentpage`，選擇&#x200B;**建立**，然後選擇&#x200B;**建立檔案**。

   1. 在對話框中，鍵入`right.jsp`作為&#x200B;**名稱**，然後按一下&#x200B;**確定**。

1. 編輯檔案`right.jsp`以移除現有內容，並以下列程式碼取代：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="right">
   <div>iparsys</div>
   </div>
   ```

1. 儲存變更。
1. 在CRXDE Lite中，在`/apps/mywebsite/components/contentpage`下建立檔案`body.jsp`:
1. 編輯檔案`body.jsp`以移除現有內容，並以下列程式碼取代：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><body>
   <div id="CQ">
   <div class="topnav">topnav</div>
   <div class="content">
   <cq:include script="left.jsp" />
   <cq:include script="center.jsp" />
   <cq:include script="right.jsp" />
   </div>
   <div class="footer">
   <div class="toolbar">toolbar</div>
   </div>
   </div>
   </body>
   ```

1. 儲存變更。
1. 在瀏覽器中，重新載入產品頁面。 如下所示：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 建立頂級導航元件{#creating-the-top-navigation-component}

在此區段中，您會建立元件，顯示網站所有頂層頁面的連結，以方便導覽。 此元件內容會顯示在使用contentpage模板建立的所有頁面的頂部。

在頂端導覽元件(topnav)的第一版中，導覽項目僅為文字連結。 在第二版中，您使用影像導覽連結實作topnav。

您的頂端導覽如下所示：

![chlimage_1-39](assets/chlimage_1-39.png)

#### 建立頂級導航元件{#creating-the-top-navigation-component-1}

1. 在CRXDE Lite中，按一下右鍵`/apps/mywebsite/components`，選擇&#x200B;**Create**，然後選擇&#x200B;**Create Component**。
1. 在&#x200B;**建立元件**&#x200B;窗口中，輸入以下內容：

   * **標籤**:  `topnav`

   * **標題**: `My Top Navigation Component`

   * **說明**: `This is My Top Navigation Component`

1. 按一下&#x200B;**Next**&#x200B;直到到達您按一下&#x200B;**OK**&#x200B;的最後一個窗口。 儲存您的變更。

#### 使用文本連結{#creating-the-top-navigation-script-with-textual-links}建立頂層導航指令碼

將呈現指令碼新增至頂端導覽，以產生子頁面的文字連結：

1. 在CRXDE Lite中，開啟`/apps/mywebsite/components/topnav`下的檔案`topnav.jsp`。
1. 複製並貼上下列程式碼，取代原有的程式碼：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
           com.day.text.Text,
           com.day.cq.wcm.api.PageFilter, com.day.cq.wcm.api.Page" %><%
       /* get starting point of navigation */
       Page navRootPage = currentPage.getAbsoluteParent(2);
       if (navRootPage == null && currentPage != null) {
       navRootPage = currentPage;
       }
       if (navRootPage != null) {
           Iterator<Page> children = navRootPage.listChildren(new PageFilter(request));
           while (children.hasNext()) {
               Page child = children.next();
               %><a href="<%= child.getPath() %>.html"><%=child.getTitle() %></a><%
           }
       }
   %>
   ```

#### 在內容頁面元件{#including-top-navigation-in-the-contentpage-component}中包括頂端導覽

若要在您的內容頁面元件中納入topnav:

1. 在CRXDE Lite中，開啟`/apps/mywebsite/components/contentpage`下的`body.jsp`並取代：

   ```xml
   <div class="topnav">topnav</div>
   ```

   替換為:

   ```xml
   <cq:include path="topnav" resourceType="mywebsite/components/topnav" />
   ```

1. 儲存變更。
1. 在您的瀏覽器中，重新載入產品頁面。 頂端導覽會顯示如下：

   ![chlimage_1-40](assets/chlimage_1-40.png)

#### 使用字幕{#enhancing-pages-with-subtitles}增強頁面

「頁面」元件定義屬性，可讓您為頁面提供字幕。 新增提供頁面內容相關資訊的字幕。

1. 在瀏覽器中，開啟&#x200B;**Products**&#x200B;頁面。
1. 在Sidekick **Page**&#x200B;標籤上，按一下&#x200B;**Page Properties**。
1. 在對話框的「基本」頁簽上，展開&#x200B;**更多標題和說明，**，並針對&#x200B;**字幕**&#x200B;屬性，鍵入&#x200B;**我們做的**。 按一下&#x200B;**「確定」**。
1. 重複上述步驟，將關於我們的服務&#x200B;**的字幕**&#x200B;添加到&#x200B;**服務**&#x200B;頁面。
1. 重複上述步驟，將我們獲得的&#x200B;**信任**&#x200B;客戶&#x200B;**頁添加到**&#x200B;頁。

   **提示：** 在CRXDE Lite中，選擇/content/mywebsite/en/products/jcr:content節點，以查看子標題屬性被添加。

#### 使用影像連結{#enhance-top-navigation-by-using-image-links}增強頂端導覽

增強頂端導覽元件的轉譯指令碼，將影像連結而非超文字用於導覽控制項。 該影像包括連結目標的標題和字幕。

本練習示範[Sling要求處理](/help/sites-developing/the-basics.md#sling-request-processing)。 topnav.jsp指令碼被修改為調用動態生成用於頁面導航連結的影像的指令碼。 在本練習中，Sling會剖析影像來源檔案的URL，以判斷用於轉譯影像的指令碼。

例如，連結至產品頁面的影像連結來源可能是https://localhost:4502/content/mywebsite/en/products.navimage.png。 Sling會剖析此URL以判斷資源類型，以及用來轉譯資源的指令碼：

1. Sling會決定要設為`/content/mwebysite/en/products.png.`的資源路徑
1. Sling會將此路徑與`/content/mywebsite/en/products`節點相符。
1. Sling會將此節點的`sling:resourceType`設為`mywebsite/components/contentpage`。

1. Sling會在此元件中找出最符合URL選取器(`navimage`)和檔案名稱副檔名(`png`)的指令碼。

在本練習中，Sling會將這些URL與您建立的/apps/mywebsite/components/contentpage/navimage.png.java指令碼相符。

1. 在「CRXDE Lite」中，開啟`/apps/mywebsite/components/topnav.`下方的`topnav.jsp`「找出錨點元素的內容」（第14行）:

   ```xml
   <%=child.getTitle() %>
   ```

1. 使用下列程式碼取代錨點內容：

   ```xml
   <img alt="<%= child.getTitle() %>" src="<%= child.getPath() %>.navimage.png">
   ```

1. 儲存變更。
1. 按一下右鍵`/apps/mywebsite/components/contentpage`節點，然後按一下&#x200B;**Create** > **Create File**。
1. 在&#x200B;**建立檔案**&#x200B;窗口中，鍵入&#x200B;**名稱**`navimage.png.java`。

   .java檔案名稱副檔名會向Sling指出應使用Apache Sling Scripting Java支援來編譯指令碼並建立Servlet。

1. 將以下代碼複製到`navimage.png.java.`中。該代碼擴展了AbstractImageServlet類：

   * [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) AbstractImageServlet會建立ImageContext物件，用於儲存目前資源的屬性。
   * 資源的上層頁面從ImageContext物件中擷取。 然後獲得頁面標題和字幕。
   * [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ImageHelper.html) ImageHelperis用於從網站設計的navimage_bg.jpg檔案、頁面標題和頁面子標題中生成影像。

   ```java
   package apps.mywebsite.components.contentpage;
   
   import java.awt.Color;
   import java.awt.Paint;
   import java.awt.geom.Rectangle2D;
   
   import java.io.IOException;
   import javax.jcr.RepositoryException;
   
   import com.day.cq.wcm.api.Page;
   import com.day.cq.wcm.api.PageManager;
   import com.day.cq.wcm.api.components.Component;
   import com.day.cq.wcm.api.designer.Designer;
   
   import com.day.cq.commons.SlingRepositoryException;
   import com.day.cq.wcm.commons.WCMUtils;
   import com.day.cq.wcm.commons.AbstractImageServlet;
   import com.day.cq.commons.ImageHelper;
   
   import com.day.image.Font;
   import com.day.image.Layer;
   
   import org.apache.sling.api.SlingHttpServletRequest;
   import org.apache.sling.api.SlingHttpServletResponse;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
   
   /**
     * Renders the navigation image
     */
   public class navimage_png extends AbstractImageServlet {
   
         protected Layer createLayer(ImageContext ctx)
                throws RepositoryException, IOException {
            PageManager pageManager = ctx.resolver.adaptTo(PageManager.class);
            Page currentPage = pageManager.getContainingPage(ctx.resource);
   
            /* constants for image appearance */
            int scale = 6;
            int paddingX = 24;
            int paddingY = 24;
            Color bgColor = new Color(0x004a565c, true);
   
            /* obtain the page title */
            String title = currentPage.getTitle();
            if (title == null) {
                title = currentPage.getName();
            }
   
            /* format the title text */
            title = title.toUpperCase();
            Paint titleColor = Color.WHITE;
            Font titleFont = new Font("Myriad Pro", 10 * scale, Font.BOLD);
            int titleBase = 10 * scale;
   
            /* obtain and format the page subtitle */
            String subtitle = currentPage.getProperties().get("subtitle", "");
            Paint subtitleColor = new Color(0xffa9afb1, true);
            Font subTitleFont = new Font("Tahoma", 7);
            int subTitleBase = 20;
   
            /* create a layer that contains the background image from the mywebsite design */
            Designer dg = ctx.resolver.adaptTo(Designer.class);
            String imgPath = new String(dg.getDesignPath(currentPage)+"/images/navimage_bg.jpg");
            Layer bg = ImageHelper.createLayer(ctx.resolver.resolve(imgPath));
   
            /* draw the title text (4 times bigger) */
            Rectangle2D titleExtent = titleFont.getTextExtent(0, 0, 0, 0, title, Font.ALIGN_LEFT, 0, 0);
            Rectangle2D subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
   
            /* ensure subtitleExtent is wide enough */
            if ( subtitle.length() > 0 ) {
                int titleWidth = (int)titleExtent.getWidth() / scale;
                if ( subtitleExtent.getWidth() > titleWidth && subtitleExtent.getWidth() + 2 * paddingX >
    bg.getWidth() ) {
                    int charWidth = (int)subtitleExtent.getWidth() / subtitle.length();
                    int maxWidth = (bg.getWidth() > titleWidth + 2  * paddingX ? bg.getWidth() - 2 * paddingX : titleWidth);
                    int len = (maxWidth - ( 2 * charWidth) ) / charWidth;
                    subtitle = subtitle.substring(0, len) + "...";
                    subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
                }
            }
            int width = Math.max((int) titleExtent.getWidth(), (int) subtitleExtent.getWidth());
           /* create the text layer */
            Layer text = new Layer(width, (int) titleExtent.getHeight() + 40, new Color(0x01ffffff, true));
            text.setPaint(titleColor);
            text.drawText(0, titleBase, 0, 0, title, titleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            text.resize(text.getWidth() / scale, text.getHeight() / scale);
            text.setX(0);
            text.setY(0);
   
            if (subtitle.length() > 0) {
                /* draw the subtitle normal sized */
                text.setPaint(subtitleColor);
                text.drawText(0, subTitleBase, 0, 0, subtitle, subTitleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            }
   
            /* merge the image and text layers */
            text.setY(paddingY);
            text.setX(paddingX);
            text.setBackgroundColor(bgColor);
   
            int bgWidth = bg.getWidth();
            if ( text.getWidth() + 2 * paddingX > bgWidth ) {
                bgWidth = text.getWidth() + 2 * paddingX;
                bg.resize(bgWidth, bg.getHeight());
            }
            bg.merge(text);
   
            return bg;
        }
    }
   ```

1. 儲存變更。
1. 在瀏覽器中，重新載入產品頁面。 頂端導覽現在顯示如下：

   ![screen_shot_2012-03-07at10047pm](assets/screen_shot_2012-03-07at10047pm.png)

### 建立清單子元件{#creating-the-list-children-component}

建立listchildren元件，該元件生成包含頁面標題、說明和日期的頁面連結清單（例如，產品頁面）。 連結會鎖定目前頁面的子頁面，或元件對話方塊中指定的根頁面。

![chlimage_1-41](assets/chlimage_1-41.png)

#### 建立產品頁面{#creating-product-pages}

在產品頁面下方建立兩個頁面。 請針對說明兩個特定產品的每個頁面，設定標題、說明和日期。

1. 在「網站」頁的資料夾樹中，選擇「網站/我的網站/英語/產品」項，然後按一下「新建」>「新建頁面」。
1. 在對話方塊中輸入下列屬性值，然後按一下建立：

   * 標題：產品1.
   * 名稱：product1。
   * 選擇「我的網站內容」頁面模板

1. 使用下列屬性值，在「產品」下方建立另一個頁面：

   * 標題：產品2
   * 名稱：product2
   * 選擇「我的網站內容」頁面模板

1. 在CRXDE Lite中，設定產品1頁面的說明和日期：

   1. 選擇`/content/mywebsite/en/products/product1/jcr:content`節點。
   1. 在&#x200B;**屬性**&#x200B;標籤中，輸入以下值：

      * 名稱: `jcr:description`
      * 類型: `String`
      * 值: `This is a description of the Product 1!.`
   1. 按一下&#x200B;**「新增」**。
   1. 在&#x200B;**Properties**&#x200B;標籤中，使用以下值建立另一個屬性：

      * 名稱：日期
      * 類型：字串
      * 值：02/14/2008
      * 按一下「新增」。
   1. 按一下「全部儲存」 。



1. 在CRXDE Lite中，設定產品2頁面的說明和日期：

   1. 選取/content/mywebsite/en/products/product2/jcr:content節點。
   1. 在&#x200B;**屬性**&#x200B;標籤中，輸入以下值：

      * 名稱：jcr:description
      * 類型：字串
      * 值：這是產品2！的說明。
   1. 按一下&#x200B;**「新增」**。
   1. 在相同的文字方塊中，以下列值取代先前的值：

      * 名稱：日期
      * 類型：字串
      * 值：05/11/2012
      * 按一下「新增」。
   1. 按一下「全部儲存」 。



#### 建立清單子元件{#creating-the-list-children-component-1}

要建立listchildren元件，請執行以下操作：

1. 在CRXDE Lite中，按一下右鍵`/apps/mywebsite/components`，選擇&#x200B;**Create**，然後選擇&#x200B;**Create Component**。
1. 在對話方塊中輸入下列屬性值，然後按一下下一步：

   * 標籤：列出孩子。
   * 標題：我的清單子項元件。
   * 說明：這是我的Listchildren元件。

1. 繼續按「下一步」，直到出現「允許的子項」面板，然後按一下「確定」。

#### 建立清單子指令碼{#creating-the-list-children-script}

開發listchildren元件的指令碼。

1. 在CRXDE Lite中，開啟`/apps/mywebsite/components/listchildren`下的檔案`listchildren.jsp`。
1. 以下列程式碼取代預設程式碼：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
            com.day.cq.wcm.api.PageFilter"%><%
        /* Create a new Page object using the path of the current page */
         String listroot = properties.get("listroot", currentPage.getPath());
        Page rootPage = pageManager.getPage(listroot);
        /* iterate through the child pages and gather properties */
        if (rootPage != null) {
            Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
            while (children.hasNext()) {
                Page child = children.next();
                String title = child.getTitle() == null ? child.getName() : child.getTitle();
                String date = child.getProperties().get("date","");
                %><div class="item">
                <a href="<%= child.getPath() %>.html"><b><%= title %></b></a>
                <span><%= date %></code><br>
                <%= child.getProperties().get("jcr:description","") %><br>
                </div><%
            }
        }
    %>
   ```

1. 儲存變更。

#### 建立清單子對話框{#creating-the-list-children-dialog}

建立用於配置listchildren元件屬性的對話框。

1. 在listchildren元件下建立對話框節點：

   1. 在CRXDE Lite中，按一下右鍵`/apps/mywebsite/components/listchildren`節點，然後按一下&#x200B;**Create** > **Create Dialog**。

   1. 在對話方塊中，輸入以下屬性值，然後按一下確定

      * **標籤**:  `dialog`

      * **標題**: `Edit Component` 然後按一 **下確定**。

   ![screen_shot_2012-03-07at45818pm](assets/screen_shot_2012-03-07at45818pm.png)

   具有下列屬性：

   ![screen_shot_2012-03-07at50415pm](assets/screen_shot_2012-03-07at50415pm.png)

1. 選擇`/apps/mywebsite/components/listchildren/dialog/items/items/tab1`節點。
1. 在「屬性」頁簽中，將&#x200B;**title**&#x200B;屬性的值更改為`List Children`

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 選擇tab1節點，然後按一下「建立」>「建立節點」，輸入以下屬性值，然後按一下「確定」：

   * 名稱：項目
   * 類型：cq:WidgetCollection

   ![screen_shot_2012-03-07at51018pm](assets/screen_shot_2012-03-07at51018pm.png)

1. 使用以下屬性值在項節點下建立節點：

   * 名稱：李斯特羅
   * 類型：cq:Widget

   ![screen_shot_2012-03-07at51031pm](assets/screen_shot_2012-03-07at51031pm.png)

1. 新增清單節點的屬性，以將其設定為文字欄位。 下表中的每一列代表一個屬性。 完成後，按一下「全部儲存」 。

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | fieldLabel | 字串 | 清單根的路徑 |
   | 名稱 | 字串 | 。/listroot |
   | xtype | 字串 | textfield |

   ![screen_shot_2012-03-07at51433pm](assets/screen_shot_2012-03-07at51433pm.png)

#### 在Contentpage元件{#including-list-children-in-the-contentpage-component}中包括清單子項

若要將listchildren元件包含在內容頁面元件中，請繼續如下：

1. 在「CRXDE Lite」中，開啟`/apps/mywebsite/components/contentpage`下的檔案`left.jsp`，然後找到以下代碼（第4行）:

   ```xml
   <div>newslist</div>
   ```

1. 以下列程式碼取代該程式碼：

   ```xml
   <cq:include path="newslist" resourceType="mywebsite/components/listchildren" />
   ```

1. 儲存變更。

#### 在{#viewing-list-children-in-a-page}頁中查看清單子項

要查看此元件的完整操作，可以查看「產品」頁：

* 當未定義上層頁面（「清單根路徑」）時。
* 定義上層頁面時（「清單根路徑」）。

1. 在您的瀏覽器中，重新載入產品頁面。 listchildren元件顯示如下：

   ![chlimage_1-43](assets/chlimage_1-43.png)

1. ![chlimage_1-44](assets/chlimage_1-44.png)

1. 作為清單根的路徑，請輸入：`/content/mywebsite/en`。 按一下「確定」。您頁面上的listchildren元件現在如下所示：

   ![chlimage_1-45](assets/chlimage_1-45.png)

### 建立徽標元件{#creating-the-logo-component}

建立元件，以顯示公司標誌並提供網站首頁的連結。 元件包含設計模式對話方塊，以便將屬性值儲存在網站設計(/etc/designs/mywebsite)中：

* 屬性值會套用至元件的所有例項，這些例項會新增至使用設計的頁面。
* 屬性可使用使用設計之頁面上元件的任何例項來設定。

您的設計模式對話方塊包含用於設定影像和連結路徑的屬性。 標誌元件將放置在網站中所有頁面的左上方。

如下所示：

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Adobe Experience Manager提供功能更全的標誌元件(`/libs/foundation/components/logo`)。

#### 建立徽標元件節點{#creating-the-logo-component-node}

要建立徽標元件，請執行以下步驟：

1. 在「CRXDE Lite」中，按一下右鍵/apps/mywebsite/components，選擇&#x200B;**Create**，然後選擇&#x200B;**Create Component**。
1. 在「建立元件」對話框中輸入以下屬性值，然後按一下「下一步」：

   * 標籤: `logo`.
   * 標題: `My Logo Component`.
   * 說明: `This is My Logo Component`.

1. 按一下「下一步」，直到到達對話框的最終面板，然後按一下「**確定**」。

#### 建立徽標指令碼{#creating-the-logo-script}

本節說明如何建立指令碼，以顯示帶有首頁連結的標誌影像。

1. 在CRXDE Lite中，開啟`/apps/mywebsite/components/logo`下的檔案`logo.jsp`。
1. 下列程式碼會建立網站首頁的連結，並新增標誌影像的參考。 將代碼複製到`logo.jsp`:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.text.Text,
                      com.day.cq.wcm.foundation.Image,
                      com.day.cq.commons.Doctype" %><%
       /* obtain the path for home */
       long absParent = currentStyle.get("absParent", 2L);
       String home = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);
       /* obtain the image */
       Resource res = currentStyle.getDefiningResource("imageReference");
       if (res == null) {
           res = currentStyle.getDefiningResource("image");
       }
       /* if no image use text link, otherwise draw the image */
       %>
   <a href="<%= home %>.html"><%
       if (res == null) {
           %>Home<%
       } else {
           Image img = new Image(res);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out);
       }
       %></a>
   ```

1. 儲存變更。

#### 建立徽標設計對話框{#creating-the-logo-design-dialog}

在「設計」模式中建立用於配置徽標元件的對話框。 設計模式對話框節點必須命名為`design_dialog`。

1. 在徽標元件下建立對話框節點：

   1. 按一下右鍵`/apps/mywebsite/components/logo`節點，然後按一下&#x200B;**Create** > **Create Dialog**。

   1. 鍵入以下屬性值，然後按一下「確定」：

      * **標籤：** `design_dialog`

      * **標題:** `Logo (Design)`

1. 按一下右鍵design_dialog分支中的tab1節點，然後按一下「刪除」。 按一下「全部儲存」 。
1. 在`design_dialog/items/items`節點下，建立類型`cq:Widget`的名為`img`的新節點。 新增下列屬性，然後按一下「儲存全部」 :

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | fileNameParameter | 字串 | 。/imageName |
   | fileReferenceParameter | 字串 | 。/imageReference |
   | 名稱 | 字串 | 。/影像 |
   | 標題 | 字串 | 影像 |
   | xtype | 字串 | html5smartimage |

   ![chlimage_1-47](assets/chlimage_1-47.png)

#### 建立徽標呈現指令碼{#creating-the-logo-render-script}

建立擷取標誌影像並將其寫入頁面的指令碼。

1. 按一下右鍵徽標元件節點，然後按一下「建立」>「建立檔案」以建立名為img.GET.java的指令碼檔案。
1. 開啟檔案，將下列程式碼複製到檔案中，然後按一下「儲存全部」 :

```java
package apps.mywebsite.components.logo;

import java.io.IOException;
import java.io.InputStream;

import javax.jcr.RepositoryException;
import javax.jcr.Property;
import javax.servlet.http.HttpServletResponse;

import com.day.cq.wcm.foundation.Image;
import com.day.cq.wcm.commons.RequestHelper;
import com.day.cq.wcm.commons.WCMUtils;
import com.day.cq.wcm.commons.AbstractImageServlet;
import com.day.cq.commons.SlingRepositoryException;
import com.day.image.Layer;
import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ValueMap;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

/**
 * Renders an image
 */
public class img_GET extends AbstractImageServlet {

    protected Layer createLayer(ImageContext c)
            throws RepositoryException, IOException {
        /* don't create the layer yet. handle everything later */
        return null;
    }

    protected void writeLayer(SlingHttpServletRequest req,
                              SlingHttpServletResponse resp,
                              ImageContext c, Layer layer)
            throws IOException, RepositoryException {

        Image image = new Image(c.resource);
        image.setItemName(Image.NN_FILE, "image");
        image.setItemName(Image.PN_REFERENCE, "imageReference");
        if (!image.hasContent()) {
            resp.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }
        /* get pure layer */
        layer = image.getLayer(false, false, false);

        /* do not re-encode layer, just spool */
        Property data = image.getData();
        InputStream in = data.getStream();
        resp.setContentLength((int) data.getLength());
        String contentType = image.getMimeType();
        if (contentType.equals("application/octet-stream")) {
            contentType=c.requestImageType;
        }
        resp.setContentType(contentType);
        IOUtils.copy(in, resp.getOutputStream());
        in.close();

        resp.flushBuffer();
    }
}
```

#### 將徽標元件添加到Contentpage元件{#adding-the-logo-component-to-the-contentpage-component}

1. 在CRXDE Lite中，開啟`/apps/mywebsite/components/contentpage file`下的`left.jsp`，並找出下列程式碼行：

   ```xml
   <div>logo</div>
   ```

1. 以下列程式碼行取代該程式碼：

   ```xml
   <cq:include path="logo" resourceType="mywebsite/components/logo" />
   ```

1. 儲存變更。
1. 在瀏覽器中，重新載入產品頁面。 標誌如下所示，不過目前只顯示基礎連結：

   ![chlimage_1-48](assets/chlimage_1-48.png)

#### 在{#setting-the-logo-image-in-a-page}頁中設定徽標影像

本節說明如何使用設計模式對話方塊，將影像設為標誌。

1. 在瀏覽器中開啟「產品」頁面時，按一下Sidekick底部的「設計」按鈕以進入設計模式。

   ![](do-not-localize/chlimage_1-1.png)

1. 在徽標欄的設計中，按一下編輯以使用對話框來編輯徽標元件的設定。
1. 在對話方塊中，按一下「影像」標籤面板中的，瀏覽您從mywebsite.zip檔案擷取的logo.png影像，然後按一下「確定」。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 按一下Sidekick標題列上的三角形以返回「編輯」模式。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 在CRXDE Lite中，轉到以下節點以查看所儲存的屬性值：

   `/etc/designs/mywebsite/jcr:content/contentpage/logo`

### 包括階層連結元件{#including-the-breadcrumb-component}

在本節中，您包含階層連結（軌跡）元件，此元件是基礎元件之一。

1. 在CRXDE Lite中，瀏覽至`/apps/mywebsite/components/contentpage`，開啟檔案`center.jsp`並取代：

   ```java
   <div>trail</div>
   ```

   替換為:

   ```xml
   <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
   ```

1. 儲存變更。
1. 在瀏覽器中，重新載入&#x200B;**產品1**&#x200B;頁面。 軌跡元件如下所示：

   ![chlimage_1-50](assets/chlimage_1-50.png)

### 包括標題元件{#including-the-title-component}

在本節中，您包含標題元件，這是其中一個基礎元件。

1. 在CRXDE Lite中，瀏覽至`/apps/mywebsite/components/contentpage`，開啟檔案`center.jsp`並取代：

   ```xml
   <div>title</div>
   ```

   替換為:

   ```xml
   <cq:include path="title" resourceType="foundation/components/title" />
   ```

1. 儲存變更。
1. 在瀏覽器中，重新載入產品頁面。 標題元件的外觀如下：

   ![chlimage_1-51](assets/chlimage_1-51.png)

   **注意**:您可以在編輯模式中設定不同的標題和類型/大小。

### 包括段落系統元件{#including-the-paragraph-system-component}

段落制度(parsys)是網站的重要組成部分，因為它管理著段落清單。 它可讓作者新增段落元件至頁面並提供結構。

將parsys元件（其中一個基礎元件）新增至內容頁面元件。

1. 在CRXDE Lite中，瀏覽至`/apps/mywebsite/components/contentpage`，開啟檔案`center.jsp`並找出下列程式碼行：

   ```xml
   <div>parsys</div>
   ```

1. 使用下列程式碼取代該行程式碼，然後儲存變更：

   ```xml
   <cq:include path="par" resourceType="foundation/components/parsys" />
   ```

1. 在瀏覽器中，重新整理產品頁面。 它現在有parsys元件，如下所示：

   ![chlimage_1-52](assets/chlimage_1-52.png)

### 建立影像元件{#creating-the-image-component}

建立在段落系統中顯示影像的元件。 為了節省時間，系統會將影像元件建立為標誌元件的復本，並變更一些屬性。

>[!NOTE]
>
>Adobe Experience Manager提供功能更全的影像元件(`/libs/foundation/components/image`)。

#### 建立影像元件{#creating-the-image-component-1}

1. 按一下右鍵`/apps/mywebsite/components/logo`節點，然後按一下「複製」。
1. 按一下右鍵`/apps/mywebsite/components`節點，然後按一下「貼上」。
1. 按一下右鍵`Copy of logo`節點，按一下「更名」，刪除現有文本並鍵入`image`。

1. 選擇`image`元件節點，並更改以下屬性值：

   * `jcr:title:` 我的影像元件。
   * `jcr:description`:這是我的影像元件。

1. 將屬性添加到`image`節點，其屬性值如下：

   * 名稱：componentGroup
   * 類型：字串
   * 值：MyWebsite

1. 在`image`節點下方，將`design_dialog`節點重新命名為`dialog`。

1. 將`logo.jsp`更名為`image.jsp.`

1. 開啟img.GET.java，並將包更改為`apps.mywebsite.components.image`。

![chlimage_1-53](assets/chlimage_1-53.png)

#### 建立影像指令碼{#creating-the-image-script}

本節說明如何建立影像指令碼。

1. 開啟 `/apps/mywebsite/components/image/` `image.jsp`
1. 使用下列程式碼取代現有程式碼，然後儲存變更：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.cq.commons.Doctype,
                       com.day.cq.wcm.foundation.Image,
                       com.day.cq.wcm.api.components.DropTarget,
                       com.day.cq.wcm.api.components.EditConfig,
                       com.day.cq.wcm.commons.WCMUtils" %><%
    /* global.jsp provides access to the current resource through the resource object */
           Image img = new Image(resource);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out); %>
   ```

1. 儲存變更。

#### 建立影像cq:editConfig節點{#creating-the-image-cq-editconfig-node}

`cq:editConfig`節點類型允許您在編輯元件的屬性時配置元件的某些行為。

在本節中，您使用cq:editConfig節點，可讓您將資產從「內容尋找器」拖曳至影像元件中。

1. 在CRXDE Lite中，在/apps/mywebsite/components/image節點下，建立新節點，如下所示：

   * 名稱：cq:editConfig。
   * 類型：cq:EditConfig。

1. 在節點cq:editConfig下，建立新節點，如下所示：

   * 名稱：cq:dropTargets。
   * 類型：cq:DropTargetConfig。

1. 在節點cq:dropTargets下，建立新節點，如下所示：

   * 名稱：影像。
   * 類型：nt：非結構化。

1. 在CRXDE中，按如下方式設定屬性：

| 名稱 | 類型 | 值 |
|---|---|---|
| 接受 | 字串 | image/(gif) | jpeg | PNG) |
| 個群組 | 字串 | 媒體 |
| propertyName | 字串 | 。/imageReference |

![chlimage_1-54](assets/chlimage_1-54.png)

#### 添加表徵圖{#adding-the-icon}

在本節中，您新增圖示，當該圖示列在Sidekick中時，會顯示在影像元件旁：

1. 在CRXDE Lite中，按一下右鍵檔案`/libs/foundation/components/image/icon.png`，然後選擇&#x200B;**Copy.**
1. 按一下右鍵節點`/apps/mywebsite/components/image`，然後按一下&#x200B;**貼上**，然後按一下&#x200B;**保存全部**。

#### 使用影像元件{#using-the-image-component}

在本節中，您將查看&#x200B;**Products**&#x200B;頁面，並將您的影像元件添加到段落系統中。

1. 在您的瀏覽器中，重新載入&#x200B;**產品**&#x200B;頁面。
1. 在Sidekick中，按一下&#x200B;**design mode**&#x200B;圖示。
1. 按一下「編輯」按鈕，編輯par的設計對話框。
1. 對話方塊中會顯示&#x200B;**允許的元件**&#x200B;清單；導覽至&#x200B;**MyWebsite**，選取&#x200B;**My Image Component**，然後按一下&#x200B;**OK。**
1. 返回&#x200B;**編輯模式。**
1. 連按兩下parsys框架（在&#x200B;**將元件或資產拖曳到此處**&#x200B;上）。 **插入新元件**&#x200B;和&#x200B;**Sidekick**&#x200B;選取器如下所示：

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

### 包括工具欄元件{#including-the-toolbar-component}

在本節中，您包括工具欄元件，該元件是基礎元件之一。

在編輯模式和設計模式中，您有數個選項。

1. 在CRXDE Lite中，導覽至`/apps/mywebsite/components/contentpage`，開啟`body.jsp`檔案並找出下列程式碼：

   ```java
   <div class="toolbar">toolbar</div>
   ```

1. 使用下列程式碼取代該程式碼，然後儲存變更。

   ```java
   <cq:include path="toolbar" resourceType="foundation/components/toolbar"/>
   ```

1. 在「AEM網站」頁面的資料夾樹中，選擇「網站/我的網站/英語」，然後按一下「新建」 > 「新建頁面」。 指定下列屬性值，然後按一下「建立」：

   * 標題：工具列
   * 選擇「我的網站內容」頁面模板

1. 在頁清單中，按一下右鍵工具欄頁，然後按一下屬性。 選擇「在導航中隱藏」，然後按一下「確定」。

   「在導覽中隱藏」選項可防止頁面出現在導覽元件中，例如topnav和listchildren。

1. 在工具列下，建立下列頁面：

   * 聯繫人
   * 意見反應
   * 登入
   * 搜尋

1. 在瀏覽器中，重新載入產品頁面。 如下所示：

   ![chlimage_1-55](assets/chlimage_1-55.png)

### 建立搜索元件{#creating-the-search-component}

在本節中，您需建立元件以搜尋網站上的內容。 此搜尋元件可放置在任何頁面的段落系統中（例如，位於專用搜尋結果頁面上）。

您的搜索輸入框在&#x200B;**English**&#x200B;頁上如下所示：

![chlimage_1-56](assets/chlimage_1-56.png)

#### 建立搜索元件{#creating-the-search-component-1}

1. 在CRXDE Lite中，按一下右鍵`/apps/mywebsite/components`，選擇&#x200B;**Create**，然後選擇&#x200B;**Create Component**。
1. 使用對話方塊來設定元件：

   1. 第一個面板，指定下列屬性值：

      * 標籤：搜尋
      * 標題：我的搜尋元件
      * 說明：這是我的搜索元件
      * 組：MyWebsite
   1. 按「下一步」，然後再按「下一步」。
   1. 在「允許的父項」面板上，按一下+按鈕並鍵入`*/parsys`。
   1. 按「下一步」，然後按一下「確定」。


1. 按一下「全部儲存」 。
1. 複製下列節點並貼到apps/mywebsite/components/search節點：

   * `/libs/foundation/components/search/dialog`
   * &quot; `/libs/foundation/components/search/i18n`

   * `/libs/foundation/components/search/icon.png`

1. 按一下「全部儲存」 。

#### 建立搜索指令碼{#creating-the-search-script}

本節說明如何建立搜索指令碼：

1. 開啟`/apps/mywebsite/components/search/search.jsp`檔案。
1. 將下列程式碼複製到`search.jsp`:

   ```java
   <%@ page import="com.day.cq.wcm.foundation.Search,com.day.cq.tagging.TagManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   %><cq:setContentBundle/><%
       Search search = new Search(slingRequest);
   
       String searchIn = (String) properties.get("searchIn");
       String requestSearchPath = request.getParameter("path");
       if (searchIn != null) {
           /* only allow the "path" request parameter to be used if it
            is within the searchIn path configured */
           if (requestSearchPath != null && requestSearchPath.startsWith(searchIn)) {
               search.setSearchIn(requestSearchPath);
           } else {
               search.setSearchIn(searchIn);
           }
       } else if (requestSearchPath != null) {
           search.setSearchIn(requestSearchPath);
       }
   
       pageContext.setAttribute("search", search);
       TagManager tm = resourceResolver.adaptTo(TagManager.class);
   %><c:set var="trends" value="${search.trends}"/><%
   %><center>
     <form action="${currentPage.path}.html">
       <input size="41" maxlength="2048" name="q" value="${fn:escapeXml(search.query)}"/>
       <input value="<fmt:message key="searchButtonText"/>" type="submit" />
     </form>
   </center>
   <br/>
   <c:set var="result" value="${search.result}"/>
   <c:choose>
     <c:when test="${empty result && empty search.query}">
     </c:when>
     <c:when test="${empty result.hits}">
       <c:if test="${result.spellcheck != null}">
         <p><fmt:message key="spellcheckText"/> <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${result.spellcheck}"/></c:url>"><b><c:out value="${result.spellcheck}"/></b></a></p>
       </c:if>
       <fmt:message key="noResultsText">
         <fmt:param value="${fn:escapeXml(search.query)}"/>
       </fmt:message>
     </c:when>
     <c:otherwise>
       <p class="searchmeta">Results ${result.startIndex + 1} - ${result.startIndex + fn:length(result.hits)} of ${result.totalMatches} for <b>${fn:escapeXml(search.query)}</b>. (${result.executionTime} seconds)</p>
      <br/>
   
     <div class="searchresults">
       <div class="results">
         <c:forEach var="hit" items="${result.hits}" varStatus="status">
           <div class="hit">
           <a href="${hit.URL}">${hit.title}</a>
           <div class="excerpt">${hit.excerpt}</div>
          <div class="hiturl"> ${hit.URL}<c:if test="${!empty hit.properties['cq:lastModified']}"> - <c:catch><fmt:formatDate value="${hit.properties['cq:lastModified'].time}" dateStyle="medium"/></c:catch></c:if> - <a href="${hit.similarURL}"><fmt:message key="similarPagesText"/></a>
           </div></div>
         </c:forEach>
       </div>
         <br/>
   
        <div class="searchRight">
             <c:if test="${fn:length(trends.queries) > 0}">
                 <p><fmt:message key="searchTrendsText"/></p>
                 <div class="searchTrends">
                     <c:forEach var="query" items="${trends.queries}">
                         <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${query.query}"/></c:url>"><span style="font-size:${query.size}px"><c:out value="${query.query}"/></code></a>
                     </c:forEach>
                 </div>
             </c:if>
             <c:if test="${result.facets.languages.containsHit}">
                 <p>Languages</p>
                 <c:forEach var="bucket" items="${result.facets.languages.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value='<%= new java.util.Locale((String) pageContext.getAttribute("bucketValue")).getDisplayLanguage(request.getLocale()) %>'/>
                     <c:choose>
                         <c:when test="${param.language != null}">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.tags.containsHit}">
                 <p>Tags</p>
                 <c:forEach var="bucket" items="${result.facets.tags.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="tag" value="<%= tm.resolve((String) pageContext.getAttribute("bucketValue")) %>"/>
                     <c:if test="${tag != null}">
                         <c:set var="label" value="${tag.title}"/>
                         <c:choose>
                             <c:when test="<%= request.getParameter("tag") != null && java.util.Arrays.asList(request.getParameterValues("tag")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="tag" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                             <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="tag" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                         </c:choose><br/>
                     </c:if>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.mimeTypes.containsHit}">
                 <jsp:useBean id="fileTypes" class="com.day.cq.wcm.foundation.FileTypes"/>
                 <p>File types</p>
                 <c:forEach var="bucket" items="${result.facets.mimeTypes.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value="${fileTypes[bucket.value]}"/>
                     <c:choose>
                         <c:when test="<%= request.getParameter("mimeType") != null && java.util.Arrays.asList(request.getParameterValues("mimeType")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.lastModified.containsHit}">
                 <p>Last Modified</p>
                 <c:forEach var="bucket" items="${result.facets.lastModified.buckets}">
                     <c:choose>
                         <c:when test="${param.from == bucket.from && param.to == bucket.to}">${bucket.value} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/><c:if test="${bucket.from != null}"><cq:addParam name="from" value="${bucket.from}"/></c:if><c:if test="${bucket.to != null}"><cq:addParam name="to" value="${bucket.to}"/></c:if></cq:requestURL>">${bucket.value} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
   
         <c:if test="${fn:length(search.relatedQueries) > 0}">
   
          <br/><br/><div class="related">
           <fmt:message key="relatedSearchesText"/>
           <c:forEach var="rq" items="${search.relatedQueries}">
               <a href="${currentPage.path}.html?q=${rq}"><c:out value="${rq}"/></a>
           </c:forEach></div>
         </c:if>
         </div>
   
         <c:if test="${fn:length(result.resultPages) > 1}">
           <div class="pagination">
               <fmt:message key="resultPagesText"/>
           <c:if test="${result.previousPage != null}">
             <a href="${result.previousPage.URL}"><fmt:message key="previousText"/></a>
           </c:if>
           <c:forEach var="page" items="${result.resultPages}">
             <c:choose>
               <c:when test="${page.currentPage}">${page.index + 1}</c:when>
               <c:otherwise>
                 <a href="${page.URL}">${page.index + 1}</a>
               </c:otherwise>
             </c:choose>
           </c:forEach>
           <c:if test="${result.nextPage != null}">
             <a href="${result.nextPage.URL}"><fmt:message key="nextText"/></a>
           </c:if>
           </div>
         </c:if>
         </div>
   
     </c:otherwise>
   </c:choose>
   ```

1. 儲存變更。

#### 在內容頁面元件{#including-a-search-box-in-the-contentpage-component}中包含搜尋方塊

若要在內容頁面的左側區段加入搜尋輸入方塊，請繼續如下：

1. 在「CRXDE Lite」中，開啟`/apps/mywebsite/components/contentpage`下的檔案`left.jsp`，然後找到以下代碼（第2行）:

   ```xml
   %><div class="left">
   ```

1. 在該行&#x200B;**之前插入以下代碼**:

   ```java
   %><%@ page import="com.day.text.Text"%><%
   %><% String docroot = currentDesign.getPath();
   String home = Text.getAbsoluteParent(currentPage.getPath(), 2);%><%
   ```

1. 找出下列程式碼行：

   ```xml
   <div>search</div>
   ```

1. 使用下列程式碼取代該程式碼，然後儲存變更。

   ```java
   <div class="form_1">
        <form class="geo" action="<%= home %>/toolbar/search.html" id="form" >
             <p>
                  <input class="geo" type="text" name="q"><br>
                  <a href="<%= home %>/toolbar/search.html" class="link_1">advanced search</a>
             </p>
        </form>
   </div>
   ```

1. 在瀏覽器中，重新載入產品頁面。 搜尋元件的外觀如下：

   ![chlimage_1-57](assets/chlimage_1-57.png)

#### 在搜索頁{#including-the-search-component-in-the-search-page}中包括搜索元件

在本節中，將搜索元件添加到段落系統。

1. 在瀏覽器中，開啟「搜尋」頁面。
1. 在Sidekick中，按一下設計模式表徵圖。
1. 在Design of par block（在Search title下）中，按一下Edit。
1. 在對話框中，向下滾動到&#x200B;**我的網站**&#x200B;組，選擇&#x200B;**我的搜索元件**，然後按一下&#x200B;**確定**。
1. 在Sidekick上，按一下三角形以返回編輯模式。
1. 將「我的搜尋元件」從Sidekick拖曳至parsys框架中。 如下所示：

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. 導覽至您的產品頁面。 在輸入框中搜索客戶，然後按Enter鍵。 系統會將您重新導向至「搜尋」頁面。 切換至預覽模式：輸出的格式與以下類似：

   ![chlimage_1-59](assets/chlimage_1-59.png)

### 包括Iparsys元件{#including-the-iparsys-component}

在本節中，您包括繼承段落系統(iparsys)元件，該元件是基礎元件之一。 此元件允許您在父頁上建立段落結構，並讓子頁繼承段落。

對於此元件，可以在編輯模式和設計模式中設定多個參數。

1. 在CRXDE Lite中，導覽至`/apps/mywebsite/components/contentpage`，開啟檔案`right.jsp`並取代：

   ```java
   <div>iparsys</div>
   ```

   替換為:

   ```java
   <cq:include path="rightpar" resourceType="foundation/components/iparsys" />
   ```

1. 儲存變更。
1. 在瀏覽器中，重新載入**產品**頁面。 整個頁面的外觀如下：

   ![chlimage_1-5](assets/chlimage_1-5.jpeg)
