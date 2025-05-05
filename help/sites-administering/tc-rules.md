---
title: 識別要翻譯的內容
description: 瞭解如何識別需要在Adobe Experience Manager中翻譯的內容。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1158'
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
>升級到6.4後，建議從/etc移動檔案。 如需詳細資訊，請參閱[AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)中的一般存放庫重組。

規則包含下列資訊：

* 規則套用的節點路徑。 此規則也會套用至節點的子代。
* 包含要翻譯之內容的節點屬性名稱。 屬性可特定於特定資源型別或所有資源型別。

例如，您可以建立規則來轉譯作者新增至您頁面上所有AEM Foundation文字元件的內容。 此規則可以識別`foundation/components/text`元件的`/content`節點和`text`屬性。

已新增一個[主控台](#translation-rules-ui)來設定翻譯規則。 UI中的定義將為您填入檔案。

如需AEM內容翻譯功能的概述，請參閱[翻譯多語言網站的內容](/help/sites-administering/translation.md)。

>[!NOTE]
>
>AEM支援資源型別和參考屬性之間的一對一對應，以便翻譯頁面上的參考內容。

## 頁面、元件和Assets的規則語法 {#rule-syntax-for-pages-components-and-assets}

規則是`node`元素，包含一或多個子`property`元素以及零個或多個子`node`元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

這些`node`元素中的每一個都具有下列特性：

* `path`屬性包含套用規則之分支的根節點的路徑。
* 子項`property`元素為所有資源型別識別要翻譯的節點屬性：

   * `name`屬性包含屬性名稱。
   * 如果屬性未轉譯，則選用的`translate`屬性等於`false`。 預設值為`true`。 覆寫先前的規則時，此屬性相當實用。

* 子項`node`元素會識別特定資源型別要翻譯的節點屬性：

   * `resourceType`屬性包含解析為實作資源型別的元件的路徑。
   * 子項`property`元素識別要翻譯的節點屬性。 以與節點規則的子`property`元素相同的方式使用此節點。

下列範例規則會為`/content`節點下的所有頁面轉譯所有`text`屬性的內容。 此規則適用於任何將內容儲存在`text`屬性中的元件，例如foundation Text元件和foundation Image元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

下列範例會轉譯所有`text`屬性的內容，也會轉譯foundation Image元件的其他屬性。 如果其他元件具有同名屬性，則規則不適用於它們。

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

## 從頁面擷取Assets的規則語法  {#rule-syntax-for-extracting-assets-from-pages}

使用下列規則語法來包含內嵌在元件中或從元件參照的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個`assetNode`元素都有下列特性：

* 一個`resourceType`屬性，代表解析為元件的路徑。
* 一個`assetReferenceAttribute`屬性，代表儲存資產二進位檔（用於內嵌資產）的屬性名稱或參考資產的路徑。

下列範例會從foundation影像元件中擷取影像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆寫規則 {#overriding-rules}

translation_rules.xml檔案包含具有數個子項`node`專案的`nodelist`專案。 AEM會從上到下讀取節點清單。 如果有多個規則鎖定同一個節點，系統會使用檔案中較低位置的規則。 例如，下列規則會翻譯`text`屬性中的所有內容，但頁面的`/content/mysite/en`分支除外：

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

您可以使用`filter`元素來篩選具有特定屬性的節點。

例如，下列規則會翻譯`text`屬性中的所有內容，但屬性`draft`設定為`true`的節點除外。

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

1. 導覽至&#x200B;**工具**，然後導覽至&#x200B;**一般**。

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 選取「**翻譯設定**」。

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

您可從這裡&#x200B;**新增內容**。 這可讓您新增路徑。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

接著您必須選取內容，然後按一下[編輯]。**&#x200B;** 如此將可開啟翻譯規則編輯器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可以透過UI變更4個屬性： `isDeep`、`inherit`、`translate`和`updateDestinationLanguage`。

**isDeep**&#x200B;此屬性適用於節點篩選器，預設為true。 它會檢查節點（或其上階）是否在篩選器中包含具有指定屬性值的屬性。 若為false，則僅檢查目前節點。

例如，即使父節點將屬性`draftOnly`設定為true以標幟草稿內容，子節點也會加入翻譯工作。 此時`isDeep`就會發揮作用，並檢查父節點是否已將屬性`draftOnly`設為true並排除這些子節點。

在編輯器中，您可以在&#x200B;**篩選器**&#x200B;索引標籤中核取/取消核取&#x200B;**Is Deep**。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是在UI中取消勾選&#x200B;**Is Deep**&#x200B;時產生的xml範例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**inherit**&#x200B;這適用於屬性。 依預設，每個屬性都會被繼承，但如果您不想讓某個屬性在子項上被繼承，則可將屬性標示為false，使其僅套用至該特定節點。

在UI中，您可以在&#x200B;**屬性**&#x200B;索引標籤中核取/取消核取&#x200B;**繼承**。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** translate屬性僅用於指定是否翻譯屬性。

在UI中，您可以在&#x200B;**屬性**&#x200B;索引標籤中勾選/取消勾選&#x200B;**Translate**。

**updateDestinationLanguage**&#x200B;此屬性用於沒有文字但有語言代碼的屬性，例如jcr：language。 使用者不會翻譯文字，而是從來源到目的地的語言地區設定。 不會傳送此類屬性以供翻譯。

在UI中，您可以在&#x200B;**Properties**&#x200B;索引標籤中勾選/取消勾選&#x200B;**Translate**，但針對語言代碼為值的特定屬性。

為協助釐清`updateDestinationLanguage`與`translate`之間的差異，以下提供僅有兩個規則之內容的簡單範例：

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
