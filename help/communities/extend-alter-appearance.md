---
title: 更改外觀(HBS)
seo-title: Alter the Appearance
description: 修改HBS指令碼
seo-description: Modify the HBS scripts
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
source-wordcount: '271'
ht-degree: 0%

---

# 更改外觀(HBS) {#alter-the-appearance-hbs}

現在應用程式目錄(/apps)中自定義注釋系統的元件已就位，並且resourceSuperType引用了預設注釋系統和已註冊的自定義模型/視圖，因此可以修改實現。

為了簡單演示，刪除發佈評論的登錄用戶所顯示的視覺功能。

>[!NOTE]
>
>要使用副檔名，要受影響的網站(/content)中注釋系統的實例必須將其resourceType設定為自定義注釋系統。

## 修改HBS指令碼 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 開啟 [/apps/custom/components/comments/comments/comments///////////////////////////////////////////////////////////////////**注釋.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注釋掉包括注釋帖子（~行21）的化身的標籤：

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* 開啟 [/apps/custom/components/comments/comments/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////**注釋.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注釋掉包含下一個注釋條目（~行44）的虛擬形象的標籤：

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 選擇 **全部保存**

### 複製自定義應用 {#replicate-custom-app}

在應用程式被修改後，必須重新複製自定義元件。

一個方法是：

* 從主菜單

   * 選擇 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**。
   * 選擇 **[!UICONTROL 激活樹]**。
   * 設定 `Start Path` 至 `/apps/custom`。
   * 取消選擇 **[!UICONTROL 僅修改]**。
   * 選擇 **[!UICONTROL 激活]** 按鈕

### 查看已發佈示例頁上的已修改注釋 {#view-modified-comment-on-published-sample-page}

[繼續體驗](/help/communities/extend-sample-page.md#publish-sample-page) 在仍以同一用戶身份登錄的發佈實例上，現在可以刷新發佈環境中的頁面，以查看修改以刪除虛擬形象：

![視圖修改內容](assets/view-modified-content.png)

### 注釋擴展包示例 {#sample-comment-extension-package}

附加是本教程中建立的自定義注釋應用程式的包。

[取得檔案](assets/sample-comment-extension-6-1-fp3.zip)
