---
title: 僅針對Adobe InDesign產生版位轉譯
description: 使用「Experience Manager資產」工作流程和ImageMagick產生新資產和現有資產的FPO轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
source-git-commit: 08de462ead66cfc8f0cadbd1070bfa12f7c0d3d6
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 0%

---

# 僅針對Adobe InDesign產生版位轉譯 {#fpo-renditions}

將大型資產從Experience Manager放入Adobe InDesign檔案時，創意專業人員必須在[放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html)後等待相當長的時間。 同時，用戶被阻止使用InDesign。 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可以暫時將小型格式副本放在InDesign文檔中以開頭。 如果需要最終輸出，例如針對列印和發佈工作流程，原始的全解析度資產會取代背景的暫時轉譯。 背景中的非同步更新可加快設計流程以提高生產力，並且不會阻礙創作流程。

Adobe Experience Manager(AEM)提供僅用於版位(FPO)的轉譯。 這些FPO轉譯的檔案大小很小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此後援機制可確保創意工作流程持續進行，不會有任何中斷。

## 產生FPO轉譯的方法 {#approach-to-generate-fpo-renditions}

Experience Manager允許許多方法處理可用於產生FPO轉譯的影像。 最常見的兩種方法是使用內建的Experience Manager工作流程和使用ImageMagick。 使用這兩種方法，您可以設定新上傳資產和Experience Manager中現有資產的轉譯產生。

您可以使用ImageMagick處理影像，包括產生FPO轉譯。 這樣的格式副本被縮減採樣，即如果原始影像的PPI大於72，則格式副本的像素尺寸按比例減少。 請參閱[安裝並設定ImageMagick以搭配Experience Manager資產](best-practices-for-imagemagick.md)使用。

|  | 使用Experience Manager內建的工作流程 | 使用ImageMagick工作流程 | 注釋 |
|--- |--- |---|--- |
| 針對新資產 | 啟用FPO轉譯([help](#generate-renditions-of-new-assets-using-aem-workflow)) | 在Experience Manager工作流程([help](#generate-renditions-of-new-assets-using-imagemagick))中新增ImageMagick命令列 | Experience Manager會針對每次上傳執行DAM更新資產工作流程。 |
| 針對現有資產 | 在新的專用Experience Manager工作流程中啟用FPO轉譯([help](#generate-renditions-of-existing-assets-using-aem-workflow)) | 在新的專用Experience Manager工作流程([help](#generate-renditions-of-existing-assets-using-imagemagick))中添加ImageMagick命令行 | 現有資產的FPO轉譯可依需求或大量建立。 |

>[!CAUTION]
>
>修改預設工作流程的復本，以建立工作流程以產生轉譯。 它可防止在更新Experience Manager時覆寫您的變更，例如安裝新的Service Pack。

## 使用Experience Manager工作流程產生新資產的轉譯 {#generate-renditions-of-new-assets-using-aem-workflow}

以下是設定DAM更新資產工作流程模型以啟用轉譯產生的步驟：

1. 按一下「**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**」。 選擇&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;模型，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 選擇&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟，然後按一下&#x200B;**[!UICONTROL 配置]**。

1. 按一下「**[!UICONTROL FPO轉譯]**」頁簽。 選擇&#x200B;**[!UICONTROL 啟用FPO格式副本建立]**。

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 根據需要調整&#x200B;**[!UICONTROL Quality]**&#x200B;並添加或修改&#x200B;**[!UICONTROL Format List]**&#x200B;值。 預設情況下，要生成FPO格式副本的MIME類型清單為pjpeg、jpeg、jpg、gif、png、x-png和tiff。 按一下&#x200B;**[!UICONTROL Done]**。

   >[!NOTE]
   >
   >檔案類型JPEG、GIF、PNG、TIFF、PSD和BMP支援生成格式副本。

1. 要激活更改，請按一下&#x200B;**[!UICONTROL Sync]**。

>[!NOTE]
>
>一側大於1280像素的影像不會保留FPO轉譯中的像素尺寸。

## 使用ImageMagick產生新資產的轉譯 {#generate-renditions-of-new-assets-using-imagemagick}

在Experience Manager中，上傳新資產時會執行DAM更新資產工作流程。 若要使用ImageMagick處理新上傳資產的轉譯，請將新命令新增至工作流程模型。

1. 按一下「**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**」。

1. 選擇&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;模型，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 按一下左上角的「**[!UICONTROL 切換側面板]**」並搜索命令行步驟。

1. 拖動&#x200B;**[!UICONTROL 命令行]**&#x200B;步驟，並將其添加到&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟之前。

1. 選擇&#x200B;**[!UICONTROL 命令行]**&#x200B;步驟，然後按一下&#x200B;**[!UICONTROL 配置]**。

1. 將所需資訊新增為自訂&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 例如，FPO轉譯（由ImageMagick提供技術）。

1. 在&#x200B;**[!UICONTROL 參數]**&#x200B;頁簽中，添加相關的&#x200B;**[!UICONTROL Mime類型]**&#x200B;以提供命令應用的檔案格式清單。

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 在&#x200B;**[!UICONTROL Arguments]**&#x200B;頁簽的&#x200B;**[!UICONTROL Commands]**&#x200B;部分中，添加相關的ImageMagick命令以生成FPO格式副本。

   以下是範例命令，其會以JPEG格式產生FPO轉譯、以10%品質設定縮減取樣至72 PPI，並透過拼合輸出來處理多層Adobe Photoshop檔案：

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 要激活更改，請按一下&#x200B;**[!UICONTROL Sync]**。

有關ImageMagick命令行功能的詳細資訊，請參見[https://imagemagick.org](https://imagemagick.org)。

## 使用Experience Manager工作流程產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-aem-workflow}

若要使用Experience Manager工作流程來產生現有資產的FPO轉譯，請建立使用內建FPO轉譯選項的專用工作流程模型。

1. 按一下「**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**」。

1. 要建立模型，請按一下「**[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**」。

1. 新增有意義的&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**。

1. 選擇模型，然後按一下&#x200B;**[!UICONTROL Edit]**。 按一下「**[!UICONTROL 頁資訊]** > **[!UICONTROL 開啟屬性]**」，然後選擇「**[!UICONTROL 暫時工作流]**」。 這提高了可擴充性和效能。

1. 按一下&#x200B;******[!UICONTROL 儲存並關閉]**。

1. 按一下左上角的「**[!UICONTROL 切換側面板]**」並搜尋處理縮圖步驟。

1. 選擇&#x200B;**[!UICONTROL 處理縮圖]**，然後按一下&#x200B;**[!UICONTROL 配置]**。 依照[設定，使用Experience Manager工作流程](#generate-renditions-of-new-assets-using-aem-workflow)產生新資產的轉譯。

1. 要激活更改，請按一下&#x200B;**[!UICONTROL Sync]**。


## 使用ImageMagick產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-imagemagick}

要使用ImageMagick處理功能生成現有資產的FPO格式副本，請建立一個專用的工作流模型，該工作流模型使用ImageMagick命令行執行此操作。

1. 請依照[設定的步驟1到步驟3，使用Experience Manager工作流程](#generate-renditions-of-existing-assets-using-aem-workflow)區段產生現有資產的轉譯。

1. 請依照[設定中的步驟4到步驟8，使用ImageMagick](#generate-renditions-of-new-assets-using-imagemagick)區段產生新資產的轉譯。


## 查看FPO轉譯 {#view-fpo-renditions}

工作流程完成後，您可以檢查產生的FPO轉譯。 在「Experience Manager資產」使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄，然後選取「轉譯」。 或者，在預覽開啟時使用鍵盤快捷鍵`Alt + 3`。

按一下&#x200B;**[!UICONTROL FPO轉譯]**&#x200B;以載入其預覽。 或者，您可以以滑鼠右鍵按一下轉譯，然後儲存至您的檔案系統。

![rendition_list](assets/rendition_list.png)


## 提示和限制 {#tips-limitations}

* 要使用基於ImageMagick的配置，請將ImageMagick安裝在與Experience Manager相同的電腦上。
* 若要產生許多資產或整個存放庫的FPO轉譯，請在低流量期間規劃並執行工作流程。 為大量資產產生FPO轉譯是一項耗用大量資源的活動，Experience Manager伺服器必須具備足夠的處理能力和可用記憶體。
* 有關效能和可擴充性，請參閱[微調ImageMagick](performance-tuning-guidelines.md)。
* 有關資產的一般命令行處理，請參見[命令行處理程式以處理資產](media-handlers.md)。