---
title: 開發沙盒應用程式
seo-title: Develop Sandbox Application
description: 使用基礎指令碼開發應用程式
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 4%

---

# 開發沙盒應用程式  {#develop-sandbox-application}

在本節中，模板已在 [初始應用](initial-app.md) ，以及 [初始內容](initial-content.md) 部分，可以使用基礎指令碼開發應用程式，包括啟用使用社區元件進行創作的能力。 本節結束時，網站將正常運行。

## 使用Foundation頁指令碼 {#using-foundation-page-scripts}

在添加呈現播放頁模板的元件時建立的預設指令碼將被修改，以包括基礎頁的head.jsp和本地body.jsp。

### 超級資源類型 {#super-resource-type}

第一步是向 `/apps/an-scf-sandbox/components/playpage` 節點，以便繼承超類型的指令碼和屬性。

使用 CRXDE Lite:

1. 選擇節點 `/apps/an-scf-sandbox/components/playpage`。
1. 在「屬性」頁籤中，輸入具有以下值的新屬性：

   名稱: `sling:resourceSuperType`

   類型: `String`

   值: `foundation/components/page`

1. 按一下綠色 **[!UICONTROL +添加]** 按鈕
1. 按一下 **[!UICONTROL 全部保存]**。

   ![頁面指令碼](assets/page-script.png)

### 頭部和身體指令碼 {#head-and-body-scripts}

1. 在 **CRXDE Lite** 瀏覽器窗格，導航至 `/apps/an-scf-sandbox/components/playpage` 並按兩下檔案 `playpage.jsp` 開啟它。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

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

1. 要瞭解open/close指令碼標籤，請替換&quot; // TODO ...&quot; 包含用於 &lt;html>。

   具有超類型 `foundation/components/page`，此資料夾中未定義的任何指令碼都將解析為中的指令碼 `/apps/foundation/components/page` 資料夾（如果存在），則指向 `/libs/foundation/components/page` 的子菜單。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

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

1. 基礎指令碼 `head.jsp` 不需要重疊，但是基本指令碼 `body.jsp` 為空。

   要設定創作，請覆蓋 `body.jsp` 帶有本地指令碼，並在正文中包含段落系統(parsys):

   1. 導覽至 `/apps/an-scf-sandbox/components`。
   1. 選擇 `playpage` 的下界。
   1. 按一下右鍵並選擇 `Create > Create File...`

      * 名稱： **body.jsp**
   1. 按一下 **[!UICONTROL 全部保存]**。

   開啟 `/apps/an-scf-sandbox/components/playpage/body.jsp` 並貼上到以下文本中：

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

1. 按一下 **[!UICONTROL 全部保存]**。

**以編輯模式在瀏覽器中查看頁面：**

* 標準 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

你不應該只看到標題 **社區遊戲**，還有用於編輯頁面內容的UI。

當兩個側面板都被切換開啟，並且窗口足夠寬，可同時顯示側面內容和頁面內容時，將顯示「資產/元件」側面板。

![視圖頁](assets/view-page.png)

* 傳統 UI: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

以下是播放頁在經典UI中的顯示方式，包括內容查找器(cf):

![播放頁面視圖](assets/play-page-view.png)

## 社區元件 {#communities-components}

要啟用社區元件進行創作，請按照以下說明開始：

* [訪問社區元件](basics.md#accessing-communities-components)

為此沙盒的目的，請從以下內容開始 **社區** 元件（通過選中框啟用）:

* 評論
* 論壇
* 評等
* 評論
* 審核摘要 (顯示)
* 投票

另外，選擇 **[!UICONTROL 常規]** 元件，如

* 影像
* 表格
* 文字
* 標題（基礎）

>[!NOTE]
>
>為頁面部分啟用的元件作為 `components` 屬性
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 的下界。

## 登陸頁面 {#landing-page}

在多語言環境中，根頁面將包括指令碼，該指令碼將分析來自客戶端的請求以確定首選語言。

在此簡單示例中，根頁被靜態設定為重定向到英文頁，該英文頁將來可能會開發為帶有到播放頁的連結的主登錄頁。

將瀏覽器URL更改為根頁： `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 選擇「頁面資訊」表徵圖
* 選擇 **[!UICONTROL 開啟屬性]**
* 在「高級」(ADVANCED)頁籤上

   * 對於重定向條目，瀏覽至 **[!UICONTROL 網站]** > **[!UICONTROL SCF沙盒站點]** > **[!UICONTROL SCF沙盒]**
   * 按一下 **[!UICONTROL 確定]**

* 按一下 **[!UICONTROL 確定]**

網站發佈後，瀏覽到發佈實例上的根頁面將重定向到英文頁面。

使用社區SCF元件前的最後一步是添加客戶端庫資料夾（客戶端庫）。..。 [添加客戶端](add-clientlibs.md)
