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

不在每個已發佈注釋旁顯示虛擬形象：

1. 複製 `comment.hbs`從 `libs`至 `apps`

   1. 選取 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選擇 **[!UICONTROL 複製]**
   1. 選取 `/apps/social/commons/components/hbs/comments/comment`
   1. 選擇 **[!UICONTROL 貼上]**

1. 開啟覆蓋 `comment.hbs`

   * 按兩下節點 `comment.hbs` 在 `/apps/social/commons/components/hbs/comments/comment folder`

1. 查找以下行，然後刪除或注釋它們：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

刪除線，或用 `<!--` 和 `-->` 來評論一下。 此外，正在添加字元「xxx」作為虛擬形象所在位置的視覺指示器。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 複製覆蓋 {#replicate-the-overlay}

使用複製工具將重疊的注釋元件推送到發佈實例。

>[!NOTE]
>
>更強健的複製形式是在包管理器中建立包， [激活](/help/sites-administering/package-manager.md#replicating-packages) 它。 可以導出和存檔包。

從全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]** 按一下 **[!UICONTROL 激活樹]**。

對於起始路徑輸入 `/apps/social/commons` 選擇 **[!UICONTROL 激活]**。

![驗證內容模板](assets/verify-content-template.png)

### 查看結果 {#view-results}

如果您以管理員身份登錄到發佈實例，例如以admin/admin身份登錄https://localhost:4503/crx/de，則可以驗證重疊的元件是否在其中。

如果註銷並重新登錄為 `aaron.mcdonald@mailinator.com/password` 刷新頁面後，您將注意到已發佈的注釋不再顯示為虛擬形象，而是顯示一個簡單的「xxx」。

![建立模板元件](assets/create-template-component.png)
