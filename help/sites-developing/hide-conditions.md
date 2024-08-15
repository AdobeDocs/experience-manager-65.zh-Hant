---
title: 使用隱藏條件
description: 隱藏條件可用於判斷元件資源是否已轉譯。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 3%

---

# 使用隱藏條件 {#using-hide-conditions}

隱藏條件可用於判斷元件資源是否已轉譯。 例如，範本作者在[範本編輯器](/help/sites-authoring/templates.md)中設定核心元件[list元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html)，並決定停用根據子頁面建立清單的選項。 在「設計」對話方塊中停用此選項會設定屬性，以便在呈現清單元件時，會評估隱藏條件，並且不會顯示顯示子頁面的選項。

## 概觀 {#overview}

對於使用者而言，對話方塊可能會因許多選項而變得複雜，他們只能使用一小部分可用的選項。 這可能會導致使用者無法承受的使用者介面體驗。

透過使用隱藏條件，管理員、開發人員和超級使用者便能根據一組規則來隱藏資源。 此功能可讓他們決定在作者編輯內容時應該顯示哪些資源。

>[!NOTE]
>
>根據運算式隱藏資源不會取代ACL許可權。 內容保持可編輯狀態但不會顯示。

## 實作與使用細節 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper`負責根據`granite:hide`屬性的存在與值來篩選資源，該屬性位於要篩選的欄位上。 `/libs/cq/gui/components/authoring/dialog/dialog.jsp`的實作包含`FilteringResourceWrapper.`的執行個體

實作使用Granite [ELResolver API](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)，並透過ExpressionCustomizer新增`cqDesign`自訂變數。

以下是位於`etc/design`下或作為內容原則之設計節點上的幾個隱藏條件範例。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏運算式時，請牢記以下事項：

* 若要有效，應該表示找到屬性的範圍（例如`cqDesign.myProperty`）。
* 值是唯讀的。
* 功能（如有需要）應限製為服務提供的一組給定值。

## 範例 {#example}

隱藏條件的範例可以在AEM中找到，特別是[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hant)。 例如，考慮[清單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html)。

[使用範本編輯器](/help/sites-authoring/templates.md)，範本作者可以在設計對話方塊中定義清單元件中哪些選項可供頁面作者使用。 您可以啟用或停用選項，例如是否允許清單成為靜態清單、子頁面清單、標籤頁面清單等。

如果範本作者選擇停用子頁面選項，則會設定設計屬性，並評估其隱藏條件，導致該選項無法針對頁面作者呈現。

1. 依預設，頁面作者可以使用清單核心元件，透過選擇選項&#x200B;**子頁面**&#x200B;來使用子頁面建立清單。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在清單核心元件的「設計」對話方塊中，範本作者可以選擇選項&#x200B;**停用子項**，以防止根據子頁面產生清單的選項顯示給頁面作者。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 原則節點是在`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`下建立，屬性`disableChildren`設定為`true`。
1. 隱藏條件定義為對話方塊屬性節點`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`上`granite:hide`屬性的值

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 從設計組態中提取`disableChildren`的值，而運算式`${cqDesign.disableChildren}`評估為`false`，表示選項將不會呈現為元件的一部分。

   您可以在GitHub](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40)中檢視隱藏運算式為`granite:hide`屬性[的值。

1. 使用清單元件時，不再為頁面作者轉譯選項&#x200B;**子頁面**。

   ![chlimage_1-221](assets/chlimage_1-221.png)
