---
title: 在設計模式中設定元件
seo-title: 在設計模式中設定元件
description: 當AEM例項安裝在現成可用時，sidekick中會立即提供選取的元件。 除了這些外，還有各種其他元件可供使用。 您可以使用「設計」模式來啟用／停用此類元件。
seo-description: 當AEM例項安裝在現成可用時，sidekick中會立即提供選取的元件。 除了這些外，還有各種其他元件可供使用。 您可以使用「設計」模式來啟用／停用此類元件。
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 在設計模式中設定元件{#configuring-components-in-design-mode}

當AEM例項安裝在現成可用時，sidekick中會立即提供選取的元件。

除了這些外，還有各種其他元件可供使用。 您可以使用「設計」模式 [來啟用／停用此類元件](#enabledisablecomponentsusingdesignmode)。 啟用並位於頁面上時，您就可以使用「設計」模式 [來編輯屬性參數](#configuringcomponentsusingdesignmode) ，以設定元件設計的各個方面。

>[!NOTE]
>
>編輯這些元件時必須小心。 設計設定通常是整個網站設計不可或缺的一環，因此只有擁有適當權限（和經驗）的人（通常是管理員或開發人員）才能變更設定。 如需詳 [細資訊](/help/sites-developing/components.md) ，請參閱開發元件。

這實際上包括新增或移除頁面段落系統中允許的元件。 段落系統( `parsys`)是包含所有其他段落元件的複合元件。 段落系統可讓作者將不同類型的元件新增至包含所有其他段落元件的頁面。 每個段落類型都表示為元件。

例如，產品頁面的內容可能包含包含下列內容的段落系統：

* 產品的影像（影像或文欄位落的形式）
* 產品說明（文欄位）
* 具有技術資料的表（作為表段）
* 表單使用者填寫（表單開頭、表單元素和表單結尾段落）

>[!NOTE]
>
>如需 [詳細資訊](/help/sites-developing/components.md#paragraphsystem) ，請參 [閱使用範本和元件的開發元件與指引](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)`parsys`。

## 啟用／停用元件 {#enable-disable-components}

在「設計」模式中，sidekick會最小化，您可以設定可供編寫的元件：

1. 若要進入「設計」模式，請開啟頁面進行編輯，然後使用「側腳」圖示：

   ![](do-not-localize/chlimage_1.png)

1. 按一 **下「段落** 」系統(**par設計**)上的「編輯」。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 將開啟一個對話框，列出Sidekick中顯示的元件組及其包含的各個元件。

   視需要選取要新增或移除的元件，以便在sidekick中使用。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. Sidekick在「設計」模式下最小化。 按一下箭頭，您可將Sidekick最大化並返回「編輯模式」:

   ![](do-not-localize/sidekick-collapsed.png)

## 配置元件設計 {#configuring-the-design-of-a-component}

在「設計」模式中，您也可以為個別元件設定屬性。 每個元件都有其自己的參數，以下示例顯示 **Image** 元件：

1. 若要進入「設計」模式，請開啟頁面進行編輯，然後使用「側腳」圖示：

   ![](do-not-localize/chlimage_1-1.png)

1. 您可以設定元件的設計。

   例如，如果按一下「影像」 **元件(** Design of image ****)上的「編輯」(Edit)，則可以配置元件特定參數：

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 按一 **下「確定** 」以儲存變更。

1. Sidekick在「設計」模式下最小化。 按一下箭頭，您可將Sidekick最大化並返回「編輯模式」:

   ![](do-not-localize/sidekick-collapsed-1.png)
