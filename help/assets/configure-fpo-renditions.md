---
title: 產生Adobe InDesign的「僅供刊登」轉譯
description: 使用Experience Manager Assets工作流程和ImageMagick產生新資產和現有資產的FPO轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: f8588ef353bd08b41202350072728d80ee51f565
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 1%

---

# 產生Adobe InDesign的「僅供刊登」轉譯 {#fpo-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

將大型資產從Experience Manager置入Adobe InDesign檔案時，創意專業人士在[置入資產](https://helpx.adobe.com/tw/indesign/using/placing-graphics.html)後，必須等候相當長的時間。 同時，使用者被封鎖而無法使用InDesign。 這會中斷創意流程，並對使用者體驗產生負面影響。 Adobe一開始可讓您將小型轉譯暫時放入InDesign檔案。 需要最終輸出時（例如針對列印及發佈工作流程），原始的完整解析度資產會在背景取代暫時轉譯。 這種背景的非同步更新可加快設計流程以提高生產力，且不會影響創作流程。

Adobe Experience Manager (AEM)提供僅用於刊登(FPO)的轉譯。 這些FPO轉譯的檔案大小較小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此遞補機制可確保創意工作流程無任何中斷地進行。

## 產生FPO轉譯的方法 {#approach-to-generate-fpo-renditions}

Experience Manager允許使用許多方法來處理影像，以用來產生FPO轉譯。 最常用的兩種方法是使用內建Experience Manager工作流程和ImageMagick。 您可使用這兩種方法，設定新上傳資產及Experience Manager中現有資產的轉譯產生方式。

您可以使用ImageMagick來處理影像，包括產生FPO轉譯。 這類轉譯會縮減取樣，也就是說，如果原始影像的PPI大於72，轉譯的畫素尺寸會按比例縮小。 請參閱[安裝並設定ImageMagick以搭配Experience Manager Assets](best-practices-for-imagemagick.md)使用。

|  | 使用Experience Manager的內建工作流程 | 使用ImageMagick工作流程 | 備註 |
|--- |--- |---|--- |
| 針對新資產 | 啟用FPO轉譯（[說明](#generate-renditions-of-new-assets-using-aem-workflow)） | 在Experience Manager工作流程中新增ImageMagick命令列（[說明](#generate-renditions-of-new-assets-using-imagemagick)） | Experience Manager會針對每次上傳執行DAM更新Assets工作流程。 |
| 針對現有資產 | 在新的專用Experience Manager工作流程中啟用FPO轉譯（[說明](#generate-renditions-of-existing-assets-using-aem-workflow)） | 在新的專用Experience Manager工作流程中新增ImageMagick命令列（[說明](#generate-renditions-of-existing-assets-using-imagemagick)） | 現有資產的FPO轉譯可隨選或大量建立。 |

>[!CAUTION]
>
>修改預設工作流程的副本，建立工作流程以產生轉譯。 這可防止在Experience Manager更新時覆寫變更，例如透過安裝新的Service Pack。

## 使用Experience Manager工作流程產生新資產的轉譯 {#generate-renditions-of-new-assets-using-aem-workflow}

以下是設定DAM更新資產工作流程模型以啟用產生轉譯的步驟：

1. 按一下「**[!UICONTROL 工具]**」>「**[!UICONTROL 工作流程]**」>「**[!UICONTROL 模型]**」。 選取&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;模型，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 選取&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟，然後按一下&#x200B;**[!UICONTROL 設定]**。

1. 按一下「**[!UICONTROL FPO轉譯]**」標籤。 選取&#x200B;**[!UICONTROL 啟用FPO轉譯建立]**。

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 調整&#x200B;**[!UICONTROL 品質]**，並視需要新增或修改&#x200B;**[!UICONTROL 格式清單]**&#x200B;值。 依預設，產生FPO轉譯的MIME型別清單為pjpeg、jpeg、jpg、gif、png、x-png和tiff。 按一下&#x200B;**[!UICONTROL 完成]**。

   >[!NOTE]
   >
   >檔案型別JPEG、GIF、PNG、TIFF、PSD和BMP支援產生轉譯。

1. 若要啟用變更，請按一下[同步]。**&#x200B;**

>[!NOTE]
>
>單面大於1280畫素的影像不會保留FPO轉譯中的畫素尺寸。

## 使用ImageMagick產生新資產的轉譯 {#generate-renditions-of-new-assets-using-imagemagick}

在Experience Manager中，當上傳新資產時，會執行DAM更新資產工作流程。 若要使用ImageMagick處理新上傳資產的轉譯，請新增命令至工作流程模型。

1. 按一下「**[!UICONTROL 工具]**」>「**[!UICONTROL 工作流程]**」>「**[!UICONTROL 模型]**」。

1. 選取&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;模型，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 按一下左上角的&#x200B;**[!UICONTROL 切換側面板]**&#x200B;並搜尋命令列步驟。

1. 拖曳&#x200B;**[!UICONTROL 命令列]**&#x200B;步驟，並在&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟之前新增該步驟。

1. 選取&#x200B;**[!UICONTROL 命令列]**&#x200B;步驟並按一下&#x200B;**[!UICONTROL 設定]**。

1. 新增所需的資訊作為自訂&#x200B;**[!UICONTROL 標題]**&#x200B;和&#x200B;**[!UICONTROL 描述]**。 例如，FPO轉譯（由ImageMagick提供技術支援）。

1. 在&#x200B;**[!UICONTROL 引數]**&#x200B;索引標籤中，新增相關的&#x200B;**[!UICONTROL Mime型別]**，以提供套用該命令的檔案格式清單。

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 在&#x200B;**[!UICONTROL 引數]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 命令]**&#x200B;區段中，新增相關的ImageMagick命令以產生FPO轉譯。

   以下是範例命令，可產生JPEG格式的FPO轉譯、縮減取樣為72 PPI、10%品質設定，並透過平面化輸出來處理多層Adobe Photoshop檔案：

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 若要啟用變更，請按一下[同步]。**&#x200B;**

如需ImageMagick命令列功能的詳細資訊，請參閱`https://imagemagick.org`網站。

## 使用Experience Manager工作流程產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-aem-workflow}

若要使用Experience Manager工作流程產生現有資產的FPO轉譯，請建立使用內建FPO轉譯選項的專用工作流程模型。

1. 按一下「**[!UICONTROL 工具]**」>「**[!UICONTROL 工作流程]**」>「**[!UICONTROL 模型]**」。

1. 若要建立模型，請按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**。

1. 新增有意義的&#x200B;**[!UICONTROL 標題]**&#x200B;和&#x200B;**[!UICONTROL 名稱]**。

1. 選取模型並按一下&#x200B;**[!UICONTROL 編輯]**。 按一下&#x200B;**[!UICONTROL 頁面資訊]** > **[!UICONTROL 開啟屬性]**，然後選取&#x200B;**[!UICONTROL 暫時性工作流程]**。 這可改善擴充性和效能。

1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;和&#x200B;**[!UICONTROL 關閉]**。

1. 按一下左上角的「**[!UICONTROL 切換側面板]**」並搜尋程式縮圖步驟。

1. 選取&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;並按一下&#x200B;**[!UICONTROL 設定]**。 依照[設定，使用Experience Manager工作流程](#generate-renditions-of-new-assets-using-aem-workflow)產生新資產的轉譯。

1. 若要啟用變更，請按一下[同步]。**&#x200B;**


## 使用ImageMagick產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-imagemagick}

若要使用ImageMagick處理功能來產生現有資產的FPO轉譯，請建立專用工作流程模型，並使用ImageMagick命令列來執行此操作。

1. 依照[設定的步驟1到步驟3操作，使用Experience Manager工作流程](#generate-renditions-of-existing-assets-using-aem-workflow)區段來產生現有資產的轉譯。

1. 依照[設定的步驟4到步驟8操作，使用ImageMagick](#generate-renditions-of-new-assets-using-imagemagick)區段產生新資產的轉譯。


## 檢視FPO轉譯 {#view-fpo-renditions}

您可以在工作流程完成後，檢查產生的FPO轉譯。 在Experience Manager Assets使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄，然後選取轉譯。 或者，在預覽開啟時使用鍵盤快速鍵`Alt + 3`。

按一下&#x200B;**[!UICONTROL FPO轉譯]**&#x200B;以載入其預覽。 或者，您也可以用滑鼠右鍵按一下轉譯，並將其儲存至您的檔案系統。

![rendition_list](assets/rendition_list.png)


## 提示和限制 {#tips-limitations}

* 若要使用ImageMagick型設定，請將ImageMagick安裝在與Experience Manager相同的機器上。
* 若要產生許多資產或整個存放庫的FPO轉譯，請在低流量期間規劃和執行工作流程。 為大量資產產生FPO轉譯是一項耗用大量資源的活動，且Experience Manager伺服器必須具備足夠的處理能力和可用記憶體。
* 如需效能與擴充能力，請參閱[微調ImageMagick](performance-tuning-guidelines.md)。
* 如需處理資產的一般命令列，請參閱[處理資產的命令列處理常式](media-handlers.md)。
