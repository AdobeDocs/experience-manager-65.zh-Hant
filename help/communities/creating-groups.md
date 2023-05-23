---
title: 社群群組
seo-title: Community Groups
description: 建立社區組
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

社區組功能是使子社區能夠由來自發佈和作者環境的授權用戶（社區成員和作者）在社區站點內動態建立。

當 [組函式](/help/communities/functions.md#groups-function) 在 [社區站點](/help/communities/sites-console.md) 結構。

A [社區組模板](/help/communities/tools-groups.md) 在動態建立社區組時提供社區組頁面的設計。

當將該功能添加到社區站點的結構或社區站點模板時，為組功能選擇一個或多個組模板。 此組模板清單將呈現給從社區站點動態建立新組的成員或作者。

## 建立新組 {#creating-a-new-group}

建立新社區組的能力取決於是否存在包含組功能的社區站點，如從 [參考網站模板](/help/communities/sites.md)。

下面的示例使用從 `Reference Site Template` 如 [AEM Communities入門](/help/communities/getting-started.md) 教程。

這是在 **組** 菜單項：

![新組](assets/new-group.png)

選擇 **新建組** 表徵圖。

在 **設定** 頁籤，可提供組的基本功能：

![組設定](assets/group-settings.png)

* **群組名稱**

   要在社區站點上顯示的組的標題。 避免使用下划線字元(_)和組名中的資源和配置等關鍵字。

* **說明**

   要在社區站點上顯示的組的說明。

* **邀請**

   要邀請加入組的成員清單。 提前鍵入搜索將提供要邀請的社區成員的建議。

* **群組 URL 名稱**

   成為URL一部分的組頁的名稱。

* **開放群組**

   選擇 `Open Group` 指示任何匿名站點訪問者都可以查看內容，並將取消選擇 `Member Only Group`。

* **僅限成員的群組**

   選擇 `Member Only Group` 指示僅組成員可以查看內容，並將取消選擇 `Open Group`。

在 **模板** tab是從社區組模板清單中進行選擇的功能，這些模板是在將組功能包括在社區站點結構或社區站點模板中時指定的。

![組模板](assets/group-template.png)

在 **影像** 頁籤是在社區站點的「組」頁面上上載顯示組的影像的功能。 預設樣式表將將影像大小設定為170 x 90像素。

![組影像](assets/group-image.png)

通過選擇 **建立組** 按鈕，組的頁面將基於所選模板建立，並且會為成員身份建立用戶組，並且「組」頁面將被更新以顯示新的子社區。

例如，帶有名為「焦點組」的新子社區的「組」頁將顯示如下（仍以社區組管理員身份登錄）:

![組頁](assets/group-page.png)

選擇 `Focus Group` 連結將在瀏覽器中開啟「焦點組」頁面，該頁面具有基於所選模板的初始外觀，並在主社區網站的菜單下麵包含一個子菜單：

![開組頁](assets/open-group-page.png)

### 社區組成員清單元件 {#community-group-member-list-component}

的 `Community Group Member List` 元件供組模板的開發人員使用。

### 其他資訊 {#additional-information}

有關 [社區組要件](/help/communities/essentials-groups.md) 頁面。

有關社區團體的其他資訊，請訪問 [管理用戶和用戶組](/help/communities/users.md)。
