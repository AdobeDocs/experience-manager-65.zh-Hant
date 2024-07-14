---
title: AEM - 使用 Commerce Integration Framework 進行商務整合常見問題集
description: AEM - 使用 Commerce Integration Framework 進行商務整合常見問題集
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 66%

---

# AEM - 使用 Commerce Integration Framework 進行商務整合常見問題集

## 1. CIF GraphQL是否僅用於商務，或可用於查詢在AEM JCR上編寫的內容？

Adobe 已採用 Adobe Commerce 的 GraphQL API 作為其所有商務相關資料的官方商務 API。因此，AEM 會使用 GraphQL 與 Adobe Commerce 以及透過 I/O 執行階段的任何商務引擎交換商務資料。此 GraphQL API 獨立於 AEM 的 GraphQL API 來存取內容片段。

## 2. 產品資產 (影像) 是否可以透過 Adobe Commerce 管理員從 AEM 儲存和參考？如何使用 Dynamic Media 中的資產？

無官方AEM Assets — 提供Adobe Commerce整合。 [市集](https://marketplace.magento.com/partner/bounteous_ecomm)上有可用的合作夥伴聯結器。

或者，作為因應措施，您可以在AEM Assets中儲存產品資產（影像），但您必須在Adobe Commerce中手動儲存資產URL。 Dynamic Media是AEM Assets的一部分，且運作方式相同。

## 3. 商務解決方案部署的位置重要嗎？(內部部署或在雲端中)

不重要，商務解決方案部署在哪裡都可以。無論部署模式為何，CIF和AEM店面都能運作。 但是，如果使用建議的 E2E 參考架構部署解決方案，則可以針對代表典型企業客戶概況的效能 KPI 執行 E2E 測試。此程式提供可作為基準的其他資訊。

## 4. 如何在 AEM 中建立目錄頁面或產品頁面？它們如何留存在 AEM 中？

目錄頁面和產品頁面是根據一般目錄和產品頁面範本，在 AEM 中動態建立和快取的。產品或目錄資料不會匯入和儲存在 AEM 中。

## 5. 當您在商務解決方案中更新產品資料時，會即時推送到 AEM 嗎？或者是採用批次處理？

搭配AEM使用的CIF附加元件可讓資料從商務解決方案依需求傳輸至AEM。 因此，當您的商務解決方案中有更新時，此工作流程不是即時推播或批次流程。

## 6. 具有 CIF 的 AEM 支援多大的目錄大小？

目錄大小支援取決於您必須考慮的一些其他方面。 您的目錄資料和頁面的快取比率是多少？您預計高峰時段有多少並行要求？您商務解決方案 API 的可擴充性如何？

## 7. PIM 如何在該框架中發揮作用？

PIM資料會透過GraphQL要求向AEM和使用者端公開。 Adobe的建議是將PIM與商務引擎(Adobe Commerce或其他)整合，以便之後可以從商務引擎擷取PIM資料。

## 8. 您是否也透過 Dispatcher 快取定價和其他資料？這是否會引發頻繁的快取失效挑戰？

價格或庫存等動態資料不會在 Dispatcher 上快取。動態資料是透過 GraphQL API 在用戶端直接使用 Web 元件擷取的。僅靜態資料 (例如產品或類別資料) 可在 Dispatcher 上快取。如果產品資料變更，則需要讓快取失效。

## 9. AEM Dispatcher 的快取失效如何與 AEM 和 Commerce 搭配使用？

Adobe 建議為 Dispatcher 上快取的頁面設定 TTL 型快取失效。若是價格或庫存等動態資訊，Adobe建議在使用者端轉譯日期。 如需TTL型快取失效的詳細資訊，請參閱[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html)

## 10. 對於使用 Commerce 跨 AEM 內容進行整合搜尋有什麼建議嗎？

提供了產品搜尋參考實施，但沒有與內容進行整合搜尋。此功能是特定於客戶的，且最好在特定專案層級上解決。

## 11.「搜尋」在 AEM 和使用 CIF 的商務上的運作方式為何？

CIF 可提供搜尋列和搜尋結果元件。搜尋列元件會將包含搜尋字詞的 GraphQL 要求傳送至商務解決方案，然後商務解決方案會傳回包含產品名稱、價格、SLUG 等的產品清單。然後，搜尋結果元件會將搜尋結果顯示在於 AEM 中所建立搜尋結果頁面的程式庫檢視中。搜尋支援基本的全文搜尋。使用SLUG/url鍵來建置PDP的參考。

## 12. 如何將產品資料用於 MSM 或翻譯？

產品資料已在 PIM 或 Adobe Commerce 中進行翻譯。AEM - Adobe Commerce整合支援連線至多個Adobe Commerce商店和商店檢視。 在 MSM 設定中，通常會將一個 AEM 網站連結到一個 Adobe Commerce 商店檢視。

## 13. 是否能夠使用商務文字來增強產品資料？如果是的話，會在哪裡進行？ 在 AEM 還是在商務解決方案中？

Adobe建議在AEM中管理與行銷相關的資料和內容。 使用內容片段透過附加屬性修飾商務解決方案中的產品資料，或為非結構化內容建立體驗片段，並將其連結到您的產品。

## 14.公司在整個簡報層使用AEM時，如何確保PCI相容性？

Adobe 建議使用抽象的付款方式。這麼做會讓瀏覽器使用者端與支付閘道提供者直接通訊，讓Adobe不會保留或傳遞持卡人日期，或商務解決方案。 此方法僅需要 3 級 PCI 合規性。然而，要完全符合 PCI 標準還需要考慮其他事項，例如員工如何與系統和資料互動。如需Adobe Commerce PCI法規遵循的詳細資訊，請參閱[PCI法規遵循](https://business.adobe.com/products/magento/pci-compliance.html)

## 15. 如果我使用 AEM 和 Adobe Commerce 雲端版本，此聯合解決方案是否符合 PCI 要求？

是的，可根據要求提供自我評估問卷 D 和合規性證明。

## 16. 如何申請 I/O 執行階段試用版授權？

您可以在「[這裡](https://adobeio.typeform.com/to/obqgRm)」申請使用 I/O 執行階段的試用版授權。
