---
title: 更改外觀(HBS)
seo-title: 更改外觀
description: 修改HBS指令碼
seo-description: 修改HBS指令碼
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 更改外觀(HBS){#alter-the-appearance-hbs}

現在，應用程式目錄(/apps)中的自訂註解系統元件已就緒，resourceSuperType參考預設註解系統和已註冊的自訂模型/檢視，便可修改實施。

對於簡單的示範，會移除張貼評論之已登入使用者的顯示頭像視覺功能。

>[!NOTE]
>
>若要使用擴充功能，要受影響(/content)的網站之留言系統的例項必須將其resourceType設為自訂留言系統。

## 修改HBS指令碼{#modify-the-hbs-scripts}

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 開啟[/apps/custom/components/comments/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 對標籤加上註解貼文（~第21行）的顯示圖片進行註解：

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* 開啟[/apps/custom/components/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 註解標籤，其中包含下一個註解項目的頭像（~第44行）:

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 選擇&#x200B;**保存全部**

### 複製自定義應用{#replicate-custom-app}

修改應用程式後，必須重新複製自訂元件。

一種方法是：

* 從主功能表

   * 選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**。
   * 選擇&#x200B;**[!UICONTROL 激活樹]**。
   * 將`Start Path`設為`/apps/custom`。
   * 取消選擇&#x200B;**[!UICONTROL 僅修改]**。
   * 選擇&#x200B;**[!UICONTROL 激活]**&#x200B;按鈕。

### 在已發佈的範例頁面{#view-modified-comment-on-published-sample-page}上檢視已修改的註解

[繼續在](/help/communities/extend-sample-page.md#publish-sample-page) 發佈例項上（仍以相同使用者身分登入）體驗，現在可以重新整理發布環境中的頁面，以檢視要移除頭像的修改：

![view-modified-content](assets/view-modified-content.png)

### 注釋擴展包示例{#sample-comment-extension-package}

附加是在本教學課程中建立的自訂註解應用程式套件。

[取得檔案](assets/sample-comment-extension-6-1-fp3.zip)
