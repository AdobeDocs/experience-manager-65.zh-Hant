---
title: 識別要翻譯的內容
description: 瞭解如何識別需要在Adobe Experience Manager中翻譯的內容。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 2%

---

# 識別要翻譯的內容{#identifying-content-to-translate}

翻譯規則會針對翻譯專案中包含或排除的頁面、元件和資產，識別要翻譯的內容。 在翻譯頁面或資產時，AEM會擷取此內容，以便將其傳送至翻譯服務。

頁面和資產在JCR存放庫中會顯示為節點。 擷取的內容是節點的一或多個屬性值。 翻譯規則會識別包含要擷取之內容的屬性。

翻譯規則會以XML格式表示，並儲存在下列可能位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

檔案適用於所有翻譯專案。

>[!NOTE]
>
>升級到6.4後，建議從/etc移動檔案。 另請參閱 [AEM 6.5中的通用存放庫重新架構](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) 以取得更多詳細資料。

規則包含下列資訊：

* 規則套用的節點路徑。 此規則也會套用至節點的子代。
* 包含要翻譯之內容的節點屬性名稱。 該屬性可專屬於特定資源類型或所有資源類型.

例如，您可以建立規則來轉譯作者新增至您頁面上所有AEM Foundation文字元件的內容。 此規則可識別 `/content` 節點和 `text` 的屬性 `foundation/components/text` 元件。

有一個 [主控台](#translation-rules-ui) 已新增用於設定翻譯規則。 UI中的定義將為您填入檔案。

如需AEM內容翻譯功能的總覽，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md).

>[!NOTE]
>
>AEM支援資源型別和參考屬性之間的一對一對應，以便翻譯頁面上的參考內容。

## 頁面、元件和資產的規則語法 {#rule-syntax-for-pages-components-and-assets}

規則是 `node` 具有一或多個子項的元素 `property` 元素和零個或多個子項 `node` 元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

每一個 `node` 元素具有下列特性：

* 此 `path` attribute包含套用規則之分支的根節點的路徑。
* 子項 `property` 元素會為所有資源型別識別要翻譯的節點屬性：

   * 此 `name` 屬性包含屬性名稱。
   * 選填 `translate` 屬性等於 `false` 如果屬性未翻譯。 預設值為 `true`. 覆寫先前的規則時，此屬性相當實用。

* 子項 `node` 元素會針對特定資源型別識別要翻譯的節點屬性：

   * 此 `resourceType` attribute包含解析為實作資源型別的元件的路徑。
   * 子項 `property` 元素會識別要翻譯的節點屬性。 以與子節點相同的方式使用此節點 `property` 節點規則的元素。

以下範例規則會導致 `text` 要為以下的所有頁面翻譯的屬性 `/content` 節點。 此規則適用於任何將內容儲存在 `text` 屬性，例如foundation文字元件和foundation影像元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下範例轉譯所有 `text` 屬性，也會轉譯foundation影像元件的其他屬性。 如果其他元件具有同名屬性，則規則不適用於它們。

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

## 從頁面擷取資產的規則語法  {#rule-syntax-for-extracting-assets-from-pages}

使用下列規則語法來包含內嵌在元件中或從元件參照的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個 `assetNode` 元素具有下列特性：

* 一 `resourceType` 屬性，代表解析為元件的路徑。
* 一 `assetReferenceAttribute` 屬性，代表儲存資產二進位檔（用於內嵌資產）之屬性的名稱或參考資產的路徑。

下列範例會從foundation影像元件中擷取影像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆寫規則 {#overriding-rules}

translation_rules.xml檔案包含 `nodelist` 具有多個子項的元素 `node` 元素。 AEM會從上到下讀取節點清單。 如果有多個規則鎖定同一個節點，系統會使用檔案中較低位置的規則。 例如，下列規則會導致所有內容在 `text` 要翻譯的屬性，但 `/content/mysite/en` 頁面分支：

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

您可以使用來篩選具有特定屬性的節點 `filter` 元素。

例如，下列規則會導致所有內容在 `text` 要翻譯的屬性，但具有屬性的節點除外 `draft` 設為 `true`.

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

控制檯也可用於設定翻譯規則。

若要存取它：

1. 瀏覽至 **工具** 然後 **一般**.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 選取 **翻譯設定**.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

從這裡，您可以 **新增內容**. 這可讓您新增路徑。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

之後，您需要選取內容，然後按一下 **編輯**. 如此將可開啟翻譯規則編輯器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可以透過UI變更四個屬性： `isDeep`， `inherit`， `translate` 和 `updateDestinationLanguage`.

**isDeep** 此屬性適用於節點篩選器，預設為true。 它會檢查節點（或其上階）是否在篩選器中包含具有指定屬性值的屬性。 若為false，則僅檢查目前節點。

例如，即使父節點具有屬性，子節點也會新增到翻譯作業中 `draftOnly` 設為true可標幟草稿內容。 此處 `isDeep` 就會開始使用，並檢查父節點是否具備屬性 `draftOnly` 為true並排除這些子節點。

在編輯器中，您可以核取/取消核取 **深入** 在 **篩選器** 標籤。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是產生之xml的範例，當 **深入** 未在UI中勾選：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**繼承** 這適用於屬性。 依預設，每個屬性都會被繼承，但如果您不想讓某個屬性在子項上被繼承，則可將屬性標示為false，使其僅套用至該特定節點。

在UI中，您可以勾選/取消勾選 **繼承** 在 **屬性** 標籤。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** translate屬性僅用於指定是否翻譯屬性。

在UI中，您可以勾選/取消勾選 **Translate** 在 **屬性** 標籤。

**updatedestinationlanguage** 此屬性用於沒有文字但有語言代碼的屬性，例如jcr：language。 使用者不會翻譯文字，而是從來源到目的地的語言地區設定。 不會傳送此類屬性以供翻譯。

在UI中，您可以勾選/取消勾選 **Translate** 在 **屬性** 標籤，但用於語言程式碼為值的特定屬性。

協助釐清兩者之間的差異 `updateDestinationLanguage` 和 `translate`，以下是僅有兩個規則之內容的簡單範例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml中的結果將如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案 {#editing-the-rules-file-manually}

與AEM一起安裝的translation_rules.xml檔案包含一組預設的翻譯規則。 您可以編輯檔案以支援翻譯專案的需求。 例如，您可以新增規則，以便翻譯自訂元件的內容。

如果您編輯translation_rules.xml檔案，請在內容封裝中保留備份復本。 安裝AEM Service Pack或重新安裝某些AEM套件可將目前的translation_rules.xml檔案取代為原始檔案。 若要在此情況下還原您的規則，您可以安裝包含備份復本的套件。

>[!NOTE]
>
>建立內容封裝後，每次編輯檔案時都會重新建置封裝。

## 範例翻譯規則檔案 {#example-translation-rules-file}

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
