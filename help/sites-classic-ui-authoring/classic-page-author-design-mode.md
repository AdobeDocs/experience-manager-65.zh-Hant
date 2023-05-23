---
title: 在設計模式下配置元件
description: 當實AEM例在開箱後安裝時，會立即在側腳中提供一系列元件。 除此之外，還提供各種其它元件。 可以使用「設計」模式啟用/禁用此類元件。
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

# 在設計模式下配置元件{#configuring-components-in-design-mode}

當實AEM例在開箱後安裝時，會立即在側腳中提供一系列元件。

除此之外，還提供各種其它元件。 可以使用「設計」模式 [啟用/禁用此類元件](#enabledisablecomponentsusingdesignmode)。 啟用並位於您的頁面上後，您可以使用「設計」模式 [配置元件設計的各個方面](#configuringcomponentsusingdesignmode) 編輯屬性參數。

>[!NOTE]
>
>編輯這些元件時必須小心。 設計設定通常是整個網站設計的一個組成部分，因此它們只應由具有適當權限（和經驗）的人（通常是管理員或開發人員）更改。 請參閱 [開發元件](/help/sites-developing/components.md) 的子菜單。

這實際上涉及添加或刪除頁面段落系統中允許的元件。 段落制度( `parsys`)是包含所有其它段落元件的複合元件。 段落系統允許作者將不同類型的元件添加到包含所有其他段落元件的頁面中。 每個段落類型都表示為元件。

例如，產品頁面的內容可能包含包含以下內容的段落系統：

* 產品的影像（以影像或文本時間段的形式）
* 產品說明（作為文本段落）
* 具有技術資料的表（表段）
* 表單用戶填寫（在表單開始、表單元素和表單結束段落時）

>[!NOTE]
>
>請參閱 [開發元件](/help/sites-developing/components.md#paragraphsystem) 和 [使用模板和元件的指南](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 有關 `parsys`。

## 啟用/禁用元件 {#enable-disable-components}

在「設計」模式下，會最小化邊框，並且您可以配置可用於創作的元件：

1. 要進入「設計」模式，請開啟頁面進行編輯並使用「側腳」表徵圖：

   ![](do-not-localize/chlimage_1.png)

1. 按一下 **編輯** (b)關於段落制度(**零件設計**)。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 將開啟一個對話框，列出Sidek中顯示的元件組及其包含的各個元件。

   根據需要選擇添加或刪除要在旁鍵中可用的元件。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. 在「設計」模式下，Sidekick最小化。 通過按一下箭頭，可以最大化「側腳」並返回「編輯模式」：

   ![](do-not-localize/sidekick-collapsed.png)

## 配置元件的設計 {#configuring-the-design-of-a-component}

在「設計」模式下，還可以為各個元件配置屬性。 每個元件都有其自己的參數，以下示例顯示 **影像** 元件：

1. 要進入「設計」模式，請開啟頁面進行編輯並使用「側腳」表徵圖：

   ![](do-not-localize/chlimage_1-1.png)

1. 可以配置元件的設計。

   例如，如果按一下 **編輯** 在映像元件(**影像設計**)可以配置元件特定的參數：

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 按一下 **確定** 的子菜單。

1. 在「設計」模式下，Sidekick最小化。 通過按一下箭頭，可以最大化「側腳」並返回「編輯模式」：

   ![](do-not-localize/sidekick-collapsed-1.png)
