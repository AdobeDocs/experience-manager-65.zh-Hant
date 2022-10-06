---
title: 社群群組主控台
seo-title: Community Groups Console
description: 群組主控台可讓您建立社群群組
seo-description: Groups console lets you create Community groups
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# 社群群組主控台 {#community-groups-console}

「群組」主控台可讓您在社群網站的 [模板結構](/help/communities/sites-console.md#step1) 包括 [組函式](/help/communities/functions.md#groups-function).

* AEM Communities支援在其他群組中巢狀內嵌群組。 在 [新集團的結構](/help/communities/tools-groups.md) 包含群組函式。
* 僅適用於製作環境，會有與網站建立精靈類似的群組建立精靈。
* 將組函式添加到社區站點結構或社區組結構時，可以配置成員是否可以在發佈環境中建立組。

在包含的三個群組範本中，僅 `Reference Group` 範本的結構中包含群組函式。

社群群組的不同層面為：

* **建立**:可在作者上建立新群組，也可在發佈例項上選擇性建立。
* **控制**:群組可為開啟或加密。
* **巢狀**:組可以包含零個或多個組。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>此組控制台僅可從Communities Sites控制台訪問，不與成員混淆 [群組主控台](/help/communities/members.md) 用於管理成員組。
>
>成員群組是在發佈環境中註冊，並使用 [隧道服務](/help/communities/deploy-communities.md#tunnel-service-on-author).

## 群組建立 {#group-creation}

若要存取「群組」主控台：

* 在作者上，以管理員權限登入。
* 從全局導航： **[!UICONTROL 社群]** > **[!UICONTROL 網站]**.
* 選擇要開啟的現有社區站點資料夾。
* 在資料夾中選取社群網站的例項。

   * 社群網站的結構必須包含群組函式。
   * 以下螢幕擷取畫面來自後續的快速入門教學課程 [在發佈時建立群組](/help/communities/published-site.md).

   ![建立群組](assets/create-group.png)

* 選取 **群組資料夾** 來開啟它。

   開啟時，會顯示所有現有群組（無論是在製作或發佈時建立）。

   在此「群組」主控台中，可以製作新群組。

   ![建立 — 新建組](assets/create-new-group.png)

* 選取 **建立群組** 按鈕。

### 步驟1:社群群組範本 {#step-community-group-template}

![多語言社群群組](assets/multi-lingual-group.png)

* **社群群組標題**

   群組的顯示標題。
標題會顯示在群組的已發佈網站上。

* **社群群組說明**

   群組的說明。

* **社群群組根**

   群組的根路徑。
預設的根為父網站，但可將根移至網站內的任何位置。 不建議更改它。

* **其他可用的社群群組語言** 功能表

   使用下拉式清單選取可用的社群群組語言。 功能表會顯示建立父社群網站的所有語言。 使用者可在這些語言中選取，以在這個單一步驟中建立多個地區設定中的群組。 系統會在個別社群網站的群組控制台中，以多種指定語言建立相同的群組。

* **社群群組名稱**

   顯示在URL中的群組根頁面名稱。 請避免在群組名稱中使用底線字元(_)和關鍵字，例如資源和設定。

   * 仔細檢查名稱，因為建立群組後不易變更。
   * 基礎URL會顯示在 `Community Group Name`.
   * 對於有效的URL，請附加&quot;。html&quot;
      *例如*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **社群群組範本** 功能表

   使用下拉式清單來選擇可用 [社群群組範本](/help/communities/tools.md).

### 步驟2:設計 {#step-design}

### 社群群組主題 {#community-group-theme}

![社區群主題](assets/communitygrouptheme.png)

框架使用 `Twitter Bootstrap` 為網站帶來回應式、彈性的設計。 可以選擇多個預載的Bootstrap主題之一來設定所選社區組模板的樣式，或者可以上載Bootstrap主題。

選取後，主題將會以不透明的藍色勾號覆蓋。

您可以選取與父網站主題不同的主題。

發佈社群網站後，您可以 [編輯屬性](#modifyinggroupproperties) 並選取不同的主題。

### 社群群品牌推廣 {#community-group-branding}

![社群品牌](assets/community-group-branding.png)

社群網站品牌化是顯示為頁首的影像，橫跨每個頁面。 可以顯示群組的橫幅，而此橫幅與其他網站頁面不同。

影像的大小應與瀏覽器中頁面的預期顯示大小一樣寬，高度應為120像素。

建立或選取影像時，請記住：

* 影像高度會裁切為120個像素，從影像的上邊緣測量
* 影像會固定至瀏覽器視窗的左側邊緣
* 影像沒有大小調整，因此當影像寬度為：

   * 小於瀏覽器的寬度，影像會水準重複。
   * 大於瀏覽器的寬度，影像就會看起來被裁切。

### 步驟3:設定 {#step-settings}

**協調**

![選擇社群組成員角色](assets/group-admin.png)

**社群群組版主**

依預設，會繼承父社群網站的協調者清單。

可以新增群組的特定協調者。 搜尋成員（從發佈環境）以將其新增為協調者

**群組管理員**

預設情況下，父社區站點管理員也是組的管理員。

但是，可以指派獨立的群組管理員。 群組管理員可以管理其群組（例如G1），並在G1下建立巢狀的子群組。 他們可進一步為子群組指派不同的管理員。

因此，用戶U1可以是組G1中的管理員，也可以是其嵌套組G2中的常規用戶。

**會籍**

成員資格設定允許選擇以下三種方法之一來保護社區組。

![社群群組成員資格](assets/community-group-membership.png)

* **可選成員資格**

   如果選中，則社區組為公共組。 網站成員可以參與群組和貼文，無需明確加入群組。 已選取預設值。

* **必要的成員資格**

   如果選中，則社區組為開啟的組。 社群網站成員可以檢視群組的內容，但需要加入群組才能張貼內容。 通過選擇 `Join` 按鈕。 未選取預設值。

* **限制的成員資格**

   如果選中，則社區組是機密組。 必須明確邀請社群成員。 已邀請的成員將輸入到搜索框中。 稍後可使用 [成員和組控制台](/help/communities/members.md) 製作環境。 未選取預設值。

**縮圖**

![community-group-thumbnail](assets/community-group-thumbnail.png)

縮圖是要在製作和發佈時針對群組顯示的影像。

群組影像的最佳大小為170 x 90像素，且為支援的影像格式(例如JPG或PNG)。

如果未新增影像，則會顯示預設影像。

![縮圖 — 影像](assets/thumbnail-image.png)

### 步驟4:建立群組 {#step-create-group}

![community-create-group](assets/community-create-group.png)

如果需要任何調整，請使用 **返回** 按鈕來製作。

一次 **建立** 已選取並啟動，則建立群組的程式無法中斷。

流程完成後，新子社區站點（組）的卡片將顯示在「社區站點組」控制台中，供作者添加頁面內容或管理員修改站點的屬性。

![建立社群群組](assets/create-community-groups.png)

>[!NOTE]
>
>群組會以所有語言建立，如 [步驟1:社群群組範本](/help/communities/groups.md#step-community-group-template) 在各個社群網站的「社群群組」主控台中，以其他可用的社群群組語言顯示。

## 作者群組內容 {#author-group-content}

![開放網站](assets/open-site.png)

群組的頁面內容可以使用與任何其他AEM頁面相同的工具進行製作。 若要開啟群組以進行製作，請選取將游標移至群組卡片時顯示的「開啟網站」圖示。

## 修改組屬性 {#modify-group-properties}

在社區組建立過程中指定的現有子社區站點的屬性可以通過選擇「編輯站點」表徵圖來修改，該表徵圖在將游標暫留在組卡上時顯示：

![編輯網站](assets/edit-site.png)

下列屬性的詳細資料與 [群組建立](#group-creation) 區段。 無論是在發佈環境或製作環境中建立，任何巢狀群組都可以修改。

![社群群組基本](assets/community-group-basic.png)

### 修改基本 {#modify-basic}

BASIC面板允許修改

* 社群群組標題
* 社群群組說明

不能修改社區組名稱。

選擇不同的社區組模板對現有的社區組站點沒有影響，因為模板和站點之間沒有連接。

反之， [結構](#modify-structure) 可以修改子社區。

### 修改結構 {#modify-structure}

「結構」面板允許修改最初從從作者或發佈環境建立子社區站點時選定的社區組模板建立的結構。 從面板，您可以：

* 拖放其他 [社群功能](/help/communities/functions.md) 進入網站結構。
* 在網站結構中的社群函式例項上：

   * **`Gear icon`**
編輯設定，包括顯示標題、URL和 [特權成員組](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
從網站結構中移除（刪除）函式。

   * **`Grid icon`**
修改網站頂層導覽列中顯示的函式順序。

>[!CAUTION]
>
>雖然顯示標題可以不產生副作用而變更，但不建議編輯屬於社群網站之社群函式的URL名稱。
>
>例如，重新命名URL不會移動現有的UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>組函式必須 *not* be *第一，也不是唯一* 功能。
>
>任何其他函式，例如 [頁面函式](/help/communities/functions.md#page-function)，必須包含在內並列出。

**範例：將日曆函式添加到子社區（組）結構**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改設計 {#modify-design}

「設計」面板允許修改主題：

* [社群群組主題](#community-group-theme)
* [社群群組品牌](#community-group-branding)

   * 捲動至面板底部以變更品牌影像。

### 修改設定 {#modify-settings}

「設定」面板可讓您新增社群 [協調者](#moderation).

### 修改成員資格 {#modify-membership}

此 [會籍](#membership) 面板僅供參考。 無法更改已建立的組成員類型，無論是可選、必需還是受限。

### 修改縮圖 {#modify-thumbnail}

此 [縮圖](#thumbnail) 面板可讓您上傳影像，以在發佈環境以及製作環境的社群網站群組控制台中，向網站訪客呈現社群群組。

## 發佈群組 {#publish-the-group}

![發佈網站](assets/publish-site.png)

在新建立或修改社群群組後，您可以選取 `Publish Site` 表徵圖。

成功發佈群組後，會顯示訊息：

![群組已發佈](assets/group-published.png)

>[!CAUTION]
>
>應已發佈父社區站點和父組。
>
>社群網站和巢狀群組應由上而下發佈。

## 刪除群組 {#delete-the-group}

![刪除圖示](assets/deleteicon.png)

通過選擇「刪除組」表徵圖，從社區組控制台中刪除組，該表徵圖顯示在將滑鼠懸停在組上。

這會刪除與組關聯的所有項，例如，組的所有內容將被永久刪除，並且用戶成員會從系統中刪除。
