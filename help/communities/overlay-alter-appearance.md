---
title: 改變外觀
seo-title: 改變外觀
description: 修改指令碼
seo-description: 修改指令碼
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 改變外觀 {#alter-the-appearance}

## 修改指令碼 {#modify-the-script}

comment.hbs指令碼負責建立每個註解的整體HTML。

若要不在每個張貼的留言旁顯示頭像：

1. 複製 `comment.hbs`自 `libs`至 `apps`

   1. select `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選擇復 **制**
   1. select `/apps/social/commons/components/hbs/comments/comment`
   1. 選擇「 **貼上」**

1. 開啟覆蓋的 `comment.hbs`

   * 按兩下中的節 `comment.hbs`點 `/apps/social/commons/components/hbs/comments/comment folder`

1. 查找以下行，然後刪除或注釋這些行：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

刪除線條，或用&#39;&lt;!—&#39;和&#39;—>&#39;來注釋掉它們。 此外，字元「xxx」也會加入，作為頭像原本所在位置的視覺指標。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 複製覆蓋 {#replicate-the-overlay}

使用複製工具將覆蓋的注釋元件推送到發佈實例。

>[!NOTE]
>
>更強穩的複製形式是在Package Manager中建立包並 [激活](/help/sites-administering/package-manager.md#replicating-packages) 。 可以導出和歸檔包。

在全局導航中，選擇「工 **具」、「部署」、「複製** 」和 **「激活樹」**。

對於「開始路徑」，請 `/apps/social/commons`輸入** **並選擇「啟 **動」**。

![chlimage_1-77](assets/chlimage_1-77.png)

### 檢視結果 {#view-results}

如果您以管理員身分登入發佈例項，例如以管理員／管理員身分登入https://localhost:4503/crx/de，則可驗證覆蓋的元件是否在此。

如果您登出並重新登入為 `aaron.mcdonald@mailinator.com/password` 頁面並重新整理，您會發現張貼的留言不再顯示為頭像，而是顯示簡單的「xxx」。

![chlimage_1-78](assets/chlimage_1-78.png)

