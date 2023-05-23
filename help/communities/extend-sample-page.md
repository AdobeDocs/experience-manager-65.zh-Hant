---
title: 將注釋添加到示例頁
seo-title: Add Comment to Sample Page
description: 將自定義注釋添加到頁面
seo-description: Add Custom Comments to a page
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
source-wordcount: '370'
ht-degree: 0%

---

# 將注釋添加到示例頁  {#add-comment-to-sample-page}

現在，自定義注釋系統的元件已位於應用程式目錄(/apps)中，可以使用擴展元件。 要受影響的網站中注釋系統的實例必須將其resourceType設定為自定義注釋系統，並包括所有必要的客戶端庫。

## 確定所需的客戶端 {#identify-required-clientlibs}

對於擴展注釋，也需要預設注釋的樣式和功能所必需的客戶端庫。

的 [社區元件指南](/help/communities/components-guide.md) 標識所需的客戶端庫。 瀏覽到「元件指南」並查看「注釋」元件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

請注意「注釋」要正常呈現和運行所需的三個客戶端庫。 需要在引用擴展注釋時包括這些注釋， [擴展注釋的客戶端庫](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`)。

![comments-component1](assets/comments-component1.png)

### 將自定義注釋添加到頁面 {#add-custom-comments-to-a-page}

由於每頁只能有一個注釋系統，因此建立示例頁更簡單，如簡短中所述 [建立示例頁](/help/communities/create-sample-page.md) 教程。

建立後，進入「設計」模式並使「自定義」元件組可用，以允許 `Alt Comments` 要添加到頁面的元件。

為了使注釋正確顯示和運行，必須將注釋的客戶端庫添加到頁面的客戶端libslist（請參見） [社區元件的客戶端](/help/communities/clientlibs.md))。

#### 示例頁上的注釋客戶端 {#comments-clientlibs-on-sample-page}

![注釋clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作者：示例頁上的Alt注釋 {#author-alt-comment-on-sample-page}

![Alt注釋](assets/alt-comment.png)

#### 作者：示例頁注釋節點 {#author-sample-page-comments-node}

通過查看示例頁的注釋節點的屬性，可以驗證CRXDE中的resourceType `/content/sites/sample/en/jcr:content/content/primary/comments`。

![驗證注釋 — crxde](assets/verify-comment-crxde.png)

#### 發佈示例頁 {#publish-sample-page}

將自定義元件添加到頁面後，還需要(re) [發佈頁面](/help/communities/sites-console.md#publishing-the-site)。

#### 發佈：示例頁上的Alt注釋 {#publish-alt-comment-on-sample-page}

在發佈自定義應用程式和示例頁面後，可以輸入注釋。 登錄時，使用 [演示用戶](/help/communities/tutorials.md#demo-users) 或admin，可以發表評論。

以下是aaron.mcdonald@mailinator.com，其中發佈一條評論：

![發佈alt注釋](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

現在，擴展元件在使用預設外觀時似乎工作正常，是時候修改外觀了。
