---
title: 管理本機憑證
seo-title: Managing local credentials
description: 了解如何管理本機憑證。
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

# 管理本機憑證 {#managing-local-credentials}

本地憑證是托管於「信任儲存管理」的私密金鑰憑證。 A *本地憑據* 標識用戶的DES憑據的儲存位置。 使用「信任儲存管理」，您可以使用（例如）現有的PFX檔案導入和管理本地憑據，以便導入、編輯和刪除本地憑據。

AEM forms支援標準PKCS12格式（.pfx和.p12檔案）中高達4096位元的RSA和DSA憑證。

您可以匯入和匯出任何數量的憑證。 如果要使用相同的別名替換過期的憑據，請刪除憑據，然後使用相同的別名導入新憑據。

如需Acrobat Reader DC擴充功能的相關資訊和指示，請參閱 [設定憑證以與Acrobat Reader DC擴充功能搭配使用](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## 導入憑據 {#import-a-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本機憑證」。
1. 按一下「匯入」。 在「信任儲存類型」下，選擇以下選項之一：

   * **文檔簽名憑據：** 用於在文檔上發出數字簽名的憑據。
   * **Acrobat Reader DC擴充功能憑證：** 專屬於Acrobat Reader DC擴充功能的數位憑證，可讓Adobe Reader使用權限在產生的PDF檔案中啟動。
   * **預設值：** 指出這是與Acrobat Reader DC擴充功能搭配使用的預設憑證。

   有關獲取憑據的資訊，請參見 [準備安裝AEM表單](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. 在「別名」框中，鍵入憑據的標識符。 此識別碼會用作Acrobat Reader DC擴充功能和簽名服務中憑證的顯示名稱。 此別名也可用來使用AEM Forms SDK以程式設計方式存取憑證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫，以便顯示。 在程式中參照別名時，別名不區分大小寫。

1. 按一下「瀏覽」以查找憑據，鍵入憑據的密碼，然後按一下「確定」。

   如果出現「由於檔案格式不正確或密碼錯誤而導致無法導入憑據」錯誤消息，請驗證密碼是否有效。

## 導出憑據 {#export-a-credential}

憑據以PKCS#12格式導出為P12檔案。

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本機憑證」。
1. 按一下要導出的憑據的別名，然後按一下「導出」。
1. 在「密碼」框中，鍵入密碼。 此密碼是新密碼，用於加密導出的憑據。
1. 按一下「導出」(Export)，按照指示導出憑據，然後按一下「確定」(OK)。

## 編輯憑據的別名或信任儲存類型 {#edit-a-credential-s-alias-or-trust-store-type}

導入憑據後，可以編輯其別名和信任儲存類型。

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本機憑證」。
1. 按一下要編輯的憑據的別名。
1. 按一下「更新憑據」。
1. 根據需要編輯別名和信任儲存類型，然後按一下「確定」。

## 刪除憑據 {#delete-a-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本機憑證」。
1. 選擇要刪除的憑據的複選框。
1. 按一下「刪除」，然後按一下「確定」。
