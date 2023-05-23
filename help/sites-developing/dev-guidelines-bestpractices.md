---
title: 開AEM發 — 指南和最佳做法
seo-title: AEM Development - Guidelines and Best Practices
description: 關於開發
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# 開AEM發 — 指南和最佳做法{#aem-development-guidelines-and-best-practices}

## 使用模板和元件的指南 {#guidelines-for-using-templates-and-components}

元件AEM和模板構成了一個功能強大的工具包。 開發人員可以使用它們為網站業務用戶、編輯和管理員提供功能，使其網站適應不斷變化的業務需求（內容靈活性），同時保留網站的統一佈局（品牌保護）。

對於負責網站或一組網站（例如全球性企業的分支機構）的人員來說，一個典型的挑戰是在其網站上引入一種新型的內容演示。

讓我們假設有必要向網站添加新聞清單頁面，該頁面列出已發佈的其他文章的摘要。 頁面的設計和結構應與網站的其他部分相同。

建議的應對這種挑戰的方法是：

* 重用現有模板以建立新類型的頁面。 模板大致定義頁面結構（導航元素、面板等），該結構通過其設計（CSS、圖形）進一步進行微調。
* 在新頁面上使用段落系統(parsys/iparsys)。
* 定義對段落系統「設計」模式的訪問權限，以便只有授權人員（通常是管理員）才能更改這些權限。
* 定義給定段落系統中允許的元件，以便編輯人員隨後可以將所需的元件放在頁面上。 在本例中，它可以是一個清單元件，它可以遍歷頁面的子樹並根據預定義的規則提取資訊。
* 編輯在他們負責的頁面上添加和配置允許的元件，以將請求的功能（資訊）交付給業務。

這說明了這種方法如何使網站的貢獻用戶和管理員能夠快速響應業務需求，而無需開發團隊的參與。 另一種方法，如建立新模板，通常需要付出高昂的代價，需要變更管理流程和開發團隊的參與。 這使得整個過程更長，成本也更高。

因此，基AEM於系統的開發人員應使用：

* 模板和訪問控制段落系統設計以實現一致性和品牌保護
* 段落系統，包括其靈活性配置選項。

在大多數通常的項目中，開發商的以下一般規則是有意義的：

* 將模板數保持為低 — 與網站上基本不同的頁面結構數一樣低。
* 為您的定製元件提供必要的靈活性和配置功能。
* 最大限度地利用段落系統（parsys和iparsys元件）AEM的功能和靈活性。

### 定制元件和其他元素 {#customizing-components-and-other-elements}

在建立您自己的元件或自定義現有元件時，重新使用現有定義通常最簡單（也最安全）。 同樣的原則也適用於內部的其AEM他元素，例如錯誤處理程式。

這可以通過複製和覆蓋現有定義來完成。 換句話說，從 `/libs` 至 `/apps/<your-project>`。 此新定義，在 `/apps`，可根據您的要求進行更新。

>[!NOTE]
>
>請參閱 [使用疊加](/help/sites-developing/overlays.md) 的子菜單。

例如：

* [自定義元件](/help/sites-developing/components.md)

   這涉及覆蓋元件定義：

   * 在中建立新元件資料夾 `/apps/<website-name>/components/<MyComponent>` 通過複製現有元件：

      * 例如，要自定義文本元件副本：

         * 從 `/libs/foundation/components/text`
         * 至 `/apps/myProject/components/text`

* [自定義錯誤處理程式顯示的頁](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   本例涉及覆蓋Servlet:

   * 在儲存庫中，複製預設指令碼：

      * 從 `/libs/sling/servlet/errorhandler/`
      * 至 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>你 **不能** 改變了 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
>
>對於配置和其他更改：
>
>1. 複製中的項 `/libs` 至 `/apps`
>1. 進行任何更改 `/apps`


## 何時使用JCR查詢以及何時不使用它們 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR查詢是正確使用時功能強大的工具。 它們適用於：

* 真正的最終用戶查詢，例如對內容的全文搜索。
* 需要在整個儲存庫中找到結構化內容的場合。

   在這種情況下，請確保查詢僅在絕對需要時運行，例如元件激活或快取無效（而不是在內容修改時觸發的工作流步驟、事件處理程式、篩選器等）。

JCR查詢不應用於純呈現請求。 例如，JCR查詢不適用於

* 繪製導航
* 建立「前10大最新新聞」概述
* 顯示內容項計數

要呈現內容，請使用對內容樹的導航訪問，而不是執行JCR查詢。

>[!NOTE]
>
>如果使用 [查詢生成器](/help/sites-developing/querybuilder-api.md)，使用「JCR查詢」(JCR Queries)，因為查詢生成器在引擎蓋下生成JCR查詢。

## 安全注意事項 {#security-considerations}

>[!NOTE]
>
>也值得參考 [安全檢查](/help/sites-administering/security-checklist.md)。

### JCR（儲存庫）會話 {#jcr-repository-sessions}

您應使用用戶會話，而不是管理會話。 這意味著您應使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect反對跨站點指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨站點指令碼(XSS)允許攻擊者將代碼注入其他用戶查看的網頁。 惡意Web用戶可利用此安全漏洞繞過訪問控制。

應AEM用輸出時過濾所有用戶提供的內容的原則。 在開發和測試期間，防止XSS是最優先的任務。

另外，Web應用防火牆，例如 [mod_security for Apache](https://modsecurity.org)，可以對部署環境的安全性提供可靠、集中的控制，並防止以前未被發現的跨站點指令碼攻擊。

>[!CAUTION]
>
>隨附的示例代AEM碼本身可能無法防止此類攻擊，並且通常依賴Web應用程式防火牆的請求過濾。

XSS API欺騙表包含您需要瞭解的資訊，以便使用XSS API並使應用更AEM加安全。 您可以從以下位置下載：

XSSAPI欺騙表。

[取得檔案](assets/xss_cheat_sheet_2016.pdf)

### 保護機密資訊的通信安全 {#securing-communication-for-confidential-information}

對於任何Internet應用程式，請確保在傳輸機密資訊時

* 通過SSL保護通信
* HTTPPOST（如果適用）

這適用於對系統保密的資訊（如配置或管理訪問），以及對用戶保密的資訊（如其個人詳細資訊）

## 不同的開發任務 {#distinct-development-tasks}

### 自定義錯誤頁 {#customizing-error-pages}

可為自定義錯誤頁AEM。 建議這樣做，以便實例不會顯示內部伺服器錯誤上的吊帶跟蹤。

請參閱 [自定義錯誤處理程式顯示的錯誤頁](/help/sites-developing/customizing-errorhandler-pages.md) 的雙曲餘切值。

### 在Java進程中開啟檔案 {#open-files-in-the-java-process}

因AEM為可以訪問大量檔案，建議 [開啟Java進程的檔案](/help/sites-deploying/configuring.md#open-files-in-the-java-process) 已明確配置AEM。

要盡量減少此問題的發展，應確保盡快（有意義地）正確關閉開啟的任何檔案。
