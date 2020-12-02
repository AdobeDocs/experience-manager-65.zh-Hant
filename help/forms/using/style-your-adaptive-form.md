---
title: '設定最適化表單的樣式 '
seo-title: '設定最適化表單的樣式 '
description: '瞭解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用網頁字型 '
seo-description: '瞭解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用網頁字型 '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: 263a25b70fe4a3e7de65b47f07932d2e5f3d0197
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 7%

---


# 設定最適化表單的樣式{#do-not-publish-style-your-adaptive-form}

瞭解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用網頁字型

![](do-not-localize/08-style_your_adaptiveformmain.png)

本教程是[建立第一個自適應表單](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的一個步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

## 關於教學課程{#about-the-tutorial}

您可以使用主題為最適化表單提供獨特的外觀和樣式。 您可以套用隨附於最適化表單編輯器的方塊外主題，或建立您自己的自訂主題。 AEM [!DNL Forms]提供[主題編輯器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)以建立自訂主題。 單一主題可針對在行動裝置、平板電腦或桌上型電腦上開啟的相同最適化表單提供不同的外觀。 使用主題編輯器時，不需具備任何CSS或LESS的先前知識，但需要它。

在教學課程結束時，您將學習：

* 將立即可用的主題套用至最適化表單
* 使用主題編輯器建立最適化表單的主題
* 設定個別元件的樣式
* 附加部分：在自訂主題中使用網頁字型

在您完成教學課程後，表單看起來會類似下列：

![具有自訂主題的表單](assets/styled-adaptive-form.png)

## 開始{#before-you-start}之前

在您的本機電腦上下載標題樣式和標誌影像，如下所示。 `shipping-address-add-update-form`最適化表單的頁首使用頁首樣式和標誌影像。 標題樣式影像會出現在標題的右側。

[取得檔案](assets/header-style.png)

[取得檔案](assets/logo-1.png)

## 步驟1:將主題套用至最適化表單{#step-apply-a-theme-to-your-adaptive-form}

最適化表單編輯器提供多種現成可用的主題。 如果您打算不針對最適化表單使用自訂樣式，也可以使用現成可用的主題來發佈最適化表單。 主題與最適化表單無關。 您可以將相同的主題套用至多個調適性表單。 若要將主題套用至最適化表單：

1. 開啟最適化表單以進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. **[!UICONTROL 最適化表單容器]**&#x200B;的開啟屬性。 在屬性瀏覽器中，導覽至&#x200B;**[!UICONTROL Basic]** > **[!UICONTROL 最適化表單主題]**。 **[!UICONTROL 最適化表單主題]**&#x200B;欄位會列出所有現成可用的主題和自訂主題。 依預設，會套用「畫布」主題。
1. 從&#x200B;**[!UICONTROL 最適化表單主題]**&#x200B;欄位中選取主題。 例如，**調查主題**。 點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以套用選取的主題。

   ![具有預設主題的最適化表單](assets/default-adaptive-form.png)

   **圖：具有** *預設主題的最適化表單*

   ![具有調查主題的最適化表單](assets/adaptive-form-with-survey-theme.png)

   **圖：具** *有調查主題的最適化表單*

## 步驟2:更新最適化表單{#step-update-your-adaptive-form}

上述設計需要變更現有最適化表單的預留位置文字和標誌。 執行下列步驟以進行必要的變更：

1. 變更標題的現有標誌和文字。 若要移除標誌：

   1. 在表單編輯器中開啟表單。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 在[!UICONTROL header]元件中點選標誌影像，然後點選![cmppr](assets/cmppr.png)**[!UICONTROL 屬性]**。 在[!UICONTROL image]屬性中，點選X以移除現有的標誌影像。
   1. 點選&#x200B;**[!UICONTROL upload]**，選取logo.png，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以儲存變更。 影像已下載於[開始](/help/forms/using/style-your-adaptive-form.md#before-you-start)區段中。
   1. 點選標題文字、`We.Retail`，然後點選![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**。 將標題文字變更為`we retail`。 僅對`we retail`中的`we`應用粗體格式。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 移除標題並新增預留位置文字：

   1. 點選「Customer ID（客戶ID）」欄位並點選「![cmppr](assets/cmppr.png)屬性」。
   1. 將&#x200B;**[!UICONTROL Title]**&#x200B;欄位的內容複製到&#x200B;**[!UICONTROL 預留位置文字]**&#x200B;欄位。
   1. 刪除&#x200B;**[!UICONTROL Title]**&#x200B;欄位的內容，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
   1. 對表單中的所有文字方塊、數值方塊和電子郵件欄位重複上述三個步驟。

      ![更新的自適應形式](assets/updated-adaptive-form.png)

## 步驟3:為最適化表單建立自訂主題{#step-create-a-custom-theme-for-your-adaptive-form}

您可以使用[主題編輯器](/help/forms/using/themes.md)來建立自訂主題。 主題編輯器是功能強大的WYSIWYG編輯器。 它是將CSS套用至自適應表單各元件的視覺化方法。 它提供更精細的控制項，讓元件和面板在最適化表單中變樣。

主題是個別的實體，如最適化表單。 它包含最適化表單的元件和面板樣式(CSS)。 樣式包括CSS屬性，例如背景顏色、狀態顏色、透明度、對齊方式和大小。 應用主題時，指定的樣式將應用於自適應表單的相應元件。

在本教學課程中，您將設定頁首和頁尾、文字和數值元件、附件元件和按鈕的樣式。 讓我們從建立主題開始：

### 建立主題{#create-a-theme}

1. 登入AEM作者例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Themes]**。 預設URL為[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)。
1. 點選「**[!UICONTROL 建立]**」並選取「**[!UICONTROL 主題]**」。 此時會出現[!UICONTROL 建立主題]頁面，其中包含建立主題所需的欄位。 **[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**&#x200B;欄位為必填欄位：

   * **標題：** 指定主題的標題。例如，**全域主題。** 標題可協助您從主題清單中識別主題。
   * **名稱：** 指定主題的名稱。例如，**Global-Theme。** 在儲存庫中建立具有指定名稱的節點。當您開始輸入標題時，系統會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。

1. 點選&#x200B;**[!UICONTROL Create]**。 將建立一個主題，並出現一個用於開啟表單進行編輯的對話框。 點選「**[!UICONTROL 開啟]**」，在新標籤中開啟新建立的主題。 主題在主題編輯器中開啟。 對於樣式，主題編輯器使用隨附於AEM [!DNL Forms]的現成可用最適化表單。

   有關使用主題編輯器UI的資訊，請參閱[關於主題編輯器](/help/forms/using/themes.md#aboutthethemeeditor)。

1. 點選「**[!UICONTROL 主題選項]** ![主題選項](assets/theme-options.png) > **[!UICONTROL 設定]**」。 在&#x200B;**[!UICONTROL 預覽表單]**&#x200B;欄位中，選取&#x200B;**shipping-address-add-update-form**&#x200B;最適化表單，點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，點選&#x200B;**[!UICONTROL Save]**。 現在，主題編輯器已設定為使用您自己的最適化表單，而非預設的最適化表單。 點選「**[!UICONTROL 取消]**」以返回主題編輯器。

   ![自訂主題](assets/custom-theme.png)

   **圖：具** *有shipping-add-update-form最適化表單的主題編輯器*

   ![create-a-theme](assets/create-a-theme.png)

   **圖：具** *有預設窗體的自適應窗體*

### 樣式頁首和頁尾{#style-header-and-footer}

頁首和頁尾為最適化表單提供一致且獨特的外觀。 一般而言，頁首包含組織的標誌和名稱，頁尾包含版權資訊，而且這些資訊在組織的多種形式上都相同。 要設定發運地址添加更新表單自適應表單的頁眉和頁腳的樣式，請執行以下操作：

1. 導覽「選擇器」面板中的「**[!UICONTROL 標題]** > **[!UICONTROL 文字]**」選項。 「選擇器」面板位於主題編輯器的左側。 如果面板不可見，請點選「切換側面板」。![](assets/toggle-side-panel.png)

1. 在&#x200B;**[!UICONTROL Text]** accordion中設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 字型系列 | Arial |
   | 字型色彩 | FFFFFF |
   | 字型大小 | 54px |

1. 點選[!UICONTROL 標題]介面工具集，點選&#x200B;**[!UICONTROL 標題]**。 標題介面工具集樣式的選項會顯示在左側。 展開&#x200B;**[!UICONTROL Dimensions &amp; Position]** accordion，將&#x200B;**[!UICONTROL Height]**&#x200B;設為`120px`，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 展開標題Widget的&#x200B;**[!UICONTROL Background]** accordion，將&#x200B;**[!UICONTROL Background Color]**&#x200B;設為`F6921E.`

   將滑鼠指標暫留在「影像與漸層」上，點選「影像」。 ************&#x200B;設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 影像 | 上傳header-style.png。 影像已下載於[開始](/help/forms/using/style-your-adaptive-form.md#before-you-start)區段中。 |
   | 位置 | 右下 |
   | 並排顯示 | 不重複 |

1. 在主題編輯器中，點選頁首中的標誌，然後點選「頁首標誌」。 ****&#x200B;展開「維度與位置」accordion，設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>邊距</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>頂部：1.5rem</li> 
        <li>底部：-35px</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>提示：點</strong> 選連結 <img src="assets/link.png"> 圖示可為每個欄位提供不同的值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. 點選頁尾Widget並點選&#x200B;**[!UICONTROL 頁尾]**。 展開&#x200B;**[!UICONTROL Background]** accordion，將&#x200B;**[!UICONTROL Background Color]**&#x200B;設為`F6921E`，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

### 設定資料擷取元件的樣式，並將背景套用至最適化表單{#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在最適化表單中使用多個元件來擷取資料。 例如，文字方塊和數值方塊。 您可以提供與所有資料擷取元件相同的樣式，或為每個元件提供個別的樣式。 在本教學課程中，相同的樣式會套用至數值方塊（客戶ID、郵遞區號）和文字方塊（客戶ID、名稱、送貨地址、狀態、電子郵件）。 要設定資料捕獲元件的樣式：

1. 點選「**[!UICONTROL 客戶ID]**」欄位，然後點選「**[!UICONTROL 欄位介面工具集]**」選項。 設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框顏色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框半徑 </td> 
      <td> 
       <ul> 
        <li>頂部：7px<br /> </li> 
        <li>右：7px<br /> </li> 
        <li>底部：7px<br /> </li> 
        <li>左：7px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型系列</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型色彩</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型大小</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>尺寸和位置</td> 
      <td>寬度</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>尺寸和位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>左：10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 點選&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位上方的空白區域，然後點選&#x200B;**[!UICONTROL 回應式面板容器]**。 將&#x200B;**[!UICONTROL 背景]** > **[!UICONTROL 背景顏色]**&#x200B;設定為F1F2F2。 點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   ![](do-not-localize/responsive-panel-container.png)

### 設定按鈕的樣式{#style-the-buttons}

您可以使用自訂主題將相同樣式套用至最適化表單的所有按鈕，而[內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md)則可將樣式套用至特定按鈕。 要設定按鈕的樣式，請執行以下操作：

1. 點選&#x200B;**[!UICONTROL Submit]**&#x200B;按鈕，點選&#x200B;**[!UICONTROL Button]**&#x200B;選項。 設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色彩</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>邊框<br /> </td> 
      <td>邊框顏色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框半徑 </td> 
      <td> 
       <ul> 
        <li>頂部：7px<br /> </li> 
        <li>右：7px<br /> </li> 
        <li>底部：7px<br /> </li> 
        <li>左：7px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文字<br /> </td> 
      <td>字型系列</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型色彩</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型大小</td> 
      <td>18px</td> 
     </tr> 
    </tbody> 
   </table>

1. [將自訂主題](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)「全域主題」套用至最適化表單。如果樣式未反映在最適化表單上，請清除瀏覽器快取，然後再試一次。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 步驟4:為各個元件設定樣式{#step-style-individual-components}

有些樣式只適用於特定元件。 這些元件是在最適化表單編輯器中建立樣式的。

1. 開啟最適化表單以進行編輯。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在頂欄上，選擇&#x200B;**[!UICONTROL Style]**&#x200B;選項。

   ![樣式——選項](assets/style-option.png)

1. 點選「**[!UICONTROL Attach]**」按鈕，然後點選「![ aem_6_3_edit](assets/aem_6_3_edit.png)」圖示。 在&#x200B;**[!UICONTROL Dimensions and Position]** accordion中設定以下屬性：

   | 屬性 | 值 |
   |---|---|
   | 浮點 | 左 |
   | 寬度 | 10% |

1. 點選「**[!UICONTROL 政府機關核准的位址證明]**」選項，點選「![ aem_6_3_edit](assets/aem_6_3_edit.png)」圖示。 設定下列屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>浮點</td> 
      <td>左</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>寬度</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>左：10px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>高度</td> 
      <td>40px</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置<br /> </td> 
      <td>邊距</td> 
      <td><br /> 
       <ul> 
        <li>右：2rem</li> 
        <li>左：10rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色彩</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框寬度</td> 
      <td>1px</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框樣式</td> 
      <td>堅固</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框顏色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框半徑</td> 
      <td>7px</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型系列</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型色彩</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字型大小</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>行高</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. 點選&#x200B;**[!UICONTROL Submit]**&#x200B;按鈕，點選![ aem_6_3_edit](assets/aem_6_3_edit.png)圖示。 設定下列屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸和位置</td> 
      <td>浮點</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>尺寸和位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>頂部：5rem</li> 
        <li>右：14rem</li> 
        <li>底部：20px</li> 
        <li>左：20px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色彩</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框顏色</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![樣式化自適應形式-1](assets/styled-adaptive-form-1.png)

## 步驟5:附加部分：在自訂主題{#step-bonus-section-using-web-fonts-in-a-custom-theme}中使用網頁字型

您可以使用各種字型來設計最適化表單。 在檢視最適化表單的所有裝置上，可能沒有用於設計最適化表單的字型。 您可以使用網頁字型服務，將必要的字型傳送至目標裝置。

[!DNL Adobe Fonts] 是網頁字型服務。您可以設定並使用具有最適化表單的服務。 要在自適應形式中使用[!DNL Adobe Fonts]:

>[!NOTE]
>
>![typekit-to-adobe-](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] fontsis現在稱為Adobe Fonts，並隨附於Creative Cloud和其他訂閱。[了解更多](https://fonts.adobe.com/).

1. 建立[Adobe Fonts](https://typekit.com/)帳戶、建立套件、將Myriad Pro字型加入套件、發佈套件並取得套件ID。 必須在最適化表單中使用[!DNL Adobe Fonts]（Web字型）。
1. 在AEM [!DNL Forms]伺服器中，導覽至![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**。 ![現在，開啟配置資料夾。 如果配置已可用，請按一下&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕以建立新實例。

   在「建立配置」對話框中，為配置指定&#x200B;**Title** ，然後按一下「建立」。 ]****[!UICONTROL &#x200B;系統會將您重新導向至設定頁面。 在出現的[!UICONTROL 編輯元件]對話框中，提供&#x200B;**套件ID**&#x200B;並按一下&#x200B;**[!UICONTROL 確定]**。

1. 設定您的主題以使用[!DNL Adobe Fonts]組態。 在作者實例上，在主題編輯器中開啟&#x200B;**[!UICONTROL 全局主題]**。 在主題編輯器中，導覽至「主題選項&#x200B;**** ![主題選項](assets/theme-options.png) > **[!UICONTROL 設定]**」。 在&#x200B;**[!UICONTROL Adobe Fonts Configuration]**&#x200B;欄位中，選取套件，然後按一下&#x200B;**[!UICONTROL Save]**。

   新增至&#x200B;**[!UICONTROL Adobe Fonts]**&#x200B;的字型可供所有元件的&#x200B;**[!UICONTROL Text]** accordion中選取。

