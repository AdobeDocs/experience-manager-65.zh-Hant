---
title: 開發沙盒應用程式
seo-title: 開發沙盒應用程式
description: 使用基礎指令碼來開發應用程式
seo-description: 使用基礎指令碼來開發應用程式
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 開發沙盒應用程式 {#develop-sandbox-application}

在本節中，由於範本已在初始應用程式區段中設定，而初始內容區段中已建立初始頁面 [](initial-app.md)[](initial-content.md) ，因此可使用基礎指令碼來開發應用程式，包括啟用使用社群元件製作內容的功能。 在本節結束時，網站將可正常運作。

## 使用Foundation頁面指令碼 {#using-foundation-page-scripts}

在新增轉譯播放頁面範本的元件時建立的預設指令碼，會加以修改，以包含基礎頁面的head.jsp和本機body.jsp。

### 超級資源類型 {#super-resource-type}

第一步是向節點添加資源super type屬性， `/apps/an-scf-sandbox/components/playpage` 以便它繼承超類型的指令碼和屬性。

使用CRXDE Lite:

<!--Resolve steps below-->
    名稱：`sling:resourceSuperType&#39;
    Type:`字串&#39;
    值：`foundation/components/page`

1. 按一下綠色 **[!UICONTROL [+]Add]**
1. 按一下「 **[!UICONTROL 全部儲存」]**

![chlimage_1-231](assets/chlimage_1-231.png)

### 頭部和身體指令碼 {#head-and-body-scripts}

1. 在 **CRXDE Lite** explorer窗格中，導覽至 `/apps/an-scf-sandbox/components/playpage` 並連按兩下檔案，以在編輯 `playpage.jsp` 窗格中開啟檔案。

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp}

```xml
<%--

  An SCF Sandbox Play Component component.

  This is the component which renders content for An SCF Sandbox page.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" %><%
%><%
 // TODO add your code here
%>
```

1. 請注意開啟／關閉指令碼標籤，請取代&quot; // TODO ...&quot; with包含&lt;html>標題和內文部分的指令碼。

   如果超類型為 `foundation/components/page`，則未在此資料夾中定義的任何指令碼都將解析為資料夾中的指令碼(如果存在 `/apps/foundation/components/page` )，否則解析為資料夾中的腳 `/libs/foundation/components/page` 本。

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp-1}

```xml
<%--

    An SCF Sandbox Play Component component: playpage.jsp

  This is the component which renders content for An SCF Sandbox page.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" %>
<html>
  <cq:include script="head.jsp"/>
  <cq:include script="body.jsp"/>
</html>
```

1. 基礎指令碼 `head.jsp` 不需要覆蓋，但基礎指令碼 `body.jsp` 是空的。

   若要設定製作，請使 `body.jsp` 用本機指令碼覆蓋，並在內文中包含段落系統(parsys):

   1. 導航到 `/apps/an-scf-sandbox/components`
   1. 選擇節 `playpage`點
   1. 按一下滑鼠右鍵並選取 `Create > Create File...`

      * 名稱： **body.jsp**
   1. 按一下「 **[!UICONTROL 全部儲存」]**
   開啟 `/apps/an-scf-sandbox/components/playpage/body.jsp` 並貼入下列文字：

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. 按一下「 **[!UICONTROL 全部儲存」]**

**以編輯模式在瀏覽器中檢視頁面：**

* 標準UI: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

您不僅應看到「社群播 **放」標題**，還應看到編輯頁面內容的UI。

當兩個側面板都開啟且視窗足夠寬，以便同時顯示側面內容和頁面內容時，就會看到「資產／元件」側面板。

![chlimage_1-232](assets/chlimage_1-232.png)

* 傳統UI: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

以下是播放頁面在傳統UI中的顯示方式，包括內容搜尋器(cf):

![chlimage_1-233](assets/chlimage_1-233.png)

## 社群元件 {#communities-components}

要啟用Communities元件進行編寫，請從以下說明開始：

* [訪問社群元件](basics.md#accessing-communities-components)

為此沙盒的目的，請從下列 **Communities** 元件開始（勾選方塊即可啟用）:

* 評論
* 論壇
* 評等
* 評論
* 審核摘要 (顯示)
* 投票

此外，選擇「 **[!UICONTROL 一般]** 」元件，例如

* 影像
* 表格
* 文字
* 標題（基礎）

>[!NOTE]
>
>為頁面par啟用的元件將作為 `components`
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 節點。

## 登陸頁面 {#landing-page}

在多語言環境中，根頁面將包含一個指令碼，該指令碼將解析來自客戶端的請求以確定首選語言。

在這個簡單範例中，根頁面會靜態設定為重新導向至英文頁面，未來可能會開發成具有播放頁面連結的主著陸頁面。

將瀏覽器URL變更為根頁面： [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* 選取「頁面資訊」圖示
* 選擇 **[!UICONTROL 開啟屬性]**
* 在「高級」頁籤上

   * 若為「重新導向」項目，請瀏 **[!UICONTROL 覽至「網站> SCF沙盒網站> SCF沙盒」]**
   * 按一下「 **[!UICONTROL 確定」]**

* 按一下「 **[!UICONTROL 確定」]**

發佈網站後，瀏覽至發佈例項的根頁面會重新導向至英文頁面。

使用社區SCF元件前的最後一個步驟是添加客戶端庫資料夾(clientlibs)。... [新增Clienlibs](add-clientlibs.md)