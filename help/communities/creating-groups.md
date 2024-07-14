---
title: 社群群組
description: 瞭解社群群組功能如何讓您透過Publish和Author中的授權使用者，在社群網站中以動態方式建立子社群。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 社群群組 {#community-groups}

社群群組功能可讓發佈和作者環境中的授權使用者（社群成員和作者）在社群網站中動態建立子社群。

當[群組函式](/help/communities/functions.md#groups-function)出現在[社群網站](/help/communities/sites-console.md)結構中時，就會出現這個能力。

當動態建立社群群組時，[社群群組範本](/help/communities/tools-groups.md)會提供社群群組頁面的設計。

將功能新增至社群網站的結構或社群網站範本時，會針對群組功能選取一或多個群組範本。 此群組範本清單會呈現給從社群網站動態建立群組的成員或作者。

## 建立新群組 {#creating-a-new-group}

建立社群群組的能力取決於社群網站是否存在，其中包含群組功能，例如從[參考網站範本](/help/communities/sites.md)建立的功能。

下列範例使用從`Reference Site Template`建立的社群網站，如[AEM Communities快速入門](/help/communities/getting-started.md)教學課程中所述。

這是選取&#x200B;**群組**&#x200B;功能表專案時載入到發佈的頁面：

![新群組](assets/new-group.png)

當您選取&#x200B;**新增群組**&#x200B;圖示時，會開啟編輯對話方塊。

在&#x200B;**設定**&#x200B;標籤下，您提供群組的基本功能：

![群組設定](assets/group-settings.png)

* **群組名稱**

  您要顯示在社群網站上的群組標題。 請避免在群組名稱中使用底線字元(_)和關鍵字（例如資源和設定）。

* **說明**

  要顯示在社群網站上的群組說明。

* **邀請**

  邀請加入群組的成員清單。 預先輸入搜尋可提供社群成員邀請的建議。

* **群組URL名稱**

  成為URL一部分的群組頁面名稱。

* **開啟群組**

  選取`Open Group`表示任何匿名網站訪客都可以檢視內容，並取消選取`Member Only Group`。

* **僅限成員的群組**

  選取`Member Only Group`表示只有群組的成員可以檢視內容，並取消選取`Open Group`。

在&#x200B;**範本**&#x200B;標籤下，您可以從社群群組範本清單中選取。 當群組功能包含在社群網站的結構或社群網站範本中時，會指定這些範本。

![群組範本](assets/group-template.png)

在&#x200B;**影像**&#x200B;標籤下方，您可以上傳要在社群網站的[群組]頁面上為群組顯示的影像。 預設樣式表會將影像大小調整為170 x 90畫素。

![群組影像](assets/group-image.png)

選取&#x200B;**建立群組**&#x200B;後，群組的頁面會根據所選的範本建立，且會為成員資格建立使用者群組，且群組頁面會更新以顯示新的子社群。

例如，具有新子社群「焦點群組」（其影像縮圖已上傳）的「群組」頁面會顯示如下（仍以社群群組管理員身分登入）：

![群組 — 頁面](assets/group-page.png)

選取`Focus Group`連結會在瀏覽器中開啟「焦點群組」頁面，此頁面具有根據所選範本的初始外觀，並包含主要社群網站功能表下的子功能表：

![open-group-page](assets/open-group-page.png)

### 社群群組成員清單元件 {#community-group-member-list-component}

`Community Group Member List`元件是供群組範本的開發人員使用。

### 其他資訊 {#additional-information}

如需開發人員的[社群群組Essentials](/help/communities/essentials-groups.md)頁面的詳細資訊。

如需與社群群組相關的其他資訊，請造訪[管理使用者和使用者群組](/help/communities/users.md)。
