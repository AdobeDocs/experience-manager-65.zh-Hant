---
title: 社群群組主控台
seo-title: 社群群組主控台
description: 群組主控台可讓您建立社群群組
seo-description: 群組主控台可讓您建立社群群組
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 2%

---


# 社群群組主控台 {#community-groups-console}

當社區站點的[模板結構](/help/communities/sites-console.md#step1)包含[組函式](/help/communities/functions.md#groups-function)時，「組」控制台提供建立社區組的訪問權限。

* AEM Communities支援在其他組內建立組。 當新組](/help/communities/tools-groups.md)的[結構包含組函式時，可進行組嵌套。
* 僅對於作者環境，有一個與站點建立嚮導類似的組建立嚮導。
* 在發佈環境中，成員是否可以建立組，在向社區站點結構或社區組結構添加組函式時可對其進行配置。

在包含的三個組模板中，只有`Reference Group`模板在其結構中包含組函式。

社群群組的不同面包括：

* **建立**:可在作者上建立新群組，也可在發佈例項上建立新群組。
* **控制**:群組可以是開放或秘密。
* **巢狀**:群組可以包含零或多個群組。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此組控制台僅可從Communities Sites控制台訪問，不要與管理成員組的成員[組控制台](/help/communities/members.md)混淆。
>
>成員組是在發佈環境中註冊的用戶組，使用[tunnel服務](/help/communities/deploy-communities.md#tunnel-service-on-author)從作者環境訪問。

## 群組建立 {#group-creation}

要訪問組控制台：

* 在作者上，以管理員權限登入。
* 從全域導覽：**[!UICONTROL 社群]** > **[!UICONTROL 網站]**。
* 選擇現有的社區站點資料夾以將其開啟。
* 在資料夾中選擇社區站點的實例。

   * 社群網站的結構必須包含群組功能。
   * 這些螢幕擷取畫面來自[在publish](/help/communities/published-site.md)上建立群組後的「快速入門」教學課程。

   ![create-group](assets/create-group.png)

* 選擇&#x200B;**Groups資料夾**&#x200B;以將其開啟。

   開啟時，會顯示所有現有群組，不論是在作者或發佈上建立。

   在此「群組」主控台中，可以編寫新群組。

   ![create-new-group](assets/create-new-group.png)

* 選擇&#x200B;**建立組**&#x200B;按鈕。

### 步驟1:社群群組範本{#step-community-group-template}

![多語言社群群組](assets/multi-lingual-group.png)

* **社群群組標題**

   群組的顯示標題。
標題會顯示在群組的發佈網站上。

* **社群群組說明**

   群組的說明。

* **社群群組根**

   群組的根路徑。
預設的根目錄是父網站，但根目錄可移至網站內的任何位置。 建議不要變更它。

* **其他可用的社群群組語言功** 能表

   使用下拉式清單來選取可用的社群群組語言。 功能表會顯示建立父社群網站的所有語言。 使用者可在這些語言中選擇，以在此單一步驟中建立多個地區設定的群組。 在相應社群網站的「群組」主控台中，以多種指定語言建立相同的群組。

* **社群群組名稱**

   顯示在URL中的群組根頁面名稱。

   * 重複勾選名稱，因為在建立群組後不易變更。
   * 基本URL將顯示在`Community Group Name`下方。
   * 若為有效的URL，請附加&quot;。html&quot;
      *例如*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`。

* **社群群組範本** 功能表

   使用下拉式清單選擇可用的[社群群組範本](/help/communities/tools.md)。

### 步驟2:設計{#step-design}

### 社群群組主題{#community-group-theme}

![社群群體主題](assets/communitygrouptheme.png)

此架構使用[TwitterBootstrap](https://twitterbootstrap.org/)為網站提供回應式、有彈性的設計。 可以選取許多預先載入的Bootstrap主題之一來設定所選社群群組範本的樣式，或上傳Bootstrap主題。

選取後，主題將會以不透明的藍色核取標籤覆蓋。

您可以選取與父網站主題不同的主題。

社群網站發佈後，[可編輯屬性](#modifyinggroupproperties)並選取不同的主題。

### 社群群組品牌推廣{#community-group-branding}

![社群——群組——品牌](assets/community-group-branding.png)

社群網站品牌是顯示為每個頁面上方標題的影像。 可顯示不同於其他網站頁面之群組的橫幅。

影像的大小應與預期的頁面在瀏覽器中顯示的大小相同，高度應為120像素。

建立或選取影像時，請記住：

* 影像高度會裁切為120像素，從影像的上邊緣測量
* 影像會固定在瀏覽器視窗的左邊緣
* 影像沒有調整大小，因此當影像寬度為：

   * 小於瀏覽器的寬度，影像會水準重複。
   * 大於瀏覽器的寬度，影像會看起來被裁切。

### 步驟3:設定{#step-settings}

**協調**

![選擇社區組成員角色](assets/group-admin.png)

**社群群組版主**

依預設，會繼承父社群網站的協調者清單。

您可以新增群組專屬的協調者。 搜尋成員（從發佈環境）以新增成員為協調者

**群組管理員**

預設情況下，父社區站點管理員也是組的管理員。

但是，可以指派獨立的群組管理員。 群組管理員可以管理其群組（例如G1），並建立G1下巢狀的子群組。 他們可進一步為子群組指派不同的管理員。

因此，用戶U1可以是組G1中的管理員，也可以是其嵌套組G2中的常規用戶。

**會籍**

成員資格設定允許選擇三種保護社區組的方法之一。

![社群群組會籍](assets/community-group-membership.png)

* **可選成員資格**

   如果選中此選項，則社區組是公共組。 網站成員可以參與群組，並張貼而不需明確加入群組。 已選取預設值。

* **必要的成員資格**

   如果選中此選項，則社群群組為開放群組。 社群網站成員可以檢視群組的內容，但需要加入群組才能張貼內容。 成員通過在發佈環境中選擇`Join`按鈕加入。 未選擇預設值。

* **限制的成員資格**

   如果選中此選項，則社群群組為機密群組。 必須明確邀請社群成員。 已邀請的成員將輸入到搜索框中。 以後可以使用作者環境[成員和組控制台](/help/communities/members.md)添加成員。 未選擇預設值。

**縮圖**

![community-group-thumbnail](assets/community-group-thumbnail.png)

縮圖是要在作者和發佈時針對群組顯示的影像。

群組影像的最佳大小為170 x 90像素，且支援的影像格式為（例如JPG或PNG）。

如果未新增影像，則會顯示預設影像。

![thumbnail-image](assets/thumbnail-image.png)

### 步驟4:建立組{#step-create-group}

![社群——建立群組](assets/community-create-group.png)

如果需要調整，請使用&#x200B;**Back**&#x200B;按鈕進行調整。

一旦選擇並啟動&#x200B;**Create**&#x200B;後，建立組的過程就無法中斷。

當程式完成時，新子社群網站（群組）的資訊卡會顯示在「社群網站群組」主控台中，供作者新增頁面內容或管理員修改網站屬性。

![建立社群群組](assets/create-community-groups.png)

>[!NOTE]
>
>按照[步驟1中的指定，以所有語言建立組：在各社區站點的「社區組」控制台中，使用「其他可用社區組語言」的社區組模板](/help/communities/groups.md#step-community-group-template)。

## 作者群組內容{#author-group-content}

![開放網站](assets/open-site.png)

群組的頁面內容可使用與任何其他頁面相同的工具AEM編寫。 若要開啟群組以進行製作，請選取將滑鼠指標暫留在群組卡片上時顯示的「開啟網站」圖示。

## 修改組屬性{#modify-group-properties}

在社群群組建立程式中指定的現有子社群網站屬性，可透過選取將滑鼠指標暫留在群組卡片上時顯示的「編輯網站」圖示來修改：

![edit-site](assets/edit-site.png)

下列屬性的詳細資料與[群組建立](#group-creation)區段中的說明相符。 任何巢狀群組都可以修改，不論是在發佈環境或作者環境中建立。

![社群群組——基本](assets/community-group-basic.png)

### 修改基本{#modify-basic}

BASIC面板允許修改

* 社群群組標題
* 社群群組說明

不得修改社群群組名稱。

選擇不同的社群群組範本對現有社群群組網站不會有任何影響，因為範本和網站之間沒有任何連接。

可以改進子社區的[STRUCTURE](#modify-structure)。

### 修改結構{#modify-structure}

STRUCTURE面板允許修改最初從作者或發佈環境建立子社區站點時選定的社區組模板建立的結構。 從面板，您可以：

* 將其他[社群函式](/help/communities/functions.md)拖放至網站結構中。
* 在網站結構中的社群功能例項上：

   * **`Gear icon`**
編輯設定，包括顯示標題、URL和特權 [成員群組](/help/communities/users.md#privilegedmembersgroups)。

   * **`Trashcan icon`**
從網站結構移除（刪除）函式。

   * **`Grid icon`**
修改網站頂層導覽列中顯示的功能順序。

>[!CAUTION]
>
>雖然顯示標題可以不產生副作用而變更，但不建議編輯屬於社群網站之社群函式的URL名稱。
>
>例如，重新命名URL不會移動現有的UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>群組函式必須&#x200B;*not*&#x200B;是&#x200B;*的第一個函式，也不是站點結構中唯一的*&#x200B;函式。
>
>任何其他函式（例如[page函式](/help/communities/functions.md#page-function)）必須先包含並列出。

**範例：將日曆函式添加到子社區（組）結構**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改設計{#modify-design}

DESIGN面板允許修改主題：

* [社群群組主題](#community-group-theme)
* [社群群組品牌](#community-group-branding)

   * 捲動至面板底部以變更品牌影像。

### 修改設定{#modify-settings}

「設定」面板可讓您新增社群[協調者](#moderation)。

### 修改成員資格{#modify-membership}

[MEMBERSHIP](#membership)面板僅提供資訊。 無論是選用、必要或受限制，都無法變更已建立的群組成員資格類型。

### 修改縮圖{#modify-thumbnail}

[THUMBNAIL](#thumbnail)面板允許上傳影像，以在發佈環境以及作者環境的「社群網站」群組主控台中，將社群群組呈現給網站訪客。

## 發佈群組{#publish-the-group}

![publish-site](assets/publish-site.png)

在新建或修改社群群組後，您可以選取`Publish Site`圖示來發佈（啟用）群組。

成功發佈群組後，會出現訊息：

![群組發佈](assets/group-published.png)

>[!CAUTION]
>
>父社區站點和父組應已發佈。
>
>社群網站和巢狀群組應以自上而下的方式發佈。

## 刪除組{#delete-the-group}

![刪除圖示](assets/deleteicon.png)

從社群群組主控台中刪除群組，方法是選取「刪除群組」圖示，此圖示會顯示在將滑鼠暫留在群組上。

這會移除與群組相關的所有項目，例如永久刪除群組的所有內容，並從系統中移除使用者成員資格。
