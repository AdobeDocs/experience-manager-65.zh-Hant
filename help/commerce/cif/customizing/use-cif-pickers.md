---
title: CIF產品和類別選取器的使用
description: 瞭解如何在客戶商務元件中使用CIF產品和類別選取器，以支援作者和營銷人員高效地處理商務產品和目錄資料。
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: dceb187ba28ad7c377e98d29d6c815fe37e23077
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 內AEM容和商業創作選擇者 {#cif-pickers}

Content &amp; Commerce AuthoringAEM提供了一組創作工具，可幫助AEM作者和營銷人員高效地處理商業產品資料和目錄。 產品選取器和類別選取器是CIF附加模組的一部分，由CIF核心元件使用。 項目可以在任何元件對話框中使用這些選擇器來選擇產品或類別。

## 產品挑選器 {#product-picker}

要在項目元件中使用產品選取器，開發人員必須添加 `commerce/gui/components/common/cifproductfield` 對話框。 例如，對cq使用以下命令:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

「產品」(product)欄位允許用戶通過不同視圖導航到要選擇的產品。 預設情況下，產品欄位返回產品的ID，但可以使用 `selectionId` 屬性。

產品選取器欄位支援以下可選屬性：

- selectionId(id、uid、sku、slug、combinedSlug、combinedSku) — 允許選擇機械臂返回的產品屬性（預設= id）。 使用sku返回選定產品的sku，而使用combinedSku返回一個字串，如base#variant，與基本產品和選定變型的sku一起返回；如果選擇了基本產品，則返回一個sku。
- filter(folderOrProduct、folderOrProductOrVariant) — 在產品樹導航時篩選要由選取器呈現的內容。 folderOrProduct — 呈現資料夾和產品。 folderOrProductOrVariant — 呈現資料夾、產品和產品變型。 如果呈現了產品或產品變型，則在選取器中也可選擇它。 （預設值= folderOrProduct）
- 多個(true、false) — 啟用選擇一個或多個產品（預設值=false）
- emptyText — 配置選取器欄位的空文本值

此外，標準的圖表欄位屬性如 `name`。 `fieldLabel`或 `fieldDescription` 也支援。

>[!CAUTION]
>
>的 `cifproductfield` 元件需要 `cif.shell.picker` 客戶端庫。 要將客戶端庫添加到對話框中，可以使用extraClientlibs屬性。
>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，支援 `id` 已移除並替換為 `uid`。 我們強烈建議使用 `sku` 或 `slug` 作為產品標識符。 我們繼續支援 `id` 僅適用於使用CIF核心元件1.x版的項目。

關於 `cifproductfield` 在 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) 項目。 另請參閱 [自定義對話框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) 核心組AEM件文檔。

## 類別選取器 {#category-picker}

類別選取器也可以用類似於產品選取器的方法在元件對話框中使用。

以下代碼段可用於cq:dialog配置：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

類別選取器欄位支援以下可選屬性：

- selectionId(id, uid, slug, urlPath, idAndUrlPath _（不建議使用）_,uidAndUrlPath _（不建議使用）_) — 允許選擇要由選取器返回的類別屬性（預設= id）。
- 多個(true、false) — 啟用選擇一個或多個類別（預設值=false）

此外，標準的圖表欄位屬性如 `name`。 `fieldLabel`或 `fieldDescription` 也支援。

>[!CAUTION]
>
>與 `cifproductfield` 元件 `cifcategoryfield` 元件還要求 `cif.shell.picker` 客戶端庫。 要將客戶端庫添加到對話框，可使用 `extraClientlibs` 屬性。 請參閱 [自定義對話框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) 核心組AEM件文檔。
>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，支援 `id` 已移除並替換為 `uid`。 我們強烈建議使用 `uid` 或 `urlPath` 作為類別標識符。 我們繼續支援 `id` &amp; `idAndUrlPath` 僅適用於使用CIF核心元件1.x版的項目。

關於 `cifcategoryfield` 在 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) 項目。
