---
title: 在We.Retail中試用核心元件
seo-title: 在We.Retail中試用核心元件
description: 在We.Retail中試用核心元件
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---

# 在We.Retail{#trying-out-core-components-in-we-retail}中試用核心元件

核心元件是現代化、有彈性的元件，具有輕鬆的擴充性，並可輕鬆整合至您的專案。 核心元件是以數種主要設計原則為基礎而建立，例如HTL、可用性、現成可用性、可設定性、版本設定和擴充性。 We.Retail已建置在核心元件上。

## 嘗試{#trying-it-out}

1. 從We.Retail範例內容開始AEM，然後開啟[元件主控台](/help/sites-authoring/default-components-console.md)。

   **全局導航 — >工具 — >元件**

1. 在「元件控制台」中開啟邊欄，您可以篩選特定元件群組。 核心元件位於

   * `.core-wcm`:標準核心元件
   * `.core-wcm-form`:表單提交核心元件

   選擇`.core-wcm`。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 請注意，所有核心元件均命名為&#x200B;**v1**，這反映出這是此核心元件的第一個版本。 日後將發行一般版本，其版本與AEM相容，且可輕鬆升級，以便您運用最新功能。
1. 按一下「**文字(v1)**」。

   請參閱元件的&#x200B;**資源類型**&#x200B;是`/apps/core/wcm/components/text/v1/text`。 核心元件位於`/apps/core/wcm/components`下，並根據元件進行版本控制。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 按一下&#x200B;**Documentation**&#x200B;標籤，查看元件的開發人員檔案。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回元件控制台。 篩選群組&#x200B;**We.Retail**&#x200B;並選取&#x200B;**Text**&#x200B;元件。
1. 請參閱&#x200B;**資源類型**&#x200B;如`/apps/weretail`下預期指向元件，但&#x200B;**資源超類型**&#x200B;指向核心元件`/apps/core/wcm/components/text/v1/text`。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 按一下&#x200B;**即時使用**&#x200B;標籤，查看目前使用此元件的頁面。 按一下第一個&#x200B;**感謝**&#x200B;頁面以編輯頁面。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在感謝頁面上，選擇文本元件，然後在元件的編輯菜單中按一下取消繼承表徵圖。

   [We.Retail具有全球化的網站結](/help/sites-developing/we-retail-globalized-site-structure.md) 構，其中內容會透過稱為繼承 [的機制從語言主版推播至即時副本](/help/sites-administering/msm.md)。因此，必須取消繼承，才能讓使用者手動編輯文字。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 按一下&#x200B;**Yes**&#x200B;確認取消。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消繼承並選取文字元件後，可使用更多選項。 按一下** Edit**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 您現在可以查看文字元件有哪些編輯選項可用。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 從&#x200B;**頁面資訊**&#x200B;菜單中選擇&#x200B;**編輯模板**。
1. 在頁面的「模板編輯器」中，按一下頁面的&#x200B;**「佈局容器」**&#x200B;中文本元件的&#x200B;**Policy**&#x200B;表徵圖。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 核心元件可讓範本作者設定頁面作者可使用的屬性。 這些功能包括允許的貼上來源、格式選項、可用的段落樣式等。

   此類設計對話方塊適用於許多核心元件，並與範本編輯器搭配運作。 啟用後，作者可透過元件編輯器使用。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多資訊 {#further-information}

如需核心元件的詳細資訊，請參閱製作檔案[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)以取得核心元件功能的概觀，並參閱開發人員檔案[開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)以取得技術概觀。

您也可以進一步調查[可編輯的範本](/help/sites-developing/we-retail-editable-templates.md)。 有關可編輯模板的完整詳細資訊，請參閱創作文檔[建立頁面模板](/help/sites-authoring/templates.md)或開發人員文檔Page [Templates - Editable](/help/sites-developing/page-templates-editable.md)。
