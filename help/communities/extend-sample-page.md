---
title: 新增註解至範例頁面
description: 瞭解網站評論系統的執行個體如何必須將其resourceType設定為自訂評論系統，並包含所有必要的使用者端程式庫。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 新增註解至範例頁面  {#add-comment-to-sample-page}

現在，自訂註解系統的元件已放置於應用程式目錄(/apps)中，可以使用擴充元件。 在受影響的網站中，註解系統執行個體必須將其resourceType設定為自訂註解系統，並包含所有必要的使用者端資料庫。

## 識別必要的Clientlibs {#identify-required-clientlibs}

對於延伸的「註釋」，預設「註釋」的樣式和功能所需的使用者端程式庫也是必要的。

此 [社群元件指南](/help/communities/components-guide.md) 會識別所需的使用者端程式庫。 瀏覽至「元件指南」並檢視「註解」元件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

請注意，Comments需要三個使用者端程式庫才能正確呈現和運作。 在參照延伸註解時，必須包含這些註解，並且 [擴充註解的使用者端程式庫](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`)。

![comments-component1](assets/comments-component1.png)

### 新增自訂評論至頁面 {#add-custom-comments-to-a-page}

由於每頁只能有一個註解系統，所以建立範例頁面會比較簡單，如簡介所述 [建立範例頁面](/help/communities/create-sample-page.md) 教學課程。

建立後，進入設計模式並讓自訂元件群組可供使用，以允許 `Alt Comments` 要新增至頁面的元件。

若要讓「註解」顯示並正常運作，必須將「註解」的使用者端程式庫新增至頁面的clientlibslist (請參閱 [適用於社群元件的Clientlibs](/help/communities/clientlibs.md))。

#### 註解範例頁面上的Clientlibs {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作者：範例頁面上的替代註解 {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### 作者：範例頁面評論節點 {#author-sample-page-comments-node}

您可以在CRXDE中檢視範例頁面comments節點的屬性，以驗證resourceType `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 發佈範例頁面 {#publish-sample-page}

將自訂元件新增至頁面後，也需要（重新） [發佈頁面](/help/communities/sites-console.md#publishing-the-site).

#### 發佈：範例頁面上的替代註解 {#publish-alt-comment-on-sample-page}

在發佈自訂應用計畫和範例頁面後，可以輸入註解。 登入時，請使用 [示範使用者](/help/communities/tutorials.md#demo-users) 或管理員可發表評論。

以下是aaron.mcdonald@mailinator.com發表評論：

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

現在，延伸元件已使用預設外觀正常運作，是修改外觀的時候了。
