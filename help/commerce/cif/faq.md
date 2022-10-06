---
title: AEM — 使用Commerce Integration Framework進行商務整合常見問題集
description: AEM — 使用Commerce Integration Framework進行商務整合常見問題集
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# AEM — 使用Commerce Integration Framework進行商務整合常見問題集

## 1. CIF GraphQL是否僅用於商務？還是可用於查詢AEM上創作的內容？ JCR?

Adobe已採用Adobe Commerce的GraphQL API作為其官方商務API，以用於所有商務相關資料。 因此，AEM使用GraphQL透過I/O Runtime與Adobe Commerce及任何商務引擎交換商務資料。 此GraphQL API獨立於AEM GraphQL API以存取內容片段。

## 2.產品資產（影像）是否可透過Adobe Commerce管理員從AEM儲存及參考？ 如何使用來自Dynamic Media的資產？

沒有官方的AEM Assets - Adobe Commerce整合可用。 上有一個合作夥伴連接器 [marketplace](https://marketplace.magento.com/bounteous-dam.html).

或者，您可以將產品資產（影像）儲存在AEM Assets中，但必須在Adobe Commerce中手動儲存資產URL。 Dynamic Media現在是AEM Assets的一部分，也會以同樣的方式運作。

## 3.商務解決方案的部署位置是否重要？ （內部或雲端）

不，您的商務解決方案部署位置並不重要。 CIF和AEM店面無論部署模式為何都能運作。 不過，如果解決方案與建議的E2E參考架構一起部署，則E2E測試可針對代表典型企業客戶設定檔的效能KPI執行。 這將提供可作為基準的其他資訊。

## 4.如何在AEM中建立目錄頁面或產品頁面？ 它們在AEM中如何持續？

目錄頁面和產品頁面會根據一般目錄和產品頁面範本，在AEM中建立並動態快取。 不會匯入或儲存任何產品或目錄資料至AEM。

## 5.當您更新商務解決方案中的產品資料時，是否為即時推送至AEM? 還是批處理？

與AEM搭配使用的CIF附加元件，可讓資料從商務解決方案隨選流向AEM。 因此，當您的商務解決方案中有更新時，這不是即時推送或批次程式。

## 6.AEM與CIF支援的目錄大小多大？

這取決於您需要考慮的其他幾個方面。 目錄資料和頁面的快取比率是多少？ 在尖峰時段，您預期會有多少個同時請求？ 您的商務解決方案的API有何可擴充性？

## 7. PIM在這個框架中如何發揮作用？

PIM資料會透過GraphQL請求公開給AEM和用戶端。 我們的建議是將PIM與商務引擎(Adobe Commerce或其他)整合，以便從商務引擎中檢索到PIM資料。

## 8.您是否也能透過Dispatcher快取定價和其他資料。 這是否會導致快取失效頻繁？

Dispatcher不會快取價格或庫存等動態資料。 動態資料會透過GraphQL API以Web元件直接擷取用戶端。 Dispatcher上只會快取靜態資料（例如產品或類別資料）。 如果產品資料變更，則需要失效快取。

## 9. AEM Dispatcher的快取失效如何與AEM和商務搭配運作？

建議針對Dispatcher上快取的頁面，設定TTL型快取失效。 如需價格或庫存等動態資訊，建議您呈現日期用戶端。 如需TTL型快取失效的詳細資訊，請參閱 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 10.是否建議使用Commerce在AEM內容間進行統一搜尋？

提供產品搜尋參考實作，但沒有內容的統一搜尋。 此功能通常非常針對客戶，而且在專案特定層級能更妥善地解決。

## 11. CIF如何搭配AEM和商務使用Search?

CIF提供搜尋列和搜尋結果元件。 搜尋列元件會傳送含有搜尋詞的GraphQL請求給商務解決方案，商務解決方案會傳回產品清單，其中包含產品名稱、價格、SLUG等。 然後，在AEM中建立的搜索結果頁面上，「搜索結果」元件將在庫視圖中顯示搜索結果。 「搜尋」支援基本全文搜尋。 我們使用SLUG/url索引鍵來建立PDP的參考。

## 12.如何在MSM或翻譯中使用產品資料？

產品資料通常已在PIM或Adobe Commerce中轉譯。 AEM - Adobe Commerce整合支援連線至多個Adobe Commerce商店和商店檢視。 在MSM設定中，通常會將一個AEM網站連結至一個Adobe Commerce商店檢視。

## 13.是否可以用商業文本增強產品資料？ 你在哪做的？ 在AEM或商務解決方案中？

建議您在AEM中管理行銷相關資料和內容。 使用內容片段使用其他屬性，或建立及連結非結構化內容的體驗片段與產品，以從您的商務解決方案裝飾產品資料。

## 14.在整個演示層使用AEM時，如何確保PCI符合性？

我們建議使用抽象的支付方法。 這使得瀏覽器客戶端與支付網關提供商直接通信，使得Adobe或商務解決方案均不保存或傳遞持卡人資料。 此方法僅需要3級PCI合規性。 但是，還有其他事項需要考慮完全符合PCI要求，例如員工與系統和資料的交互方式。 有關Adobe Commerce PCI合規性的詳細資訊，請參閱 [PCI合規性](https://business.adobe.com/products/magento/pci-compliance.html)

## 15.如果我使用AEM和Adobe Commerce雲版本，此聯合解決方案是否符合PCI標準？

是的，可應要求提供自我評估調查表D和合規性證明。

## 16.如何申請I/O運行時試用許可證？

您可以申請試用許可以使用I/O Runtime [此處](https://adobeio.typeform.com/to/obqgRm).
