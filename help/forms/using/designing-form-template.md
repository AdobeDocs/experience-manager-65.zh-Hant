---
title: 為HTML5表單設計表單模板
seo-title: Designing form templates for HTML5 forms
description: AEM Forms提供將XFA表單模板呈現為HTML5格式。 表單設計者可以使用設計器設計表單模板，並使用HTML5格式副本功能。
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
ht-degree: 1%

---

# 為HTML5表單設計表單模板{#designing-form-templates-for-html-forms}

中的HTML5表單組AEM件將XFA表單模板呈現為HTML5格式。 表單設計者可以使用 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw) 並使用HTML5格式副本功能。 這些表單模板及其資產可以駐留在儲存庫AEM、檔案系統中，或通過http公開。 但是，如果您計畫使用Forms管理器管理表單，模板和資產應駐留在儲存AEM庫中。

儘管HTML5表單在很大程度上與PDF forms的行為匹配，但兩種格式中都有一些不適用於其他格式的功能。 例如，在Adobe Reader的PDF表單上應用條形碼的方式因移動表單而異，或表單的數字簽名方式也因格式而異。 有關此類變體的詳細資訊，請參見 [HTML5形式與PDF forms的特徵區分](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)。

有關XFA的常見功能，請參閱以下最佳實踐和指導原則來設計兩種格式的表單。

## 最佳做法 {#best-practices}

設計表單模板（如架構綁定或編寫表單邏輯）的大多數步驟都相同。 但是，由於Adobe Reader和基於瀏覽器的表單等厚客戶端的呈現引擎和指令碼引擎之間固有的差異，在 [最佳做法](/help/forms/using/design-accessible-html5-forms.md) 文章。 這些最佳做法可幫助您設計表單模板以按兩種格式的預期工作。

### AEM Forms設計器中的HTML5Forms功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 預覽HTML {#preview-html}

「預覽HTML」(Preview)頁籤將在「設計」模式下添加，以便在設計過程中以HTML5格式預覽表單。 有關如何在AEM Forms設計器中啟用和配置此功能的詳細資訊，請參見 [預覽HTML](../../forms/using/preview-xdp-forms-html.md)。

#### Scribble簽名 {#scribble-signature}

HTML5表單的關鍵目標是觸摸設備。 因此，在AEM Forms設計器中添加了新的手寫簽名控制項。 您可以按一下或拖放表單模板上的手寫簽名控制項並對其進行配置。 它被呈現為HTML5格式副本中的手寫欄位，並可用於在觸摸設備上手寫簽名。 在台式機上，它可以用作使用滑鼠控制的手寫欄位。 有關如何使用此功能的詳細資訊，請參見 [XFA Scribble欄位](../../forms/using/scribble-signature.md)。

![4](assets/4.png)

#### RTF格式 {#rich-text-format}

可以將文本欄位轉換為富格文本欄位。 它會向文本欄位添加格式選項清單。 要轉換，請開啟Forms設計器，點擊 **[!UICONTROL 設計視圖]**。 在 **[!UICONTROL 欄位]** 頁籤 **[!UICONTROL 富文本]** 從 **[!UICONTROL 欄位格式]** 的子菜單。 現在，當XFA表單呈現為HTML5表單時，該欄位將呈現為富文本欄位。 點擊 ![最大化](assets/maximize_icon.svg) 的子菜單。
