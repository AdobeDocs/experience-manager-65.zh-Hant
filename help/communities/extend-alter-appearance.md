---
title: 變更外觀(HBS)
seo-title: 改變外觀
description: 修改HBS指令碼
seo-description: 修改HBS指令碼
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 變更外觀(HBS){#alter-the-appearance-hbs}

現在，應用程式目錄(/apps)中自訂註解系統的元件已就緒，resourceSuperType會參照預設註解系統並註冊自訂模型／檢視，因此可修改實施。

若要進行簡單展示，會移除張貼評論之已登入使用者所顯示的視覺功能。

>[!NOTE]
>
>若要使用擴充功能，受影響網站(/content)中之留言系統的例項必須將其resourceType設為自訂留言系統。

## 修改HBS指令碼 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* open [/apps/custom/components/comments/comment/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注釋掉標籤，其中包含評論貼文的頭像(~ line 21):

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* open [/apps/custom/components/comments/**comments.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注釋掉標籤，其中包含頭像做為下一個注釋項目(~ line 44):

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* 選擇「 **全部保存」**

### 複製自訂應用程式 {#replicate-custom-app}

修改應用程式後，必須重新複製自訂元件。

一種方法是

* 從主菜單

   * 選擇 **工具>操作>複製**
   * select `Activate Tree`
   * 設定 `Start Path`:to `/apps/custom`
   * deselect `Only Modified`
   * 選擇按 `Activate`鈕

### 在發佈的範例頁面上檢視已修改的註解 {#view-modified-comment-on-published-sample-page}

[繼續在發佈例項](/help/communities/extend-sample-page.md#publish-sample-page) （仍以相同使用者的身分登入）上的體驗，現在可以在發佈環境中重新整理頁面，以檢視修改以移除頭像：

![chlimage_1-136](assets/chlimage_1-136.png)

### 範例注釋擴充功能套件 {#sample-comment-extension-package}

附加是本教學課程中建立的自訂註解應用程式套件。

[取得檔案](assets/sample-comment-extension-6-1-fp3.zip)
