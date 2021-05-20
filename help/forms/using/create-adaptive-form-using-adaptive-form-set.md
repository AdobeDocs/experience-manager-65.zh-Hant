---
title: 使用一組最適化表單建立最適化表單
seo-title: 使用一組最適化表單建立最適化表單
description: '透過AEM Forms，將最適化表單整合在一起，製作單一大型最適化表單，並了解其功能。 '
seo-description: '透過AEM Forms，將最適化表單整合在一起，製作單一大型最適化表單，並了解其功能。 '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
feature: 適用性表單
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# 使用一組最適化表單建立最適化表單{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 概覽 {#overview}

在工作流程（例如開立銀行帳戶的應用程式）中，您的使用者會填入多份表單。 您可以將表單堆疊在一起並建立大型表單（父表單），而不要求他們填寫一組表單。 將最適化表單新增至較大的表單時，會將其新增為面板（子表單）。 添加一組子表單以建立父表單。 您可以根據使用者輸入來顯示或隱藏面板。 父表單的按鈕（如提交和重置）覆蓋子表單的按鈕。 若要在父表單中新增最適化表單，您可以從資產瀏覽器拖放最適化表單（如最適化表單片段）。

可用功能包括：

* 獨立製作
* 顯示/隱藏適當的表單
* 延遲載入

與使用個別元件來建立父表單相比，獨立製作和延遲載入等功能可提供效能改善。

>[!NOTE]
>
>您無法使用XFA型適用性表單/片段作為子表單或父表單。

## 幕後{#behind-the-scenes}

您可以在父表單中新增XSD式最適化表單和片段。 父表單的結構與[任何最適化表單](../../forms/using/prepopulate-adaptive-form-fields.md)相同。 將適用性表單新增為子表單時，會將其新增為父表單中的面板。 綁定子表單的資料儲存在父表單XML架構的`afBoundData`部分的`data`根下。

例如，您的客戶會填寫應用程式表單。 表單的前兩個欄位是名稱和身分。 其XML為：

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

您可在應用程式中新增另一個表單，讓客戶填寫其辦公室地址。 子窗體的架構根為`officeAddress`。 應用`bindref` `/application/officeAddress`或`/officeAddress`。 如果未提供`bindref`，則子表單會新增為`officeAddress`子樹狀結構。 請參閱下面的表單XML:

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

如果插入另一個允許客戶提供住宅地址的表單，請應用`bindref` `/application/houseAddress or /houseAddress.` XML如下：

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

如果要保留與架構根（在本示例中為`Address`）相同的子根名稱，請使用索引二進位檔。

例如，應用bindrefs `/application/address[1]`或`/address[1]`和`/application/address[2]`或`/address[2]`。 表單的XML為：

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

您可以使用`bindRef`屬性來變更最適化表單/片段的預設子樹狀結構。 `bindRef`屬性可以指定指向XML架構樹結構中某個位置的路徑。

如果子表單未綁定，則其資料儲存在父表單XML架構的`afUnboundData`部分的`data`根下。

您可以將適用性表單新增為子表單多次。 請確定已正確修改`bindRef`，讓適用性表單的每個已使用例項指向資料根底下的不同子根。

>[!NOTE]
>
>如果不同的表單/片段對應至相同的子根，則資料會遭到覆寫。

## 使用資產瀏覽器{#adding-an-adaptive-form-as-a-child-form-using-asset-browser}將最適化表單新增為子表單

執行下列步驟，使用資產瀏覽器將最適化表單新增為子表單。

1. 在編輯模式中開啟父表單。
1. 在側邊欄中，按一下&#x200B;**Assets** ![assets-browser](assets/assets-browser.png)。 在「資產」下，從下拉式清單中選取&#x200B;**適用性表單**。
   [ ![在「資產」下選取最適化表單](assets/asset.png)](assets/asset-1.png)

1. 拖放您要新增為子表單的最適化表單。
   [ ![拖放網站中的最適化表](assets/drag-drop.png)](assets/drag-drop-1.png)單拖放的最適化表單會新增為子表單。
