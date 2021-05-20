---
title: 新增Clientlibs
seo-title: 新增Clientlibs
description: 添加ClientLibraryFolder
seo-description: 添加ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# 新增Clientlibs {#add-clientlibs}

## 新增ClientLibraryFolder(clientlibs){#add-a-clientlibraryfolder-clientlibs}

建立名為`clientlibs`的ClientLibraryFolder，其中包含用於呈現網站頁面的JS和CSS。

指定給此客戶端庫的`categories`屬性值是用於直接從內容頁面包括此clientlib或將其嵌入到其他客戶端庫的標識符。

1. 使用&#x200B;**CRXDE Lite**，展開`/etc/designs`

1. 按一下右鍵`an-scf-sandbox`並選擇`Create Node`

   * 名稱 : `clientlibs`
   * 類型 : `cq:ClientLibraryFolder`

1. 按一下&#x200B;**OK**

![add-client-library](assets/add-client-library.png)

在新`clientlibs`節點的&#x200B;**屬性**&#x200B;頁簽中，輸入&#x200B;**categories**&#x200B;屬性：

* 名稱：**類別**
* 類型：**字串**
* 值：**apps.an-scf-sandbox**
* 按一下&#x200B;**Add**
* 按一下「**全部保存**」

注意：使用「apps」為類別值加上前置詞。 是將「擁有的應用程式」標識為位於/apps資料夾（而非/libs）的慣例。  重要：添加佔位符`js.tx`t和&#x200B;**`css.txt`**&#x200B;檔案。 （若沒有cq:ClientLibraryFolder，則不是正式的。）

1. 按一下右鍵&#x200B;**`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選擇&#x200B;**建立檔案……**
1. 輸入&#x200B;**名稱：** `css.txt`
1. 選擇&#x200B;**建立檔案……**
1. 輸入&#x200B;**名稱：** `js.txt`
1. 按一下「**全部保存**」

![clientlibs-css](assets/clientlibs-css.png)

css.txt和js.txt的第一行標識了從中找到下列檔案清單的基本位置。

請嘗試將css.txt的內容設定為

```
#base=.
 style.css
```

然後在clientlibs下建立名為style.css的檔案，並將內容設定為

`body {`

`background-color: #b0c4de;`

`}`

### 內嵌SCF Clientlibs {#embed-scf-clientlibs}

在`clientlibs`節點的&#x200B;**屬性**&#x200B;標籤中，輸入多值字串屬性&#x200B;**embed**。 這嵌入了SCF元件](/help/communities/client-customize.md#clientlibs-for-scf)所需的[客戶端庫(clientlibs)。 在本教學課程中，新增了Communities元件所需的許多clientlib。

**** 請注意，由於考量到為每個頁面下載的clientlib的方便性與大小/速度，因此這可能或不是生產網站所需的方法。

如果只在一個頁面上使用一個功能，您可以直接在頁面上包含該功能的完整clientlib，例如

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在這種情況下，包括所有的，因此，更基本的SCF客戶端庫（即作者客戶端庫）被推薦：

* 名稱 : **`embed`**
* 類型 : **`String`**
* 按一下 **`Multi`**
* 值: **`cq.social.scf`**

   * 它會彈出對話，
按一下每個項目後的**`+`**&#x200B;以新增下列clientlib類別：

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 按一下&#x200B;**OK**

* 按一下「**全部保存**」

![scf-clientlibs](assets/scf-clientlibs.png)

以下說明`/etc/designs/an-scf-sandbox/clientlibs`現在在存放庫中的顯示方式：

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### 在PlayPage範本{#include-clientlibs-in-playpage-template}中包含Clientlibs

如果頁面上未包含`apps.an-scf-sandbox` ClientLibraryFolder類別，則SCF元件將無法工作，也無法設定樣式，因為必要的Javascript和樣式將不可用。

例如，在不包含clientlib的情況下，SCF注釋元件將顯示為未設定樣式：

![clientlibs-comment](assets/clientlibs-comment.png)

納入apps.an-scf-sandbox clientlibs後，SCF注釋元件就會顯示樣式：

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include語句屬於`html`指令碼的`head`部分。 預設&#x200B;**`foundation head.jsp`**&#x200B;包含可重疊的指令碼：**`headlibs.jsp`**。

**複製headlibs.jsp並包含clientlibs:**

1. 使用&#x200B;**CRXDE Lite**，選擇&#x200B;**`/libs/foundation/components/page/headlibs.jsp`**

1. 按一下右鍵並選擇&#x200B;**複製**（或從工具欄選擇複製）
1. 選取 **`/apps/an-scf-sandbox/components/playpage`**
1. 按一下右鍵並選擇&#x200B;**貼上**（或從工具欄選擇貼上）
1. 按兩下&#x200B;**`headlibs.jsp`**&#x200B;以開啟它
1. 將下列行附加到檔案的結尾
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 按一下「**全部保存**」

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

在瀏覽器中載入您的網站，查看背景是否不是藍色。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![社群播放](assets/community-play.png)

### 到目前為止保存您的工作{#saving-your-work-so-far}

此時，存在一個極簡的沙箱，因此，在播放時，如果您的儲存庫已損壞且您希望重新開始，您可以關閉伺服器、更名或刪除資料夾crx-quickstart/、開啟伺服器、上傳和安裝此保存的包，而不必重複這些最基本的步驟。

此套件存在於[建立範例頁面](/help/communities/create-sample-page.md)教學課程中，供迫不及待要跳入並開始播放的使用者使用！..

要建立包：

* 從CRXDE Lite按一下[包表徵圖](https://localhost:4502/crx/packmgr/)
* 按一下&#x200B;**建立包**

   * 包名稱：an-scf-sandbox-minimal-pkg
   * 版本：0.1
   * 群組: `leave as default`
   * 按一下&#x200B;**OK**

* 按一下&#x200B;**編輯**

   * 選擇&#x200B;**Filters**&#x200B;頁簽

      * 按一下「**新增篩選器**」
      * 根路徑：瀏覽`/apps/an-scf-sandbox`
      * 按一下&#x200B;**Done**
      * 按一下「**新增篩選器**」
      * 根路徑：瀏覽`/etc/designs/an-scf-sandbox`
      * 按一下&#x200B;**Done**
      * 按一下「**新增篩選器**」
      * 根路徑：瀏覽`/content/an-scf-sandbox**`
      * 按一下&#x200B;**Done**
   * 按一下&#x200B;**儲存**


* 按一下&#x200B;**Build**

現在，您可以選取&#x200B;**Download**&#x200B;將其儲存至磁碟，並在其他位置選取&#x200B;**Upload Package**，以及選取&#x200B;**More > Replicate**，以便將沙箱推送至localhost發佈例項，以擴展沙箱的領域。
