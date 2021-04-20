---
title: 匯入和匯出PDF產生器組態檔
seo-title: 匯入和匯出PDF產生器組態檔
description: 瞭解如何匯入和匯出PDF Generator設定檔。
seo-description: 瞭解如何匯入和匯出PDF Generator設定檔。
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# 匯入和匯出PDF產生器組態檔{#importing-and-exporting-pdf-generator-configuration-files}

設定檔包含PDF Generator轉換資訊，包括PDF、檔案類型和安全性設定。

>[!NOTE]
>
>您無法匯入自訂native2pdfconfig.xml檔案，以變更PDF產生器的逾時設定。 該檔案中的逾時設定僅供參考，並在PDF產生器中顯示目前的設定。 若要變更逾時設定，請參閱[安裝和部署表單](https://www.adobe.com/go/learn_aemforms_installJBoss_63)中的「設定PDF產生器AEM效能參數」。

## 導出當前配置檔案{#export-your-current-configuration-file}

1. 在管理控制台中，按一下「服務> PDF產生器>設定檔案>匯出設定」。
1. 若要匯出設定，請選取適當的選項：

   * 若要匯出所有命名設定，請選取「下載整個設定」。
   * 要僅導出一個Adobe PDF設定、安全設定或檔案類型設定，請選擇下載最小配置。

      如果要導出最小配置，請選擇要導出的Adobe PDF、安全性和檔案類型設定。

1. 按一下「下載」，並將XML檔案儲存在適當的位置。

## 導入配置檔案{#import-a-configuration-file}

>[!NOTE]
>
>系統將根據導入檔案中的資訊重新配置系統。

1. 在管理控制台中，按一下「服務> PDF產生器>設定檔案>匯入設定」。
1. 選擇導入現有配置檔案。
1. 要在「配置檔案」框中指定檔案位置，請按一下「瀏覽」查找並選擇檔案，然後按一下「導入」****。

## 轉換AutoCAD檔案{#convert-all-layers-within-autocad-files}中的所有圖層

根據預設，PDF產生器僅將AutoCAD檔案的預設圖層轉換為PDF，而非檔案中的所有圖層。 要轉換所有圖層，請遵循此過程。

1. 在管理控制台中，按一下「服務> PDF產生器>設定檔案>匯出設定」。
1. 選擇「下載整個配置」，然後按一下「下載」。
1. 在文字編輯器中，開啟已下載的檔案，並在`PDFMaker`標籤內的`AutoCAD`標籤下，新增文字`convertAllPages="true"`。
1. 在管理控制台中，按一下「服務> PDF產生器>設定檔案>匯入設定」。
1. 選擇「導入現有配置檔案」，指定更新的檔案，然後按一下「導入」。

   使用修改的配置檔案轉換的任何AutoCAD檔案都將轉換所有層。

## 將配置重置為隨PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}安裝的原始設定

1. 在管理控制台中，按一下「服務> PDF產生器>設定檔案>匯入設定」。
1. 選擇「將配置重置為預設設定」，然後按一下「導入」。

