---
title: 設計 HTML5 表單的表單範本
description: AEM Forms可將XFA表單範本轉譯為HTML5格式。 表單設計人員可以使用Designer設計表單範本並使用HTML5轉譯功能。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 3%
---
# 設計 HTML5 表單的表單範本{#designing-form-templates-for-html-forms}

AEM中的HTML5表單元件可將XFA表單範本轉譯為HTML5格式。 表單設計人員可以使用[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)設計表單範本，並使用HTML5轉譯功能。 這些表單範本及其資產可以位於AEM存放庫、檔案系統，或透過http公開。 不過，如果您打算使用Forms Manager管理表單，範本和資產應存放在AEM存放庫中。

雖然HTML5表單在很大程度上符合PDF forms的行為，但兩種格式都有部分功能不適用於其他格式。 例如，Adobe Reader在PDF表單上套用條碼的方式，會因行動表單而異，或是表單的數位簽署方式也會因格式而異。 如需這類變化的詳細資訊，請參閱[HTML5表單與PDF forms之間的功能差異](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)。

如需常見的XFA功能，請參閱下列最佳實務和指導方針，以設計同時適用於兩種格式的表單。

## 最佳做法 {#best-practices}

設計表單範本的大部分步驟（例如結構描述繫結或撰寫表單邏輯）都是相同的。 不過，由於Adobe Reader等厚型使用者端的轉譯與指令碼引擎與瀏覽器表單的內在差異，[最佳實務](/help/forms/using/design-accessible-html5-forms.md)文章中會說明一些建議。 這些最佳實務可協助您設計表單範本，使其在兩種格式中都能如預期般運作。

### 適用於HTML5 Forms的AEM Forms Designer功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 預覽HTML {#preview-html}

「預覽HTML」標籤會新增至「設計」模式，供表單設計人員在設計過程中以HTML5格式預覽表單。 如需如何在AEM Forms Designer中啟用及設定此功能的詳細資訊，請參閱[預覽HTML](../../forms/using/preview-xdp-forms-html.md)。

#### 手寫簽名 {#scribble-signature}

HTML5 Forms的主要目標是觸控裝置。 因此，AEM Forms Designer中新增了塗鴉簽名控制項。 您可以按一下或拖放表單範本上的手寫簽名控制項並進行設定。 它在HTML5轉譯中呈現為草寫欄位，並可用於在觸控裝置上草寫簽名。 在桌上型電腦上，它可以使用滑鼠控制項做為塗鴉欄位。 如需有關如何使用此功能的詳細資訊，請參閱[XFA手寫欄位](../../forms/using/scribble-signature.md)。

![4](assets/4.png)

#### RTF格式 {#rich-text-format}

您可以將文字欄位轉換為RTF文字欄位。 這會新增格式選項清單至文字欄位。 若要轉換，請開啟Forms Designer，並在&#x200B;**[!UICONTROL 設計檢視]**&#x200B;中選取文字欄位。 在&#x200B;**[!UICONTROL 欄位]**&#x200B;索引標籤中，從&#x200B;**[!UICONTROL 欄位格式]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL RTF]**。 現在，當XFA表單呈現為HTML5表單時，欄位會呈現為RTF文字欄位。 選取![最大化](assets/maximize_icon.svg)以檢視其他格式選項。
