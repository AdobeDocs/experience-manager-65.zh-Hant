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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 更改外觀{#alter-the-appearance}

## 修改指令碼{#modify-the-script}

comment.hbs指令碼負責建立每個註解的整體HTML。

若要不在每個張貼的留言旁顯示頭像：

1. 將`comment.hbs`從`libs`複製到`apps`

   1. 選取 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選擇&#x200B;**[!UICONTROL Copy]**
   1. 選取 `/apps/social/commons/components/hbs/comments/comment`
   1. 選擇&#x200B;**[!UICONTROL 貼上]**

1. 開啟覆蓋的`comment.hbs`

   * 按兩下`/apps/social/commons/components/hbs/comments/comment folder`中的節點`comment.hbs`

1. 查找以下行並刪除或注釋它們：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

請刪除這些行，或用`<!--`和`-->`將它們圍起來以注釋掉。 此外，字元「xxx」也會加入，作為頭像原本所在位置的視覺指標。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 複製覆蓋{#replicate-the-overlay}

使用複製工具將覆蓋的注釋元件推送到發佈實例。

>[!NOTE]
>
>更強穩的複製形式是在「包管理器」中建立包，並[activate](/help/sites-administering/package-manager.md#replicating-packages)。 可以導出和歸檔包。

在全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]**，然後按一下&#x200B;**[!UICONTROL 激活樹]**。

對於開始路徑，輸入`/apps/social/commons`並選擇&#x200B;**[!UICONTROL 激活]**。

![verify-content-template](assets/verify-content-template.png)

### 查看結果{#view-results}

如果您以管理員身分登入發佈例項，例如以管理員／管理員身分登入https://localhost:4503/crx/de，則可驗證覆蓋的元件是否在此。

如果您登出並重新登入為`aaron.mcdonald@mailinator.com/password`並重新整理頁面，您會發現張貼的留言不再顯示為頭像，而是顯示簡單的「xxx」。

![create-template-component](assets/create-template-component.png)

