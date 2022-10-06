---
title: 範本
seo-title: Templates
description: 建立將用作新頁面基礎的頁面時，會使用範本
seo-description: Templates are used when creating a page which will be used as the base for the new page
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
source-wordcount: '963'
ht-degree: 1%

---

# 範本{#templates}

範本會用於AEM中的各個時間點：

* 當 [建立需要選擇模板的頁面](#templates-pages);這將用作新頁面的基礎。 範本會定義產生的頁面、任何初始內容和 [元件](/help/sites-authoring/default-components.md) 可使用（設計屬性）。

* 當 [建立內容片段，您也需要選取範本](#templates-content-fragments). 此範本會定義結構、初始元素和變異。

以下範本將詳細說明：

* [頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md)
* [頁面範本 — 靜態](/help/sites-developing/page-templates-static.md)
* [內容片段範本](/help/sites-developing/content-fragment-templates.md)
* [最適化範本轉譯](/help/sites-developing/templates-adaptive-rendering.md)

## 範本 — 頁面 {#templates-pages}

AEM現在提供兩種建立頁面的基本範本類型：

>[!NOTE]
>
>將範本用於 [建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page) 沒有可見的差異（對頁面作者而言），也沒有使用範本類型的指示。

### 可編輯的範本 {#editable-templates}

使用AEM開發時，可編輯的範本現在被視為最佳作法。

可編輯範本的優點：

* 可以是 [已建立](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 和 [編輯](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 作者的。

* 已導入，可讓您為使用範本建立的任何頁面定義下列項目：

   * 結構
   * 初始內容
   * 內容原則

* 建立新頁面後，頁面與範本之間會維持動態連線；這表示使用該範本建立的任何頁面上都會反映對範本結構的變更（不會反映初始內容的變更）。
* 使用內容原則（從範本編輯器編輯）來保留設計屬性（不在頁面編輯器內使用設計模式）。
* 儲存於 `/conf`
* 請參閱 [可編輯的範本](/help/sites-developing/page-templates-editable.md) 以取得更多資訊。

>[!NOTE]
>
>AEM社群文章可供參考，說明如何使用可編輯的範本開發Experience Manager網站，請參閱 [使用可編輯的範本建立Adobe Experience Manager 6.5網站](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### 靜態範本 {#static-templates}

靜態範本:

* 必須由開發人員定義和設定。
* 這是AEM的原始範本系統，可用於許多版本。
* 靜態範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。
* 系統會複製以建立新頁面，之後不會有動態連線。
* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 保留設計屬性。
* 儲存於 `/apps`
* 請參閱 [靜態範本](/help/sites-developing/page-templates-static.md) 以取得更多資訊。

>[!NOTE]
>
>自AEM 6.5起，使用靜態範本不被視為最佳實務。 請改用可編輯的範本。
>
>[AEM現代化](modernization-tools.md) 工具可協助您從靜態範本移轉至可編輯的範本。

### 範本可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供多個屬性，以控制 **網站**. 但是，結合這些規則可能會產生非常複雜的規則，且難以追蹤和管理。
>
>因此，Adobe建議您透過定義：
>
>* 只有 `cq:allowedTemplates` 屬性
>
>* 僅位於站點根
>
>如需範例，請參閱We.Retail: `/content/we-retail/jcr:content`
>
>屬性 `allowedPaths`, `allowedParents`，和 `allowedChildren` 也可以放在範本上，以定義更複雜的規則。 但是，如果可能， *mod* 更簡單地定義 `cq:allowedTemplates` 屬性（如果需要進一步限制允許的範本）。
>
>另一個優點是 `cq:allowedTemplates` 屬性可由作者在 **進階** 的 **頁面屬性**. 無法使用（標準）UI更新其他範本屬性，因此需要開發人員來維護每次變更的規則和程式碼部署。

在網站管理員介面中建立新頁面時，可用範本清單會根據新頁面的位置，以及每個範本中指定的位置限制而定。

下列屬性決定範本是否為 `T` 可用於將新頁面放置為頁面子項 `P`. 這些屬性中的每個都是多值字串，包含零個或多個用於與路徑比對的規則運算式：

* 此 `cq:allowedTemplates` 屬性 `jcr:content` 子節點 `P` 或祖先 `P`.

* 此 `allowedPaths` 屬性 `T`.

* 此 `allowedParents` 屬性 `T`.

* 此 `allowedChildren` 模板的屬性 `P`.

評價工作如下：

* 第一個非空白 `cq:allowedTemplates` 遞增頁面階層時找到的屬性，開頭為 `P` 與 `T`. 如果沒有任何值相符， `T` 被拒絕。

* 若 `T` 非空白 `allowedPaths` 屬性，但沒有任何值符合 `P`, `T` 被拒絕。

* 如果上述兩個屬性均為空或不存在， `T` 拒絕，除非它屬於與 `P`. `T` 屬於與 `P` 如果且唯若路徑的第二層名稱 `T` 與路徑的第二層的名稱相同 `P`. 例如，範本 `/apps/geometrixx/templates/foo` 屬於與頁面相同的應用程式 `/content/geometrixx`.

* 若 `T` 具有非空白 `allowedParents` 屬性，但沒有任何值符合 `P`, `T` 被拒絕。

* 若範本為 `P` 非空白 `allowedChildren` 屬性，但沒有任何值符合 `T`, `T` 被拒絕。

* 在其他所有情況下， `T` 中指定的規則。

下圖描述了模板評估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子頁面中使用的模板 {#limiting-templates-used-in-child-pages}

若要限制哪些範本可用來建立指定頁面下的子頁面，請使用 `cq:allowedTemplates` 屬性 `jcr:content` 頁的節點，以指定允許作為子頁的模板清單。 例如，清單中的每個值必須是允許的子頁面範本的絕對路徑 `/apps/geometrixx/templates/contentpage`.

您可以使用 `cq:allowedTemplates` 範本的屬性  `jcr:content` 節點，將此配置應用於使用此模板的所有新建立的頁面。

如果您想要新增更多限制（例如關於範本階層），可使用 `allowedParents/allowedChildren` 屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父/子頁面。

## 範本 — 內容片段 {#templates-content-fragments}

請參閱 [內容片段範本](/help/sites-developing/content-fragment-templates.md) 以取得完整資訊。
