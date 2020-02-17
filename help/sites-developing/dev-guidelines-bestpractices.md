---
title: AEM開發——准則與最佳實務
seo-title: AEM開發——准則與最佳實務
description: 針對AEM開發的准則和最佳實務
seo-description: 針對AEM開發的准則和最佳實務
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM開發——准則與最佳實務{#aem-development-guidelines-and-best-practices}

## 使用範本和元件的指引 {#guidelines-for-using-templates-and-components}

AEM元件和範本構成功能強大的工具套件。 開發人員可運用這些工具，為網站商業使用者、編輯和管理員提供功能，讓他們的網站適應不斷變化的商業需求（內容敏捷性），同時保留網站的統一版面（品牌保護）。

負責網站或網站組（例如全球企業的分支機構）的人員，在其網站上推出新型的內容簡報，是一項典型的挑戰。

讓我們假設有必要將新聞清單頁面新增至網站，列出已發佈之其他文章的摘要。 頁面的設計和結構應與網站的其他部分相同。

解決此類挑戰的建議方式是：

* 重複使用現有範本以建立新的頁面類型。 範本大致定義頁面結構（導覽元素、面板等），並透過其設計（CSS、圖形）進一步微調。
* 在新頁面上使用段落系統(parsys/iparsys)。
* 定義段落系統「設計」模式的存取權，讓只有授權人員（通常是管理員）才能變更。
* 定義指定段落系統中允許的元件，讓編輯人員將必要的元件置於頁面上。 在我們的例子中，它可以是一個清單元件，它可以遍歷頁面的子樹，並根據預定義規則提取資訊。
* 編輯人員可在他們負責的頁面上新增及設定允許的元件，以將要求的功能（資訊）提供給企業。

這說明此方法如何讓網站的貢獻使用者和管理員快速回應業務需求，而不需要開發團隊的參與。 其他方法，例如建立新範本，通常是一項耗費成本的工作，需要變更管理程式和開發團隊的參與。 這使得整個流程更長，成本也更高。

因此，AEM系統的開發人員應使用：

* 範本和存取控制段落系統設計，以提供一致性和品牌保護
* 段落系統包括其靈活性的配置選項。

在大部分的一般專案中，開發人員適用的下列一般規則都有意義：

* 將範本數保持在低位——低至網站上基本不同的頁面結構數。
* 為您的自訂元件提供必要的彈性和設定功能。
* 充份運用AEM段落系統的強大功能與彈性- parsys &amp; iparsys元件。

### 自訂元件和其他元素 {#customizing-components-and-other-elements}

建立您自己的元件或自訂現有元件時，重新使用現有定義通常最簡單（而且最安全）。 相同的原則也適用於AEM中的其他元素，例如錯誤處理常式。

這可以通過複製和覆蓋現有定義來完成。 換句話說，將定義從複製到 `/libs` 中 `/apps/<your-project>`。 此新定義(在中 `/apps`)可根據您的需求進行更新。

>[!NOTE]
>
>如需詳 [細資訊](/help/sites-developing/overlays.md) ，請參閱使用覆蓋。

例如：

* [自訂元件](/help/sites-developing/components.md)

   這涉及覆蓋元件定義：

   * 通過複製現有元件在中 `/apps/<website-name>/components/<MyComponent>` 建立新元件資料夾：

      * 例如，要自定義Text元件副本：

         * 從 `/libs/foundation/components/text`
         * 至 `/apps/myProject/components/text`

* [自訂錯誤處理常式所顯示的頁面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   這種情況涉及覆蓋servlet:

   * 在儲存庫中，複製預設指令碼：

      * 從 `/libs/sling/servlet/errorhandler/`
      * 至 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>您 **不得變** 更路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
>
>對於配置和其他更改：
>
>1. 將項目複製到 `/libs``/apps`
>1. 在 `/apps`


## 何時使用JCR查詢以及何時不使用它們 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR查詢在正確使用時是功能強大的工具。 它們適合：

* 真正的使用者查詢，例如內容的全文搜尋。
* 需要在整個儲存庫中找到結構化內容的場合。

   在這種情況下，請確定查詢僅在絕對需要時執行，例如元件啟動或快取失效（而非工作流程步驟、觸發內容修改的事件處理常式、篩選等）。

JCR查詢不應用於純演算請求。 例如，JCR查詢不適用於

* 渲染導航
* 建立「前10大最新消息」總覽
* 顯示內容項目計數

若要轉譯內容，請使用內容樹狀結構的導覽存取權，而非執行JCR查詢。

>[!NOTE]
>
>如果您使用 [Query Builder](/help/sites-developing/querybuilder-api.md)，則會使用JCR查詢，因為Query Builder會在引擎蓋下產生JCR查詢。


## 安全性考量 {#security-considerations}

>[!NOTE]
>
>此外，參考安全性檢查清單也 [是值得的](/help/sites-administering/security-checklist.md)。

### JCR（儲存庫）會話 {#jcr-repository-sessions}

您應使用使用者工作階段，而非管理工作階段。 這表示您應使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### 防止跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼注入其他使用者檢視的網頁。 惡意Web使用者可利用此安全性弱點略過存取控制。

AEM會套用在輸出時篩選所有使用者提供內容的原則。 在開發和測試期間，防止XSS的優先順序最高。

此外，Web應用程式防火牆(例如 [mod_security for Apache](https://modsecurity.org))可提供可靠、集中的部署環境安全控制，並防止先前未偵測到的跨網站指令碼攻擊。

>[!CAUTION]
>
>AEM提供的范常式式碼本身可能無法針對此類攻擊提供保護，而且通常需仰賴網路應用程式防火牆的請求篩選。

XSS API快速參考表包含您需要知道的資訊，以便使用XSS API並讓AEM應用程式更安全。 您可從以下網址下載：

XSAPI快速參考表。

[取得檔案](assets/xss_cheat_sheet_2016.pdf)

### 保護機密資訊的通訊安全 {#securing-communication-for-confidential-information}

至於任何網際網路應用程式，請務必在傳送機密資訊時

* 通信通過SSL受到保護
* HTTP POST已使用（如果適用）

這適用於對系統保密的資訊（如設定或管理存取），以及對其使用者保密的資訊（如其個人詳細資訊）

## 不同的開發任務 {#distinct-development-tasks}

### 自訂錯誤頁面 {#customizing-error-pages}

可針對AEM自訂錯誤頁面。 這是建議的，因此實例不會顯示內部伺服器錯誤上的吊索跟蹤。

如需 [完整詳細資訊，請參閱自訂錯誤處理常式所顯示的錯誤頁](/help/sites-developing/customizing-errorhandler-pages.md) 。

### 在Java進程中開啟檔案 {#open-files-in-the-java-process}

由於AEM可存取大量檔案，因此建議明確設定Java [程式的開啟檔案數](/help/sites-deploying/configuring.md#open-files-in-the-java-process) ，以供AEM使用。

為了盡量減少此問題的發展，應確保所開啟的檔案能盡快（有意義）正確關閉。
