---
title: 為HTML5表單設計表單模板
seo-title: Designing form templates for HTML5 forms
description: AEM Forms提供將XFA表單範本轉譯為HTML5格式。 表單設計人員可以使用Designer設計表單模板，並使用HTML5轉譯功能。
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# 為HTML5表單設計表單模板{#designing-form-templates-for-html-forms}

AEM中的HTML5表單元件提供將XFA表單範本轉譯為HTML5格式。 表單設計人員可使用 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) 並使用「HTML5」轉譯功能。 這些表單範本及其資產可位於AEM存放庫、檔案系統，或透過http公開。 不過，如果您打算使用Forms Manager管理表單，範本和資產應位於AEM存放庫。

雖然HTML5表單在很大程度上符合PDF forms的行為，但兩種格式中都有某些功能不適用於其他格式。 例如，在Adobe Reader中，條碼如何套用至PDF表單，會因行動表單而異，或表單的數位簽署方式也會因格式而異。 如需此類變異的詳細資訊，請參閱 [HTML5表單和PDF forms之間的功能差異](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

如需常見XFA功能，請參閱下列最佳實務和准則，以設計可同時以兩種格式運作的表單。

## 最佳實務 {#best-practices}

設計表單範本的大部分步驟（例如架構系結或編寫表單邏輯）相同。 不過，由於Adobe Reader等厚型用戶端的轉譯和指令碼引擎與瀏覽器型表單之間固有的差異，有一些建議在 [最佳實務](/help/forms/using/design-accessible-html5-forms.md) 文章。 這些最佳實務可協助您設計表單範本，以便以兩種格式如預期般運作。

### AEM Forms Designer中適用於HTML5 Forms的功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 預覽HTML {#preview-html}

「預覽HTML」頁簽在「設計」模式中添加，以便「表單設計者」在設計過程中以HTML5格式預覽表單。 如需如何在AEM Forms Designer中啟用和設定此功能的詳細資訊，請參閱 [預覽HTML](../../forms/using/preview-xdp-forms-html.md).

#### 手寫簽名 {#scribble-signature}

HTML5表單的主要目標是觸控裝置。 因此，AEM Forms Designer中新增了新的手寫簽名控制項。 您可以按一下或拖放表單範本上的手寫簽名控制項並加以設定。 在HTML5轉譯中，它會呈現為手寫欄位，且可用於在觸控裝置上手寫簽名。 在桌上型電腦上，它可作為手寫欄位使用滑鼠控制。 如需如何使用此功能的詳細資訊，請參閱 [XFA手寫欄位](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### RTF格式 {#rich-text-format}

您可以將文字欄位轉換為RTF欄位。 它會將格式選項清單新增至文字欄位。 若要轉換，請開啟Forms Designer，點選 **[!UICONTROL 設計檢視]**. 在 **[!UICONTROL 欄位]** 索引標籤，選取 **[!UICONTROL RTF]** 從 **[!UICONTROL 欄位格式]** 下拉式清單。 現在，當XFA表單轉譯為「HTML5表單」時，欄位會轉譯為RTF欄位。 點選 ![最大化](assets/maximize_icon.svg) 來查看其他格式選項。
