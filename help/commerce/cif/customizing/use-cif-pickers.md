---
title: CIF產品及類別選擇器的使用
description: 瞭解如何在客戶商務元件中使用CIF產品與類別選擇器，以支援作者和行銷人員有效率地處理商務產品與型錄資料。
sub-product: 商務
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: 商務整合框架
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# 內AEM容與商務製作挑選器{#cif-pickers}

內容與AEM商務製作提供一套製作工具，可協助作者和AEM行銷人員有效率地使用商務產品資料和型錄。 產品選擇器和類別選擇器是CIF附加元件的一部分，並由CIF核心元件使用。 專案可在任何元件對話方塊中使用這些選擇器來選取產品或類別。

## 產品挑選器 {#product-picker}

若要在專案元件中使用產品選擇器，開發人員必須將`commerce/gui/components/common/cifproductfield`新增至元件對話方塊。 例如，請針對cq:dialog使用下列項目：

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

產品欄位可讓使用者透過不同的檢視，導覽至想要選擇的產品。 依預設，產品欄位會傳回產品的ID，但可使用`selectionId`屬性加以設定。

產品選擇器欄位支援下列選用屬性：

- selectionId(id、uid、sku、slug、combinedSlug、combinedSku)-允許選擇器傳回的產品屬性（預設= id）。 使用sku會傳回所選產品的sku，而使用combinedSku會傳回字串，例如base#variant與基本產品的sku和所選變體，或是單一sku（如果選取了基本產品）。
- filter(folderOrProduct、folderOrProductOrVariant)-篩選檢查器在產品樹狀結構中顯示的內容。 folderOrProduct —— 轉換資料夾和產品。 folderOrProductOrVariant —— 轉換資料夾、產品和產品變型。 如果轉譯了產品或產品變型，在選擇器中也可以選擇它。 (default = folderOrProduct)
- 多重(true, false)-啟用選擇一或多個產品（預設= false）
- emptyText —— 配置選擇器欄位的空文本值

此外，也支援標準診斷欄位屬性，例如`name`、`fieldLabel`或`fieldDescription`。

`cifproductfield`元件需要cif.shell.picker clientlib。 若要將clientlib新增至對話方塊，您可以使用extraClientlibs屬性。

[CIF核心元件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)項目中提供了`cifproductfield`的完整工作示例。 另請參閱核心元件文檔的[自定義對AEM話框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)。

## 類別選擇器{#category-picker}

類別選擇器也可以像產品選擇器一樣，在元件對話方塊中使用。

下列程式碼片段可用於cq:dialog設定：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

類別選擇器欄位支援以下可選屬性：

- selectionId(id, uid, slug, idAndUrlPath, uidAndUrlPath)-允許選擇器返回的類別屬性（預設= id）。 idAndUrlPath &amp; uidAndUrlPath是儲存類別id/uid和url_path的特殊選項，以 |字元，例如1|men/tops。
- 多個(true, false)-啟用選擇一或多個類別（預設= false）

此外，也支援標準診斷欄位屬性，例如`name`、`fieldLabel`或`fieldDescription`。

與`cifproductfield`元件相同，`cifcategoryfield`元件也需要cif.shell.picker clientlib。 要將clientlib添加到對話框中，可以使用`extraClientlibs`屬性。 請參閱核心元件檔案的[自訂對話AEM框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)。

[CIF核心元件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)項目中提供了`cifcategoryfield`的完整工作示例。
