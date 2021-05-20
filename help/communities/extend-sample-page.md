---
title: 將注釋添加到示例頁
seo-title: 將注釋添加到示例頁
description: 將自訂備注新增至頁面
seo-description: 將自訂備注新增至頁面
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 將注釋添加到示例頁{#add-comment-to-sample-page}

現在，自訂註解系統的元件已置於應用程式目錄(/apps)中，因此可以使用擴充元件。 要受影響的網站中評論系統的例項必須將其resourceType設定為自訂評論系統，並包含所有必要的用戶端程式庫。

## 識別所需的Clientlib {#identify-required-clientlibs}

對於擴展注釋，也需要預設注釋的樣式和功能所需的客戶端庫。

[社群元件指南](/help/communities/components-guide.md)識別所需的用戶端程式庫。 瀏覽至「元件指南」並檢視「註解」元件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

請注意，注釋必須有三個用戶端程式庫才能正常呈現和運作。 在引用擴展注釋時需要包括這些注釋，以及[擴展注釋的客戶端庫](/help/communities/extend-create-components.md#create-a-client-library-folder)(`apps.custom.comments`)。

![comments-component1](assets/comments-component1.png)

### 將自訂備注新增至頁面{#add-custom-comments-to-a-page}

由於每頁只能有一個注釋系統，因此建立範例頁面更簡單，如簡短的[建立範例頁面](/help/communities/create-sample-page.md)教學課程所述。

建立後，進入「設計」模式，並使「自定義」元件組可用，以允許將`Alt Comments`元件添加到頁面中。

為了讓注釋顯示並正常運作，必須將注釋的客戶端庫添加到頁的clientlibslist（請參閱[Clientlibs for Communities Components](/help/communities/clientlibs.md)）。

#### 範例頁面{#comments-clientlibs-on-sample-page}上的註解用戶端

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作者：範例頁面{#author-alt-comment-on-sample-page}上的替代註解

![alt-comment](assets/alt-comment.png)

#### 作者：範例頁面註解節點{#author-sample-page-comments-node}

您可以在`/content/sites/sample/en/jcr:content/content/primary/comments`查看範例頁面的注釋節點屬性，以驗證CRXDE中的resourceType。

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 發佈範例頁面{#publish-sample-page}

將自訂元件新增至頁面後，也必須(re)[發佈頁面](/help/communities/sites-console.md#publishing-the-site)。

#### 發佈：範例頁面{#publish-alt-comment-on-sample-page}上的替代註解

發佈自訂應用程式和範例頁面後，即可輸入註解。 登入時，若使用[示範使用者](/help/communities/tutorials.md#demo-users)或管理員，便可張貼留言。

以下是aaron.mcdonald@mailinator.com發佈評論：

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

現在，擴展元件在預設外觀中工作正常，是時候修改外觀了。
