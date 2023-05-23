---
title: 配置用於Acrobat Reader DC擴展的憑據
seo-title: Configuring credentials for use with Acrobat Reader DC extensions
description: 瞭解如何配置憑據以與Acrobat Reader DC擴展一起使用。
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

# 配置用於Acrobat Reader DC擴展的憑據{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

要對PDF文檔應用使用權限，請配AEM置具有Acrobat Reader DC擴展的有效憑據的表單。 在安裝表單期間可能已配置了憑據AEM。 如果在運行Configuration Manager時未配置Acrobat Reader DC擴展憑據，或者需要導入新憑據或替換憑據，則可以使用「信任儲存管理」頁進行配置。

如果您正在使用評估憑據，請在移至生產環境時將其替換為生產憑據。 要更新過期或評估憑據，請先刪除舊的Acrobat Reader DC擴展憑據。

有關獲取憑據的資訊，請參見 [準備安AEM裝表單（單伺服器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

信任儲存可能包含多個Acrobat Reader DC擴展憑據。 必須將其中一個憑據指定為預設的Reader擴展憑據。 當Workbench用戶無法確定在建立流程期間要使用的憑據時，將使用預設憑據。 這些規則適用於預設憑據：

* 如果導入Acrobat Reader DC擴展憑據，而信任儲存不包含其他Acrobat Reader DC擴展憑據，則將其設定為預設值。
* 如果導入了「預設」選項的Acrobat Reader DC擴展憑據，則會從現有預設憑據中刪除預設類型。 導入的憑據將成為預設值。
* 無法刪除預設的Acrobat Reader DC擴展憑據。 要刪除預設憑據，請先將另一個憑據設定為預設憑據。 此規則的一個例外是，如果只有一個憑據，則即使是預設憑據，也可以刪除它。
* 無法更新預設的Acrobat Reader DC擴展憑據。

>[!NOTE]
>
>您也可以以寫程式方式導入和刪除憑據。 (請參閱 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63)。)

## 導入Acrobat Reader DC擴展憑據 {#import-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 按一下導入，在信任儲存類型下，選擇Acrobat Reader DC擴展憑據。
1. （可選）要指明此憑據是與Acrobat Reader DC擴展一起使用的預設憑據，請選擇「預設」。
1. 在「別名」框中，鍵入憑據的標識符。 此標識符用作Acrobat Reader DC擴展中憑據的顯示名稱。 此別名還用於使用表單SDK以寫程式方式訪AEM問憑據。

   >[!NOTE]
   >
   >別名將自動轉換為大寫，以便顯示。 在進程中引用別名時，別名不區分大小寫。

1. 按一下選擇檔案以查找憑據，鍵入憑據的密碼，然後按一下確定。

   如果出現錯誤消息「由於檔案格式不正確或密碼不正確而導入憑據失敗」，請驗證密碼是否有效。

## 刪除Acrobat Reader DC擴展憑據 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 選擇憑據並按一下刪除。

## 替換Acrobat Reader DC擴展憑據 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 記下現有憑據的別名，然後選擇它，然後按一下刪除。
1. 使用完全相同的別名導入新憑據。
