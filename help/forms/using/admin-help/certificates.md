---
title: 管理憑證
seo-title: 管理憑證
description: 了解如何匯入和匯出憑證，以及編輯其信任設定。
seo-description: 了解如何匯入和匯出憑證，以及編輯其信任設定。
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 管理證書{#managing-certificates}

使用「信任儲存管理」，您可以導入、編輯和刪除您在伺服器上信任的證書，以驗證數字簽名和證書驗證。 您可以匯入和匯出任何數量的憑證。 匯入憑證後，您可以編輯信任設定和信任存放區類型。 合併信任儲存類型時，請考慮下列選項：

* **使用CA進行證書驗證信任：** 對於CRL驗證，也選擇「對身份的信任」。
* **使用ICA進行憑證驗證信任：** 僅選取以身分驗證信任。不應信任ICA進行證書身份驗證。 如果您信任ICA以進行憑證驗證，則ICA會變成CA以建立路徑。 如果ICA在「證書驗證」和「標識」中都受信任，則CA供應商證書將被忽略，因為ICA將成為CA。
* **使用HTTP信任OCSP伺服器：** 如果OSCP回應者伺服器位於HTTP位置，您也必須選取SSL連線信任。如果OSCP響應者需要CRL驗證，請確保您也選擇「身份信任」。
* **Adobe根：** 請勿選取SSL連線或OCSP伺服器信任存放區類型。Adobe根不受信任用於SSL連接和OCSP伺服器。 Adobe不會核發OCSP和SSL憑證。 Adobe根以別名=&quot;ADOBEROOT&quot;隱式信任。

僅支援X509v3憑證。 此憑證類型可以以二進位DER編碼檔案（.cer檔案）或包含相同DER編碼憑證(包括隱私權增強郵件(PEM)格式的Base64編碼版本的文字檔案提供。

完成簽名驗證所需的證書必須位於同一儲存（HSM或資料庫）中。

您也可以使用信任管理器API匯入和刪除憑證。 如需詳細資訊，請參閱[使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63)中的「使用信任管理器API匯入憑證」和「使用信任管理器API刪除憑證」。

## 導入證書{#import-a-certificate}

1. 在管理控制台中，按一下「**[!UICONTROL 設定>信任儲存管理>證書]**」。
1. 按一下「導入」，然後在「信任儲存類型」下，選擇以下選項之一：

   * **信任SSL連線：** 指定AEM表單可使用憑證透過SSL連線至外部系統。
   * **認證簽名信任：** 指定證書在用於認證作者數字簽名的文檔簽名操作中受信任。
   * **信任簽名：** 指定在非作者數位簽名的文檔簽名操作中信任證書。
   * **憑證驗證信任：** 指定AEM表單使用憑證，以使用憑證或智慧卡驗證來驗證使用者。
   * **信任OCSP伺服器：** 指定AEM表單可使用憑證連線至外部OCSP回應器
   * **身分信任：** 指定除了上述指定的類型外，可使用憑證來信任資訊。

   >[!NOTE]
   >
   >信任儲存器隱式信任Adobe根證書，以用於證書驗證、簽名、認證簽名和身份。

1. 在「別名」框中，鍵入證書的標識符。
1. 按一下&#x200B;**[!UICONTROL Browse]**&#x200B;以找到憑證，然後按一下&#x200B;**[!UICONTROL OK]**。

## 導出證書{#export-a-certificate}

1. 在管理控制台中，按一下「**[!UICONTROL 設定>信任儲存管理>證書]**」。
1. 按一下要匯出之憑證的別名。 此時將顯示&#x200B;**[!UICONTROL 證書詳細資訊]**&#x200B;頁。
1. 按一下&#x200B;**[!UICONTROL Export]**，按照指示導出證書，然後按一下&#x200B;**[!UICONTROL OK]**。

## 編輯證書的信任設定和信任儲存類型{#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制台中，按一下「**[!UICONTROL 設定>信任儲存管理>證書]**」。
1. 按一下要編輯的證書的別名。
1. 按一下&#x200B;**[!UICONTROL 更新證書]**。
1. 要更改證書的別名，請在「別名」框中鍵入新名稱。
1. 要更新證書的信任儲存類型，請選擇相應的信任儲存類型。
1. 要更新策略限制，請在「證書策略」框中鍵入策略資訊，然後按一下&#x200B;**[!UICONTROL OK]**。

## 刪除證書{#delete-a-certificate}

1. 在管理控制台中，按一下「**[!UICONTROL 設定>信任儲存管理>證書]**」。
1. 選擇要刪除的證書的複選框，按一下&#x200B;**[!UICONTROL Delete]**，然後按一下&#x200B;**[!UICONTROL OK]**。
