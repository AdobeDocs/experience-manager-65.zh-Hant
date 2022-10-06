---
title: 更改外觀
seo-title: Alter the Appearance
description: 修改指令碼
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# 更改外觀 {#alter-the-appearance}

## 修改指令碼 {#modify-the-script}

comment.hbs指令碼負責為每個注釋建立整體HTML。

若要不在每個已張貼留言旁顯示頭像：

1. 複製 `comment.hbs`從 `libs`to `apps`

   1. 選取 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選擇 **[!UICONTROL 複製]**
   1. 選取 `/apps/social/commons/components/hbs/comments/comment`
   1. 選擇 **[!UICONTROL 貼上]**

1. 開啟覆蓋物 `comment.hbs`

   * 按兩下節點 `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. 找到以下行，然後刪除或注釋這些行：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

刪除線，或用 `<!--` 和 `-->` 去評論一下。 此外，會新增字元「xxx」，作為顯示頭像原本會變成何處的視覺指標。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 復寫覆蓋 {#replicate-the-overlay}

使用復寫工具將重疊的註解元件推送至發佈執行個體。

>[!NOTE]
>
>更強大的複製形式是在Package Manager中建立包，並 [啟用](/help/sites-administering/package-manager.md#replicating-packages) 它。 可匯出和封存套件。

在全域導覽中，選取 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** 按一下 **[!UICONTROL 激活樹]**.

對於起始路徑，請輸入 `/apps/social/commons` 選取 **[!UICONTROL 啟動]**.

![verify-content-template](assets/verify-content-template.png)

### 查看結果 {#view-results}

如果您以管理員身分登入發佈執行個體(例如，以管理員/管理員身分登入https://localhost:4503/crx/de)，即可驗證覆蓋的元件是否位於該處。

如果您登出並重新登入為 `aaron.mcdonald@mailinator.com/password` 重新整理頁面後，您會看到張貼的留言不再以頭像顯示，而是顯示簡單的「xxx」。

![create-template-component](assets/create-template-component.png)
