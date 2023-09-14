---
title: 社群群組
description: 建立社群群組
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# 社群群組 {#community-groups}

社群群組功能可讓發佈和作者環境中的授權使用者（社群成員和作者）在社群網站中動態建立子社群。

此功能出現於 [群組功能](/help/communities/functions.md#groups-function) 中存在於 [社群網站](/help/communities/sites-console.md) 結構。

A [社群群組範本](/help/communities/tools-groups.md) 動態建立社群群組時，提供社群群組頁面的設計。

將功能新增至社群網站的結構或社群網站範本時，會針對群組功能選取一或多個群組範本。 此群組範本清單會呈現給從社群網站動態建立群組的成員或作者。

## 建立新群組 {#creating-a-new-group}

建立社群群組的能力取決於社群網站是否存在，其中包含群組功能，例如從 [引用網站範本](/help/communities/sites.md).

下列範例使用從建立的社群網站 `Reference Site Template` 如 [AEM Communities快速入門](/help/communities/getting-started.md) 教學課程。

這是會在以下動作時載入到發佈上的頁面： **群組** 已選取功能表專案：

![new-group](assets/new-group.png)

當您選取 **新增群組** 圖示時，編輯對話方塊隨即開啟。

在 **設定** 標籤上，您會提供群組的基本功能：

![群組設定](assets/group-settings.png)

* **群組名稱**

  您要顯示在社群網站上的群組標題。 請避免在群組名稱中使用底線字元(_)和關鍵字（例如資源和設定）。

* **說明**

  要顯示在社群網站上的群組說明。

* **邀請**

  邀請加入群組的成員清單。 預先輸入搜尋可提供社群成員邀請的建議。

* **群組 URL 名稱**

  成為URL一部分的群組頁面名稱。

* **開放群組**

  選取 `Open Group` 指出任何匿名網站訪客都可以檢視內容，並取消選取 `Member Only Group`.

* **僅限成員的群組**

  選取 `Member Only Group` 表示只有群組的成員可以檢視內容，並取消選取 `Open Group`.

在 **範本** 索引標籤中，您可以從社群群組範本清單中選取。 當群組功能包含在社群網站的結構或社群網站範本中時，會指定這些範本。

![group-template](assets/group-template.png)

在 **影像** 索引標籤上，您可以上傳要在社群網站的「群組」頁面上顯示的群組影像。 預設樣式表會將影像大小調整為170 x 90畫素。

![group-image](assets/group-image.png)

藉由選取 **建立群組**，群組的頁面會根據所選的範本建立，且會為成員資格建立使用者群組，且「群組」頁面會更新，以顯示新的子社群。

例如，標題為「焦點群組」且已為其上傳影像縮圖的新子社群之「群組」頁面會顯示如下（仍以社群群組管理員身分登入）：

![group-page](assets/group-page.png)

選取 `Focus Group` 連結會在瀏覽器中開啟「焦點群組」頁面，該頁面具有根據所選範本的初始外觀，並在主要社群網站的功能表底下包含一個子功能表：

![open-group-page](assets/open-group-page.png)

### 社群群組成員清單元件 {#community-group-member-list-component}

此 `Community Group Member List` 元件僅供群組範本的開發者使用。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [社群群組要點](/help/communities/essentials-groups.md) 開發人員頁面。

如需與社群群組相關的其他資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).
