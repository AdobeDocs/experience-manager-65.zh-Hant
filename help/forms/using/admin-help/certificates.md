---
title: 管理憑證
seo-title: Managing certificates
description: 了解如何匯入和匯出憑證，以及編輯其信任設定。
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# 管理憑證 {#managing-certificates}

使用「信任儲存管理」，您可以導入、編輯和刪除您在伺服器上信任的證書，以驗證數字簽名和證書驗證。 您可以匯入和匯出任何數量的憑證。 匯入憑證後，您可以編輯信任設定和信任存放區類型。 合併信任儲存類型時，請考慮下列選項：

* **CA信任證書身份驗證：** 要進行CRL驗證，還請選擇「身份信任」。
* **信任ICA證書驗證：** 僅選擇「Trust for Identity（信任）」。 不應信任ICA進行證書身份驗證。 如果您信任ICA以進行憑證驗證，則ICA會變成CA以建立路徑。 如果ICA在「證書驗證」和「標識」中都受信任，則CA供應商證書將被忽略，因為ICA將成為CA。
* **信任OCSP伺服器（帶HTTP）:** 如果OSCP回應者伺服器位於HTTP位置，您也必須選取信任SSL連線。 如果OSCP響應者需要CRL驗證，請確保您也選擇「身份信任」。
* **Adobe根：** 請勿選擇SSL連接或OCSP伺服器信任儲存類型。 Adobe根不受信任用於SSL連接和OCSP伺服器。 Adobe不會核發OCSP和SSL憑證。 Adobe根以別名=&quot;ADOBEROOT&quot;隱式信任。

僅支援X509v3憑證。 此憑證類型可以以二進位DER編碼檔案（.cer檔案）或包含相同DER編碼憑證(包括隱私權增強郵件(PEM)格式的Base64編碼版本的文字檔案提供。

完成簽名驗證所需的證書必須位於同一儲存（HSM或資料庫）中。

您也可以使用信任管理器API匯入和刪除憑證。 如需詳細資訊，請參閱以下主題中的「使用信任管理器API匯入憑證」和「使用信任管理器API刪除憑證」： [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).

## 匯入憑證 {#import-a-certificate}

1. 在管理控制台中，按一下 **[!UICONTROL 「設定」>「信任儲存管理」>「證書」]**.
1. 按一下「導入」，然後在「信任儲存類型」下，選擇以下選項之一：

   * **信任SSL連接：** 指定AEM表單可使用憑證透過SSL連線至外部系統。
   * **認證簽名信任：** 指定在用於驗證作者數字簽名的文檔簽名操作中信任證書。
   * **信任簽名：** 指定在非作者數位簽名的文檔簽名操作中信任證書。
   * **信任證書驗證：** 指定AEM表單使用憑證來使用憑證或智慧卡驗證來驗證使用者。
   * **信任OCSP伺服器：** 指定AEM表單可使用憑證連線至外部OCSP回應器
   * **對身份的信任：** 指定可以使用證書來信任上述指定類型以外的資訊。

   >[!NOTE]
   >
   >信任儲存器隱式信任Adobe根證書，以用於證書驗證、簽名、認證簽名和身份。

1. 在「別名」框中，鍵入證書的標識符。
1. 按一下 **[!UICONTROL 瀏覽]** 若要找到憑證，然後按一下 **[!UICONTROL 確定]**.

## 匯出憑證 {#export-a-certificate}

1. 在管理控制台中，按一下 **[!UICONTROL 「設定」>「信任儲存管理」>「證書」]**.
1. 按一下要匯出之憑證的別名。 此 **[!UICONTROL 證書詳細資訊]** 頁面。
1. 按一下 **[!UICONTROL 匯出]**，請依照匯出憑證的指示，然後按一下 **[!UICONTROL 確定]**.

## 編輯證書的信任設定和信任儲存類型 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制台中，按一下 **[!UICONTROL 「設定」>「信任儲存管理」>「證書」]**.
1. 按一下要編輯的證書的別名。
1. 按一下 **[!UICONTROL 更新證書]**.
1. 要更改證書的別名，請在「別名」框中鍵入新名稱。
1. 要更新證書的信任儲存類型，請選擇相應的信任儲存類型。
1. 要更新策略限制，請在「證書策略」框中鍵入策略資訊，然後按一下 **[!UICONTROL 確定]**.

## 刪除憑證 {#delete-a-certificate}

1. 在管理控制台中，按一下 **[!UICONTROL 「設定」>「信任儲存管理」>「證書」]**.
1. 選取要刪除的憑證核取方塊，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 確定]**.
