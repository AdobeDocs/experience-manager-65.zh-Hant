---
title: 管理證書
seo-title: Managing certificates
description: 瞭解如何導入和導出證書以及編輯其信任設定。
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

# 管理證書 {#managing-certificates}

使用信任儲存管理，您可以導入、編輯和刪除在伺服器上信任的證書，以驗證數字簽名和證書身份驗證。 您可以導入和導出任意數量的證書。 導入證書後，可以編輯信任設定和信任儲存類型。 組合信任儲存類型時請考慮以下選項：

* **使用CA進行證書身份驗證的信任：** 對於CRL驗證，也選擇「信任」以識別。
* **使用ICA進行證書身份驗證的信任：** 僅選擇「信任」以識別。 不應信任ICA進行證書身份驗證。 如果信任ICA進行證書驗證，則ICA將成為路徑生成的CA。 如果ICA在證書身份驗證和身份上都受信任，則CA供應商證書將被忽略，因為ICA將成為CA。
* **對具有HTTP的OCSP伺服器的信任：** 如果OSCP應答伺服器駐留在HTTPs位置，則還必須選擇「信任SSL連接」。 如果OSCP應答者需要CRL驗證，請確保您還選擇「信任身份」。
* **Adobe根：** 不要選擇SSL連接或OCSP伺服器信任儲存類型。 Adobe根不受SSL連接和OCSP伺服器的信任。 Adobe不頒發OCSP和SSL證書。 Adobe根被隱式信任，別名為=&quot;ADOBEROOT&quot;。

僅支援X509v3證書。 此證書類型可以以二進位DER編碼檔案（.cer檔案）或文本檔案提供，該文本檔案包含相同DER編碼證書(包括以隱私增強郵件(PEM)格式的X509證書)的Base64編碼版本。

完成簽名驗證所需的證書必須位於同一儲存（HSM或資料庫）中。

您還可以使用信任管理器API導入和刪除證書。 有關詳細資訊，請參閱中的「使用信任管理器API導入證書」和「使用信任管理器API刪除證書」 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63)。

## 導入證書 {#import-a-certificate}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>信任儲存管理>證書]**。
1. 按一下導入，然後在信任儲存類型下選擇以下選項之一：

   * **信任SSL連接：** 指定表AEM單可以使用證書通過SSL連接到外部系統。
   * **信任認證簽名：** 指定證書在文檔簽名操作中受信任，用於驗證作者數字簽名。
   * **簽名信任：** 指定證書在非作者數字簽名的文檔簽名操作中受信任。
   * **證書身份驗證信任：** 指定AEM表單使用證書來使用證書或智慧卡身份驗證驗證用戶。
   * **OCSP伺服器信任：** 指定表AEM單可以使用證書連接到外部OCSP響應器
   * **身份信任：** 指定證書可用於信任除上述指定類型之外的其他資訊。

   >[!NOTE]
   >
   >信任儲存隱式信任Adobe根證書以進行證書驗證、簽名、認證簽名和身份。

1. 在「別名」框中，鍵入證書的標識符。
1. 按一下 **[!UICONTROL 瀏覽]** 查找證書，然後按一下 **[!UICONTROL 確定]**。

## 導出證書 {#export-a-certificate}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>信任儲存管理>證書]**。
1. 按一下要導出的證書的別名。 的 **[!UICONTROL 證書詳細資訊]** 的上界。
1. 按一下 **[!UICONTROL 導出]**，請按照導出證書的說明，然後按一下 **[!UICONTROL 確定]**。

## 編輯證書的信任設定和信任儲存類型 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>信任儲存管理>證書]**。
1. 按一下要編輯的證書的別名。
1. 按一下 **[!UICONTROL 更新證書]**。
1. 要更改證書的別名，請在「別名」框中鍵入新名稱。
1. 要更新證書的信任儲存類型，請選擇相應的信任儲存類型。
1. 要更新策略限制，請在「證書策略」框中鍵入策略資訊，然後按一下 **[!UICONTROL 確定]**。

## 刪除證書 {#delete-a-certificate}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>信任儲存管理>證書]**。
1. 選中要刪除的證書的複選框，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 確定]**。
