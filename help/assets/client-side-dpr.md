---
title: 使用具有用戶端裝置像素比的智慧型影像
description: 了解如何搭配Dynamic Media在Adobe Experience Manager as a Cloud Service中使用用戶端裝置像素比率與智慧型影像。
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 關於使用用戶端裝置像素比率(DPR)的智慧型影像 {#client-side-dpr}

目前的智慧型影像處理解決方案使用使用者代理字串，來判斷所使用的裝置類型（桌上型電腦、平板電腦、行動裝置等）。

裝置偵測功能（根據使用者代理字串的DPR）通常不準確，尤其是Apple裝置。 此外，每當新裝置啟動時，都必須驗證它。

用戶端DPR可提供100%的精確值，且適用於任何裝置，無論是Apple或任何其他已啟動的新裝置皆然。

## 使用用戶端DPR程式碼

**伺服器端轉譯的應用程式**

1. 載入服務工作器初始化(`srvinit.js`)，並在HTML頁面的標題區段中加入下列指令碼：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe建議您載入此指令碼 _befor_ 任何其他指令碼，以便服務工作人員立即開始初始化。

1. 在HTML頁面內文區段頂端加入下列DPR影像標籤程式碼：

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   您必須加入此DPR影像標籤程式碼 _befor_ HTML頁面中的所有靜態影像。

**用戶端轉譯的應用程式**

1. 在HTML頁面的標題區段中加入下列DPR指令碼：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   您可以將兩個DPR指令碼合併為一個，以避免多個網路請求。

   Adobe建議您載入這些指令碼 _befor_ 「HTML」頁面中的任何其他指令碼。
Adobe也建議您以diffHTML標籤（而非內文元素）Bootstrap應用程式。 原因是 `dprImageInjection.js` 在「HTML」頁面的內文區段頂端動態插入影像標籤。

## JavaScript檔案下載 {#client-side-dpr-script}

下載中的下列JavaScript檔案僅供您參考。 如果您想在HTML頁面中使用這些檔案，請務必編輯每個檔案的程式碼，以符合您自己的需求。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript檔案下載](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [智慧型影像](/help/assets/imaging-faq.md)

