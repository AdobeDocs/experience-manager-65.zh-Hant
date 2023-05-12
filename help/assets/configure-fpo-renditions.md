---
title: 僅針對Adobe InDesign產生版位轉譯
description: 使用Experience Manager Assets工作流程和ImageMagick產生新資產和現有資產的FPO轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# 僅針對Adobe InDesign產生版位轉譯 {#fpo-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | 本文 |

將大型資產從Experience Manager放入Adobe InDesign檔案時，創意專業人員必須等待一段長時間 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同時，用戶被阻止使用InDesign。 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可以暫時將小型格式副本放在InDesign文檔中以開頭。 如果需要最終輸出，例如針對列印和發佈工作流程，原始的全解析度資產會取代背景的暫時轉譯。 背景中的非同步更新可加快設計流程以提高生產力，並且不會阻礙創作流程。

Adobe Experience Manager(AEM)提供僅用於版位(FPO)的轉譯。 這些FPO轉譯的檔案大小很小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此後援機制可確保創意工作流程持續進行，不會有任何中斷。

## 產生FPO轉譯的方法 {#approach-to-generate-fpo-renditions}

Experience Manager允許許多方法處理可用於產生FPO轉譯的影像。 最常見的兩種方法是使用內建的Experience Manager工作流程和使用ImageMagick。 使用這兩種方法，您可以設定新上傳資產和Experience Manager中現有資產的轉譯產生。

您可以使用ImageMagick處理影像，包括產生FPO轉譯。 這樣的格式副本被縮減採樣，即如果原始影像的PPI大於72，則格式副本的像素尺寸按比例減少。 請參閱 [安裝並設定ImageMagick以與Experience Manager Assets搭配使用](best-practices-for-imagemagick.md).

|  | 使用Experience Manager內建的工作流程 | 使用ImageMagick工作流程 | 注釋 |
|--- |--- |---|--- |
| 針對新資產 | 啟用FPO轉譯([說明](#generate-renditions-of-new-assets-using-aem-workflow)) | 在Experience Manager工作流程中新增ImageMagick命令列([說明](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager會針對每次上傳執行DAM更新資產工作流程。 |
| 針對現有資產 | 在新的專用Experience Manager工作流程中啟用FPO轉譯([說明](#generate-renditions-of-existing-assets-using-aem-workflow)) | 在新的專用Experience Manager工作流程中新增ImageMagick命令列([說明](#generate-renditions-of-existing-assets-using-imagemagick)) | 現有資產的FPO轉譯可依需求或大量建立。 |

>[!CAUTION]
>
>修改預設工作流程的復本，以建立工作流程以產生轉譯。 它可防止在更新Experience Manager時覆寫您的變更，例如安裝新的Service Pack。

## 使用Experience Manager工作流程產生新資產的轉譯 {#generate-renditions-of-new-assets-using-aem-workflow}

以下是設定DAM更新資產工作流程模型以啟用轉譯產生的步驟：

1. 按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**. 選擇 **[!UICONTROL DAM更新資產]** 模型和按一下 **[!UICONTROL 編輯]**.

1. 選擇 **[!UICONTROL 處理縮圖]** 按一下步驟 **[!UICONTROL 設定]**.

1. 按一下 **[!UICONTROL FPO轉譯]** 標籤。 選擇 **[!UICONTROL 啟用FPO格式副本建立]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 調整 **[!UICONTROL 品質]** 添加或修改 **[!UICONTROL 格式清單]** 值。 預設情況下，要生成FPO格式副本的MIME類型清單為pjpeg、jpeg、jpg、gif、png、x-png和tiff。 按一下 **[!UICONTROL 完成]**.

   >[!NOTE]
   >
   >檔案類型JPEG、GIF、PNG、TIFF、PSD和BMP支援產生轉譯。

1. 若要啟動變更，請按一下 **[!UICONTROL 同步]**.

>[!NOTE]
>
>一側大於1280像素的影像不會保留FPO轉譯中的像素尺寸。

## 使用ImageMagick產生新資產的轉譯 {#generate-renditions-of-new-assets-using-imagemagick}

在Experience Manager中，上傳新資產時會執行DAM更新資產工作流程。 若要使用ImageMagick處理新上傳資產的轉譯，請將新命令新增至工作流程模型。

1. 按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 選擇 **[!UICONTROL DAM更新資產]** 模型和按一下 **[!UICONTROL 編輯]**.

1. 按一下 **[!UICONTROL 切換側面板]** 在左上角，搜索命令行步驟。

1. 拖曳 **[!UICONTROL 命令列]** 步驟，並將其新增至 **[!UICONTROL 處理縮圖]** 步驟。

1. 選擇 **[!UICONTROL 命令列]** 按一下步驟 **[!UICONTROL 設定]**.

1. 將所需資訊新增為自訂 **[!UICONTROL 標題]** 和 **[!UICONTROL 說明]**. 例如，FPO轉譯（由ImageMagick提供技術）。

1. 在 **[!UICONTROL 引數]** 標籤，添加相關 **[!UICONTROL Mime類型]** 提供命令應用的檔案格式清單。

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 在 **[!UICONTROL 引數]** 標籤中 **[!UICONTROL 命令]** 區段中，添加相關的ImageMagick命令以生成FPO轉譯。

   以下是範例命令，其會以JPEG格式產生FPO轉譯、縮減取樣為72 PPI、以10%品質設定，並透過拼合輸出來處理多層Adobe Photoshop檔案：

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 若要啟動變更，請按一下 **[!UICONTROL 同步]**.

有關ImageMagick命令行功能的詳細資訊，請參見 [https://imagemagick.org](https://imagemagick.org).

## 使用Experience Manager工作流程產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-aem-workflow}

若要使用Experience Manager工作流程來產生現有資產的FPO轉譯，請建立使用內建FPO轉譯選項的專用工作流程模型。

1. 按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 要建立模型，請按一下 **[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**.

1. 新增有意義的 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]**.

1. 選取模型，然後按一下 **[!UICONTROL 編輯]**. 按一下 **[!UICONTROL 頁面資訊]** > **[!UICONTROL 開啟屬性]**，然後選取 **[!UICONTROL 暫時性工作流程]**. 這提高了可擴充性和效能。

1. 按一下&#x200B;******[!UICONTROL 儲存並關閉]**。

1. 按一下 **[!UICONTROL 切換側面板]** 在左上角，搜尋處理縮圖步驟。

1. 選擇 **[!UICONTROL 處理縮圖]** 按一下 **[!UICONTROL 設定]**. 關注 [使用Experience Manager工作流程產生新資產轉譯的設定](#generate-renditions-of-new-assets-using-aem-workflow).

1. 若要啟動變更，請按一下 **[!UICONTROL 同步]**.


## 使用ImageMagick產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-imagemagick}

要使用ImageMagick處理功能生成現有資產的FPO格式副本，請建立一個專用的工作流模型，該工作流模型使用ImageMagick命令行執行此操作。

1. 請依照 [設定，使用Experience Manager工作流程產生現有資產的轉譯](#generate-renditions-of-existing-assets-using-aem-workflow) 區段。

1. 請依照 [設定，使用ImageMagick產生新資產的轉譯](#generate-renditions-of-new-assets-using-imagemagick) 區段。


## 查看FPO轉譯 {#view-fpo-renditions}

工作流程完成後，您可以檢查產生的FPO轉譯。 在Experience Manager Assets使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄，然後選取「轉譯」。 或者，使用鍵盤快速鍵 `Alt + 3` 預覽時顯示。

按一下 **[!UICONTROL FPO轉譯]** 以載入其預覽。 或者，您可以以滑鼠右鍵按一下轉譯，然後儲存至您的檔案系統。

![rendition_list](assets/rendition_list.png)


## 提示和限制 {#tips-limitations}

* 要使用基於ImageMagick的配置，請將ImageMagick安裝在與Experience Manager相同的電腦上。
* 若要產生許多資產或整個存放庫的FPO轉譯，請在低流量期間規劃並執行工作流程。 為大量資產產生FPO轉譯是一項耗用大量資源的活動，Experience Manager伺服器必須具備足夠的處理能力和可用記憶體。
* 有關效能和可擴充性，請參閱 [微調ImageMagick](performance-tuning-guidelines.md).
* 如需資產的一般命令列處理，請參閱 [處理資產的命令列處理常式](media-handlers.md).
