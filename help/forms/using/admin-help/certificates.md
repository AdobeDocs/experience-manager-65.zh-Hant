---
title: 管理憑證
seo-title: 管理憑證
description: 瞭解如何匯入和匯出憑證，以及編輯其信任設定。
seo-description: 瞭解如何匯入和匯出憑證，以及編輯其信任設定。
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# 管理證書{#managing-certificates}

使用信任商店管理，您可以匯入、編輯和刪除您信任伺服器的憑證，以驗證數位簽章和憑證驗證。 您可以匯入和匯出任意數量的憑證。 在匯入憑證後，您可以編輯信任設定和信任商店類型。 組合信任存放區類型時，請考慮下列選項：

* **使用CA信任證書驗證：對於** CRL驗證，也選擇信任身份。
* **使用ICA信任認證：僅選** 擇信任身份。ICA不應受信任以進行認證驗證。 如果您信任ICA進行認證驗證，ICA就會成為建立路徑的CA。 如果ICA同時受信任於「認證驗證」和「身分」，則會忽略CA廠商憑證，因為ICA會變成CA。
* **使用HTTP信任OCSP伺服器：如** 果OSCP回應伺服器位於HTTP位置，則還必須選擇「信任SSL連接」。如果OSCP回應者需要CRL驗證，請確定您也選取「信任身分」。
* **Adobe Root：不** 要選取「SSL連線」或「OCSP伺服器信任商店類型」。SSL連線和OCSP伺服器不信任Adobe Root。 Adobe不會核發OCSP和SSL憑證。 Adobe Root是含有別名=&quot;ADOBEROOT&quot;的隱式信任。

僅支援X509v3憑證。 此憑證類型可以以二進位DER編碼檔案（.cer檔案）或包含相同DER編碼憑證(包括隱私權增強郵件(PEM)格式的X509憑證)之Base64編碼版本的文字檔案提供。

完成簽名驗證所需的憑證必須位於同一商店（HSM或資料庫）。

您也可以使用信任管理員API匯入和刪除憑證。 如需詳細資訊，請參閱「使用AEM表單進行程式設計」中的「使用信任管理員API匯入憑證」和「使用信任管理員API刪除憑證」。[](https://www.adobe.com/go/learn_aemforms_programming_63)

## 匯入憑證{#import-a-certificate}

1. 在管理控制台中，按一下「設定>信任商店管理>憑證&#x200B;**[!UICONTROL 」。]**
1. 按一下「匯入」，然後在「信任商店類型」下方，選取下列其中一個選項：

   * **信任SSL連線：指** 定AEM表單可使用憑證透過SSL連線至外部系統。
   * **信任認證簽名：指** 定憑證在檔案簽署作業中受信任，以認證作者數位簽名。
   * **信任簽名：指** 定非作者數位簽名的檔案簽署作業中信任憑證。
   * **認證驗證的信任：指** 定AEM表單使用憑證來驗證使用認證或智慧卡驗證的使用者。
   * **信任OCSP伺服器：指** 定AEM表單可以使用憑證連線至外部OCSP回應器
   * **信任身分：指** 定可使用憑證來信任上述指定類型以外的資訊。

   >[!NOTE]
   >
   >信任存放區會隱式信任Adobe根憑證，以取得憑證驗證、簽名、認證簽名和身分。

1. 在「別名」框中，鍵入證書的標識符。
1. 按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;找到證書，然後按一下&#x200B;**[!UICONTROL 確定]**。

## 匯出憑證{#export-a-certificate}

1. 在管理控制台中，按一下「設定>信任商店管理>憑證&#x200B;**[!UICONTROL 」。]**
1. 按一下要導出的證書的別名。 此時將顯示&#x200B;**[!UICONTROL 證書詳細資訊]**&#x200B;頁。
1. 按一下&#x200B;**[!UICONTROL 導出]** ，按照指示導出證書，然後按一下&#x200B;**[!UICONTROL 確定]**。

## 編輯憑證的信任設定和信任存放區類型{#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制台中，按一下「設定>信任商店管理>憑證&#x200B;**[!UICONTROL 」。]**
1. 按一下要編輯的證書的別名。
1. 按一下&#x200B;**[!UICONTROL 更新證書]**。
1. 要更改證書的別名，請在「別名」框中鍵入新名稱。
1. 要更新證書的信任儲存類型，請選擇適當的信任儲存類型。
1. 要更新策略限制，請在「證書策略」框中鍵入策略資訊，然後按一下&#x200B;**[!UICONTROL 確定]**。

## 刪除證書{#delete-a-certificate}

1. 在管理控制台中，按一下「設定>信任商店管理>憑證&#x200B;**[!UICONTROL 」。]**
1. 選擇要刪除證書的複選框，按一下&#x200B;**[!UICONTROL Delete]** ，然後按一下&#x200B;**[!UICONTROL OK]**。

