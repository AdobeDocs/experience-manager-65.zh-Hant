---
title: ' — 使用AEMCommerce Integration Framework進行Commerce Integration常見問題'
description: ' — 使用AEMCommerce Integration Framework進行Commerce Integration常見問題'
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

#  — 使用AEMCommerce Integration Framework進行Commerce Integration常見問題

## 1。CIF GraphQL是否僅用於商業，或者它是否可用於查詢在上創作的AEM內容？ JCR?

Adobe已採用Adobe Commerce的GraphQL APIs作為所有商業相關資料的官方商業API。 因此，AEM使用GraphQL通過I/O Runtime與Adobe Commerce和任何商務引擎交換商務資料。 此GraphQL API獨立於AEMGraphQL API以訪問內容片段。

## 2.產品資產（映像）是否可以通過Adobe Commerce管理員AEM進行儲存和引用？ 如何消費Dynamic Media的資產？

目前沒有正式的AEM Assets-Adobe Commerce一體化。 上有一個夥伴連接器 [市場](https://marketplace.magento.com/bounteous-dam.html)。

或者作為一種變通辦法，您可以在AEM Assets儲存產品資產（影像），但必須在Adobe Commerce手動儲存資產URL。 Dynamic Media現在是AEM Assets的一部分，也將採取同樣的方式。

## 3.在何處部署商務解決方案是否重要？ （在雲中或在雲中）

不，無論您的商業解決方案部署在何處。 CIF和店AEM面無論部署模式如何都能工作。 但是，如果解決方案與推薦的E2E參考體系結構一起部署，則E2Etest可以針對代表典型企業客戶配置的效能KPI運行。 這將提供可作為基準的其他資訊。

## 4.如何在中建立目錄頁或產品頁AEM? 他們如何堅持AEM?

目錄頁和產品頁基於通用目錄和產AEM品頁模板動態建立和快取。 未導入和儲存任何產品或目錄數AEM據。

## 5.當您在您的商業解決方案中更新產品資料時，這是否是即時推AEM動？ 還是批處理？

與一起使用的CIF附加AEM項使資料能夠從商業解決方案流AEM入按需。 因此，當您的商業解決方案中存在更新時，這不是即時推送或批處理。

## 6。CIF支援使目AEM錄大小是多少？

這取決於您需要考慮的其他方面。 目錄資料和頁的快取比率是多少？ 在高峰時段，您預期有多少個併發請求？ 您的商業解決方案的API的可擴充性如何？

## 7。PIM如何在此框架中發揮作用？

PIM資料通過GraphQL請AEM求暴露給客戶端。 我們的建議是將PIM與商業引擎(Adobe Commerce或其他)整合，這樣PIM資料就可以從商業引擎中檢索出來。

## 8.是否還通過Dispatcher快取定價和其他資料。 這是否會帶來頻繁的快取失效挑戰？

動態資料（如價格或庫存）不快取在Dispatcher上。 通過GraphQL API直接使用Web元件獲取動態資料。 僅靜態資料（如產品或類別資料）會快取在Dispatcher上。 如果產品資料發生更改，則需要快取失效。

## 9。Dispatcher的快取失效與AEM商業如何AEM協作？

我們建議為Dispatcher上快取的頁設定基於TTL的快取無效。 對於價格或庫存等動態資訊，我們建議呈現日期客戶端。 有關基於TTL的快取無效的詳細資訊，請參閱 [調度AEM程式](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 10.是否建議使用Commerce跨內容AEM進行統一搜索？

提供了一種產品搜索參考實現，但沒有與內容進行統一搜索。 此功能通常是非常特定於客戶的，並且在項目特定級別上能更好地解決。

## 11.使用CIF搜索與AEM商業如何協作？

CIF提供搜索欄和搜索結果元件。 搜索欄元件將帶有搜索項的GraphQL請求發送到商業解決方案，然後商業解決方案返回包括產品名稱、價格、SLUG等的產品清單。 然後，「搜索結果」元件將搜索結果顯示在中建立的搜索結果頁面的庫視圖中AEM。 「搜索」支援基本全文搜索。 我們使用SLUG/url鍵構建對PDP的引用。

## 12.如何在MSM或翻譯中使用產品資料？

產品資料通常已在PIM或Adobe Commerce中翻譯。 - AEMAdobe Commerce整合支援與多個Adobe Commerce商店和商店視圖的連接。 在MSM設定中，通常一AEM個站點連結到一個Adobe Commerce商店視圖。

## 13.是否有一種方法通過商業文本增強產品資料？ 你在哪做的？ 在商AEM業解決方案中？

我們建議管理中與市場營銷相關的資料和AEM內容。 使用使用內容片段的其他屬性來裝飾您的商業解決方案中的產品資料，或建立並連結非結構化內容的體驗片段與您的產品。

## 14.在整個演示層使用時，我們如AEM何確保PCI合規性？

我們建議使用抽象的支付方式。 這使瀏覽器客戶端與支付網關提供商直接通信，從而Adobe或商業解決方案都不保存或傳遞持卡人資料。 此方法只需要3級PCI合規性。 但是，還有其他需要考慮的完全符合PCI的條件，例如員工如何與系統和資料交互。 有關Adobe CommercePCI合規性的詳細資訊，請參閱 [PCI合規性](https://business.adobe.com/products/magento/pci-compliance.html)

## 15.如果我使用和AEMAdobe Commerce雲版本，此聯合解決方案是否符合PCI標準？

是，自我評估調查表D和合規性證明可應要求提供。

## 16.如何請求I/O運行時試用許可證？

您可以請求試用許可證以使用I/O運行時 [這裡](https://adobeio.typeform.com/to/obqgRm)。
