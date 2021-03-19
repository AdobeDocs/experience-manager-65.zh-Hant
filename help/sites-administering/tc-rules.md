---
title: 識別要翻譯的內容
seo-title: 識別要翻譯的內容
description: 瞭解如何識別需要翻譯的內容。
seo-description: 瞭解如何識別需要翻譯的內容。
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: 語言副本
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# 識別要翻譯的內容{#identifying-content-to-translate}

翻譯規則可識別翻譯專案中包含或排除的頁面、元件和資產的翻譯內容。 當翻譯頁面或資產時，AEM請擷取此內容，以便將其傳送至翻譯服務。

頁面和資產在JCR儲存庫中以節點表示。 提取的內容是節點的一個或多個屬性值。 翻譯規則可識別包含要提取內容的屬性。

翻譯規則以XML格式表示，並儲存在以下可能的位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

該檔案適用於所有翻譯項目。

>[!NOTE]
>
>升級至6.4後，建議將檔案從/etc移動。 有關詳細資訊，請參見6.5&lt;a1/AEM>中的[通用儲存庫重組。](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)

規則包含下列資訊：

* 應用規則的節點的路徑。 該規則也適用於節點的後代。
* 包含要翻譯內容的節點屬性的名稱。 屬性可以特定於特定資源類型或所有資源類型。

例如，您可以建立規則，將作者新增的內容轉譯至頁面上AEM的所有基礎文字元件。 該規則可標識`/content`節點和`foundation/components/text`元件的`text`屬性。

已添加[控制台](#translation-rules-ui)用於配置轉換規則。 UI中的定義將為您填入檔案。

有關中的內容翻譯功能的概AEM述，請參閱[多語言站點的翻譯內容](/help/sites-administering/translation.md)。

>[!NOTE]
>
>支AEM持資源類型和引用屬性之間的一對一映射，以轉換頁面上的引用內容。

## 頁面、元件和資產的規則語法{#rule-syntax-for-pages-components-and-assets}

規則是`node`元素，包含一個或多個子`property`元素，以及零個或多個子`node`元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

這些`node`元素中的每個都具有以下特徵：

* `path`屬性包含規則所應用分支的根節點路徑。
* 子`property`元素標識要轉換所有資源類型的節點屬性：

   * `name`屬性包含屬性名稱。
   * 如果屬性未翻譯，則可選的`translate`屬性等於`false`。 預設值為`true`。 此屬性在覆寫先前的規則時很有用。

* 子`node`元素標識要針對特定資源類型轉換的節點屬性：

   * `resourceType`屬性包含解析到實現資源類型的元件的路徑。
   * 子`property`元素標識要轉換的節點屬性。 使用此節點的方式與節點規則的子`property`元素相同。

下列範例規則會針對`/content`節點下的所有頁面轉換所有`text`屬性的內容。 此規則對於將內容儲存在`text`屬性中的任何元件（例如基礎文字元件和基礎影像元件）都有效。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下示例將轉換所有`text`屬性的內容，還將轉換基礎Image元件的其他屬性。 如果其他元件具有相同名稱的屬性，則規則不適用於這些元件。

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

## 從頁面{#rule-syntax-for-extracting-assets-from-pages}擷取資產的規則語法

使用下列規則語法，以包含內嵌在元件中或從元件參考的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個`assetNode`元素具有以下特性：

* 一個`resourceType`屬性，等於解析至元件的路徑。
* 一個`assetReferenceAttribute`屬性，等於儲存資產二進位檔（針對內嵌資產）或參考資產路徑的屬性名稱。

下列範例從基礎影像元件擷取影像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆蓋規則{#overriding-rules}

translation_rules.xml檔案由`nodelist`元素組成，其中包含多個子`node`元素。 AEM從上到下讀取節點清單。 當多個規則指向相同節點時，會使用檔案中較低的規則。 例如，下列規則會導致翻譯`text`屬性中的所有內容，但頁面的`/content/mysite/en`分支除外：

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

例如，下列規則會導致翻譯`text`屬性中的所有內容，但屬性`draft`設為`true`的節點除外。

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

然後，您需要選取您的內容，然後按一下「編輯」**。**&#x200B;這將開啟翻譯規則編輯器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可透過UI變更4個屬性：`isDeep`、`inherit`、`translate`和`updateDestinationLanguage`。

**isDeep** 此屬性適用於節點篩選器，且預設為true。它會檢查節點（或其祖先）是否包含篩選器中具有指定屬性值的屬性。 如果為false，則只會檢查目前節點。

例如，即使父節點的屬性`draftOnly`設定為true以標籤草稿內容，子節點仍將被添加到轉譯作業中。 此處`isDeep`將開始運行，並檢查父節點是否具有`draftOnly`屬性，並排除這些子節點。

在編輯器中，可以在&#x200B;**過濾器**&#x200B;頁籤中選中／取消選中&#x200B;**Is Deep**。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是在UI中未勾選「**Is Deep**」時產生的xml範例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**繼** 承這適用於屬性。依預設，會繼承每個屬性，但是如果您希望某些屬性不會繼承到子項上，則可將該屬性標示為false，以便只套用到該特定節點。

在UI中，您可以在&#x200B;**屬性**&#x200B;標籤中選中／取消選中&#x200B;**繼承**。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**轉** 換屬性僅用於指定是否轉換屬性。

在UI中，您可以在&#x200B;**屬性**&#x200B;標籤中選中／取消選中&#x200B;**翻譯**。

**updateDestinationLanguage** 此屬性用於沒有文本但沒有語言代碼的屬性，例如jcr:language。用戶不是在翻譯文本，而是在從源到目標的語言區域設定。 這些屬性不會發送用於翻譯。

在UI中，您可以在&#x200B;**屬性**&#x200B;標籤中勾選／取消勾選&#x200B;**翻譯**，但是對於具有語言代碼作為值的特定屬性。

為協助釐清`updateDestinationLanguage`和`translate`之間的差異，以下是僅包含兩個規則之上下文的簡單範例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml的結果如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案{#editing-the-rules-file-manually}

隨安裝的translation_rules.xml檔案包AEM含一組預設的翻譯規則。 您可以編輯檔案以支援翻譯項目的要求。 例如，您可以新增規則，以便翻譯自訂元件的內容。

如果編輯translation_rules.xml檔案，請將備份副本保存在內容包中。 安裝AEMService Pack或重新安AEM裝某些軟體包可以用原始檔案替換當前的translation_rules.xml檔案。 要在這種情況下恢復規則，可以安裝包含備份副本的軟體包。

>[!NOTE]
>
>建立內容套件後，請在每次編輯檔案時重建該套件。

## 翻譯規則檔案{#example-translation-rules-file}示例

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

