---
title: 新增Clientlibs
seo-title: 新增Clientlibs
description: 新增ClientLibraryFolder
seo-description: 新增ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 新增Clientlibs{#add-clientlibs}

## 新增ClientLibraryFolder(clientlibs) {#add-a-clientlibraryfolder-clientlibs}

建立名為的ClientLibraryFolder, `clientlibs`其中將包含用於呈現您網站頁面的JS和CSS。

給 `categories`予此用戶端程式庫的屬性值是用來直接從內容頁面包含此clientlib，或將其內嵌在其他clientlib中的識別碼。

1. 使用 **CRXDE Lite**，展開 `/etc/designs`

1. 按一下右鍵 `an-scf-sandbox` 並選擇 `Create Node`

   * 名稱 : `clientlibs`
   * 類型 : `cq:ClientLibraryFolder`

1. 按一下「 **確定」**

![chlimage_1-47](assets/chlimage_1-47.png)

在新節 **點的** 「屬性」選 `clientlibs` 項卡中，輸入**`categories`**屬性：

* 名稱：類 **別**
* 類型：字 **串**
* 值： **apps.an-scf-sandbox**
* click **Add**
* 按一 **下「全部儲存」**

注意：使用「應用程式」來預設類別值。 是將「擁有的應用程式」識別為位於/apps資料夾而非/libs的慣例。  重要：新增預留 `js.tx`位置t和**`css.tx`*t檔案。 （沒有cq:ClientLibraryFolder，它並非正式。）

1. 右鍵 **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選擇 **建立檔案……**
1. **輸入**&#x200B;名稱： `css.txt`
1. 選擇 **建立檔案……**
1. **輸入**&#x200B;名稱： `js.txt`
1. 按一 **下「全部儲存」**

![chlimage_1-48](assets/chlimage_1-48.png)

css.txt和js.txt的第一行會識別從中可找到下列檔案清單的基本位置。

嘗試將css.txt的內容設定為

```
#base=.
 style.css
```

然後，在clientlibs下建立名為style.css的檔案，並將內容設為

`body {`

`background-color: #b0c4de;`

`}`

### 嵌入SCF客戶端 {#embed-scf-clientlibs}

在節 **點的** 「屬性」 `clientlibs` 標籤中，輸入多值String屬性 **embed**。 這將嵌入SCF [元件的必要客戶端庫(clientlibs)](/help/communities/client-customize.md#clientlibs-for-scf)。 在本教程中，將添加Communities元件所需的許多客戶端。

**請注意** ，這可能是生產網站所需使用的方法，因為有考慮到每個頁面所下載的clientlib的便利性與大小／速度。

如果只在單一頁面上使用一項功能，您可以直接在頁面上包含該功能的完整clientlib，例如&lt;% ui:includeClientLib類別=cq.social.hbs.forum&quot; %>

在本例中，包括所有的SCF客戶端，因此，作者clientlibs的更基本的SCF客戶端：

* 名稱 : **`embed`**
* 類型 : **`String`**
* 按一下 **`Multi`**
* 值： **`cq.social.scf`***&lt;enter>會在每個項目後彈出對話方塊，按一下**[+] **以新增下列clientlib類別：*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * 按一下「 **確定」**

* 按一 **下「全部儲存」**

![chlimage_1-49](assets/chlimage_1-49.png)

這是現在 `/etc/designs/an-scf-sandbox/clientlibs` 在儲存庫中的顯示方式：

![chlimage_1-50](assets/chlimage_1-50.png)

### 在PlayPage範本中包含Clientlibs {#include-clientlibs-in-playpage-template}

如果頁面 `apps.an-scf-sandbox` 上未包含ClientLibraryFolder類別，SCF元件將無法正常工作，也無法設定樣式，因為不提供必要的Javascript和樣式。

例如，如果不包含clientlibs,SCF注釋元件將顯示為未樣式化：

![chlimage_1-51](assets/chlimage_1-51.png)

一旦包含apps.an-scf-sandbox clientlibs後，SCF注釋元件就會顯示樣式化：

![chlimage_1-52](assets/chlimage_1-52.png)

包含語句屬於 <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 的 <html> 指令碼. 預設值 **`foundation head.jsp`** 包含可重疊的指令碼： **`headlibs.jsp`**。

**複製headlibs.jsp並包含clientlibs:**

1. 使用 **CRXDE Lite**，選擇 **`/libs/foundation/components/page/headlibs.jsp`**

1. 按一下右鍵並選擇**複製**（或從工具欄中選擇「複製」）
1. select**`/apps/an-scf-sandbox/components/playpage`**
1. 按一下右鍵並選擇**貼上**（或從工具欄中選擇貼上）
1. 按兩下 **`headlibs.jsp`** 將其開啟
1. 在檔案末尾附加以下行
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 按一 **下「全部儲存」**

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

![chlimage_1-53](assets/chlimage_1-53.png)

### 保存您的作品 {#saving-your-work-so-far}

此時，存在極簡的沙盒，因此，在播放時，如果儲存庫損壞並想要重頭開始，您可以關閉伺服器、更名或刪除資料夾crx-quickstart/、開啟伺服器、上傳和安裝此保存的軟體包，而不必重複這些最基本的步驟。

此套件存在於「建 [](/help/communities/create-sample-page.md) 立範例頁面」教學課程中，供迫不及待要跳入並開始播放的使用者使用……

要建立包：

* 從CRXDE Lite按一下「套 [件」圖示](https://localhost:4502/crx/packmgr/)
* 按一 **下「建立套件」**

   * 包名：an-scf-sandbox-minimal-pkg
   * 版本：0.1
   * 群組：&lt;leave as default>
   * 按一下「 **確定」**

* 按一下「編 **輯」**

   * 選擇**篩選器**tab

      * 按一 **下新增篩選**
      * 根路徑：&lt;browse to** /apps/an-scf-sandbox*>
      * 按一下「完 **成」**
      * 按一 **下新增篩選**
      * 根路徑：&lt;browse to **/etc/designs/an-scf-sandbox**>
      * 按一下「完 **成」**
      * 按一 **下新增篩選**
      * 根路徑：&lt;browse to **/content/an-scf-sandbox**>
      * 按一下「完 **成」**
   * click **Save**


* 按一下「建 **立」**

現在，您可以選取「 **Download** 」（下載）以儲存至磁碟並將它上傳至其他位置的「 **Upload Package** 」（上傳套件），並選取「 **More」（更多）>「Replicate** 」（複製），將沙盒推送至localhost發佈例項，以擴展沙盒的領域。