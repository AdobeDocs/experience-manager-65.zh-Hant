---
title: 使用一組自適應表單建立自適應表單
seo-title: 使用一組自適應表單建立自適應表單
description: '使用AEM Forms，將最適化表單整合在一起，以製作單一大型最適化表單，並瞭解其功能。 '
seo-description: '使用AEM Forms，將最適化表單整合在一起，以製作單一大型最適化表單，並瞭解其功能。 '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 使用一組自適應表單建立自適應表單{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 概覽 {#overview}

在工作流程（例如開立銀行帳戶的應用程式）中，您的使用者會填寫多個表格。 您可以將表單堆疊在一起並建立大型表單（父級表單），而不是要求他們填寫一組表單。 當您將最適化表單新增至較大的表單時，它會新增為面板（子表單）。 您可以新增一組子表單來建立父表單。 您可以根據使用者輸入來顯示或隱藏面板。 父表單的按鈕（例如提交和重設）會覆寫子表單的按鈕。 若要在父表單中新增最適化表單，您可以從資產瀏覽器拖放最適化表單（如最適化表單片段）。

可用的功能包括：

* 獨立製作
* 顯示／隱藏適當的表單
* 延遲載入

相較於使用個別元件來建立父表單，獨立製作和延遲載入等功能可改善效能。

>[!NOTE]
>
>您不能將XFA架構的最適化表單／片段用作子表單或父表單。

## 幕後秘辛 {#behind-the-scenes}

您可以在父表單中新增以XSD為基礎的最適化表單和片段。 父表單的結構與任何最適化表 [單相同](../../forms/using/prepopulate-adaptive-form-fields.md)。 當您將最適化表單新增為子表單時，它會新增為父表單中的面板。 綁定子表單的資料儲存在父表 `data`單的XML `afBoundData` 架構部分的根目錄下。

例如，您的客戶會填寫申請表。 表單的前兩個欄位是名稱和身分。 其XML為：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

您在應用程式中新增另一個表格，讓客戶填寫其辦公室地址。 子表單的模式根為 `officeAddress`。 套 `bindref` 用 `/application/officeAddress` 或 `/officeAddress`。 如果 `bindref`未提供，則子表單將添加為子 `officeAddress` 樹。 請參閱下清單格的XML:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

如果您插入另一個表單，讓客戶提供住宅地址，請套用 `bindref` XML `/application/houseAddress or /houseAddress.`的外觀如下：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

如果要保留與方案根（在本示例中）相同的 `Address`子根名稱，請使用索引bindrefs。

例如，套用bindrefs `/application/address[1]` 或 `/address[1]` and `/application/address[2]` or `/address[2]`。 表單的XML為：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

可以使用屬性更改自適應表單／片段的預設子 `bindRef` 樹。 該 `bindRef` 屬性可以指定指向XML架構樹結構中某個位置的路徑。

如果子表單未綁定，則其資料將存 `data`儲在父表 `afUnboundData` 單的XML架構部分的根目錄下。

您可以多次將最適化表單新增為子表單。 請確定已正 `bindRef` 確修改，以便每個使用的自適應表單實例都指向資料根目錄下的不同子根目錄。

>[!NOTE]
>
>如果不同的表單／片段對應至相同的子根，則會覆寫資料。

## 使用資產瀏覽器將最適化表單新增為子表單 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

執行下列步驟，使用資產瀏覽器將最適化表單新增為子表單。

1. 在編輯模式中開啟父表格。
1. 在側欄中，按一下「 **Assets** - ![browser](assets/assets-browser.png)」。 在「資產」下方， **從下拉式清單中選取「最適化表單** 」。
   [ 在「資 ![產」下選擇最適化表單](assets/asset.png)](assets/asset-1.png)

1. 拖放您要新增為子表單的最適化表單。
   [ 拖 ![放網站中的最適化表](assets/drag-drop.png)](assets/drag-drop-1.png)單您拖放的最適化表單會新增為子表單。

