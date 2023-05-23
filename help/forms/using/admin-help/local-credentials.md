---
title: 管理本地憑據
seo-title: Managing local credentials
description: 瞭解如何管理本地憑據。
seo-description: Learn how to manage local credentials.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 管理本地憑據 {#managing-local-credentials}

本地憑據是托管儲存管理中的私鑰憑據。 A *本地憑證* 標識用戶的DES憑據的儲存位置。 使用信任儲存管理，可以通過使用（例如）現有PFX檔案來導入和管理本地憑據，以便導入、編輯和刪除本地憑據。

表AEM單支援標準PKCS12格式（.pfx和.p12檔案）中高達4096位的RSA和DSA憑據。

您可以導入和導出任意數量的憑據。 如果要使用相同的別名替換過期的憑據，請刪除該憑據，然後使用相同的別名導入新憑據。

有關Acrobat Reader DC擴展的資訊和說明，請參見 [配置用於Acrobat Reader DC擴展的憑據](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。

## 導入憑據 {#import-a-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 按一下「導入」。 在信任儲存類型下，選擇以下選項之一：

   * **文檔簽名憑據：** 用於在文檔上發出數字簽名的憑據。
   * **Acrobat Reader DC擴展憑據：** 特定於Acrobat Reader DC擴展的數字證書，使Adobe Reader的使用權能夠在生成的PDF檔案中激活。
   * **預設值：** 指示這是用於Acrobat Reader DC擴展的預設憑據。

   有關獲取憑據的資訊，請參見 [準備安裝表AEM單](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

1. 在「別名」框中，鍵入憑據的標識符。 此標識符用作Acrobat Reader DC擴展和簽名服務中憑據的顯示名稱。 此別名還用於使用表單SDK以寫程式方式訪AEM問憑據。

   >[!NOTE]
   >
   >別名將自動轉換為大寫，以便顯示。 在進程中引用別名時，別名不區分大小寫。

1. 按一下「瀏覽」查找憑據，鍵入憑據的密碼，然後按一下「確定」。

   如果出現錯誤消息「由於檔案格式不正確或密碼不正確而導入憑據失敗」，請驗證密碼是否有效。

## 導出憑據 {#export-a-credential}

憑據以PKCS#12格式導出為P12檔案。

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 按一下要導出的憑據的別名，然後按一下導出。
1. 在「密碼」框中，鍵入密碼。 此密碼是新密碼，用於加密導出的憑據。
1. 按一下「導出」，按照說明導出憑據，然後按一下「確定」。

## 編輯憑據的別名或信任儲存類型 {#edit-a-credential-s-alias-or-trust-store-type}

導入憑據後，可以編輯其別名和信任儲存類型。

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 按一下要編輯的憑據的別名。
1. 按一下「更新憑據」。
1. 根據需要編輯別名和信任儲存類型，然後按一下確定。

## 刪除憑據 {#delete-a-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 選中要刪除的憑據的複選框。
1. 按一下「刪除」，然後按一下「確定」。
