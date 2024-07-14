---
title: 範本
description: 建立作為新頁面基礎的頁面時，會使用範本。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# 範本{#templates}

範本在AEM中的不同時間點使用：

* [當您建立頁面時，請選取範本](#templates-pages)。 此範本用作新頁面的基礎。 範本定義了頁面的結構、任何初始內容，以及可用的[元件](/help/sites-authoring/default-components.md) （設計屬性）。

* [當您建立內容片段時，您也可以選取範本](#templates-content-fragments)。 此範本定義結構、初始元素和變數。

以下範本將詳細說明：

* [頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md)
* [頁面範本 — 靜態](/help/sites-developing/page-templates-static.md)
* [內容片段範本](/help/sites-developing/content-fragment-templates.md)
* [最適化範本演算](/help/sites-developing/templates-adaptive-rendering.md)

## 範本 — 頁面 {#templates-pages}

AEM現在提供兩種基本型別的範本以用於建立頁面：

>[!NOTE]
>
>使用範本來[建立頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)時，沒有可見的差異（對頁面作者而言），也沒有指示使用的範本型別。

### 可編輯的範本 {#editable-templates}

可編輯的範本現在被認為是使用AEM進行開發的最佳實務。

可編輯範本的優點：

* 可以由您的作者[建立](/help/sites-authoring/templates.md#creating-a-new-template-template-author)和[編輯](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

* 此更新已引入，可讓您為使用範本建立的任何頁面定義下列內容：

   * 結構
   * 初始內容
   * 內容原則

* 建立新頁面後，頁面與範本之間會維持動態連線。 此連線表示對範本結構的變更會反映在使用該範本建立的任何頁面上；初始內容的變更不會反映出來。
* 使用內容原則（從範本編輯器編輯）來儲存設計屬性（不使用頁面編輯器中的設計模式）。
* 儲存在`/conf`下
* 如需進一步資訊，請參閱[可編輯的範本](/help/sites-developing/page-templates-editable.md)。

>[!NOTE]
>
>請參閱[使用可編輯的頁面範本來開發Experience Manager網站](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html)。

### 靜態範本 {#static-templates}

靜態範本：

* 必須由您的開發人員定義和設定。
* 已推出許多版本的AEM原始範本系統。
* 靜態範本是指與要建立之頁面結構相同，但沒有任何實際內容的節點階層。
* 建立頁面時會複製，之後不會有任何動態連線。
* 使用[設計模式](/help/sites-authoring/default-components-designmode.md)來儲存設計屬性。
* 儲存在`/apps`下
* 如需進一步資訊，請參閱[靜態範本](/help/sites-developing/page-templates-static.md)。

>[!NOTE]
>
>自AEM 6.5起，使用靜態範本已不再是最佳做法。 請改用可編輯的範本。
>
>[AEM現代化](modernization-tools.md)工具可協助您從靜態範本移轉至可編輯的範本。

### 範本可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供多個屬性，可控制&#x200B;**網站**&#x200B;下允許的範本。 不過，將其合併可能會導致複雜規則，難以追蹤和管理。
>
>因此，Adobe建議您透過定義以下內容來開始簡化：
>
>* 僅`cq:allowedTemplates`屬性
>
>* 僅於網站根目錄上
>
>如需範例，請參閱We.Retail： `/content/we-retail/jcr:content`
>
>屬性`allowedPaths`、`allowedParents`和`allowedChildren`也可以放在範本上，以定義更複雜的規則。 不過，如果可能的話，如果需要進一步限制允許的範本，在網站的子區段上定義其他`cq:allowedTemplates`屬性會更簡單&#x200B;*許多*。
>
>另一個優點是`cq:allowedTemplates`屬性可由作者在&#x200B;**頁面屬性**&#x200B;的&#x200B;**進階**&#x200B;索引標籤中更新。 無法使用（標準） UI更新其他範本屬性，因此需要開發人員維護規則和每次變更的程式碼部署。

在網站管理員介面中建立頁面時，可用範本清單會根據新頁面的位置及每個範本中指定的版位限制而定。

下列屬性決定範本`T`是否用於要放置為頁面`P`子項的新頁面。 這些屬性都是多值字串，其中包含零個或多個用於和路徑比對的規則運算式：

* `P`的`jcr:content`子節點或`P`的上階的`cq:allowedTemplates`屬性。

* `T`的`allowedPaths`屬性。

* `T`的`allowedParents`屬性。

* `P`之範本的`allowedChildren`屬性。

評估的運作方式如下：

* 以`P`開頭的頁面階層遞增時，找到的第一個非空白`cq:allowedTemplates`屬性與`T`的路徑相符。 如果沒有任何相符的值，則會拒絕`T`。

* 如果`T`具有非空白的`allowedPaths`屬性，但沒有符合`P`路徑的值，則會拒絕`T`。

* 如果上述兩個屬性都是空白或不存在，則會拒絕`T`，除非它與`P`屬於相同的應用程式。 當`T`路徑的第二層級名稱與`P`路徑的第二層級名稱相同時，`T`才屬於與`P`相同的應用程式。 例如，範本`/apps/geometrixx/templates/foo`與頁面`/content/geometrixx`屬於相同的應用程式。

* 如果`T`具有非空白的`allowedParents`屬性，但沒有符合`P`路徑的值，則會拒絕`T`。

* 如果`P`的範本有非空白的`allowedChildren`屬性，但沒有符合`T`路徑的值，則會拒絕`T`。

* 在所有其他情況下，都允許`T`。

下圖說明範本評估程式：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子頁面中使用的範本 {#limiting-templates-used-in-child-pages}

若要限制哪些範本可用於在指定頁面下建立子頁面，請使用頁面`jcr:content`節點的`cq:allowedTemplates`屬性，指定允許做為子頁面的範本清單。 清單中的每個值都必須是允許之子頁面的範本的絕對路徑，例如`/apps/geometrixx/templates/contentpage`。

您可以在範本的`jcr:content`節點上使用`cq:allowedTemplates`屬性，將此設定套用至使用此範本的所有新建立頁面。

如果您想要新增更多限制，例如關於範本階層，您可以在範本上使用`allowedParents/allowedChildren`屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父項/子項。

## 範本 — 內容片段 {#templates-content-fragments}

請參閱[內容片段範本](/help/sites-developing/content-fragment-templates.md)。
