---
title: 範本
seo-title: 範本
description: 建立將用作新頁面基礎的頁面時，會使用範本
seo-description: 建立將用作新頁面基礎的頁面時，會使用範本
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 1%

---

# 範本{#templates}

範本會用於AEM中的各個時間點：

* 當[建立頁面時，需要選擇模板](#templates-pages);這將用作新頁面的基礎。 該模板定義了生成的頁的結構、任何初始內容以及可使用的[元件](/help/sites-authoring/default-components.md)（設計屬性）。

* 當[建立內容片段時，您還需要選取範本](#templates-content-fragments)。 此範本會定義結構、初始元素和變異。

以下範本將詳細說明：

* [頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md)
* [頁面範本 — 靜態](/help/sites-developing/page-templates-static.md)
* [內容片段範本](/help/sites-developing/content-fragment-templates.md)
* [最適化範本轉譯](/help/sites-developing/templates-adaptive-rendering.md)

## 範本 — 頁面{#templates-pages}

AEM現在提供兩種建立頁面的基本範本類型：

>[!NOTE]
>
>使用範本建立新頁面[時，沒有顯示差異（對頁面作者而言），也沒有顯示使用的範本類型。](/help/sites-authoring/managing-pages.md#creating-a-new-page)

### 可編輯的範本 {#editable-templates}

使用AEM開發時，可編輯的範本現在被視為最佳作法。

可編輯範本的優點：

* 可由作者建立[](/help/sites-authoring/templates.md#creating-a-new-template-template-author)和[edited](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

* 已導入，可讓您為使用範本建立的任何頁面定義下列項目：

   * 結構
   * 初始內容
   * 內容原則

* 建立新頁面後，頁面與範本之間會維持動態連線；這表示使用該範本建立的任何頁面上都會反映對範本結構的變更（不會反映初始內容的變更）。
* 使用內容原則（從範本編輯器編輯）來保留設計屬性（不在頁面編輯器內使用設計模式）。
* 儲存在`/conf`下
* 如需詳細資訊，請參閱[可編輯的範本](/help/sites-developing/page-templates-editable.md) 。

>[!NOTE]
>
>AEM社群文章可供說明如何使用可編輯的範本開發Experience Manager網站，請參閱[使用可編輯的範本建立Adobe Experience Manager 6.5網站](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)。

### 靜態範本 {#static-templates}

靜態範本:

* 必須由開發人員定義和設定。
* 這是AEM的原始範本系統，可用於許多版本。
* 靜態範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。
* 系統會複製以建立新頁面，之後不會有動態連線。
* 使用[設計模式](/help/sites-authoring/default-components-designmode.md)來保存設計屬性。
* 儲存在`/apps`下
* 如需詳細資訊，請參閱[靜態範本](/help/sites-developing/page-templates-static.md)。

>[!NOTE]
>
>自AEM 6.5起，使用靜態範本不被視為最佳作法。 請改用可編輯的範本。
>
>[AEM ](modernization-tools.md) Modernizationtools可協助您從靜態範本移轉至可編輯的範本。

### 範本可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供多個屬性，以控制&#x200B;**Sites**&#x200B;下允許的範本。 但是，結合這些規則可能會產生非常複雜的規則，且難以追蹤和管理。
>
>因此，Adobe建議您透過定義：
>
>* 僅`cq:allowedTemplates`屬性
   >
   >
* 僅位於站點根
>
>
如需範例，請參閱We.Retail:`/content/we-retail/jcr:content`
>
>屬性`allowedPaths`、`allowedParents`和`allowedChildren`也可放置在範本上，以定義更複雜的規則。 不過，如果需要進一步限制允許的範本，在網站的子區段上進一步定義`cq:allowedTemplates`屬性會更簡單。**
>
>另一個好處是，`cq:allowedTemplates`屬性可由作者在&#x200B;**Page Properties**&#x200B;的&#x200B;**Advanced**&#x200B;標籤中更新。 無法使用（標準）UI更新其他範本屬性，因此需要開發人員來維護每次變更的規則和程式碼部署。

在網站管理員介面中建立新頁面時，可用範本清單會根據新頁面的位置，以及每個範本中指定的位置限制而定。

以下屬性確定是否允許將模板`T`用於將新頁面作為頁面`P`的子頁面。 這些屬性中的每個都是多值字串，包含零個或多個用於與路徑比對的規則運算式：

* `P`的`jcr:content`子節點或`P`的祖先的`cq:allowedTemplates`屬性。

* `T`的`allowedPaths`屬性。

* `T`的`allowedParents`屬性。

* `P`範本的`allowedChildren`屬性。

評價工作如下：

* 從`P`開始的頁面階層遞增時找到的第一個非空白`cq:allowedTemplates`屬性與`T`的路徑相符。 如果沒有任何值相符，則拒絕`T`。

* 如果`T`具有非空`allowedPaths`屬性，但沒有任何值與`P`路徑匹配，則拒絕`T`。

* 如果上述兩個屬性為空或不存在，則拒絕`T`，除非它屬於與`P`相同的應用程式。 `T` 屬於同一應用程 `P` 式，只有當路徑的第二級名稱與路 `T` 徑的第二級名稱相同時才 `P`會。例如，範本`/apps/geometrixx/templates/foo`與頁面`/content/geometrixx`屬於相同的應用程式。

* 如果`T`具有非空`allowedParents`屬性，但沒有任何值與`P`路徑匹配，則拒絕`T`。

* 如果`P`的模板具有非空`allowedChildren`屬性，但沒有任何值與`T`的路徑匹配，則`T`將被拒絕。

* 在所有其他情況下，允許`T`。

下圖描述了模板評估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子頁{#limiting-templates-used-in-child-pages}中使用的模板

要限制哪些模板可用於在指定頁面下建立子頁面，請使用頁面`jcr:content`節點的`cq:allowedTemplates`屬性指定允許作為子頁面的模板清單。 清單中的每個值必須是允許的子頁面（例如`/apps/geometrixx/templates/contentpage`）的模板的絕對路徑。

您可以使用範本`jcr:content`節點上的`cq:allowedTemplates`屬性，將此設定套用至使用此範本的所有新建立頁面。

如果要添加更多約束（例如關於模板層次結構），可以在模板上使用`allowedParents/allowedChildren`屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父/子頁面。

## 範本 — 內容片段{#templates-content-fragments}

如需完整資訊，請參閱[內容片段範本](/help/sites-developing/content-fragment-templates.md) 。
