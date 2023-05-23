---
title: 在We.Retail中嘗試核心元件
seo-title: Trying out Core Components in We.Retail
description: 在We.Retail中嘗試核心元件
seo-description: null
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 3%

---

# 在We.Retail中嘗試核心元件{#trying-out-core-components-in-we-retail}

核心元件是現代、靈活的元件，具有易於擴展性，並允許將簡單整合到項目中。 核心元件是圍繞幾個主要設計原則構建的，如HTL、開箱即用、可配置性、版本控制和可擴充性。 我們，零售是建立在核心元件上。

## 嘗試 {#trying-it-out}

1. 從AEMWe.Retail示例內容開始，然後開啟 [元件控制台](/help/sites-authoring/default-components-console.md)。

   **全局導航 — >工具 — >元件**

1. 在「元件控制台」中開啟滑軌，可以過濾特定元件組。 核心元件可在

   * `.core-wcm`:標準核心元件
   * `.core-wcm-form`:表單提交核心元件

   選擇 `.core-wcm`。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 請注意，所有核心元件均命名為 **v1**&#x200B;這反映出這是這個核心元件的第一版。 常規版本將繼續發佈，它將與版本相容，AEM並允許輕鬆升級，以便您能夠利用最新功能。
1. 按一下 **文本(v1)**。

   看看 **資源類型** 的 `/apps/core/wcm/components/text/v1/text`。 核心元件位於 `/apps/core/wcm/components` 並按元件進行版本控制。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 按一下 **文檔** 頁籤，查看元件的開發人員文檔。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回到元件控制台。 組的篩選器 **We.Retail** 的 **文本** 元件。
1. 看看 **資源類型** 指向元件（如預期） `/apps/weretail` 但 **資源超級類型** 指向核心元件 `/apps/core/wcm/components/text/v1/text`。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 按一下 **即時使用** 頁籤，查看當前使用此元件的頁。 按一下第一個 **謝謝** 的子菜單。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在「感謝您」頁上，選擇文本元件，然後在元件的編輯菜單中按一下「取消繼承」表徵圖。

   [We.Retail擁有一個全球化的網站結構](/help/sites-developing/we-retail-globalized-site-structure.md) 內容從語言母版推送到 [通過稱為繼承的機制進行活動拷貝](/help/sites-administering/msm.md)。 因此，必須取消繼承，以允許用戶手動編輯文本。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 通過按一下 **是**。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消繼承並選擇文本元件後，將有更多選項可用。 按一下** 「編輯」**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 現在，您可以看到文本元件可用的編輯選項。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 從 **頁面資訊** 菜單 **編輯模板**。
1. 在頁面的模板編輯器中，按一下 **策略** 表徵圖 **佈局容器** 的下界。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 核心元件允許模板作者配置頁面作者可使用的屬性。 這些功能包括允許的貼上源、格式設定選項、可用段落樣式等。

   此類設計對話框可用於許多核心元件，並與模板編輯器手動工作。 啟用後，作者可通過元件編輯器獲得這些功能。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多資訊 {#further-information}

有關核心元件的詳細資訊，請參閱創作文檔 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 查看核心元件和開發人員文檔的功能 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 的子菜單。

另外，您可能希望進一步調查 [可編輯模板](/help/sites-developing/we-retail-editable-templates.md)。 請參閱創作文檔 [建立頁面模板](/help/sites-authoring/templates.md) 或開發人員文檔頁面 [模板 — 可編輯](/help/sites-developing/page-templates-editable.md) 的子菜單。
