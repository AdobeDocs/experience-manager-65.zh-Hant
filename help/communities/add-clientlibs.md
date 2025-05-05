---
title: 新增Clientlibs
description: 瞭解如何新增用來包含JavaScript的ClientLibraryFolder (clientlibs)以及用來呈現網站頁面的階層式樣式表。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 新增Clientlibs {#add-clientlibs}

## 新增ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

建立名為`clientlibs`的ClientLibraryFolder，其中包含用於呈現網站頁面的JavaScript (JS)和階層式樣式表(CSS)。

指定給此使用者端程式庫的`categories`屬性值是用來從內容頁面直接包含此clientlib或將其嵌入其他clientlibs的識別碼。

1. 使用&#x200B;**CRXDE Lite**，展開`/etc/designs`

1. 用滑鼠右鍵按一下`an-scf-sandbox`並選取`Create Node`

   * 名稱： `clientlibs`
   * 型別： `cq:ClientLibraryFolder`

1. 按一下&#x200B;**確定**

![add-client-library](assets/add-client-library.png)

在新`clientlibs`節點的&#x200B;**屬性**&#x200B;標籤中，輸入&#x200B;**類別**&#x200B;屬性：

* 名稱： **類別**
* 型別： **字串**
* 值： **apps.an-scf-sandbox**
* 按一下&#x200B;**新增**
* 按一下&#x200B;**全部儲存**

注意：在類別值前面加上「apps」。 是將「擁有的應用程式」識別為/apps資料夾中的慣例，而非/libs。 重要：新增預留位置`js.tx`t和&#x200B;**`css.txt`**&#x200B;檔案。 （這並非正式的cq：ClientLibraryFolder缺少它們。）

1. 用滑鼠右鍵按一下&#x200B;**`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選取&#x200B;**建立檔案……**
1. 輸入&#x200B;**名稱：** `css.txt`
1. 選取&#x200B;**建立檔案……**
1. 輸入&#x200B;**名稱：** `js.txt`
1. 按一下&#x200B;**全部儲存**

![clientlibs-css](assets/clientlibs-css.png)

css.txt和js.txt的第一行會識別要尋找下列檔案清單的基本位置。

嘗試將css.txt的內容設定為

```
#base=.
 style.css
```

接著，在clientlibs下建立名為style.css的檔案，並將內容設為

`body {`

`background-color: #b0c4de;`

`}`

### 內嵌SCF Clientlibs {#embed-scf-clientlibs}

在`clientlibs`節點的&#x200B;**屬性**&#x200B;標籤中，輸入多值字串屬性&#x200B;**內嵌**。 這會為SCF元件[&#128279;](/help/communities/client-customize.md#clientlibs-for-scf)嵌入必要的使用者端資料庫(clientlibs)。 在本教學課程中，已新增Communities元件所需的許多clientlibs。

這可能是或不可能是用於生產網站的理想方法，因為考量便利性與每個頁面下載的clientlibs的大小/速度而定。

如果在一個頁面上只使用一個功能，您可以直接在頁面上包含該功能的完整clientlib，例如，

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在此情況下，請將它們全部納入，因此偏好使用作者clientlibs且更基本的SCF clientlibs：

* 名稱： **`embed`**
* 型別： **`String`**
* 按一下&#x200B;**`Multi`**
* 值： **`cq.social.scf`**

   * 它將會彈出一個對話方塊，
在每個專案後按一下&#x200B;**`+`**&#x200B;以新增下列clientlib類別：

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 按一下&#x200B;**確定**

* 按一下&#x200B;**全部儲存**

![scf-clientlibs](assets/scf-clientlibs.png)

這是`/etc/designs/an-scf-sandbox/clientlibs`現在出現在存放庫中的方式：

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### 在PlayPage範本中包含Clientlibs {#include-clientlibs-in-playpage-template}

如果頁面上未包含`apps.an-scf-sandbox` ClientLibraryFolder類別，則SCF元件將無法運作，也無法設定樣式，因為必要的JavaScript和CSS樣式無法使用。

例如，若不包含clientlibs，SCF註解元件會以無樣式顯示：

![clientlibs-comment](assets/clientlibs-comment.png)

納入apps.an-scf-sandbox clientlibs後，SCF註解元件會以樣式顯示：

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

Include陳述式屬於`html`指令碼的`head`區段。 預設&#x200B;**`foundation head.jsp`**&#x200B;包含可覆蓋的指令碼： **`headlibs.jsp`**。

**複製headlibs.jsp並包含clientlibs：**

1. 使用&#x200B;**CRXDE Lite**，選取&#x200B;**`/libs/foundation/components/page/headlibs.jsp`**

1. 按一下滑鼠右鍵並選取&#x200B;**複製** （或從工具列選取「複製」）
1. 選取&#x200B;**`/apps/an-scf-sandbox/components/playpage`**
1. 按一下滑鼠右鍵並選取&#x200B;**貼上** （或從工具列選取「貼上」）
1. 連按兩下&#x200B;**`headlibs.jsp`**&#x200B;以將其開啟
1. 將下列行附加至檔案結尾
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 按一下&#x200B;**全部儲存**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

在瀏覽器中載入您的網站，並檢視背景是否不是藍色陰影。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![社群遊戲](assets/community-play.png)

### 目前儲存您的工作 {#saving-your-work-so-far}

此時，存在最低限度的沙箱。 或許值得另存為套件，這樣在播放時，如果您的存放庫損毀，而您想要重新開始，您可以關閉伺服器。 然後重新命名或刪除資料夾crx-quickstart/、開啟伺服器、上傳並安裝此儲存的套件，且不必重複這些最基本的步驟。

此套件存在於[建立範例頁面](/help/communities/create-sample-page.md)教學課程中，適用於無法等待跳入並開始播放的使用者。

若要建立封裝：

* 在CRXDE Lite中，按一下[封裝圖示](https://localhost:4502/crx/packmgr/)
* 按一下&#x200B;**建立封裝**

   * 套件名稱： an-scf-sandbox-minimal-pkg
   * 版本： 0.1
   * 群組： `leave as default`
   * 按一下&#x200B;**確定**

* 按一下&#x200B;**編輯**

   * 選取&#x200B;**篩選器**&#x200B;索引標籤

      * 按一下&#x200B;**新增篩選器**
      * 根路徑：瀏覽至`/apps/an-scf-sandbox`
      * 按一下&#x200B;**完成**
      * 按一下&#x200B;**新增篩選器**
      * 根路徑：瀏覽至`/etc/designs/an-scf-sandbox`
      * 按一下&#x200B;**完成**
      * 按一下&#x200B;**新增篩選器**
      * 根路徑：瀏覽至`/content/an-scf-sandbox**`
      * 按一下&#x200B;**完成**

   * 按一下&#x200B;**儲存**

* 按一下&#x200B;**建置**

現在您可以選取&#x200B;**下載**&#x200B;以儲存至磁碟，再選取&#x200B;**上傳封裝**&#x200B;至其他位置，然後選取&#x200B;**更多>復寫**&#x200B;以將沙箱推送至localhost發佈執行個體，以擴展沙箱的領域。
