---
title: 變更外觀
description: 修改指令碼
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 變更外觀 {#alter-the-appearance}

## 修改指令碼 {#modify-the-script}

comment.hbs指令碼負責為每個評論建立整體HTML。

不顯示每個張貼的評論旁的頭像：

1. 複製 `comment.hbs`從 `libs`至 `apps`

   1. 選取 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選取 **[!UICONTROL 複製]**
   1. 選取 `/apps/social/commons/components/hbs/comments/comment`
   1. 選取 **[!UICONTROL 貼上]**

1. 開啟覆蓋的 `comment.hbs`

   * 按兩下節點 `comment.hbs` 在 `/apps/social/commons/components/hbs/comments/comment folder`

1. 尋找下列行，然後刪除或註解它們：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

請刪除線段或將其周圍加上 `<!--` 和 `-->` 所以您應將其註釋掉。 此外，字元「xxx」也會新增為顯示頭像位置的視覺指標。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 復寫覆蓋 {#replicate-the-overlay}

使用復寫工具將覆蓋的註解元件推送至發佈例項。

>[!NOTE]
>
>更強大的復寫形式是在封裝管理員中建立封裝，並且 [啟用](/help/sites-administering/package-manager.md#replicating-packages) it. 套件可以匯出和封存。

在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** 並按一下 **[!UICONTROL 啟動樹狀結構]**.

在起始路徑中，輸入 `/apps/social/commons` 並選取 **[!UICONTROL 啟動]**.

![verify-content-template](assets/verify-content-template.png)

### 檢視結果 {#view-results}

如果您以管理員身分登入發佈執行個體，例如，以admin/admin身分登入https://localhost:4503/crx/de ，則可驗證是否有覆蓋的元件存在。

如果您登出，然後登入身份 `aaron.mcdonald@mailinator.com/password` 並重新整理頁面，您會發現顯示的人偶沒有顯示張貼的評論。 而是顯示簡單的「xxx」。

![create-template-component](assets/create-template-component.png)
