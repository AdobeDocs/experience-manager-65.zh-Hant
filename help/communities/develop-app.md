---
title: 開發沙箱應用程式
description: 瞭解如何開發沙箱應用程式，該應用程式使用基礎指令碼，並包含啟用使用Communities元件編寫的功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# 開發沙箱應用程式  {#develop-sandbox-application}

在此區段中，範本已設定在[初始應用程式](initial-app.md)區段中，而初始頁面已建立在[初始內容](initial-content.md)區段中，現在您可以開發應用程式。 若要這麼做，請使用基礎指令碼，其中包括啟用使用Communities元件編寫的功能。 在本節的結尾，您會看到功能完整的網站。

## 使用基礎頁面命令檔 {#using-foundation-page-scripts}

預設指令碼是在新增轉譯播放頁面範本的元件時建立的，經過修改後會包含基礎頁面的head.jsp和本機body.jsp。

### 超級資源型別 {#super-resource-type}

第一個步驟是將資源超級型別屬性新增到`/apps/an-scf-sandbox/components/playpage`節點，以便它繼承超級型別的指令碼和屬性。

使用CRXDE Lite：

1. 選取節點`/apps/an-scf-sandbox/components/playpage`。
1. 在屬性標籤中，輸入具有下列值的新屬性：

   名稱：`sling:resourceSuperType`

   類型：`String`

   值： `foundation/components/page`

1. 按一下綠色&#x200B;**[!UICONTROL +新增]**&#x200B;按鈕。
1. 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   ![page-script](assets/page-script.png)

### Head和body指令碼 {#head-and-body-scripts}

1. 在&#x200B;**CRXDE Lite**&#x200B;總管窗格中，瀏覽至`/apps/an-scf-sandbox/components/playpage`並連按兩下檔案`playpage.jsp`，以在編輯窗格中開啟它。

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

1. 注意開啟/關閉指令碼標籤，將「 // TODO ...」取代為&lt;html>的head和body部分的`includes`個指令碼。

   若超級型別為`foundation/components/page`，未定義在此相同資料夾中的任何指令碼都會解析為`/apps/foundation/components/page`資料夾中的指令碼（如果存在），或解析為`/libs/foundation/components/page`資料夾中的指令碼。

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

1. 不需要覆蓋基礎指令碼`head.jsp`，但基礎指令碼`body.jsp`是空的。

   若要設定進行編寫，請使用本機指令碼覆蓋`body.jsp`，並在內文中加入段落系統(parsys)：

   1. 導覽至 `/apps/an-scf-sandbox/components`。
   1. 選取`playpage`節點。
   1. 按一下滑鼠右鍵並選取`Create > Create File...`

      * 名稱： **body.jsp**

   1. 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   開啟`/apps/an-scf-sandbox/components/playpage/body.jsp`並貼入下列文字：

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

1. 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

**在瀏覽器中以編輯模式檢視頁面：**

* 標準UI： `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

您應該不僅會看到標題&#x200B;**社群播放**，還會看到用於編輯頁面內容的UI。

當兩側面板都切換為開啟，且視窗夠寬，足以顯示側邊內容和頁面內容時，會看到Assets/元件側面板。

![檢視頁面](assets/view-page.png)

* 傳統UI： `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

以下是「播放」頁面在傳統UI中的顯示方式，包括透過內容尋找器(cf)：

![play-page-view](assets/play-page-view.png)

## Communities元件 {#communities-components}

若要啟用Communities元件以供撰寫，請依照下列指示開始進行：

* [存取Communities元件](basics.md#accessing-communities-components)

在此沙箱中，請從這&#x200B;**個Communities**&#x200B;元件開始（核取方塊以啟用）：

* 評論
* 論壇
* 評等
* 評論
* 審核摘要 (顯示)
* 投票

此外，請選擇&#x200B;**[!UICONTROL 一般]**&#x200B;元件，例如

* 影像
* 表格
* 文字
* 標題（基礎）

>[!NOTE]
>
>為頁面par啟用的元件會儲存於存放庫中，作為的`components`屬性值
>
>節點`/etc/designs/an-scf-sandbox/jcr:content/playpage/par`。

## 登陸頁面 {#landing-page}

在多語言環境中，根頁面會包含指令碼，此指令碼會剖析使用者端的請求，以決定偏好的語言。

在此範例中，會將根頁面以靜態方式設定為重新導向至英文頁面，而英文頁面可能會在日後發展為具有播放頁面連結的主要登陸頁面。

將瀏覽器URL變更為根頁面： `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 選取頁面資訊圖示
* 選取&#x200B;**[!UICONTROL 開啟屬性]**
* 在進階標籤上

   * 針對重新導向專案，瀏覽至&#x200B;**[!UICONTROL 網站]** > **[!UICONTROL SCF沙箱網站]** > **[!UICONTROL SCF沙箱]**
   * 按一下&#x200B;**[!UICONTROL 確定]**

* 按一下&#x200B;**[!UICONTROL 確定]**

發佈網站後，在發佈執行個體上瀏覽至根頁面時，會重新導向至英文頁面。

播放Communities SCF元件之前的最後一步是新增使用者端程式庫資料夾(clientlibs) .... [新增Clientlibs](add-clientlibs.md)
