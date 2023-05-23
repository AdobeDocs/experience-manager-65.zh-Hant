---
title: 編寫
seo-title: Authoring
description: 創作概AEM念
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

# 編寫{#authoring}

## 創作（和發佈）的概念 {#concept-of-authoring-and-publishing}

AEM提供了兩種環境：

* 作者
* 發佈

這些交互功能使您能夠在您的網站上提供內容，以便您的訪問者可以閱讀內容。

作者環境提供了在實際發佈此內容之前建立、更新和審閱此內容的機制：

* 作者建立和審閱內容(這可以是幾種類型；例如，頁面、資產、出版物等)
* 在某個時候，它將被發佈到您的網站。

![chlimage_1-132](assets/chlimage_1-132.png)

在作者環境中，通AEM過兩個UI提供功能。 對於發佈環境，您設計了提供給用戶的介面的整個外觀。

### 作者環境 {#author-environment}

作者的作品 **作者環境**。 這為建立內容提供了一個易於使用的介面(圖形用戶介面（GUI或UI）)。 它通常位於提供完全保護並要求作者使用已分配適當訪問權限的帳戶登錄的公司防火牆之後。

>[!NOTE]
>
>您的帳戶需要相應的訪問權限才能建立、編輯或發佈內容。

根據您的實例和個人訪問權限的配置方式，您可以對內容執行許多任務，包括：

* 在頁面上生成新內容或編輯現有內容
* 使用預定義模板建立新內容頁
* 建立、編輯和管理您的資產和收集
* 建立、編輯和管理出版物
* 開發您的活動和相關資源
* 開發和管理社區站點
* 移動、複製或刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等

此外，還有一些管理任務可幫助您管理內容：

* 控制更改管理方式的工作流；例如。 在發佈前強制執行審查
* 協調單個任務的項目

>[!NOTE]
>
>AEM也 [管](/help/sites-administering/home.md) （對於大多數任務）。

#### 發佈環境 {#publish-environment}

準備好後，AEM網站的內容將發佈到 **發佈環境**。 此處，網站的頁面根據設計介面的外觀向目標受眾提供。

通常，發佈環境位於非軍事區內；也就是說，網際網路上可用，但不再受到內部網路的完全保護。

當站AEM點是 [社區站點](/help/communities/overview.md)或包括 [社區元件](/help/communities/author-communities.md)，登錄站點訪問者（成員）可以與社區功能交互。 例如，他們可以發佈到論壇、發佈評論或跟隨其他成員。 可以授予成員執行通常限於作者環境的活動的權限，例如建立新頁面（團體組）、部落格和調整其他成員的帖子。

>[!NOTE]
>
>遺憾的是，使用的術語有時有重疊。 這可能發生在：
>
>* **發佈/取消發佈**
   >  這些是使您的內容在發佈環境中（或不在發佈環境中）公開可用的操作的主要條款。
>
>* **激活/停用**
   >  這些術語與發佈/取消發佈是同義的。
>
>* **複製/複製**
   >  這些技術術語用於指示資料從一個環境到另一個環境的移動（如頁面內容、檔案、代碼、用戶注釋）;即發佈或反向複製用戶注釋時。
>


#### Dispatcher {#dispatcher}

為優化網站訪問者的效能， **[調度](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)** 實現負載平衡和快取。
