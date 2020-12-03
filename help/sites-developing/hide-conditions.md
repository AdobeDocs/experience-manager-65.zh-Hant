---
title: 使用隱藏條件
seo-title: 使用隱藏條件
description: 隱藏條件可用於確定是否渲染元件資源。
seo-description: 隱藏條件可用於確定是否渲染元件資源。
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# 使用隱藏條件{#using-hide-conditions}

隱藏條件可用於確定是否渲染元件資源。 範本作者在[範本編輯器](/help/sites-authoring/templates.md)中設定核心元件[清單元件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)，並決定停用以子頁面為基礎建立清單的選項時，就是一例。 在設計對話框中禁用此選項會設定屬性，以便在顯示清單元件時，將評估隱藏條件，並且不顯示顯示顯示子頁的選項。

## 概覽 {#overview}

對話方式可能會變得十分複雜，使用者可能只使用其可用選項的一小部分。 這可為使用者帶來龐大的使用者介面體驗。

管理員、開發人員和超級使用者可以使用隱藏條件，根據一組規則來隱藏資源。 這項功能可讓他們決定當作者編輯內容時應顯示哪些資源。

>[!NOTE]
>
>根據表達式隱藏資源不會替換ACL權限。 內容仍可編輯，但不會顯示。

## 實施和使用詳細資訊{#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 負責根據屬性的存在性和值來篩選資 `granite:hide` 源，該屬性位於要篩選的欄位上。`/libs/cq/gui/components/authoring/dialog/dialog.jsp`的實施包含`FilteringResourceWrapper.`的例項

實作會使用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)，並透過ExpressionCustomizer新增`cqDesign`自訂變數。

以下是位於`etc/design`下或作為內容原則之設計節點上的隱藏條件範例。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定義隱藏運算式時，請記住：

* 若要有效，應表示找到屬性的範圍(例如`cqDesign.myProperty`)。
* 值為只讀。
* 函式（如有需要）應限於服務提供的指定集。

## 範例 {#example}

您可在AEM中找到隱藏條件的範例，尤其是[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)。 例如，請考慮[清單核心元件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)。

[使用範本編輯器](/help/sites-authoring/templates.md)，範本作者可在設計對話方塊中定義頁面作者可使用的清單元件選項。例如是否允許清單為靜態清單、子頁清單、標籤頁清單等。 可以啟用或停用。

如果範本作者選擇停用子頁面選項，則會設定設計屬性並評估隱藏條件，這會導致選項無法為頁面作者呈現。

1. 依預設，頁面作者可使用清單核心元件來建立使用子頁面的清單，方法是選擇選項&#x200B;**子頁面**。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在清單核心元件的設計對話框中，模板作者可以選擇&#x200B;**禁用子代**&#x200B;選項，以防止基於子頁生成清單的選項顯示給頁面作者。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 策略節點在`/conf/we-retail/settings/wcm/policies/weretail/components/content/lis`t下建立，屬性`disableChildren`設定為`true`。
1. hide條件定義為對話屬性節點`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`上`granite:hid`e屬性的值

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 從設計配置提取`disableChildren`的值，表達式`${cdDesign.disableChildren}`的求值為`false`，這表示該選項不會作為元件的一部分呈現。

   您可以在GitHub中將hide運算式視為`granite:hide`屬性[的值，此處為](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40)。

1. 當使用清單元件時，頁面作者不再呈現選項&#x200B;**子頁面**。

   ![chlimage_1-221](assets/chlimage_1-221.png)

