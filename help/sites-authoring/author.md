---
title: 製作
description: Adobe Experience Manager 6.5中的製作和發佈概念。
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 製作{#authoring}

## 製作（和發佈）的概念 {#concept-of-authoring-and-publishing}

AEM提供您兩個環境：

* 作者
* 發佈

這些互動可讓您在網站上提供內容，讓訪客能夠閱讀。

製作環境提供可在實際發佈內容之前，建立、更新和檢閱此內容的機制：

* 作者建立和檢閱內容（可能是幾種型別；例如，頁面、資產、出版物等）
* 這些將在某個時間點發佈到您的網站。

![環境概觀](assets/chlimage_1-132.png)

在製作環境中，AEM的功能可透過兩個UI使用。 對於發佈環境，您可以設計可供使用者使用的介面的完整外觀。

### 作者環境 {#author-environment}

作者在稱為&#x200B;**作者環境**&#x200B;的環境中工作。 這提供了建立內容時易於使用的介面(圖形使用者介面（GUI或UI）)。 它位於提供完整保護的公司防火牆後面，並要求作者使用已指派適當存取許可權的帳戶登入。

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

* 控制變更管理方式的工作流程；例如，在發佈之前強制審查
* 協調個別任務的專案

>[!NOTE]
>
>AEM也是來自製作環境的[已管理](/help/sites-administering/home.md) （針對大部分工作）。

#### Publish環境 {#publish-environment}

準備就緒後，AEM網站的內容會發佈至&#x200B;**發佈環境**。 在此處，根據設計介面的外觀，可將網站頁面提供給目標對象。

通常，發佈環境位於非軍事區內；換言之，可供網際網路使用，但不再受內部網路的完全保護。

當AEM網站是[社群網站](/help/communities/overview.md)，或包含[社群元件](/help/communities/author-communities.md)時，登入網站訪客（成員）可能會與Communities功能互動。 例如，他們可能會張貼至論壇、張貼評論或追蹤其他成員。 可以授予成員執行通常僅限於作者環境的活動的許可權，例如建立新頁面（社群群組）、部落格和稽核其他成員的文章。

>[!NOTE]
>
>不幸的是，使用的術語有時會出現重疊。 這可能發生在以下情況中：
>
>* **Publish /取消發佈**
>  這些是讓您的內容在發佈環境中公開使用（或不公開使用）的動作主要詞語。
>
>* **啟用/停用**
>  這些辭彙與發佈/取消發佈同義。
>
>* **復寫/復寫**
>  這些是技術術語，用於表示資料（例如頁面內容、檔案、程式碼、使用者註解）從一個環境移動到另一個環境；即在發佈或反向複製使用者註解時。
>

#### Dispatcher {#dispatcher}

為了最佳化網站訪客的效能，**[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)**&#x200B;實作負載平衡和快取。
