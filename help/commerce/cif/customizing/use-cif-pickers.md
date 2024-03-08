---
title: CIF產品和類別選擇器的使用情況
description: 瞭解如何在您的客戶商務元件中使用CIF產品和類別選擇器，以支援作者和行銷人員有效使用商務產品和目錄資料。
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# AEM Content &amp; Commerce編寫選擇器 {#cif-pickers}

AEM Content &amp; Commerce Authoring提供一套製作工具，可協助AEM作者和行銷人員有效使用商務產品資料和目錄。 產品選擇器和類別選擇器是CIF附加元件的一部分，由CIF核心元件使用。 專案可以在任何元件對話方塊中使用這些選擇器來選取產品或類別。

## 產品挑選器 {#product-picker}

若要在專案元件中使用產品選擇器，開發人員必須新增 `commerce/gui/components/common/cifproductfield` 至元件對話方塊。 例如，使用下列專案進行 `cq:dialog`：

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

產品欄位可讓您透過不同檢視導覽至使用者想要選取的產品。 依預設，產品欄位會傳回產品的ID，但可使用 `selectionId` 屬性。

產品選取器欄位支援下列選擇性屬性：

- selectionId (id、uid、sku、slug、combinedSlug、combinedSku) — 可讓您選擇選擇器要傳回的產品屬性（預設值= id）。 使用sku會傳回所選產品的sku，而使用combinedSku則會傳回字串，例如base#variant以及基礎產品和所選變體的sku，如果基礎產品已選取，則傳回單一sku。
- filter (folderOrProduct， folderOrProductOrVariant) — 篩選在導覽產品樹狀結構時挑選器要呈現的內容。 folderOrProduct — 轉譯資料夾和產品。 folderOrProductOrVariant — 轉譯資料夾、產品和產品變體。 如果轉譯了產品或產品變體，也可在選擇器中選取它。 （預設= folderOrProduct）
- 多個(true， false) — 啟用選取一或多個產品的功能（預設= false）
- emptyText — 設定選擇器欄位的空白文字值

此外，標準對話方塊欄位屬性如 `name`， `fieldLabel`，或 `fieldDescription`也支援。

>[!CAUTION]
>
>此 `cifproductfield` 元件需要 `cif.shell.picker` clientlib。 若要將clientlib新增至對話方塊，您可以使用extraClientlibs屬性。
>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，支援 `id` 已移除並取代為 `uid`. Adobe建議使用 `sku` 或 `slug` 作為產品識別碼。 Adobe持續支援 `id` 僅適用於使用CIF核心元件1.x版的專案。

的完整工作範例 `cifproductfield` 您可在以下網址找到： [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) 專案。 另請參閱 [自訂對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) AEM核心元件說明檔案的摘要。

## 類別選取器 {#category-picker}

類別選擇器可用於元件對話方塊中，其使用方式與產品選擇器類似。

以下程式碼片段可用於cq：dialog設定：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

類別選擇器欄位支援下列選擇性屬性：

- selectionId(id， uid， slug， urlPath， idAndUrlPath _（已棄用）_， uidAndUrlPath _（已棄用）_) — 可讓您選擇選擇器要傳回的類別屬性（預設為= id）。
- multiple (true， false) — 啟用選取一或多個類別（預設= false）

此外，標準對話方塊欄位屬性如 `name`， `fieldLabel`，或 `fieldDescription` 也受支援。

>[!CAUTION]
>
>與 `cifproductfield` 組成 `cifcategoryfield` 元件還需要 `cif.shell.picker` clientlib。 若要將clientlib新增至對話方塊，您可以使用 `extraClientlibs` 屬性。 另請參閱 [自訂對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) AEM核心元件說明檔案的摘要。
>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，支援 `id` 已移除並取代為 `uid`. Adobe建議使用 `uid` 或 `urlPath` 作為類別識別碼。 Adobe持續支援 `id` &amp; `idAndUrlPath` 僅適用於使用CIF核心元件1.x版的專案。

的完整工作範例 `cifcategoryfield` 您可在以下網址找到： [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) 專案。
