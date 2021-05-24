---
title: 識別要翻譯的內容
seo-title: 識別要翻譯的內容
description: 了解如何識別需要翻譯的內容。
seo-description: 了解如何識別需要翻譯的內容。
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: 語言副本
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# 識別要翻譯的內容{#identifying-content-to-translate}

翻譯規則可識別要翻譯的頁面、元件及翻譯專案中包含或排除的資產內容。 翻譯頁面或資產時，AEM會擷取此內容，以便傳送至翻譯服務。

頁面和資產在JCR存放庫中會以節點呈現。 提取的內容是節點的一個或多個屬性值。 翻譯規則可識別包含要擷取內容的屬性。

翻譯規則以XML格式表示，並儲存在以下可能的位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

該檔案適用於所有翻譯項目。

>[!NOTE]
>
>升級至6.4後，建議從/etc移動檔案。 如需詳細資訊，請參閱AEM 6.5中的[常見存放庫重新調整架構。](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)

規則包含下列資訊：

* 規則套用的節點路徑。 此規則也適用於節點的子系。
* 包含要翻譯內容的節點屬性的名稱。 該屬性可以特定於特定資源類型或所有資源類型。

例如，您可以建立規則，將作者新增的內容轉譯至您頁面上的所有AEM foundation Text元件。 該規則可標識`/content`節點和`foundation/components/text`元件的`text`屬性。

已新增[控制台](#translation-rules-ui)以用於設定轉換規則。 UI中的定義會填入您的檔案。

如需AEM中內容翻譯功能的概觀，請參閱[多語言網站的翻譯內容](/help/sites-administering/translation.md)。

>[!NOTE]
>
>AEM支援資源類型和參考屬性之間的一對一對應，以轉譯頁面上的參考內容。

## 頁面、元件和資產的規則語法{#rule-syntax-for-pages-components-and-assets}

規則是`node`元素，其中包含一個或多個子`property`元素以及零個或多個子`node`元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

這些`node`元素的每個都具有以下特性：

* `path`屬性包含規則所應用分支的根節點的路徑。
* 子`property`元素標識要針對所有資源類型轉換的節點屬性：

   * `name`屬性包含屬性名稱。
   * 如果屬性未翻譯，則選用的`translate`屬性等於`false`。 預設值為`true`。 此屬性在覆寫先前的規則時很實用。

* 子`node`元素標識要針對特定資源類型轉換的節點屬性：

   * `resourceType`屬性包含解析到實現資源類型的元件的路徑。
   * 子`property`元素標識要轉換的節點屬性。 使用此節點的方式與節點規則的子`property`元素相同。

下列範例規則會針對`/content`節點下方的所有頁面，翻譯所有`text`屬性的內容。 此規則對於任何儲存`text`屬性中內容的元件都有效，如基礎文本元件和基礎影像元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下示例轉換所有`text`屬性的內容，也轉換基礎影像元件的其他屬性。 如果其他元件具有相同名稱的屬性，則不會套用規則。

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="foundation/components/textimage">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## 從頁面擷取資產的規則語法{#rule-syntax-for-extracting-assets-from-pages}

使用下列規則語法來包含內嵌在元件中或從元件參照的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個`assetNode`元素具有以下特性：

* 一個`resourceType`屬性，等於解析到元件的路徑。
* 一個`assetReferenceAttribute`屬性等於儲存資產二進位檔（針對內嵌資產）或參考資產路徑之屬性的名稱。

下列範例會從基礎影像元件中擷取影像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆蓋規則{#overriding-rules}

translation_rules.xml檔案由`nodelist`元素組成，其中包含多個子`node`元素。 AEM會從上到下讀取節點清單。 當多個規則以相同節點為目標時，會使用檔案中較低的規則。 例如，下列規則會導致除頁面的`/content/mysite/en`分支外，`text`屬性中的所有內容都翻譯：

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## 篩選屬性{#filtering-properties}

您可以使用`filter`元素來篩選具有特定屬性的節點。

例如，下列規則會導致除了將屬性`draft`設為`true`的節點之外，轉換`text`屬性中的所有內容。

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻譯規則UI {#translation-rules-ui}

控制台也可用於配置翻譯規則。

若要存取：

1. 導覽至&#x200B;**工具**，然後導覽至&#x200B;**一般**。

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 選擇&#x200B;**翻譯配置**。

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

從這裡，您可以&#x200B;**新增內容**。 這可讓您新增路徑。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

然後，您需要選擇上下文，然後按一下「**編輯**」。 這會開啟翻譯規則編輯器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可以透過UI變更4個屬性：`isDeep`、`inherit`、`translate`和`updateDestinationLanguage`。

**** isDeep此屬性適用於節點篩選器，預設為true。它會檢查節點（或其祖先）是否包含篩選器中具有指定屬性值的屬性。 若為false，則只會檢查目前節點。

例如，即使父節點的屬性`draftOnly`設定為true來標幟草稿內容，子節點仍會新增至翻譯工作。 在此`isDeep`中，會開始運作並檢查父節點是否將屬性`draftOnly`設為true，並排除這些子節點。

在編輯器中，您可以在&#x200B;**篩選器**&#x200B;標籤中勾選/取消勾選&#x200B;**深度**。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是UI中取消勾選&#x200B;**深度**&#x200B;時產生的xml範例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**** inherit（繼承）這適用於屬性。依預設，會繼承每個屬性，但如果您不希望某些屬性在子項上繼承，則可以將該屬性標示為false，以便僅在該特定節點上套用該屬性。

在UI中，您可以在&#x200B;**Properties**&#x200B;標籤中勾選/取消勾選&#x200B;**Inherit**。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**** translate（翻譯）轉換屬性只用於指定是否翻譯屬性。

在UI中，您可以在&#x200B;**Properties**&#x200B;標籤中勾選/取消勾選&#x200B;**Translate**。

**** updateDestinationLanguage此屬性用於沒有文本但語言代碼的屬性，例如jcr:language。用戶未翻譯文本，而是語言區域設定從源到目標。 這些屬性不會傳送以供翻譯。

在UI中，您可以在&#x200B;**Properties**&#x200B;標籤中勾選/取消勾選&#x200B;**Translate**，但針對語言代碼為值的特定屬性。

為協助釐清`updateDestinationLanguage`與`translate`之間的差異，以下是只有兩個規則的上下文的簡單範例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml中的結果如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案{#editing-the-rules-file-manually}

隨AEM安裝的translation_rules.xml檔案包含一組預設的翻譯規則。 您可以編輯檔案以支援翻譯專案的需求。 例如，您可以新增規則，以便翻譯自訂元件的內容。

如果編輯translation_rules.xml檔案，請將備份副本保留在內容包中。 安裝AEM Service Pack或重新安裝某些AEM軟體包可以將當前的translation_rules.xml檔案替換為原始檔案。 若要在此情況下還原規則，您可以安裝包含備份副本的套件。

>[!NOTE]
>
>建立內容套件後，請在每次編輯檔案時重建套件。

## 翻譯規則檔案範例{#example-translation-rules-file}

```xml
<nodelist>
    <!-- translation rules for Geometrixx Demo site (example) -->
    <node path="/content/geometrixx">
        <!-- list all node properties that should be translated -->
        <property name="jcr:title" /> <!-- translation workflows running on content saved in /content/geometrixx, will extract jcr:title values independent of the component. -->
        <property name="jcr:description" />
        <node resourceType ="foundation/components/image"> <!-- translation workflows running on content saved in /content/geometrixx, will extract alternateText values only for Image component. -->
            <property name="alternateText"/>
        </node>
        <node resourceType ="geometrixx/components/title">
            <property name="richText"/>
            <property name="jcr:title" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract jcr:title for Title component, but instead use richText. -->
        </node>
        <node pathContains="/cq:annotations">
            <property name="text" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract text if part of cq:annotations node. -->
        </node>
    </node>
    <!-- translation rules for Geometrixx Outdoors site (example) -->
    <node path="/content/geometrixx-outdoors">
        <node resourceType ="foundation/components/image">
            <property name="alternateText"/>
            <property name="jcr:title" />
        </node>
        <node resourceType ="geometrixx-outdoors/components/title">
            <property name="richText"/>
        </node>
    </node>
    <!-- translation rules for ASSETS (example) -->
    <node path="/content/dam">
        <!-- configure list of metadata properties here -->
        <property name="dc:title" />
        <property name="dc:description" />
    </node>
    <!-- translation rules for extracting ASSETS from SITES content, configure all components that embed or reference assets -->
    <assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/video" assetReferenceAttribute="asset"/>
    <assetNode resourceType="foundation/components/download" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/mobileimage" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="wcm/foundation/components/image" assetReferenceAttribute="fileReference"/>
</nodelist>
```
