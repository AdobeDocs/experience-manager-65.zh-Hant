---
title: 設計HTML5表單的表單範本
seo-title: 設計HTML5表單的表單範本
description: AEM Forms提供將XFA表單範本轉換為HTML5格式的功能。 表單設計人員可使用設計人員來設計表單範本，並使用HTML5轉譯功能。
seo-description: AEM Forms提供將XFA表單範本轉換為HTML5格式的功能。 表單設計人員可使用設計人員來設計表單範本，並使用HTML5轉譯功能。
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# 設計HTML5表單的表單範本{#designing-form-templates-for-html-forms}

AEM中的HTML5表單元件提供將XFA表單範本轉換為HTML5格式。 表單設計人員可使用[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)來設計表單範本，並使用HTML5轉譯功能。 這些表單範本及其資產可以駐留在AEM儲存庫、檔案系統或透過http公開。 不過，如果您打算使用Forms Manager管理表單，範本和資產應位於AEM儲存庫中。

雖然HTML5表格在很大程度上與PDF表格的行為相符，但這兩種格式中都有某些功能不適用於其他格式。 例如，Adobe Reader中PDF表單上套用條碼的方式會因行動表單而異，或表格的數位簽署方式也會因格式而異。 如需此類變化的詳細資訊，請參閱[HTML5表單與PDF表單的功能區隔](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)。

如需常見的XFA功能，請參閱下列最佳實務和准則，以設計兩種格式的表格。

## 最佳做法{#best-practices}

設計表單範本（例如架構系結或寫入表單邏輯）的大部分步驟都相同。 但是，由於厚型用戶端（例如Adobe Reader）的轉換和指令碼引擎與瀏覽器表單之間的固有差異，在[最佳實務](/help/forms/using/design-accessible-html5-forms.md)文章中已說明一些建議。 這些最佳實務可協助您設計表單範本，以在兩種格式中都能如預期般運作。

### AEM Forms Designer for HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}的功能

#### 預覽HTML {#preview-html}

「預覽HTML」索引標籤會新增至「表單設計人員的設計」模式中，以在設計程式期間預覽HTML5格式的表單。 如需如何在AEM Forms Designer中啟用和設定此功能的詳細資訊，請參閱「預覽HTML[」。](../../forms/using/preview-xdp-forms-html.md)

#### 塗鴉簽名{#scribble-signature}

HTML5表單的主要目標是觸控裝置。 因此，AEM Forms Designer中新增了新的塗鴉簽名控制項。 您可以按一下或拖放表格範本上的塗鴉簽名控制項，並加以設定。 它會在HTML5轉譯中呈現為塗鴉欄位，並可用於在觸控裝置上塗鴉簽名。 在桌上型電腦上，它可使用滑鼠控制項，做為塗鴉欄位。 如需如何使用此功能的詳細資訊，請參閱[XFA塗鴉欄位](../../forms/using/scribble-signature.md)。

![4](assets/4.png)

#### 富格文本格式{#rich-text-format}

您可以將文字欄位轉換為豐富式文字欄位。 它會在文字欄位中新增格式選項清單。 若要轉換，請開啟Forms Designer，點選&#x200B;**[!UICONTROL 設計檢視]**&#x200B;中的文字欄位。 在&#x200B;**[!UICONTROL 欄位]**&#x200B;頁籤中，從&#x200B;**[!UICONTROL 欄位格式]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 富格文本]**。 現在，當XFA表單轉譯為HTML5表單時，該欄位會轉譯為RTF欄位。 點選「![最大化](assets/maximize_icon.svg)」以檢視其他格式選項。
