---
title: 首頁畫面
seo-title: 首頁畫面
description: AEM Forms應用程式首頁畫面的元件說明
seo-description: AEM Forms應用程式首頁畫面的元件說明
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# 首頁畫面{#home-screen}

當您登入AEM Forms應用程式時，會將您重新導向至「首頁」畫面。

## 預設首頁畫面 {#default-home-screen}

依預設，「首頁」畫面會顯示所有表單，包括起點和工作（如果連線的伺服器已啟用AEM Forms Workflow），以及相關縮圖。 您可以在AEM Forms伺服器中指定縮圖。

下圖為預設「首頁」畫面上基本元件的註解。

![表單應用程式首頁畫面](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **功能表按鈕**:點選「 **功能表** 」按鈕，以導覽至「工作」、「表單」、「輸出方塊」和「設定」。 如果您的AEM Forms應用程式已連線至AEM Forms JEE伺服器，您就可以看到「工作」選項。 「任務」選項還儲存從進程中的任務建立的草稿。 對於AEM Forms OSGi伺服器，「工作」選項會隱藏。 Outbox會先儲儲存儲存存的表單和草稿，再與伺服器同步。 當應用程式與伺服器同步時，Outbox中所有儲存的表格和草稿都會上傳到AEM Forms [伺服器](../../forms/using/sync-app.md)。 如需「設定」的詳細資訊，請參閱「 [更新一般設定」](../../forms/using/update-general-settings.md)。
1. **任務或表單**:點選您要使用的清單工作或表格。
1. **水準省略號**:表示表單有可用的動作。 點選省略號會顯示作者提供的動作和說明。 點選 **省略號時** ，會顯 **** 示「刪除草稿和完成」選項。
1. **重新整理圖示**:點選重新整理圖示，將您的應用程式與AEM Forms伺服器同步。

### 自訂首頁畫面 {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

您可以從應用程式的「一般設定」或HTML工作區的「偏好設定」索引標籤，變更應用程 **[](../../forms/using/update-general-settings.md)******式的預設「首頁」畫面。

應用程式上對「首頁」畫面設定所做的變更，會對目前已記錄的使用者或目前行動裝置上的使用者產生「首頁」畫面。

不過，在HTML Workspace中所做的變更會影響所有登入AEM Forms伺服器的AEM Forms應用程式使用者。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
