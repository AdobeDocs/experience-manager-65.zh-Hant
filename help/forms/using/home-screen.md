---
title: 主畫面
description: AEM Forms應用程式首頁畫面的元件說明
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 主畫面{#home-screen}

當您登入AEM Forms應用程式時，系統會將您重新導向至首頁畫面。

## 預設主畫面 {#default-home-screen}

依預設，首頁畫面會顯示所有表單，包括起點和任務(如果連線的伺服器已啟用AEM Forms Workflow)，以及關聯的縮圖。 您可以在AEM Forms伺服器中指定縮圖。

下圖會在預設的Home畫面上以重要元件的標註進行註解。

![Forms應用程式主畫面](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **功能表按鈕**：選取&#x200B;**功能表**&#x200B;按鈕以瀏覽至[工作]、[Forms]、[寄件匣]和[設定]。 如果您的AEM Forms應用程式已連線至AEM Forms JEE伺服器，您會看到「工作」選項。 「工作」選項也會儲存從處理序中的工作建立的草稿。 若為AEM Forms OSGi伺服器，會隱藏工作選項。 Outbox會在與伺服器同步之前儲存已儲存的表單和草稿。 當應用程式與伺服器[&#128279;](../../forms/using/sync-app.md)進行同步處理時，「寄件匣」中所有儲存的表單和草稿都會上傳至AEM Forms伺服器。 如需設定的詳細資訊，請參閱[更新一般設定](../../forms/using/update-general-settings.md)。
1. **任務或表單**：選取您想要使用的列出任務或表單。
1. **水準省略符號**：表示表單有可用的動作。 點選省略符號會顯示作者提供的動作和說明。 當您選取省略符號時，**刪除草稿**&#x200B;和&#x200B;**完成**&#x200B;選項會顯示。
1. **重新整理圖示**：選取重新整理圖示，即可將您的應用程式與AEM Forms伺服器同步。

### 自訂首頁畫面 {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

您可以從應用程式的&#x200B;**[一般設定](../../forms/using/update-general-settings.md)**&#x200B;或HTMLWorkspace上的&#x200B;**偏好設定**&#x200B;標籤變更應用程式的預設主畫面。

對應用程式上首頁畫面設定所做的變更，會影響到目前登入使用者或目前行動裝置上使用者的首頁畫面。

不過，HTMLWorkspace中所做的變更會影響所有登入AEM Forms伺服器的AEM Forms應用程式使用者。
