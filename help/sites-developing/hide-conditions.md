---
title: 使用隱藏條件
seo-title: 使用隱藏條件
description: 隱藏條件可用來判斷元件資源是否已呈現。
seo-description: 隱藏條件可用來判斷元件資源是否已呈現。
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: baf2c6339a554743b6cc69486fb77b121048ba4b
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# 使用隱藏條件{#using-hide-conditions}

隱藏條件可用來判斷元件資源是否已呈現。 範本作者在[範本編輯器](/help/sites-authoring/templates.md)中設定核心元件[清單元件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)並決定停用根據子頁面建立清單的選項時，就會是這個例子。 在設計對話框中禁用此選項會設定一個屬性，以便在呈現清單元件時計算隱藏條件，並且不顯示顯示子頁的選項。

## 概覽 {#overview}

對話可能會變得非常複雜，用戶可能只使用一小部分可供選擇的選項。 這可能導致使用者的使用者介面體驗過量。

使用隱藏條件，管理員、開發人員和超級使用者就能根據一組規則來隱藏資源。 此功能可讓作者決定當作者編輯內容時應顯示哪些資源。

>[!NOTE]
>
>根據運算式隱藏資源不會取代ACL權限。 內容仍可編輯，但不會顯示。

## 實作與使用詳細資料{#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 負責根據屬性的存在和值來篩選 `granite:hide` 資源，此屬性位於要篩選的欄位上。`/libs/cq/gui/components/authoring/dialog/dialog.jsp`的實作包含`FilteringResourceWrapper.`的例項

實作會使用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)並透過ExpressionCustomizer新增`cqDesign`自訂變數。

以下是位於`etc/design`下或作為「內容策略」的設計節點上隱藏條件的一些示例。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏運算式時請記住：

* 為了有效，應表示找到屬性的範圍(例如`cqDesign.myProperty`)。
* 值為唯讀。
* 函式（如有需要）應限於服務提供的指定集。

## 範例 {#example}

您可以在AEM中找到隱藏條件的範例，尤其是[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)。 例如，請考慮[清單核心元件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)。

[範本作者可使用範本編輯器](/help/sites-authoring/templates.md)，在設計對話方塊中定義頁面作者可使用的清單元件選項。例如是否允許該清單為靜態清單、子頁清單、標籤頁清單等。 可啟用或停用。

如果範本作者選擇停用子頁面選項，則會設定設計屬性並據此評估隱藏條件，導致選項無法為頁面作者呈現。

1. 依預設，頁面作者可使用清單核心元件，透過選擇&#x200B;**Child pages**&#x200B;選項，使用子頁面來建立清單。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在清單核心元件的設計對話方塊中，範本作者可選擇選項&#x200B;**停用子項**，以防止將根據子頁面產生清單的選項顯示給頁面作者。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 在`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`下建立策略節點，其屬性`disableChildren`設定為`true`。
1. 隱藏條件定義為對話屬性節點`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`上`granite:hide`屬性的值

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 從設計配置提取`disableChildren`值，表達式`${cqDesign.disableChildren}`評估為`false`，這表示將不會在元件中呈現該選項。

   您可以在此處](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40)檢視GitHub中以`granite:hide`屬性[值形式顯示隱藏運算式。

1. 使用清單元件時，頁面作者不再轉譯&#x200B;**子頁面**&#x200B;選項。

   ![chlimage_1-221](assets/chlimage_1-221.png)
