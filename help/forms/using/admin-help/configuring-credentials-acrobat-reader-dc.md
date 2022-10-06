---
title: 設定憑證以與Acrobat Reader DC擴充功能搭配使用
seo-title: Configuring credentials for use with Acrobat Reader DC extensions
description: 了解如何設定憑證以搭配Acrobat Reader DC擴充功能使用。
seo-description: Learn how to configure credentials for use with Acrobat Reader DC extensions.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# 設定憑證以與Acrobat Reader DC擴充功能搭配使用{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

若要將使用權套用至PDF檔案，請使用Acrobat Reader DC擴充功能的有效憑證設定AEM表單。 在安裝AEM表單期間，可能已設定憑證。 如果您在執行Configuration Manager時未設定Acrobat Reader DC擴充功能憑證，或需要匯入新憑證或取代憑證，則可使用「信任存放區管理」頁面進行設定。

如果您正在使用評估憑據，請在遷移到生產環境時用生產憑據替換它。 若要更新過期或評估憑證，請先刪除舊的Acrobat Reader DC擴充功能憑證。

有關獲取憑據的資訊，請參見 [準備安裝AEM表單（單一伺服器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

信任存放區可包含多個Acrobat Reader DC擴充功能憑證。 您必須指定其中一個憑據作為預設Reader擴展憑據。 當Workbench使用者無法判斷在建立程式期間要使用的憑證時，會使用預設憑證。 這些規則適用於預設憑證：

* 如果您匯入Acrobat Reader DC擴充功能憑證，且信任存放區不包含其他Acrobat Reader DC擴充功能憑證，則會將其設為預設。
* 如果導入了「預設」選項的Acrobat Reader DC擴展憑據，則預設類型將從現有預設憑據中刪除。 導入的憑據成為預設憑據。
* 您無法刪除預設的Acrobat Reader DC擴充功能憑證。 要刪除預設憑據，請首先將另一個憑據設定為預設憑據。 此規則的一個例外是，如果只有一個憑據，則即使是預設憑證，您仍可將其刪除。
* 您無法更新預設的Acrobat Reader DC擴充功能憑證。

>[!NOTE]
>
>您也可以以程式設計方式匯入和刪除憑證。 (請參閱 [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).)

## 匯入Acrobat Reader DC擴充功能憑證 {#import-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定>信任儲存管理>本機憑證」。
1. 按一下「匯入」 ，然後在「信任存放區類型」下方選取「Acrobat Reader DC擴充功能憑證」。
1. （可選）若要指出此憑證是搭配Acrobat Reader DC擴充功能使用的預設憑證，請選取「預設」。
1. 在「別名」框中，鍵入憑據的標識符。 此識別碼會作為Acrobat Reader DC擴充功能中憑證的顯示名稱。 此別名也可用來使用AEM Forms SDK以程式設計方式存取憑證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫，以便顯示。 在程式中參照別名時，別名不區分大小寫。

1. 按一下選擇檔案以查找憑據，鍵入憑據的密碼，然後按一下確定。

   如果出現「由於檔案格式不正確或密碼錯誤而導致無法導入憑據」錯誤消息，請驗證密碼是否有效。

## 移除Acrobat Reader DC擴充功能憑證 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定>信任儲存管理>本機憑證」。
1. 選擇憑據，然後按一下「刪除」。

## 取代Acrobat Reader DC擴充功能憑證 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定>信任儲存管理>本機憑證」。
1. 記下現有憑據的別名，然後選擇它，然後按一下「刪除」。
1. 使用完全相同的別名導入新憑據。
