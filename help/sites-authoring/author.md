---
title: 製作
seo-title: 製作
description: 在AEM中編寫概念
seo-description: 在AEM中編寫概念
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 製作{#authoring}

## 製作（和發佈）的概念 {#concept-of-authoring-and-publishing}

AEM提供您兩種環境：

* 作者
* 發佈

這些互動功能可讓您在網站上提供內容——讓您的訪客能夠閱讀。

作者環境提供在實際發佈內容之前建立、更新和檢視此內容的機制：

* 作者會建立並審閱內容(這可以是幾種類型；例如頁面、資產、出版物等)
* 在某個時候，它將發佈到您的網站。

![chlimage_1-132](assets/chlimage_1-132.png)

在作者環境中，AEM的功能可透過兩個UI使用。 針對發佈環境，您設計的整個介面外觀和感覺都提供給您的使用者。

>[!NOTE]
>
>AEM本身可用來製作AEM檔案。
>
>它與Dispatcher一起也用於發佈。

### 作者環境 {#author-environment}

作者的工作環境稱為作 **者環境**。 這為建立內容提供了易於使用的介面(圖形用戶介面（GUI或UI）)。 它通常位於提供完整保護的公司防火牆後方，並要求作者使用已指派適當存取權限的帳戶登入。

>[!NOTE]
>
>您的帳戶需要適當的存取權，才能建立、編輯或發佈內容。

視您的例項和個人存取權限的設定而定，您可以對內容執行許多工作，包括：

* 在頁面上產生新內容或編輯現有內容
* 使用預先定義的範本建立新的內容頁面
* 建立、編輯及管理您的資產和系列
* 建立、編輯及管理出版物
* 開發您的宣傳活動和相關資源
* 開發和管理社群網站
* 移動、複製或刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等

此外，還有管理工作可協助您管理內容：

* 控制變更管理的工作流程；例如。 在發佈前強制執行審核
* 協調單個任務的項目

>[!NOTE]
>
>AEM也由作 [者環境](/help/sites-administering/home.md) （針對大部分工作）管理。

#### 發佈環境 {#publish-environment}

準備就緒後，AEM網站的內容會發佈至發 **布環境**。 在這裡，網站的頁面會根據設計介面的外觀和感覺提供給預期的讀者。

通常，發佈環境位於非軍事區內；換言之，它可供Internet使用，但不再受到內部網路的完全保護。

當AEM網站是社群網站 [，或包含](/help/communities/overview.md)Communities元件時 [](/help/communities/author-communities.md)，登入網站訪客（成員）可能會與社群功能互動。 例如，他們可張貼至論壇、張貼意見或關注其他成員。 會員可以獲得執行通常限於作者環境的活動的權限，例如建立新頁面（社群群組）、部落格文章和協調其他成員的貼文。

>[!NOTE]
>
>遺憾的是，使用的術語有時會有重疊。 這可能發生於：
>
>* **發佈／取消發佈**
   >  這些是讓您的內容在發佈環境（或非）上公開提供之動作的主要條款。
   >
   >
* **啟用／停用**
   >  這些詞語與publish/unpublish同義。
   >
   >
* **複製／複製**
   >  這些是用於指示資料（如頁面內容、檔案、代碼、用戶注釋）在一個環境之間移動的技術術語；例如，在發佈時，或反向複製使用者注釋。
>



#### Dispatcher {#dispatcher}

為了最佳化網站訪客的效能，Dispatcher **[實作](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**負載平衡和快取。
