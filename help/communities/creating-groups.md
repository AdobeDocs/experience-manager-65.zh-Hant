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
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# 社群群組 {#community-groups}

社群群組功能是讓來自發佈和作者環境的授權使用者（社群成員和作者）在社群網站中動態建立子社群的能力。

當[社群網站](/help/communities/sites-console.md)結構中存在[群組函式](/help/communities/functions.md#groups-function)時，即會存在此能力。

[社區組模板](/help/communities/tools-groups.md)在動態建立社區組時提供社區組頁面的設計。

當將該功能添加到社區站點的結構或社區站點模板時，為組功能選擇一個或多個組模板。 此群組範本清單會顯示給從社群網站動態建立新群組的成員或作者。

## 建立新組{#creating-a-new-group}

建立新社群群組的能力取決於是否存在包含群組函式的社群網站，例如從[參考網站範本](/help/communities/sites.md)建立的社群網站。

下列範例使用從`Reference Site Template`建立的社群網站，如[AEM Communities](/help/communities/getting-started.md)快速入門教學課程所述。

這是選取&#x200B;**群組**&#x200B;功能表項目時在發佈時載入的頁面：

![新組](assets/new-group.png)

選擇&#x200B;**新建組**&#x200B;表徵圖時，將開啟編輯對話框。

在&#x200B;**Settings**&#x200B;標籤下，提供組的基本功能：

![群組設定](assets/group-settings.png)

* **群組名稱**

   要在社群網站上顯示的群組標題。

* **說明**

   要在社群網站上顯示的群組說明。

* **邀請**

   要邀請加入組的成員清單。 預先輸入搜尋可提供社群成員邀請的建議。

* **群組 URL 名稱**

   成為URL一部分的群組頁面名稱。

* **開放群組**

   選擇`Open Group`表示任何匿名網站訪客可以查看該內容，並將取消選擇`Member Only Group`。

* **僅限成員的群組**

   選擇`Member Only Group`僅指示組的成員可以查看內容，並將取消選擇`Open Group`。

在&#x200B;**Template**標籤下，
從群組模板清單中選擇，當群組函式包含在社區站點的結構或社區站點模板中時，這些模板已指定。

![群組範本](assets/group-template.png)

在&#x200B;**Image**&#x200B;標籤下，可上傳影像以在社群網站的「群組」頁面上顯示群組。 預設樣式表會將影像大小為170 x 90像素。

![群組影像](assets/group-image.png)

通過選擇&#x200B;**建立組**&#x200B;按鈕，組的頁面將根據所選模板建立，並為成員身份建立用戶組，而「組」頁面將更新以顯示新的子社區。

例如，具有名為「焦點組」的新子社區的「組」頁將顯示如下（仍以社區組管理員身份登錄）:

![群組頁面](assets/group-page.png)

選擇`Focus Group`連結將在瀏覽器中開啟焦點組頁面，該頁面具有基於所選模板的初始外觀，並在主社區站點的菜單下包含子菜單：

![open-group-page](assets/open-group-page.png)

### 社區組成員清單元件{#community-group-member-list-component}

`Community Group Member List`元件供群組範本的開發人員使用。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[社群群組基本資訊](/help/communities/essentials-groups.md)頁面。

有關社區組的其他資訊，請訪問[管理用戶和用戶組](/help/communities/users.md)。
