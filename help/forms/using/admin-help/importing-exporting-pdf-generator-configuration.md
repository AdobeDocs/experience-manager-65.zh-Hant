---
title: 匯入和匯出PDF產生器組態檔
seo-title: 匯入和匯出PDF產生器組態檔
description: 了解如何匯入和匯出PDF產生器組態檔。
seo-description: 了解如何匯入和匯出PDF產生器組態檔。
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF 產生器
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 匯入和匯出PDF產生器組態檔{#importing-and-exporting-pdf-generator-configuration-files}

設定檔案包含PDF產生器轉換資訊，包括PDF、檔案類型和安全性設定。

>[!NOTE]
>
>無法通過導入自定義native2pdfconfig.xml檔案來更改PDF生成器的超時設定。 該檔案中的逾時設定僅供參考，並在PDF產生器中顯示目前設定。 若要變更逾時設定，請參閱[安裝和部署AEM表單](https://www.adobe.com/go/learn_aemforms_installJBoss_63)中的「設定PDF產生器效能參數」。

## 導出當前配置檔案{#export-your-current-configuration-file}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導出配置」。
1. 若要匯出設定，請選取適當的選項：

   * 要導出所有命名設定，請選擇「下載整個配置」。
   * 若只要匯出一個Adobe PDF設定、安全設定或檔案類型設定，請選取「下載最低配置」。

      如果要導出最小配置，請選擇要導出的Adobe PDF、安全性和檔案類型設定。

1. 按一下「下載」，並將XML檔案保存到適當的位置。

## 導入配置檔案{#import-a-configuration-file}

>[!NOTE]
>
>系統將根據導入檔案中的資訊重新配置。

1. 在管理控制台中，按一下「服務> PDF產生器>組態檔>匯入組態」 。
1. 選取「匯入現有組態檔」 。
1. 要在「配置檔案」框中指定檔案位置，請按一下「瀏覽」以查找並選擇檔案，然後按一下「**導入**」。

## 轉換AutoCAD檔案{#convert-all-layers-within-autocad-files}內的所有圖層

預設情況下，PDF生成器僅將AutoCAD檔案的預設層轉換為PDF，而不是檔案內的所有層。 要轉換所有圖層，請按照此過程操作。

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「配置檔案」>「導出配置」。
1. 選擇「Download Entire Configuration（下載整個配置）」 ，然後按一下「Download（下載）」。
1. 在文字編輯器中，開啟下載的檔案，並在`PDFMaker`標籤內的`AutoCAD`標籤下，新增文字`convertAllPages="true"`。
1. 在管理控制台中，按一下「服務> PDF產生器>組態檔>匯入組態」 。
1. 選擇「導入現有配置檔案」，指定更新的檔案，然後按一下「導入」。

   使用修改的配置檔案轉換的任何AutoCAD檔案都將轉換所有圖層。

## 將配置重置為隨PDF生成器{#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}安裝的原始設定

1. 在管理控制台中，按一下「服務> PDF產生器>組態檔>匯入組態」 。
1. 選擇「將配置重置為預設設定」 ，然後按一下「導入」。
