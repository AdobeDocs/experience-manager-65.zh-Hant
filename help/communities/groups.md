---
title: 社群群組主控台
description: 瞭解社群群組主控台，可在社群網站的範本結構包含群組功能時，讓您建立社群群組。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 2%

---

# 社群群組主控台 {#community-groups-console}

「群組」主控台提供在社群網站建立社群群組的許可權 [範本結構](/help/communities/sites-console.md#step1) 包含 [群組功能](/help/communities/functions.md#groups-function).

* AEM Communities支援在其他群組內巢狀內嵌群組。 群組巢狀可在以下情況下使用 [新群組的結構](/help/communities/tools-groups.md) 包含群組功能。
* 僅適用於作者環境，有一個群組建立精靈，類似於網站建立精靈。
* 成員是否可以在發佈環境中建立群組，可以在將群組功能新增至社群網站結構或社群群組結構時進行設定。

在包含的三個群組範本中，只有 `Reference Group` 範本在其結構中包含群組功能。

社群群組的不同面向如下：

* **建立**：新群組可在作者上建立，並可選擇在發佈執行個體上建立。
* **控制**：群組可以是開啟或秘密的。
* **巢狀**：群組可包含零個或多個群組。

<!-- This is a 404 on helpx. Update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), is not listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此「群組」主控台只能從「社群網站」主控台存取，切勿與成員混淆 [群組主控台](/help/communities/members.md) 用於管理成員群組。
>
>成員群組是在發佈環境中註冊的使用者群組，並可使用從製作環境存取。 [通道服務](/help/communities/deploy-communities.md#tunnel-service-on-author).

## 群組建立 {#group-creation}

若要存取「群組」主控台：

* 在Author上，使用管理員許可權登入。
* 從全域導覽： **[!UICONTROL Communities]** > **[!UICONTROL 網站]**.
* 選取現有的社群網站資料夾，以便開啟。
* 在資料夾中選取社群網站的執行個體。

   * 社群網站的結構必須包含群組功能。
   * 這些熒幕擷取畫面來自之後的快速入門教學課程 [在發佈時建立群組](/help/communities/published-site.md).

  ![create-group](assets/create-group.png)

* 選取 **群組資料夾** 以便開啟。

  開啟時，所有現有群組（無論是在「作者」或「發佈」中建立）都會顯示。

  在此「群組」主控台中，可以編寫新的群組。

  ![create-new-group](assets/create-new-group.png)

* 選取 **建立群組** 按鈕。

### 步驟1：社群群組範本 {#step-community-group-template}

![多語言社群群組](assets/multi-lingual-group.png)

* **社群群組標題**

  群組的顯示標題。
標題會顯示在群組的已發佈網站上。

* **社群群組說明**

  群組的說明。

* **社群群組根**

  群組的根路徑。
預設的根是父網站，但根可以移至網站內的任何位置。 不建議進行變更。

* **其他可用的社群群組語言** 功能表

  使用下拉式清單來選取可用的社群群組語言。 功能表會顯示建立上層社群網站的所有語言。 使用者可以選取這些語言之一，以在此單一步驟中建立多個地區設定的群組。 在個別社群網站的「群組」主控台中，以多種指定語言建立相同的群組。

* **社群群組名稱**

  顯示在URL中的群組根頁面名稱。 請避免在群組名稱中使用底線字元(_)和關鍵字（例如資源和設定）。

   * 請仔細檢查名稱，因為建立群組後不易變更。
   * 基底URL會顯示在 `Community Group Name`.
   * 對於有效的URL，附加「.html」
     *例如*， `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **社群群組範本** 功能表

  使用下拉式選單來選擇可用的 [社群群組範本](/help/communities/tools.md).

### 步驟2：設計 {#step-design}

### 社群群組主題 {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

框架使用 `Twitter Bootstrap` 為網站帶來回應式彈性設計。 您可以選取預先載入的Bootstrap主題之一，來設定所選社群群組範本的樣式，也可以上傳Bootstrap主題。

選取時，佈景主題會以不透明的藍色勾號覆蓋。

您可以選取與上層網站主題不同的主題。

社群網站發佈後，您可以 [編輯屬性](#modifyinggroupproperties) 並選取不同的主題。

### 社群群組品牌 {#community-group-branding}

![社群群組品牌](assets/community-group-branding.png)

社群網站品牌化是在每個頁面頂端以標題顯示的影像。 可以顯示群組與其他網站頁面不同的橫幅。

影像大小應如瀏覽器中頁面的預期顯示一樣寬，且高度應為120畫素。

建立或選取影像時，請記住：

* 影像高度會裁剪成從影像上邊緣測量的120畫素
* 影像已釘選至瀏覽器視窗的左邊緣
* 不會調整影像大小，因此當影像寬度為：

   * 影像小於瀏覽器的寬度，便會在水準方向重複。
   * 大於瀏覽器寬度時，影像會顯示為已裁切。

### 步驟3：設定 {#step-settings}

**稽核**

![選取社群群組成員角色](assets/group-admin.png)

**社群群組版主**

依預設，會繼承上層社群網站的版主清單。

您可以專門將版主新增至群組。 搜尋成員（從發佈環境）以將他們新增為版主

**群組管理員**

依預設，父級社群網站管理員也是群組的管理員。

但是，可以指派獨立的群組管理員。 群組管理員可以管理群組（例如G1），並在G1下建立巢狀的子群組。 他們可為子群組進一步指派不同的管理員。

因此，使用者U1可以是群組G1的管理員，也可以是其巢狀群組G2的一般使用者。

**會籍**

成員資格設定允許從三種確保社群群組安全的方法中選擇一種。

![community-group-membership](assets/community-group-membership.png)

* **可選成員資格**

  如果選取，社群群組為公用群組。 網站成員可以加入群組及張貼，而無需明確加入群組。 預設為已選取。

* **必要的成員資格**

  如果選取，社群群組為開放群組。 社群網站成員可以檢視群組的內容，但必須加入群組才能發佈內容。 成員透過選取 `Join` 按鈕來設定。 未選取預設。

* **限制的成員資格**

  如果選取，則社群群組為機密群組。 必須明確邀請社群成員。 邀請的成員會輸入搜尋方塊。 稍後可以使用新增成員 [成員和群組主控台](/help/communities/members.md) 作者環境。 未選取預設。

**縮圖**

![community-group-thumbnail](assets/community-group-thumbnail.png)

縮圖是要在製作和發佈時為群組顯示的影像。

群組影像的最佳大小為支援的影像格式(例如JPG或PNG)為170 x 90畫素。

如果未新增影像，則會顯示預設影像。

![thumbnail-image](assets/thumbnail-image.png)

### 步驟4：建立群組 {#step-create-group}

![community-create-group](assets/community-create-group.png)

如果需要任何調整，請使用 **返回** 按鈕來進行變更。

一次 **建立** 已選取並啟動，建立群組的程式無法中斷。

程式完成時，新子社群網站（群組）的卡片會顯示在Communities Sites群組主控台中，作者可在其中新增頁面內容，或管理員可修改網站的屬性。

![建立社群群組](assets/create-community-groups.png)

>[!NOTE]
>
>群組會以所有語言建立，如中所指定 [步驟1：社群群組範本](/help/communities/groups.md#step-community-group-template) 在其他可用的社群群組語言中，在個別社群網站的社群群組主控台中。

## 作者群組內容 {#author-group-content}

![open-site](assets/open-site.png)

群組的頁面內容可使用與任何其他AEM頁面相同的工具進行編寫。 若要開啟群組以進行編寫，請選取「開啟網站」圖示，將滑鼠游標停留在群組卡片上時就會顯示。

## 修改群組屬性 {#modify-group-properties}

選取將游標停留在群組卡片上時顯示的「編輯網站」圖示，可以修改現有子社群網站（在社群群組建立過程中指定）的屬性：

![edit-site](assets/edit-site.png)

下列屬性的詳細資料與 [群組建立](#group-creation) 區段。 可以修改任何巢狀群組，無論是在發佈環境或作者環境中建立。

![community-group-basic](assets/community-group-basic.png)

### 修改基本 {#modify-basic}

「基本」面板允許修改

* 社群群組標題
* 社群群組說明

社群群組名稱不可修改。

選擇不同的社群群組範本對於現有的社群群組網站沒有影響，因為範本和網站之間沒有連線。

而是 [結構](#modify-structure) 可以修改子社群的。

### 修改結構 {#modify-structure}

「結構」面板可讓您修改最初從作者或發佈環境建立子社群網站時，從社群群組範本選取的結構。 您可以從面板執行下列作業：

* 拖放其他專案 [社群功能](/help/communities/functions.md) 放入網站結構中。
* 在網站結構中的社群功能例項上：

   * **`Gear icon`**
編輯設定，包括顯示標題、URL和 [有特殊許可權的成員群組](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
從網站結構中移除（刪除）函式。

   * **`Grid icon`**
修改網站最上層導覽列中顯示的函式順序。

>[!CAUTION]
>
>雖然顯示標題可以變更而不會產生副作用，但建議您不要編輯屬於社群網站的社群功能的URL名稱。
>
>例如，重新命名URL不會移動現有的UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>群組功能必須 *非* 成為 *第一或唯一* 功能在網站結構中。
>
>任何其他函式，例如 [頁面函式](/help/communities/functions.md#page-function)，必須先包含並列出。

**範例：新增行事曆功能至子社群（群組）結構**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改設計 {#modify-design}

DESIGN面板允許修改主題：

* [社群群組主題](#community-group-theme)
* [社群群組品牌](#community-group-branding)

   * 捲動至面板底部，以便變更品牌影像。

### 修改設定 {#modify-settings}

「設定」面板可讓您新增社群 [版主](#moderation).

### 修改成員資格 {#modify-membership}

此 [會籍](#membership) 面板僅供參考。 無法變更已建立的群組成員資格型別，不論是選擇性、必要或限制。

### 修改縮圖 {#modify-thumbnail}

此 [縮圖](#thumbnail) 面板可讓您上傳影像，以在「發佈」環境中及製作環境中的Communities網站的「群組」主控台中，代表社群群組至網站訪客。

## 發佈群組 {#publish-the-group}

![publish-site](assets/publish-site.png)

建立或修改社群群組後，您可以選取 `Publish Site` 圖示。

成功發佈群組後，會顯示下列訊息：

![group-published](assets/group-published.png)

>[!CAUTION]
>
>上層社群網站和上層群組應已發佈。
>
>社群網站和巢狀群組應以由上而下的方式發佈。

## 刪除群組 {#delete-the-group}

![刪除圖示](assets/deleteicon.png)

選取「刪除群組」圖示（將滑鼠懸停在群組上時顯示），從社群群組主控台中刪除群組。

這會移除與群組相關的所有專案，例如，群組的所有內容會永久刪除，而使用者成員資格會從系統中移除。
