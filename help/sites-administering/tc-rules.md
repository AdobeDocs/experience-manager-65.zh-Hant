---
title: 識別要翻譯的內容
seo-title: Identifying Content to Translate
description: 瞭解如何識別需要翻譯的內容。
seo-description: Learn how to identify content that needs translating.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# 識別要翻譯的內容{#identifying-content-to-translate}

翻譯規則標識要翻譯的內容，這些內容包括在翻譯項目中或從翻譯項目中排除。 當正在翻譯頁面或資產時，AEM請提取此內容，以便將其發送到翻譯服務。

頁面和資產在JCR儲存庫中以節點表示。 提取的內容是節點的一個或多個屬性值。 翻譯規則標識包含要提取的內容的屬性。

翻譯規則以XML格式表示並儲存在以下可能的位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

該檔案適用於所有翻譯項目。

>[!NOTE]
>
>升級到6.4後，建議將檔案從/etc中移動。 請參閱 [6.5版中的通AEM用儲存庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) 的子菜單。

規則包括以下資訊：

* 應用規則的節點的路徑。 該規則也適用於節點的後代。
* 包含要翻譯的內容的節點屬性的名稱。 該屬性可專屬於特定資源類型或所有資源類型.

例如，您可以建立一個規則來翻譯作者添加到頁面上AEM所有基礎文本元件中的內容。 該規則可識別 `/content` 和 `text` 屬性 `foundation/components/text` 元件。

有 [控制台](#translation-rules-ui) 已添加的用於配置轉換規則的轉換。 UI中的定義將為您填充檔案。

有關中的內容翻譯功能的概AEM述，請參見 [翻譯多語言站點的內容](/help/sites-administering/translation.md)。

>[!NOTE]
>
>支AEM持資源類型和引用屬性之間的一對一映射，以翻譯頁面上引用的內容。

## 頁面、元件和資產的規則語法 {#rule-syntax-for-pages-components-and-assets}

規則是 `node` 一個或多個子元素 `property` 元素和零個或多個子項 `node` 元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

每個 `node` 元素具有以下特徵：

* 的 `path` 屬性包含規則所應用的分支的根節點的路徑。
* 子 `property` 元素標識要轉換的所有資源類型的節點屬性：

   * 的 `name` 屬性包含屬性名稱。
   * 可選 `translate` 屬性等於 `false` 的子菜單。 預設情況下，值為 `true`。 此屬性在覆蓋以前的規則時非常有用。

* 子 `node` 元素標識要轉換特定資源類型的節點屬性：

   * 的 `resourceType` 屬性包含解析為實現資源類型的元件的路徑。
   * 子 `property` 元素標識要轉換的節點屬性。 以與子節點相同的方式使用此節點 `property` 節點規則的元素。

以下示例規則將導致所有 `text` 要翻譯的屬性 `/content` 的下界。 該規則對於儲存內容的任何元件都有效 `text` 屬性，如foundation Text元件和foundation Image元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

下面的示例翻譯所有內容 `text` 屬性，還可以轉換基礎Image元件的其他屬性。 如果其他元件具有同名屬性，則規則不適用於這些屬性。

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

## 用於從頁面中提取資產的規則語法  {#rule-syntax-for-extracting-assets-from-pages}

使用以下規則語法包括嵌入元件或從元件引用的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個 `assetNode` 元素具有以下特徵：

* 一 `resourceType` 與解析到元件的路徑相等的屬性。
* 一 `assetReferenceAttribute` 屬性，該屬性等於儲存資產二進位檔案（對於嵌入資產）或引用資產路徑的屬性的名稱。

下面的示例從基礎影像元件中提取影像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆蓋規則 {#overriding-rules}

translation_rules.xml檔案由 `nodelist` 元素具有多個子項 `node` 元素。 從AEM上到下讀取節點清單。 當多個規則針對同一節點時，將使用檔案中較低的規則。 例如，以下規則導致 `text` 要轉換的屬性， `/content/mysite/en` 頁的分支：

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## 篩選屬性 {#filtering-properties}

可以使用 `filter` 的子菜單。

例如，以下規則導致 `text` 要轉換的屬性，但具有該屬性的節點除外 `draft` 設定為 `true`。

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻譯規則UI {#translation-rules-ui}

還有一個控制台可用於配置轉換規則。

若要存取它：

1. 導航到 **工具** 然後 **常規**。

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 選擇 **翻譯配置**。

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

從這裡，你可以 **添加上下文**。 這允許您添加路徑。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

然後，您需要選擇上下文，然後按一下 **編輯**。 這將開啟翻譯規則編輯器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

可通過UI更改4個屬性： `isDeep`。 `inherit`。 `translate` 和 `updateDestinationLanguage`。

**深** 此屬性適用於節點篩選器，預設為true。 它將檢查節點（或其祖先）是否包含篩選器中具有指定屬性值的屬性。 如果為false，則只檢查當前節點。

例如，子節點即使在父節點具有屬性時，也會被添加到轉換作業中 `draftOnly` 設定為true可標籤草稿內容。 這裡 `isDeep` 開始播放並檢查父節點是否具有屬性 `draftOnly` 並排除這些子節點。

在編輯器中，可以選中/取消選中 **深** 的 **篩選器** 頁籤。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是生成的xml的示例 **深** 在UI中未選中：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**繼承** 這適用於屬性。 預設情況下，每個屬性都是繼承的，但如果希望某些屬性不能繼承到子代上，則可以將該屬性標籤為false，以便它僅應用於該特定節點。

在UI中，您可以選中/取消選中 **繼承** 的 **屬性** 頁籤。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**翻譯** 轉換屬性僅用於指定是否轉換屬性。

在UI中，您可以選中/取消選中 **翻譯** 的 **屬性** 頁籤。

**updateDestinationLanguage** 此屬性用於沒有文本但沒有語言代碼的屬性，例如jcr:language。 用戶不是在翻譯文本，而是在從源到目標的語言區域設定。 這些屬性不會發送到翻譯。

在UI中，您可以選中/取消選中 **翻譯** 的 **屬性** 頁籤，但是對於將語言代碼作為值的特定屬性。

幫助澄清 `updateDestinationLanguage` 和 `translate`，下面是只有兩個規則的上下文的簡單示例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml的結果將如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案 {#editing-the-rules-file-manually}

隨一起安裝的translation_rules.xml檔案AEM包含一組預設的轉換規則。 您可以編輯檔案以支援翻譯項目的要求。 例如，您可以添加規則，以便翻譯自定義元件的內容。

如果編輯translation_rules.xml檔案，請在內容包中保留備份副本。 安AEM裝Service Pack或重新安AEM裝某些軟體包可以用原始檔案替換當前的translation_rules.xml檔案。 要在這種情況下恢復規則，可以安裝包含備份副本的包。

>[!NOTE]
>
>建立內容包後，每次編輯檔案時都重新生成包。

## 翻譯規則檔案示例 {#example-translation-rules-file}

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
