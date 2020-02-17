---
title: 社群群組
seo-title: 社群群組
description: 建立社群群組
seo-description: 建立社群群組
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 社群群組{#community-groups}

社群群組功能是讓來自發佈和作者環境的授權使用者（社群成員和作者）在社群網站中動態建立子社群的能力。

當群組功能出現在社 [群網站結構](/help/communities/functions.md#groups-function) 中時，就會 [出現此功能](/help/communities/sites-console.md) 。

社 [群群組範本](/help/communities/tools-groups.md) ，可在動態建立社群群組時，提供社群群組頁面的設計。

將該功能添加到社區站點的結構或社區站點模板時，為組功能選擇一個或多個組模板。 此群組範本清單會顯示給從社群網站動態建立新群組的成員或作者。

## 建立新群組 {#creating-a-new-group}

建立新社群群群組的能力，取決於是否有包含群組功能的社群網站，例如從建立的網站 ` [Reference Site Template](/help/communities/sites.md)`。

下列範例使用從中建立的社群網站，如「AEM社群快速入門」教 `Reference Site Template` 學課程中 [所述](/help/communities/getting-started.md) 。

這是在選取**群組**功能表項目時載入發佈的頁面：

![chlimage_1-85](assets/chlimage_1-85.png)

選擇「新建組」 **表徵圖後** ，將開啟編輯對話框。

在「**設定**」標籤下，您提供群組的基本功能：

![chlimage_1-86](assets/chlimage_1-86.png)

* **群組名**&#x200B;稱要顯示在社群網站上的群組標題。

* **說**&#x200B;明要在社群網站上顯示的群組說明。

* **邀請**&#x200B;要邀請加入群組的成員清單。 提前輸入搜尋將提供社群成員的邀請建議。

* **群組URL名**&#x200B;稱成為URL一部分之群組頁面的名稱。

* **開啟群組**&#x200B;選 `Open Group` 取表示任何匿名網站訪客皆可檢視內容，並會取消選取 `Member Only Group`。

* **僅成員組**&#x200B;選 `Member Only Group` 擇只表示組的成員可以查看內容，並將取消選擇 `Open Group`。

在**模板**頁籤下，可以從社區組模板清單中進行選擇，這些模板是在社區站點結構或社區站點模板中包含組功能時指定的。

![chlimage_1-87](assets/chlimage_1-87.png)

在**Image **標籤下，可上傳影像，以便在社群網站的「群組」頁面上顯示群組。 預設樣式表會將影像大小設為170 x 90像素。

![chlimage_1-88](assets/chlimage_1-88.png)

選取「建 **立群組** 」按鈕後，會根據所選範本建立群組的頁面，並為會籍建立使用者群組，而「群組」頁面將會更新以顯示新的子社群。

例如，具有名為「焦點群組」的新子社群的「群組」頁面（已上傳影像縮圖）會顯示如下（仍以社群群組管理員身分登入）:

![chlimage_1-89](assets/chlimage_1-89.png)

選取連 `Focus Group` 結會在瀏覽器中開啟「焦點群組」頁面，此頁面會根據所選範本具有初始外觀，並在主社群網站的功能表下方包含子功能表：

![chlimage_1-90](assets/chlimage_1-90.png)

### Community Group Member List Component {#community-group-member-list-component}

此元 `Community Group Member List` 件僅供群組範本開發人員使用。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發 [人員的Community Group Essentials](/help/communities/essentials-groups.md) （社群群組基本工具）頁面。

如需社群群組的其他相關資訊，請造 [訪管理使用者和使用者群組](/help/communities/users.md)。
