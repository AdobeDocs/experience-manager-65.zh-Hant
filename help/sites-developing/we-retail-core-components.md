---
title: 在We.Retail中試用核心元件
seo-title: 在We.Retail中試用核心元件
description: 'null'
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 1%

---


# 在We.Retail中試用核心元件{#trying-out-core-components-in-we-retail}

核心元件是現代化、有彈性的元件，具備簡單的擴充性，並可讓您輕鬆整合至專案中。 核心元件是以數種主要設計原則為基礎，例如HTL、可用性立即可用、可設定性、版本控制和擴充性。 We.Retail是建立在核心元件上。

## 試用{#trying-it-out}

1. 使用We.Retail範例內容啟動AEM，並開啟[元件主控台](/help/sites-authoring/default-components-console.md)。

   **全域導覽->工具->元件**

1. 在「元件控制台」中開啟邊欄時，您可以篩選特定元件群組。 核心元件位於

   * `.core-wcm`:標準核心元件
   * `.core-wcm-form`:表單提交核心元件

   選擇`.core-wcm`。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 請注意，所有核心元件皆命名為&#x200B;**v1**，這反映出這是此核心元件的第一個版本。 日後將推出一般版本，其版本將與AEM相容，並可輕鬆升級，讓您運用最新的功能。
1. 按一下「**文字(v1)**」。

   查看元件的&#x200B;**資源類型**&#x200B;是`/apps/core/wcm/components/text/v1/text`。 核心元件位於`/apps/core/wcm/components`下，並且每個元件的版本化。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 按一下&#x200B;**Documentation**&#x200B;標籤，以檢視該元件的開發人員檔案。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回元件控制台。 篩選群組&#x200B;**We.Retail**，並選取&#x200B;**Text**&#x200B;元件。
1. 查看&#x200B;**資源類型**&#x200B;如`/apps/weretail`下預期指向元件，但&#x200B;**資源超級類型**&#x200B;指向核心元件`/apps/core/wcm/components/text/v1/text`。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 按一下「**即時使用**」標籤，查看此元件目前使用的頁面。 按一下第一個&#x200B;**感謝您**&#x200B;頁面以編輯頁面。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在「感謝」頁面上，選擇文本元件，然後在元件的編輯菜單中按一下「取消繼承」表徵圖。

   [We.Retail擁有全球化的網站結](/help/sites-developing/we-retail-globalized-site-structure.md) 構，其中內容會透過稱為繼承的 [機制從語言母版推送至即時副本](/help/sites-administering/msm.md)。因此，必須取消繼承，才能允許用戶手動編輯文本。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 按一下&#x200B;**是**&#x200B;確認取消。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消繼承後，您選擇文本元件後，可以使用更多選項。 按一下**編輯**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 您現在可以看到文字元件有哪些編輯選項可用。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 從&#x200B;**頁資訊**&#x200B;菜單中選擇&#x200B;**編輯模板**。
1. 在頁面的「範本編輯器」中，按一下頁面的「版面容器」中「文字」元件的「原則」圖示。********

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 核心元件可讓範本作者設定頁面作者可使用的屬性。 這些功能包括允許的貼上來源、格式選項、可用段落樣式等。

   此類設計對話方塊適用於許多核心元件，並可與範本編輯器搭配運作。 在啟用後，作者可透過元件編輯器使用這些工具。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多資訊 {#further-information}

有關核心元件的詳細資訊，請參閱編寫文檔[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)以獲得核心元件功能的概述，有關技術概述，請參閱開發人員文檔[開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)。

此外，您可能希望進一步調查[可編輯的範本](/help/sites-developing/we-retail-editable-templates.md)。 有關可編輯模板的完整詳細資訊，請參閱編寫文檔[建立頁面模板](/help/sites-authoring/templates.md)或開發人員文檔Page [Templates - Editable](/help/sites-developing/page-templates-editable.md)。
