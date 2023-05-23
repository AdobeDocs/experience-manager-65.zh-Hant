---
title: 範本
description: 在建立用作新頁面基礎的頁面時使用模板。
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---

# 範本{#templates}

模板用於以下各個AEM點：

* [建立頁面時，將選擇模板](#templates-pages)。 此模板用作新頁面的基礎。 模板定義頁面結構、任何初始內容以及 [元件](/help/sites-authoring/default-components.md) （設計屬性）。

* [建立內容片段時，還會選擇模板](#templates-content-fragments)。 此模板定義結構、初始元素和變體。

下面的模板將詳細介紹：

* [頁面模板 — 可編輯](/help/sites-developing/page-templates-editable.md)
* [頁面模板 — 靜態](/help/sites-developing/page-templates-static.md)
* [內容片段模板](/help/sites-developing/content-fragment-templates.md)
* [自適應模板渲染](/help/sites-developing/templates-adaptive-rendering.md)

## 模板 — 頁面 {#templates-pages}

現AEM在提供了兩種基本類型的模板來建立頁面：

>[!NOTE]
>
>使用模板時 [建立頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)，沒有可見的差異（對頁面作者而言），也沒有正在使用的模板類型的指示。

### 可編輯的範本 {#editable-templates}

現在，可編輯模板被視為使用開發的最佳AEM做法。

可編輯模板的優點：

* 可以 [建立](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 和 [編輯](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 你的作者。

* 已引入，以允許您為使用模板建立的任何頁面定義以下內容：

   * 結構
   * 初始內容
   * 內容策略

* 建立新頁面後，將在頁面和模板之間保持動態連接。 這種連接意味著對模板結構的更改反映在使用該模板建立的任何頁面上；不反映對初始內容的更改。
* 使用內容策略（從模板編輯器編輯）來保留設計屬性（不在頁面編輯器中使用「設計」模式）。
* 儲存在 `/conf`
* 請參閱 [可編輯模板](/help/sites-developing/page-templates-editable.md) 的上界。

>[!NOTE]
>
>請參閱 [使用可編輯頁面模板開發Experience Manager站點](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en)。

### 靜態範本 {#static-templates}

靜態範本:

* 必須由開發人員定義和配置。
* 原有的模AEM板系統已用於多個版本。
* 靜態模板是節點的層次結構，該層次結構與要建立的頁面相同，但沒有任何實際內容。
* 複製以建立頁面，之後不存在動態連接。
* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 來保留設計屬性。
* 儲存在 `/apps`
* 請參閱 [靜態模板](/help/sites-developing/page-templates-static.md) 的上界。

>[!NOTE]
>
>截至AEM6.5，使用靜態模板不被視為最佳做法。 改用可編輯模板。
>
>[現代AEM化](modernization-tools.md) 工具可幫助您從靜態模板遷移到可編輯模板。

### 範本可用性 {#template-availability}

>[!CAUTION]
>
>提供AEM多個屬性，以控制在 **站點**。 但是，將它們組合起來會導致複雜的規則難以跟蹤和管理。
>
>因此，Adobe建議您通過定義：
>
>* 只有 `cq:allowedTemplates` 屬性
>
>* 僅在站點根目錄上
>
>有關示例，請參見We.Retail: `/content/we-retail/jcr:content`
>
>屬性 `allowedPaths`。 `allowedParents`, `allowedChildren` 也可以放在模板上以定義更複雜的規則。 但是，如果可能的話 *多* 更簡單地定義 `cq:allowedTemplates` 如果需要進一步限制允許的模板，請在站點的子部分上顯示屬性。
>
>另外一個優勢是 `cq:allowedTemplates` 屬性可由作者在 **高級** 頁籤 **頁面屬性**。 其他模板屬性無法使用（標準）UI更新，因此需要開發人員來維護每次更改的規則和代碼部署。

在站點管理介面中建立頁面時，可用模板清單取決於新頁面的位置以及每個模板中指定的放置限制。

以下屬性確定模板 `T` 用於作為頁面子項放置的新頁面 `P`。 每個屬性都是一個多值字串，包含零個或多個用於與路徑匹配的規則運算式：

* 的 `cq:allowedTemplates` 屬性 `jcr:content` 子節點 `P` 或是 `P`。

* 的 `allowedPaths` 物業 `T`。

* 的 `allowedParents` 物業 `T`。

* 的 `allowedChildren` 模板的屬性 `P`。

評價工作如下：

* 第一個非空 `cq:allowedTemplates` 升序頁層次結構時找到的屬性 `P` 與 `T`。 如果所有值都不匹配， `T` 已拒絕。

* 如果 `T` 具有非空 `allowedPaths` 屬性，但所有值均與 `P`。 `T` 已拒絕。

* 如果上述兩個屬性都為空或不存在， `T` 除非它屬於與 `P`。 `T` 屬於與 `P` 如果且僅當路徑的第二級的名稱 `T` 與路徑的第二級的名稱相同 `P`。 例如，模板 `/apps/geometrixx/templates/foo` 屬於與頁面相同的應用程式 `/content/geometrixx`。

* 如果 `T` 具有非空 `allowedParents` 屬性，但所有值均與 `P`。 `T` 已拒絕。

* 如果的模板 `P` 具有非空 `allowedChildren` 屬性，但所有值均與 `T`。 `T` 已拒絕。

* 在其他情況下， `T` 的子菜單。

下圖描述了模板評估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子頁中使用的模板 {#limiting-templates-used-in-child-pages}

要限制可用於在給定頁面下建立子頁面的模板，請使用 `cq:allowedTemplates` 物業 `jcr:content` 的子頁。 清單中的每個值必須是允許的子頁模板的絕對路徑，例如 `/apps/geometrixx/templates/contentpage`。

您可以使用 `cq:allowedTemplates` 模板的  `jcr:content` 節點，以將此配置應用於使用此模板的所有新建立的頁面。

如果要添加更多約束，例如，關於模板層次結構，可以使用 `allowedParents/allowedChildren` 屬性。 然後，可以明確指定從模板T建立的頁面必須是從模板T建立的頁面的父/子。

## 模板 — 內容片段 {#templates-content-fragments}

請參閱 [內容片段模板](/help/sites-developing/content-fragment-templates.md)。
