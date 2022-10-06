---
title: AEM開發 — 准則和最佳實務
seo-title: AEM Development - Guidelines and Best Practices
description: 在AEM上開發的准則和最佳實務
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

# AEM開發 — 准則和最佳實務{#aem-development-guidelines-and-best-practices}

## 使用範本和元件的准則 {#guidelines-for-using-templates-and-components}

AEM元件和範本提供強大的工具套件。 開發人員可使用這些功能，為網站業務使用者、編輯和管理員提供調整其網站以適應不斷變化的業務需求（內容靈活性）的功能，同時保留網站的統一版面配置（品牌保護）。

對於負責網站或一組網站（例如全球企業的分支辦公室）的人來說，一個典型的挑戰是在其網站上引入新類型的內容演示。

假設有必要將新聞清單頁面新增至網站，列出已發佈之其他文章的摘要。 頁面的設計和結構應與網站的其他部分相同。

應對這種挑戰的建議方法是：

* 重複使用現有模板以建立新類型的頁面。 範本粗略定義頁面結構（導覽元素、面板等），並透過其設計（CSS、圖形）進一步微調。
* 在新頁面上使用段落系統(parsys/iparsys)。
* 定義段落系統的「設計」模式的訪問權限，以便只有授權人員（通常是管理員）才能更改它們。
* 定義指定段落系統中允許的元件，以便編輯人員將必要的元件放置在頁面上。 在本例中，它可以是清單元件，可以遍歷頁面的子樹狀結構，並根據預先定義的規則擷取資訊。
* 編輯人員在他們負責的頁面上新增並設定允許的元件，以將要求的功能（資訊）傳遞至企業。

這說明此方法如何讓網站的貢獻使用者和管理員能夠快速回應業務需求，而不需要開發團隊的參與。 其他方法，例如建立新模板，通常是一項代價高昂的工作，需要變革管理流程和開發團隊的參與。 這使得整個過程更長，成本也更高。

因此，AEM型系統的開發人員應使用：

* 段落系統設計的模板和訪問控制，以實現一致性和品牌保護
* 段落系統，包括其靈活性配置選項。

在大部分的常見專案中，開發人員適用的下列一般規則是有意義的：

* 將範本數量保持在較低，低至網站上基本不同的頁面結構數量。
* 為您的自訂元件提供必要的彈性和設定功能。
* 充分運用AEM段落系統（parsys &amp; iparsys元件）的強大功能和彈性。

### 自訂元件和其他元素 {#customizing-components-and-other-elements}

建立自己的元件或自訂現有元件時，最簡單（最安全）的做法是重複使用現有定義。 同樣的原則也適用於AEM內的其他元素，例如錯誤處理常式。

您可以複製並覆寫現有定義來完成此操作。 換言之，將定義從 `/libs` to `/apps/<your-project>`. 此新定義，位於 `/apps`，可根據您的需求更新。

>[!NOTE]
>
>請參閱 [使用覆蓋](/help/sites-developing/overlays.md) 以取得更多詳細資訊。

例如：

* [自訂元件](/help/sites-developing/components.md)

   這涉及覆蓋元件定義：

   * 在中建立新元件資料夾 `/apps/<website-name>/components/<MyComponent>` 複製現有元件：

      * 例如，要自定義文本元件副本：

         * 從 `/libs/foundation/components/text`
         * 至 `/apps/myProject/components/text`

* [自訂由錯誤處理常式顯示的頁面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   此情況涉及覆蓋servlet:

   * 在存放庫中，複製預設指令碼：

      * 從 `/libs/sling/servlet/errorhandler/`
      * 至 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>您 **不能** 改變 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>針對設定和其他變更：
>
>1. 複製項目 `/libs` to `/apps`
>1. 在 `/apps`


## JCR查詢的使用時機和不使用時機 {#when-to-use-jcr-queries-and-when-not-to-use-them}

正確使用時，JCR查詢是功能強大的工具。 這些規則適合：

* 真正的一般使用者查詢，例如內容的全文搜尋。
* 需要在整個儲存庫中找到結構化內容的場合。

   在這種情況下，請確保查詢僅在絕對需要時運行，例如元件激活或快取失效時（而不是工作流步驟、在內容修改時觸發的事件處理程式、篩選器等）。

JCR查詢絕不應用於純轉譯請求。 例如，JCR查詢不適用於

* 呈現導覽
* 建立「前10大最新消息」概述
* 顯示內容項目計數

若要轉譯內容，請使用內容樹狀結構的導覽存取權，而非執行JCR查詢。

>[!NOTE]
>
>如果您使用 [查詢產生器](/help/sites-developing/querybuilder-api.md)，您會使用JCR查詢，因為查詢產生器會在標題下產生JCR查詢。

## 安全性考量事項 {#security-considerations}

>[!NOTE]
>
>也值得參考 [安全檢查清單](/help/sites-administering/security-checklist.md).

### JCR（儲存庫）會話 {#jcr-repository-sessions}

您應使用使用者工作階段，而非管理工作階段。 這表示您應使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect反對跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁。 惡意Web用戶可利用此安全漏洞繞過訪問控制。

AEM會套用在輸出時篩選所有使用者提供的內容的原則。 在開發和測試期間，防止XSS的優先順序最高。

此外，Web應用程式防火牆，例如 [Apache的mod_security](https://modsecurity.org)，可提供對部署環境安全性的可靠中央控制，並防止先前未偵測到的跨網站指令碼攻擊。

>[!CAUTION]
>
>隨AEM提供的范常式式碼本身可能無法抵御這類攻擊，且通常需仰賴Web應用程式防火牆的要求篩選。

XSS API速查表包含您需知的資訊，以便使用XSS API並讓AEM應用程式更安全。 您可以在此處下載：

XSSAPI速查表。

[取得檔案](assets/xss_cheat_sheet_2016.pdf)

### 保護機密資訊的通信 {#securing-communication-for-confidential-information}

至於任何網際網路應用程式，請務必在傳輸機密資訊時

* 通過SSL保護流量
* 若適用，則使用HTTPPOST

這適用於對系統保密的資訊（如配置或管理訪問），以及對其用戶保密的資訊（如其個人詳細資訊）

## 獨特的開發任務 {#distinct-development-tasks}

### 自訂錯誤頁面 {#customizing-error-pages}

可針對AEM自訂錯誤頁面。 建議您這麼做，這樣執行個體就不會在內部伺服器錯誤上顯示Sling追蹤。

請參閱 [自定義錯誤處理程式顯示的錯誤頁](/help/sites-developing/customizing-errorhandler-pages.md) 以取得完整詳細資訊。

### 在Java進程中開啟檔案 {#open-files-in-the-java-process}

由於AEM可以存取大量檔案，因此建議將 [開啟Java進程的檔案](/help/sites-deploying/configuring.md#open-files-in-the-java-process) 為AEM明確設定。

為了盡量減少此問題的發展，應確保盡快（有意義地）正確關閉任何開啟的檔案。
