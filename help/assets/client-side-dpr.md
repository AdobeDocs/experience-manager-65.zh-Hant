---
title: 使用具有客戶端設備像素比的智慧映像
description: 瞭解如何將客戶端設備像素比率與Adobe Experience Manager as a Cloud Service的智慧映像結合使用Dynamic Media。
role: Admin,User
source-git-commit: 9b02a5363d32771cd9c039f97044e8a1d72fe286
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 關於具有客戶端設備像素比(DPR)的智慧成像 {#client-side-dpr}

當前的智慧映像解決方案使用用戶代理字串來確定正在使用的設備類型（案頭、平板電腦、移動設備等）。

設備檢測功能 — 基於用戶代理字串的DPR — 往往不準確，特別是對於Apple設備。 此外，只要新設備啟動，就必須對其進行驗證。

客戶端DPR為您提供100%的準確值，適用於任何設備，無論是Apple設備還是任何其他已啟動的新設備。

## 使用客戶端DPR代碼

**伺服器端呈現的應用**

1. 載入服務工作器初始化(`srvinit.js`)，在HTML頁的標題部分包含以下指令碼：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe建議您載入此指令碼 _先_ 任何其他指令碼，以便服務工作人員立即開始初始化。

1. 在HTML頁的正文部分頂部包括以下DPR影像標籤代碼：

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   必須包括此DPR影像標籤代碼 _先_ HTML頁中的所有靜態映像。

**客戶端呈現的應用**

1. 在HTML頁的標題部分包括以下DPR指令碼：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   您可以將兩個DPR指令碼合併為一個，以避免多個網路請求。

   Adobe建議您載入這些指令碼 _先_ 「HTML」頁中的任何其他指令碼。
Adobe還建議您在diffHTML標籤而不是body元素下Bootstrap應用。 原因是 `dprImageInjection.js` 動態地在HTML頁的body部分頂部彈出影像標籤。

## JavaScript檔案下載 {#client-side-dpr-script}

下載中的以下JavaScript檔案僅作為示例引用提供給您。 如果要在HTML頁中使用這些檔案，請確保編輯每個檔案的代碼以符合您自己的要求。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript檔案下載](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [智慧型影像](/help/assets/imaging-faq.md)