---
title: 導入和導出PDF生成器配置檔案
seo-title: Importing and exporting PDF Generator configuration files
description: 瞭解如何導入和導出PDF生成器配置檔案。
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 導入和導出PDF生成器配置檔案 {#importing-and-exporting-pdf-generator-configuration-files}

配置檔案包含PDF生成器轉換資訊，包括PDF、檔案類型和安全設定。

>[!NOTE]
>
>無法通過導入自定義native2pdfconfig.xml檔案來更改PDF生成器的超時設定。 該檔案中的超時設定僅供參考，並在PDF生成器中顯示當前設定。 要更改超時設定，請參閱中的「設定PDF生成器效能參數」 [安裝和部署表AEM單](https://www.adobe.com/go/learn_aemforms_installJBoss_63)。

## 導出當前配置檔案 {#export-your-current-configuration-file}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導出配置」。
1. 要導出設定，請選擇相應的選項：

   * 要導出所有命名設定，請選擇「下載整個配置」。
   * 要僅導出一個Adobe PDF設定、安全設定或檔案類型設定，請選擇下載最小配置。

      如果要導出最小配置，請選擇要導出的Adobe PDF、安全性和檔案類型設定。

1. 按一下「下載」，將XML檔案保存到適當的位置。

## 導入配置檔案 {#import-a-configuration-file}

>[!NOTE]
>
>將根據導入檔案中的資訊重新配置您的系統。

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導入配置」。
1. 選擇導入現有配置檔案。
1. 要在「配置檔案」框中指定檔案位置，請按一下「瀏覽」查找並選擇檔案，然後按一下 **導入**。

## 轉換AutoCAD檔案內的所有層 {#convert-all-layers-within-autocad-files}

預設情況下，「PDF生成器」(AutoCAD Generator)只將AutoCAD檔案的預設層轉換為PDF，而不是檔案中的所有層。 要轉換所有圖層，請遵循此過程。

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導出配置」。
1. 選擇「下載整個配置」，然後按一下「下載」。
1. 在文本編輯器中，開啟下載的檔案，並在 `AutoCAD` 標籤 `PDFMaker` 標籤，添加文本 `convertAllPages="true"`。
1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導入配置」。
1. 選擇「導入現有配置檔案」，指定更新的檔案，然後按一下「導入」。

   使用修改的配置檔案轉換的任何AutoCAD檔案都將轉換所有層。

## 將配置重置為隨PDF生成器一起安裝的原始設定 {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導入配置」。
1. 選擇「將配置重置為預設設定」，然後按一下「導入」。
