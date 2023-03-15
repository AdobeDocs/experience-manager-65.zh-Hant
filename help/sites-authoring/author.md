---
title: 製作
seo-title: Authoring
description: AEM中的製作概念
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 製作{#authoring}

## 製作（和發佈）的概念 {#concept-of-authoring-and-publishing}

AEM提供兩種環境：

* 作者
* 發佈

這些內容可讓您在網站上取得內容，以便讓訪客閱讀。

製作環境提供在實際發佈前建立、更新和檢閱此內容的機制：

* 作者會建立並檢閱內容(這可以是數種類型；例如頁面、資產、出版物等)
* 在某個時候，它將發佈到您的網站。

![chlimage_1-132](assets/chlimage_1-132.png)

在製作環境中，AEM的功能可透過兩個UI使用。 針對發佈環境，您可設計供使用者使用之介面的完整外觀與風格。

### 製作環境 {#author-environment}

作者的工作方式為 **作者環境**. 這為建立內容提供了一個易於使用的介面(圖形用戶介面（GUI或UI）)。 它通常位於提供完整保護的公司防火牆後，需要作者使用已指派適當存取權限的帳戶登入。

>[!NOTE]
>
>您的帳戶需要適當的存取權來建立、編輯或發佈內容。

根據您的執行個體和您的個人存取權限的設定方式，您可以對您的內容執行許多工作，包括：

* 在頁面上產生新內容或編輯現有內容
* 使用預先定義的範本建立新內容頁面
* 建立、編輯及管理資產和集合
* 建立、編輯和管理出版物
* 開發您的行銷活動和相關資源
* 開發和管理社群網站
* 移動、複製或刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等

此外，還有一些管理任務可幫助您管理內容：

* 控制如何管理變更的工作流程；例如， 在發佈前強制執行審核
* 協調單個任務的項目

>[!NOTE]
>
>AEM也 [受管](/help/sites-administering/home.md) （大部分任務）。

#### 發佈環境 {#publish-environment}

準備就緒後，AEM網站的內容會發佈至 **發佈環境**. 在此，網站的頁面會根據設計介面的外觀與風格提供給預定對象使用。

發佈環境通常位於非軍事區內；換句話說，網際網路可用，但不再受內部網路的完全保護。

當AEM網站為 [社群網站](/help/communities/overview.md)，或包含 [Communities元件](/help/communities/author-communities.md)，登入網站訪客（成員）可能會與Communities功能互動。 例如，他們可以張貼至論壇、張貼意見或關注其他成員。 可授予成員執行通常限於製作環境之活動的權限，例如建立新頁面（社群群組）、部落格文章及協調其他成員的貼文。

>[!NOTE]
>
>不幸的是，使用的術語有時會重疊。 這可能發生於：
>
>* **發佈/取消發佈**
   >  這些是可讓您的內容在您的發佈環境（或不可）上公開的動作的主要辭彙。
>
>* **啟用/停用**
   >  這些詞語等同於發佈/取消發佈。
>
>* **複製/複製**
   >  這些技術術語用於指示資料（例如頁面內容、檔案、代碼、用戶注釋）從一個環境到另一個環境的移動；即發佈或反向復寫使用者留言時。
>


#### Dispatcher {#dispatcher}

若要最佳化網站訪客的效能，請 **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)** 實作負載平衡和快取。
