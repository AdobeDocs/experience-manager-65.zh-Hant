---
title: 管理本機憑證
seo-title: 管理本機憑證
description: 瞭解如何管理本機認證。
seo-description: 瞭解如何管理本機認證。
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理本機憑證 {#managing-local-credentials}

本機憑證是托管於信任商店管理中的私密金鑰憑證。 本 *機憑證* ，可識別使用者的DES憑證儲存位置。 使用信任商店管理，您可以使用（例如）現有的PFX檔案來匯入及管理您的本機憑證，以便您匯入、編輯和刪除本機憑證。

AEM表單支援RSA和DSA憑證，最多4096位元的標準PKCS12格式（.pfx和。p12檔案）。

您可以匯入和匯出任意數量的憑證。 如果要使用相同的別名替換過期的憑據，請刪除憑據，然後使用相同的別名導入新憑據。

如需有關Acrobat Reader DC擴充功能的資訊和指示，請參 [閱設定認證以搭配Acrobat Reader DC擴充功能使用](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。

## 導入憑據 {#import-a-credential}

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 按一下「匯入」。 在「信任商店類型」下，選取下列其中一個選項：

   * **** 檔案簽署憑證：用於在檔案上發行數位簽名的憑證。
   * **** Acrobat Reader DC擴充功能憑證：Acrobat Reader DC擴充功能專用的數位憑證，可讓Adobe Reader使用權限在產生的PDF檔案中啟動。
   * **** 預設值：指出這是與Acrobat Reader DC擴充功能搭配使用的預設憑證。
   如需有關取得憑證的詳細資訊，請參 [閱「準備安裝AEM表單」](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

1. 在「別名」框中，鍵入憑據的標識符。 此識別碼會用作Acrobat Reader DC擴充功能和簽名服務中憑證的顯示名稱。 此別名也可用來使用AEM表單SDK以程式設計方式存取憑證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫，以便顯示。 在進程中引用別名時，別名不區分大小寫。

1. 按一下瀏覽以查找憑據，鍵入憑據的密碼，然後按一下確定。

   如果出現錯誤消息「由於檔案格式錯誤或密碼錯誤而導入憑據失敗」，請驗證密碼是否有效。

## 匯出憑證 {#export-a-credential}

憑據將導出為PKCS#12格式的P12檔案。

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 按一下要導出的憑據的別名，然後按一下導出。
1. 在「密碼」框中，鍵入密碼。 此密碼是新密碼，用於加密導出的憑據。
1. 按一下「導出」(Export)，按照指示導出憑據，然後按一下「確定」(OK)。

## 編輯憑證的別名或信任存放區類型 {#edit-a-credential-s-alias-or-trust-store-type}

導入憑據後，您可以編輯其別名和信任儲存類型。

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 按一下要編輯的憑據的別名。
1. 按一下「更新憑證」。
1. 根據需要編輯別名和信任儲存類型，然後按一下確定。

## 刪除憑證 {#delete-a-credential}

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 選中要刪除的憑據的複選框。
1. 按一下「刪除」，然後按一下「確定」。

