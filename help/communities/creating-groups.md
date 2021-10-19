---
title: 社群群組
seo-title: Community Groups
description: 建立社群群組
seo-description: Creating community groups
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# 社群群組 {#community-groups}

社群群組功能是讓來自發佈和作者環境的授權使用者（社群成員和作者）在社群網站中動態建立子社群的能力。

若 [組函式](/help/communities/functions.md#groups-function) 存在於 [社群網站](/help/communities/sites-console.md) 結構。

A [社群群組範本](/help/communities/tools-groups.md) 提供動態建立社群群組時的社群群組頁面設計。

當將該功能添加到社區站點的結構或社區站點模板時，為組功能選擇一個或多個組模板。 此群組範本清單會顯示給從社群網站動態建立新群組的成員或作者。

## 建立新群組 {#creating-a-new-group}

建立新社群群組的能力取決於是否有社群網站包含群組函式，例如從 [參考網站範本](/help/communities/sites.md).

以下範例使用從 `Reference Site Template` 如 [開始使用AEM Communities](/help/communities/getting-started.md) 教學課程。

這是在 **群組** 已選取功能表項目：

![新組](assets/new-group.png)

選取 **新組** 表徵圖，將開啟編輯對話框。

在 **設定** 頁簽，您可以提供組的基本功能：

![群組設定](assets/group-settings.png)

* **群組名稱**

   要在社群網站上顯示的群組標題。 請避免在群組名稱中使用底線字元(_)和關鍵字，例如資源和設定。

* **說明**

   要在社群網站上顯示的群組說明。

* **邀請**

   要邀請加入組的成員清單。 預先輸入搜尋可提供社群成員邀請的建議。

* **群組 URL 名稱**

   成為URL一部分的群組頁面名稱。

* **開放群組**

   選取 `Open Group` 指出任何匿名網站訪客都可檢視內容，並將取消選取 `Member Only Group`.

* **僅限成員的群組**

   選取 `Member Only Group` 僅指示組的成員可以查看內容，並將取消選擇 `Open Group`.

在 **範本** 索引標籤是從社區站點結構或社區站點模板中包含組函式時指定的社區組模板清單中進行選擇的功能。

![群組範本](assets/group-template.png)

在 **影像** 索引標籤是上傳影像的功能，可在社群網站的「群組」頁面上顯示群組的影像。 預設樣式表會將影像大小為170 x 90像素。

![群組影像](assets/group-image.png)

選取 **建立群組** 按鈕，則會根據所選的模板建立組的頁面，並為成員資格建立用戶組，並且「組」頁將被更新以顯示新的子社區。

例如，具有名為「焦點組」的新子社區的「組」頁將顯示如下（仍以社區組管理員身份登錄）:

![群組頁面](assets/group-page.png)

選取 `Focus Group` 連結將在瀏覽器中開啟「焦點組」頁面，該頁面具有基於所選模板的初始外觀，並在主社區網站菜單下包含子菜單：

![open-group-page](assets/open-group-page.png)

### 社區組成員清單元件 {#community-group-member-list-component}

此 `Community Group Member List` 元件供群組範本的開發人員使用。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [社群群組要點](/help/communities/essentials-groups.md) 頁面。

如需社群群組的其他相關資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).
