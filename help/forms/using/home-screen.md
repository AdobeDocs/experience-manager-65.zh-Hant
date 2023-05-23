---
title: 主螢幕
seo-title: Home screen
description: AEM Forms應用主屏的元件說明
seo-description: Description of the components of the AEM Forms app Home screen
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 主螢幕{#home-screen}

登錄到AEM Forms應用時，您將重定向到「首頁」螢幕。

## 預設首頁螢幕 {#default-home-screen}

預設情況下，「首頁」螢幕顯示所有表單，包括起點和任務(如果連接的伺服器啟用了「AEM Forms工作流」)，以及關聯的縮略圖。 可以在AEM Forms伺服器中指定縮略圖。

下圖注釋為預設「首頁」(Home)螢幕上的基本元件的呼出。

![Formsapp首頁](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **菜單按鈕**:點擊 **菜單** 按鈕以導航到任務、Forms、發件箱和設定。 如果您的AEM Forms應用已連接到AEM FormsJEE伺服器，則可以看到「任務」選項。 「任務」選項還儲存從進程中的任務建立的草稿。 對於AEM FormsOSGi伺服器，「任務」選項隱藏。 發件箱在與伺服器同步之前儲存已保存的表單和草稿。 在應用程式被載入時，「發件箱」中所有保存的表單和草稿都會上載到AEM Forms伺服器 [與伺服器同步](../../forms/using/sync-app.md)。 有關「設定」的資訊，請參見 [更新常規設定](../../forms/using/update-general-settings.md)。
1. **任務或窗體**:按一下要使用的列出任務或表單。
1. **水準省略號**:表示可用於表單的操作。 點擊省略號將顯示作者提供的操作和說明。 的 **刪除草稿** 和 **完成** 選項在按一下省略號時可見。
1. **「刷新」表徵圖**:按一下刷新表徵圖以將你的應用與AEM Forms伺服器同步。

### 自定義主螢幕 {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

您可以從 **[常規設定](../../forms/using/update-general-settings.md)** 或從 **首選項** 頁籤。

對應用上的「首頁」螢幕設定所做的更改將影響當前已記錄或當前移動設備上用戶的「首頁」螢幕。

但是，在HTML工作區中所做的更改會影響登錄到AEM Forms伺服器的所有AEM Forms應用用戶。
