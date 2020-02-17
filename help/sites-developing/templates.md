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
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 範本{#templates}

範本用於AEM的不同點：

* 建 [立頁面時，需要選取範本](#templates-pages);這將用作新頁面的基礎。 範本會定義結果頁面的結構、任何初始內容 [及可使用](/help/sites-authoring/default-components.md) 的元件（設計屬性）。

* 建立 [內容片段時，您也需要選取範本](#templates-content-fragments)。 此範本會定義結構、初始元素和變化。

以下範本將詳細說明：

* [頁面範本——可編輯](/help/sites-developing/page-templates-editable.md)
* [頁面範本——靜態](/help/sites-developing/page-templates-static.md)
* [內容片段範本](/help/sites-developing/content-fragment-templates.md)
* [最適化範本演算](/help/sites-developing/templates-adaptive-rendering.md)

## 範本——頁面 {#templates-pages}

AEM現在提供兩種基本範本類型，以建立頁面：

>[!NOTE]
>
>使用範本建立新 [頁面時](/help/sites-authoring/managing-pages.md#creating-a-new-page) ，沒有顯示差異（對頁面作者而言），也沒有顯示使用的範本類型。

### 可編輯的範本 {#editable-templates}

可編輯的範本現在被視為使用AEM進行開發的最佳實務。

可編輯範本的優點：

* 您的作 [者可](/help/sites-authoring/templates.md#creating-a-new-template-template-author)[以建](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 立和編輯。

* 已引入此功能，可讓您為使用範本建立的任何頁面定義下列項目：

   * 結構
   * 初始內容
   * 內容策略

* 建立新頁面後，頁面與範本之間會維持動態連線；這表示對範本結構所做的變更將反映在該範本所建立的任何頁面上（不會反映對初始內容的變更）。
* 使用內容原則（從範本編輯器編輯）來保存設計屬性（不在頁面編輯器中使用設計模式）。
* 儲存於 `/conf`
* 如需詳 [細資訊](/help/sites-developing/page-templates-editable.md) ，請參閱可編輯範本。

>[!NOTE]
>
>AEM社群文章會說明如何使用可編輯範本開發Experience Manager網站，請參閱「使用可編輯範本建立 [Adobe Experience Manager 6.5網站」](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)。

### 靜態範本 {#static-templates}

靜態範本：

* 必須由您的開發人員定義和設定。
* 這是AEM的原始範本系統，已推出許多版本。
* 靜態範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。
* 複製以建立新頁面，之後不存在動態連線。
* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) ，保留設計屬性。
* 儲存於 `/apps`
* 如需詳 [細資訊，請參閱](/help/sites-developing/page-templates-static.md) 「靜態範本」。

>[!NOTE]
>
>自AEM 6.5起，使用靜態範本並不被視為最佳實務。 請改用可編輯的範本。
>
>[AEM Muderation](modernization-tools.md) tools可協助您從靜態範本移轉至可編輯的範本。

### 範本可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供多個屬性，以控制「網站」下允許的 **範本**。 但是，結合這些規則可能會產生非常複雜的規則，而且難以追蹤和管理。
>
>因此，Adobe建議您從定義：
>
>* 只有屬 `cq:allowedTemplates` 性
   >
   >
* 僅位於站點根目錄
>
>
如需範例，請參閱We.Retail: `/content/we-retail/jcr:content`
>
>屬性 `allowedPaths`、 `allowedParents`和 `allowedChildren` 也可放在範本上，以定義更複雜的規則。 不過，如果有必要 *進一步限制* ，在網站 `cq:allowedTemplates` 的子區段上定義更多屬性會更簡單。
>
>另一個好處是， `cq:allowedTemplates` 「頁面屬性」的「進階」索引標籤中的作者 **可更新** 屬性 ****。 其他範本屬性無法使用（標準）UI進行更新，因此需要開發人員來維護規則和程式碼部署以進行每項變更。

在網站管理介面中建立新頁面時，可用範本的清單會視新頁面的位置以及每個範本中指定的位置限制而定。

下列屬性可決定是否允 `T` 許範本用於新頁面，以做為頁面的子頁面 `P`。 這些屬性中的每個屬性都是一個多值字串，其中包含0或多個規則運算式，用於與路徑進行比對：

* 子 `cq:allowedTemplates` 節點或 `jcr:content` 祖先的 `P` 屬性 `P`。

* 屬 `allowedPaths` 性 `T`。

* 屬 `allowedParents` 性 `T`。

* 的 `allowedChildren` 模板屬性 `P`。

評價工作如下：

* 遞增頁面階層時找 `cq:allowedTemplates` 到的第一個非空白屬性(以開頭為 `P` 單位)與路徑相符 `T`。 如果沒有任何值符合，則 `T` 會拒絕。

* 如 `T` 果具有非空 `allowedPaths` 白屬性，但沒有任何值與路徑相符 `P`，則 `T` 拒絕。

* 如果上述兩個屬性皆為空白或不存在，則 `T` 會拒絕，除非屬於與相同的應用程式 `P`。 `T` 僅當路徑的第二 `P` 級名稱與路徑的第二級名稱相同 `T` 時，才屬於相同的應用程式 `P`。 例如，範本屬 `/apps/geometrixx/templates/foo` 於與頁面相同的應用程式 `/content/geometrixx`。

* 如 `T` 果具有非空 `allowedParents` 白屬性，但沒有任何值與路徑相符 `P`，則 `T` 拒絕。

* 如果的模板 `P` 具有非空 `allowedChildren` 屬性，但沒有任何值與路徑匹配 `T`，則 `T` 拒絕。

* 在其他所有情況下， `T` 都允許。

下圖描述了模板評估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子頁面中使用的範本 {#limiting-templates-used-in-child-pages}

若要限制在指定頁面下可用來建立子頁面的範本，請使用頁面 `cq:allowedTemplates` 節 `jcr:content` 點的屬性來指定範本清單，以允許做為子頁面。 例如，清單中的每個值都必須是允許子頁面範本的絕對路徑 `/apps/geometrixx/templates/contentpage`。

您可以使用范 `cq:allowedTemplates` 本節點上的屬性，將 `jcr:content` 此組態套用至使用此範本的所有新建立頁面。

如果要添加更多約束（例如，關於模板層次），可以使用模 `allowedParents/allowedChildren` 板上的屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父項／子項。

## 範本——內容片段 {#templates-content-fragments}

如需完 [整資訊，請參閱內容片段範本](/help/sites-developing/content-fragment-templates.md) 。
