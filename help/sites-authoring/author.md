---
title: 編寫
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

# 編寫{#authoring}

## 製作（和發佈）的概念 {#concept-of-authoring-and-publishing}

AEM提供您兩個環境：

* 作者
* 發佈

這些互動可讓您在網站上提供內容，讓訪客能夠閱讀。

作者環境提供機制，可在實際發佈此內容之前建立、更新和檢閱此內容：

* 作者建立並檢閱內容（可以是數種型別；例如，頁面、資產、出版物等）
* 之後會發佈至您的網站。

![chlimage_1-132](assets/chlimage_1-132.png)

在製作環境中，AEM的功能可透過兩個UI使用。 對於發佈環境，您可以設計可供使用者使用的介面的完整外觀。

### 作者環境 {#author-environment}

作者的工作方式稱為 **作者環境**. 這提供建立內容時易於使用的介面(圖形化使用者介面（GUI或UI）)。 它通常位於公司防火牆後面，提供完整保護，並要求作者使用已指派適當存取許可權的帳戶登入。

>[!NOTE]
>
>您的帳戶需要適當的存取權才能建立、編輯或發佈內容。

根據您設定執行個體和個人存取許可權的方式，您可以對內容執行許多工作，包括（其中包括）：

* 在頁面上產生新內容或編輯現有內容
* 使用預先定義的範本來建立新內容頁面
* 建立、編輯及管理您的資產和集合
* 建立、編輯及管理您的出版物
* 開發您的行銷活動和相關資源
* 開發及管理社群網站
* 移動、複製或刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等

此外，還有一些管理任務可協助您管理內容：

* 控制變更管理方式的工作流程；例如。 在發佈前強制執行稽核
* 協調個別任務的專案

>[!NOTE]
>
>AEM也是 [已管理](/help/sites-administering/home.md) （適用於大部分任務）來自製作環境。

#### 發佈環境 {#publish-environment}

準備就緒後，AEM網站的內容會發佈至 **發佈環境**. 在此處，根據設計介面的外觀，目標受眾可以使用網站頁面。

通常，發佈環境位於非軍事區內；換言之，可供網際網路使用，但不再受內部網路的完全保護。

當AEM網站為 [社群網站](/help/communities/overview.md)，或包含 [Communities元件](/help/communities/author-communities.md)，登入的網站訪客（成員）可與Communities功能互動。 例如，他們可能會張貼至論壇、張貼評論或追蹤其他成員。 可以授予成員執行通常僅限於作者環境的活動的許可權，例如建立新頁面（社群群組）、部落格和稽核其他成員的文章。

>[!NOTE]
>
>遺憾的是，使用的術語有時會出現重疊。 這種情況可能發生在以下位置：
>
>* **發佈/取消發佈**
   >  這些是讓您的內容在發佈環境中公開使用（或不公開使用）之動作的主要詞語。
>
>* **啟用/停用**
   >  這些辭彙與發佈/取消發佈同義。
>
>* **復寫/複製**
   >  這些是技術術語，用於表示資料（例如頁面內容、檔案、程式碼、使用者註解）從一個環境移動到另一個環境（即發佈或反向複製使用者註解時）。
>


#### Dispatcher {#dispatcher}

若要最佳化網站訪客的效能， **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)** 實作負載平衡和快取。
