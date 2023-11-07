---
title: AEM開發 — 指導方針與最佳作法
description: 在AEM上開發的准則和最佳實務
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# AEM開發 — 指導方針與最佳作法{#aem-development-guidelines-and-best-practices}

## 使用範本和元件的准則 {#guidelines-for-using-templates-and-components}

Adobe Experience Manager (AEM)元件和範本包含強大的工具組。 開發人員可使用這些變數，為網站業務使用者、編輯和管理員提供調整其網站以符合不斷變化的業務需求（內容靈敏度）的功能。 所有這些，同時保留網站的統一配置（品牌保護）。

對於負責一個網站或一組網站（例如，在全球企業的分支機構）的人來說，一個典型的挑戰是在他們的網站上引入一種新的內容簡報。

假設需要將新聞清單頁面新增至網站，其中會列出從其他已發佈文章中擷取的資訊。 此頁面應具有與網站其他部分相同的設計和結構。

解決此類難題的建議方法是：

* 重複使用現有的範本，以便建立頁面型別。 範本會粗略定義頁面結構（導覽元素、面板等），並透過其設計（CSS、圖形）進一步微調。
* 在新頁面上使用段落系統(parsys/iparsys)。
* 定義段落系統「設計」模式的存取權，以便只有授權人員（通常是管理員）才能變更它們。
* 定義指定段落系統中允許的元件，讓編輯人員隨後可將所需元件放置到頁面上。 在這種情況下，它可能是清單元件，可周遊頁面的子樹狀結構，並根據預先定義的規則擷取資訊。
* 編輯者在他們負責的頁面上新增並設定允許的元件，以將要求的功能（資訊）提供給企業。

這說明了此方法如何讓網站貢獻的使用者和管理員能夠快速回應業務需求，而不需要開發團隊的參與。 替代方法，例如建立範本，通常是一項成本高昂的工作，需要變更管理流程和開發團隊的參與。 這會導致整個程式更長且成本高昂。

因此，AEM系統的開發人員應該使用：

* 範本和段落系統設計的存取控制，以統一和品牌保護
* 段落系統，包括其彈性設定選項。

以下為開發人員的一般規則，在大多數的常見專案中都有意義：

* 維持低範本數量 — 與網站上完全不同的頁面結構數量一樣低。
* 為您的自訂元件提供必要的彈性和設定功能。
* 充分運用AEM段落系統（parsys和iparsys元件）的強大功能與彈性。

### 自訂元件和其他元素 {#customizing-components-and-other-elements}

建立您自己的元件或自訂現有的元件時，通常最容易（也最安全）重複使用現有的定義。 同樣的原則也適用於AEM內的其他元素，例如錯誤處理常式。

這可以透過複製和覆蓋現有定義來完成。 換言之，復制定義來源 `/libs` 至 `/apps/<your-project>`. 此新定義，在 `/apps`，可根據您的需求進行更新。

>[!NOTE]
>
>另請參閱 [使用覆蓋](/help/sites-developing/overlays.md) 以取得更多詳細資料。

例如：

* [自訂元件](/help/sites-developing/components.md)

  這涉及覆蓋元件定義：

   * 在中建立元件資料夾 `/apps/<website-name>/components/<MyComponent>` 透過複製現有元件：

      * 例如，若要自訂文字元件複製：

         * 從 `/libs/foundation/components/text`
         * 至 `/apps/myProject/components/text`

* [自訂錯誤處理常式顯示的頁面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  此案例涉及覆蓋servlet：

   * 在存放庫中，複製一或多個預設指令碼：

      * 從 `/libs/sling/servlet/errorhandler/`
      * 至 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**不要** 變更 `/libs` 路徑。
>
>原因是因為的內容 `/libs` 下次升級執行個體時會被覆寫（當您套用hotfix或feature pack時，很可能會被覆寫）。
>
>設定和其他變更：
>
>1. 複製專案於 `/libs` 至 `/apps`
>1. 進行任何變更 `/apps`

## 何時應使用JCR查詢以及何時不應使用 {#when-to-use-jcr-queries-and-when-not-to-use-them}

正確使用時，JCR查詢是功能強大的工具。 它們適用於：

* 真實的一般使用者查詢，例如對內容進行全文搜尋。
* 在整個存放庫中必須找到結構化內容的情況。

  在這種情況下，請確保僅在需要時執行查詢。 例如，在元件啟動或快取失效時（與例如工作流程步驟、觸發內容修改的事件處理常式及篩選器相反）。

請勿將JCR查詢用於純呈現請求。 例如，JCR查詢不適用於以下情況：

* 轉譯導覽
* 建立「前10大最新新聞專案」概觀
* 顯示內容專案計數

若要呈現內容，請使用內容樹狀結構的導覽存取權，而非執行JCR查詢。

>[!NOTE]
>
>如果您使用 [查詢產生器](/help/sites-developing/querybuilder-api.md)，您會使用JCR查詢，因為查詢產生器會在幕後產生JCR查詢。
>

## 安全性考量 {#security-considerations}

>[!NOTE]
>
>此外，也值得一提 [安全性檢查清單](/help/sites-administering/security-checklist.md).

### JCR （存放庫）工作階段 {#jcr-repository-sessions}

使用使用者工作階段，而不是管理工作階段。 這表示您應該使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect避免跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁。 惡意的Web使用者可能會利用這個安全性弱點來略過存取控制。

AEM會套用輸出時篩選所有使用者提供內容的原則。 在開發和測試期間，防止XSS都被給予最高優先順序。

此外，Web應用程式防火牆，例如 [Apache適用的mod_security](https://modsecurity.org)，可提供部署環境安全性的可靠集中控制，並防止先前未偵測到的跨網站指令碼攻擊。

>[!CAUTION]
>
>隨AEM提供的範常式式碼本身可能無法抵禦這類攻擊，通常需要透過網頁應用程式防火牆進行請求篩選。

XSS API速查表包含您必須知道的資訊，才能使用XSS API並讓AEM應用程式更安全。 您可以在這裡下載：

XSSAPI速查表。

[取得檔案](assets/xss_cheat_sheet_2016.pdf)

### 保護機密資訊的通訊安全 {#securing-communication-for-confidential-information}

對於任何網際網路應用程式，在傳輸機密資訊時，請務必確認

* 流量會透過SSL受到保護
* 若適用的話，會使用HTTPPOST

這適用於系統機密資訊（如設定或管理存取權）和使用者機密資訊（如個人詳細資訊）

## 不同的開發任務 {#distinct-development-tasks}

### 自訂錯誤頁面 {#customizing-error-pages}

可針對AEM自訂錯誤頁面。 這是建議做法，讓執行個體不會顯示內部伺服器錯誤上的Sling追蹤。

另請參閱 [自訂錯誤處理常式顯示的錯誤頁面](/help/sites-developing/customizing-errorhandler-pages.md) 以取得完整詳細資訊。

### 在Java™程式中開啟檔案 {#open-files-in-the-java-process}

由於AEM可以存取許多檔案，因此建議將 [開啟Java™程式的檔案](/help/sites-deploying/configuring.md#open-files-in-the-java-process) 已針對AEM明確設定。

為了將這個問題降至最低，開發應確保在（有意義的）可能時，正確關閉任何開啟的檔案。
