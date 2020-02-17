---
title: 設定認證以搭配Acrobat Reader DC擴充功能使用
seo-title: 設定認證以搭配Acrobat Reader DC擴充功能使用
description: 瞭解如何設定認證以搭配Acrobat Reader DC擴充功能使用。
seo-description: 瞭解如何設定認證以搭配Acrobat Reader DC擴充功能使用。
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定認證以搭配Acrobat Reader DC擴充功能使用{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

若要套用PDF檔案的使用權，請使用Acrobat Reader DC擴充功能的有效憑證來設定AEM表單。 在安裝AEM表單時，可能已設定憑證。 如果您在執行Configuration manager時未設定Acrobat Reader DC擴充功能憑證，或者您需要匯入新憑證或取代憑證，則可使用「信任商店管理」頁面來設定。

如果您使用評估憑證，請在移至生產環境時，以生產憑證來取代。 若要更新過期或評估憑證，請先刪除舊版Acrobat Reader DC擴充功能憑證。

如需有關取得憑證的詳細資訊，請 [參閱「準備安裝AEM表單（單一伺服器）」](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

信任商店可能包含多份Acrobat Reader DC擴充功能憑證。 您必須將其中一個認證指定為預設的Reader Extensions憑證。 當Workbench使用者無法決定在建立流程期間要使用哪些憑證時，就會使用預設憑證。 這些規則適用於預設憑據：

* 如果您匯入Acrobat Reader DC擴充功能憑證，而信任存放區則不包含其他Acrobat Reader DC擴充功能憑證，則會設為預設值。
* 如果您在選取「預設」選項的情況下匯入Acrobat Reader DC擴充功能憑證，預設類型會從現有的預設憑證中移除。 導入的憑據將成為預設憑據。
* 您無法刪除預設的Acrobat Reader DC擴充功能憑證。 要刪除預設憑據，請首先將另一個憑據設定為預設值。 此規則的例外是，如果只有一個憑證，則即使是預設憑證，您仍可將其刪除。
* 您無法更新預設的Acrobat Reader DC擴充功能憑證。

>[!NOTE]
>
>您也可以以程式設計方式匯入和刪除認證。 (請參 [閱「使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63)」)。

## 匯入Acrobat Reader DC擴充功能憑證 {#import-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 按一下「匯入」，然後在「信任商店類型」下方，選取「Acrobat Reader DC擴充功能憑證」。
1. （可選）若要指出此憑證是與Acrobat Reader DC擴充功能搭配使用的預設憑證，請選取「預設」。
1. 在「別名」框中，鍵入憑據的標識符。 此識別碼會用作Acrobat Reader DC擴充功能中憑證的顯示名稱。 此別名也可用來使用AEM表單SDK以程式設計方式存取憑證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫，以便顯示。 在進程中引用別名時，別名不區分大小寫。

1. 按一下選擇檔案以查找憑據，鍵入憑據的密碼，然後按一下確定。

   如果出現錯誤消息「由於檔案格式錯誤或密碼錯誤而導入憑據失敗」，請驗證密碼是否有效。

## 移除Acrobat Reader DC擴充功能憑證 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 選擇憑據並按一下刪除。

## 取代Acrobat Reader DC擴充功能憑證 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定>信任商店管理>本機認證」。
1. 記下現有憑證的別名，然後選取它，然後按一下「刪除」。
1. 使用完全相同的別名導入新憑據。

