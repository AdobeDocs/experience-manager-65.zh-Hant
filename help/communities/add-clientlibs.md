---
title: 添加客戶端
seo-title: Add Clientlibs
description: 添加ClientLibraryFolder
seo-description: Add a ClientLibraryFolder
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
source-wordcount: '682'
ht-degree: 1%

---

# 添加客戶端 {#add-clientlibs}

## 添加ClientLibraryFolder（客戶端） {#add-a-clientlibraryfolder-clientlibs}

建立名為的ClientLibraryFolder `clientlibs` 包含用於呈現站點頁面的JS和CSS。

的 `categories` 賦予此客戶端庫的屬性值是用於從內容頁面直接包括此客戶端庫或將其嵌入其他客戶端庫的標識符。

1. 使用 **CRXDE Lite**&#x200B;展開 `/etc/designs`

1. 按一下右鍵 `an-scf-sandbox` 選擇 `Create Node`

   * 名稱 : `clientlibs`
   * 類型 : `cq:ClientLibraryFolder`

1. 按一下 **確定**

![add-client-library](assets/add-client-library.png)

在 **屬性** 按鈕 `clientlibs` 節點，輸入 **類別** 屬性：

* 名稱： **類別**
* 類型： **字串**
* 值： **apps.an scf沙盒**
* 按一下 **添加**
* 按一下 **全部保存**

注：用「apps」預先標籤類別值。 是將「擁有的應用程式」標識為位於/apps資料夾而不是/libs中的約定。  重要：添加佔位符 `js.tx`t **`css.txt`** 的子菜單。 （沒有它們，它不是正式的cq:ClientLibraryFolder。）

1. 按一下右鍵 **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選擇 **建立檔案……**
1. 輸入 **名稱：** `css.txt`
1. 選擇 **建立檔案……**
1. 輸入 **名稱：** `js.txt`
1. 按一下 **全部保存**

![客戶端CSS](assets/clientlibs-css.png)

css.txt和js.txt的第一行標識了要從中找到以下檔案清單的基本位置。

嘗試將css.txt的內容設定為

```
#base=.
 style.css
```

然後，在名為style.css的客戶端下建立一個檔案，並將內容設定為

`body {`

`background-color: #b0c4de;`

`}`

### 嵌入SCF客戶端 {#embed-scf-clientlibs}

在 **屬性** 頁籤 `clientlibs` 節點，輸入多值字串屬性 **嵌入**。 這就嵌入了 [用於SCF元件的客戶端庫](/help/communities/client-customize.md#clientlibs-for-scf)。 在本教程中，將添加社區元件所需的許多客戶端。

**注釋** 這可能是生產站點所希望採用的方法，也可能不是，因為考慮到了每頁下載的客戶端的方便性與大小/速度。

如果僅在一個頁面上使用一個功能，則可以將該功能的完整客戶端庫直接包含在頁面上，例如，

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在本例中，包括所有客戶端，因此更基本的SCF客戶端是作者的客戶端：

* 名稱 : **`embed`**
* 類型 : **`String`**
* 按一下 **`Multi`**
* 值: **`cq.social.scf`**

   * 它將彈出一個對話框，按一下 **`+`** 在每個條目後添加以下客戶端庫類別：

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 按一下 **確定**

* 按一下 **全部保存**

![scf-clientlibs](assets/scf-clientlibs.png)

這就是 `/etc/designs/an-scf-sandbox/clientlibs` 現在應出現在儲存庫中：

![scf客戶端視圖](assets/scf-clientlibs1.png)

### 在PlayPage模板中包括客戶端 {#include-clientlibs-in-playpage-template}

不包括 `apps.an-scf-sandbox` 頁面上的ClientLibraryFolder類別，SCF元件將無法正常工作，也無法設定樣式，因為必需的Javascript和樣式將不可用。

例如，如果不包括客戶端，則SCF注釋元件將顯示為未樣式：

![客戶端注釋](assets/clientlibs-comment.png)

一旦包括apps.an-scf-sandbox客戶端，SCF注釋元件將顯示為樣式：

![客戶端注釋風格](assets/clientlibs-comment1.png)

包含語句屬於 `head` 的下界 `html` 的下界。 預設 **`foundation head.jsp`** 包括可重疊的指令碼： **`headlibs.jsp`**。

**複製headlibs.jsp並包括客戶端：**

1. 使用 **CRXDE Lite**&#x200B;選中 **`/libs/foundation/components/page/headlibs.jsp`**

1. 按一下右鍵並選擇 **複製** （或從工具欄中選擇複製）
1. 選取 **`/apps/an-scf-sandbox/components/playpage`**
1. 按一下右鍵並選擇 **貼上** （或從工具欄中選擇貼上）
1. 按兩下 **`headlibs.jsp`** 開啟
1. 將以下行添加到檔案末尾
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 按一下 **全部保存**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

在瀏覽器中載入您的網站，並查看背景是否不是藍色。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![社區遊戲](assets/community-play.png)

### 保存到目前為止的工作 {#saving-your-work-so-far}

此時，存在極簡的沙箱，因此，在播放時，如果儲存庫損壞並要重新啟動，您可以關閉伺服器、更名或刪除資料夾crx-quickstart/、開啟伺服器、上載和安裝此保存的包，而不必重複這些最基本的步驟。

此包存在於 [建立示例頁](/help/communities/create-sample-page.md) 教那些迫不及待地跳入並開始播放的人……

要建立包：

* 從CRXDE Lite按一下 [包表徵圖](https://localhost:4502/crx/packmgr/)
* 按一下 **建立包**

   * 包名稱：an scf-sandbox-minimal-pkg
   * 版本：0.1
   * 群組: `leave as default`
   * 按一下 **確定**

* 按一下 **編輯**

   * 選擇 **篩選器** 頁籤

      * 按一下 **添加篩選器**
      * 根路徑：瀏覽 `/apps/an-scf-sandbox`
      * 按一下 **完成**
      * 按一下 **添加篩選器**
      * 根路徑：瀏覽 `/etc/designs/an-scf-sandbox`
      * 按一下 **完成**
      * 按一下 **添加篩選器**
      * 根路徑：瀏覽 `/content/an-scf-sandbox**`
      * 按一下 **完成**
   * 按一下 **保存**


* 按一下 **生成**

現在您可以選擇 **下載** 保存到磁碟和 **上載包** 的 **更多>複製** 以便將沙盒推送到本地主機發佈實例以擴展沙盒的領域。
