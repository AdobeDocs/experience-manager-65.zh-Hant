---
title: 在設計模式中配置元件
description: 當AEM執行個體安裝為現成可用時，sidekick中會立即提供一系列元件。 除此之外，您也可以使用各種其他元件。 您可以使用「設計」模式來啟用/停用此類元件。
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 在設計模式中配置元件{#configuring-components-in-design-mode}

當AEM執行個體安裝為現成可用時，sidekick中會立即提供一系列元件。

除此之外，您也可以使用各種其他元件。 您可以使用「設計」模式來 [啟用/停用此類元件](#enabledisablecomponentsusingdesignmode). 啟用後，若您的頁面上已找到，則可使用「設計」模式， [配置元件設計的各個方面](#configuringcomponentsusingdesignmode) 編輯屬性參數。

>[!NOTE]
>
>編輯這些元件時請務必小心。 設計設定通常是整個網站設計的必要部分，因此只有具有適當權限（和體驗）的人（通常為管理員或開發人員）才應變更這些設定。 請參閱 [開發元件](/help/sites-developing/components.md) 以取得更多資訊。

這實際上包括新增或移除頁面段落系統中允許的元件。 段落制度( `parsys`)是包含所有其他段落元件的複合元件。 段落系統允許作者將不同類型的元件添加到頁面中，因為它包含所有其他段落元件。 每個段落類型都以元件的形式表示。

例如，產品頁面的內容可能包含包含下列內容的段落系統：

* 產品的影像（以影像或文字時段的形式）
* 產品說明（作為文欄位落）
* 具有技術資料的表（作為表段）
* 表單使用者填寫（表單開始、表單元素和表單結束段落）

>[!NOTE]
>
>請參閱 [開發元件](/help/sites-developing/components.md#paragraphsystem) 和 [使用範本和元件的准則](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 如需詳細資訊，請參閱 `parsys`.

## 啟用/停用元件 {#enable-disable-components}

在「設計」模式中，sidekick會最小化，您可以設定可供編寫存取的元件：

1. 若要進入「設計」模式，請開啟要編輯的頁面，並使用Sidekick圖示：

   ![](do-not-localize/chlimage_1.png)

1. 按一下 **編輯** 關於段落制度(**零件設計**)。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 將會開啟對話方塊，列出Sidekick中顯示的元件群組及其所包含的個別元件。

   視需要選取，以新增或移除要在sidekick中使用的元件。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. 在「設計」模式下，Sidekick會最小化。 按一下箭頭，可將Sidekick最大化並返回「編輯模式」：

   ![](do-not-localize/sidekick-collapsed.png)

## 配置元件的設計 {#configuring-the-design-of-a-component}

在「設計」模式中，您也可以為個別元件設定屬性。 每個元件都有其專屬的參數，下列範例顯示 **影像** 元件：

1. 若要進入「設計」模式，請開啟要編輯的頁面，並使用Sidekick圖示：

   ![](do-not-localize/chlimage_1-1.png)

1. 您可以設定元件的設計。

   例如，如果您按一下 **編輯** 在影像元件上(**影像設計**)您可以設定元件特定參數：

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 按一下 **確定** 來儲存變更。

1. 在「設計」模式下，Sidekick會最小化。 按一下箭頭，可將Sidekick最大化並返回「編輯模式」：

   ![](do-not-localize/sidekick-collapsed-1.png)
