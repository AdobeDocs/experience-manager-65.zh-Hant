---
title: 使用隱藏條件
description: 隱藏條件可用於判斷元件資源是否已轉譯。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# 使用隱藏條件 {#using-hide-conditions}

隱藏條件可用於判斷元件資源是否已轉譯。 範本作者設定核心元件時，便屬於此情況 [清單元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) 在 [範本編輯器](/help/sites-authoring/templates.md) 並決定停用根據子頁面建立清單的選項。 在「設計」對話方塊中停用此選項會設定屬性，以便在呈現清單元件時，會評估隱藏條件，並且不會顯示顯示子頁面的選項。

## 概觀 {#overview}

對話方塊可能會變得複雜，使用者可能會使用許多選項，而他們只能使用一小部分可用的選項。 這可能會導致使用者無法承受的使用者介面體驗。

透過使用隱藏條件，管理員、開發人員和超級使用者便能根據一組規則來隱藏資源。 此功能可讓他們決定在作者編輯內容時應該顯示哪些資源。

>[!NOTE]
>
>根據運算式隱藏資源不會取代ACL許可權。 內容保持可編輯狀態但不會顯示。

## 實作和使用方式詳細資料 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 負責根據資源的存在和值來篩選資源 `granite:hide` 屬性，位於要篩選的欄位上。 實作 `/libs/cq/gui/components/authoring/dialog/dialog.jsp` 包含的執行個體 `FilteringResourceWrapper.`

實施作業會使用Granite [ELResolver API](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) 並新增 `cqDesign` 透過ExpressionCustomizer的自訂變數。

以下是位於下方的設計節點上的幾個隱藏條件範例。 `etc/design` 或作為內容原則。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏運算式時，請記住以下事項：

* 若要有效，應表示找到屬性的範圍(例如， `cqDesign.myProperty`)。
* 值為唯讀。
* 功能（如有需要）應限定於服務提供的一組指定功能。

## 範例 {#example}

在整個AEM和 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 尤其是。 例如，請考慮 [列出核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en).

[使用範本編輯器](/help/sites-authoring/templates.md)，範本作者可在「設計」對話方塊中定義清單元件的哪些選項可供頁面作者使用。 您可以啟用或停用選項，例如是否允許清單為靜態清單、子頁面清單、標籤頁面清單等。

如果範本作者選擇停用子頁面選項，則會設定設計屬性並評估隱藏條件，導致選項不為頁面作者呈現。

1. 依預設，頁面作者可以透過選擇選項，使用清單核心元件來使用子頁面建立清單 **子頁面**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在清單核心元件的「設計」對話方塊中，範本作者可以選擇選項 **停用子項** 以防止根據子頁面產生清單的選項顯示給頁面作者。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 原則節點建立於 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` 具有屬性 `disableChildren` 設定為 `true`.
1. 隱藏條件的定義為 `granite:hide` 對話方塊屬性節點上的屬性 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 的值 `disableChildren` 從設計設定和運算式中提取 `${cqDesign.disableChildren}` 評估至 `false`，表示選項不會呈現為元件的一部分。

   您可以將隱藏運算式檢視為 `granite:hide` 屬性 [在此填入GitHub](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. 選項 **子頁面** 使用清單元件時，不再為頁面作者轉譯。

   ![chlimage_1-221](assets/chlimage_1-221.png)
