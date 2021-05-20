---
title: '設定最適化表單的樣式 '
seo-title: '設定最適化表單的樣式 '
description: '了解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用網頁字型 '
seo-description: '了解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用網頁字型 '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: 適用性表單
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 8%

---

# 設定最適化表單的樣式{#do-not-publish-style-your-adaptive-form}

了解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用網頁字型

![](do-not-localize/08-style_your_adaptiveformmain.png)

本教學課程是[建立第一個最適化表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程{#about-the-tutorial}

您可以使用主題為最適化表單提供獨特的外觀和樣式。 您可以套用最適化表單編輯器隨附的現成主題，或建立您自己的自訂主題。 AEM [!DNL Forms]提供[主題編輯器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)以建立自訂主題。 單一主題可為在行動裝置、平板電腦或桌上型電腦上開啟的相同最適化表單提供不同的外觀。 使用主題編輯器不需要任何先前的CSS或LESS知識，但需要它。

在教學課程結束前，您將學習：

* 將現成可用的主題套用至最適化表單
* 使用主題編輯器建立最適化表單的主題
* 設定個別元件的樣式
* 附加部分：在自訂主題中使用網頁字型

完成本教學課程後，表單看起來會類似下列：

![具有自訂主題的表單](assets/styled-adaptive-form.png)

## 開始之前{#before-you-start}

在您的本機電腦上下載標題樣式和標誌影像（如下所示）。 `shipping-address-add-update-form`最適化表單的標題使用標題樣式和標誌影像。 標題樣式影像會顯示在標題的右側。

[取得檔案](assets/header-style.png)

[取得檔案](assets/logo-1.png)

## 步驟1:將主題套用至最適化表單{#step-apply-a-theme-to-your-adaptive-form}

適用性表單編輯器提供多種現成可用的主題。 如果您不想針對最適化表單使用自訂樣式，也可以使用現成可用的主題發佈最適化表單。 主題與最適化表單無關。 您可以將相同的主題套用至多個最適化表單。 若要將主題套用至最適化表單：

1. 開啟最適化表單以進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 開啟&#x200B;**[!UICONTROL 適用性表單容器]**&#x200B;的屬性。 在屬性瀏覽器中，導覽至&#x200B;**[!UICONTROL Basic]** > **[!UICONTROL 適用性表單主題]**。 **[!UICONTROL 適用性表單主題]**&#x200B;欄位會列出所有現成可用和自訂主題。 依預設，會套用畫布主題。
1. 從&#x200B;**[!UICONTROL 適用性表單主題]**&#x200B;欄位中選取主題。 例如，**調查主題**。 點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以套用選取的主題。

   ![具有預設主題的最適化表單](assets/default-adaptive-form.png)

   **圖：** *具有預設主題的最適化表單*

   ![具有調查主題的最適化表單](assets/adaptive-form-with-survey-theme.png)

   **圖：** *具有調查主題的最適化表單*

## 步驟2:更新最適化表單{#step-update-your-adaptive-form}

上方顯示的設計需要變更現有最適化表單的預留位置文字和標誌。 執行下列步驟以進行所需的變更：

1. 變更標題的現有標誌和文字。 要刪除徽標，請執行以下操作：

   1. 在表單編輯器中開啟表單。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 點選[!UICONTROL header]元件中的標誌影像，然後點選![cmppr](assets/cmppr.png) **[!UICONTROL properties]**。 在[!UICONTROL image]屬性中，點選X以移除現有的標誌影像。
   1. 點選&#x200B;**[!UICONTROL upload]**，選取logo.png，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以儲存變更。 影像下載於[開始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start)區段。
   1. 點選標題文字`We.Retail`，然後點選![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**。 將標題文本更改為`we retail`。 僅對`we retail`中的`we`應用粗體格式。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 移除標題並新增預留位置文字：

   1. 點選「客戶ID」欄位，然後點選![cmppr](assets/cmppr.png)屬性。
   1. 將&#x200B;**[!UICONTROL Title]**&#x200B;欄位的內容複製到&#x200B;**[!UICONTROL 預留位置文字]**&#x200B;欄位。
   1. 刪除&#x200B;**[!UICONTROL Title]**&#x200B;欄位的內容，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
   1. 對表單中的所有文本框、數值框和電子郵件欄位重複前三個步驟。

      ![更新的adaptive-form](assets/updated-adaptive-form.png)

## 步驟3:為最適化表單建立自訂主題{#step-create-a-custom-theme-for-your-adaptive-form}

您可以使用[主題編輯器](/help/forms/using/themes.md)建立自訂主題。 主題編輯器是功能全面的WYSIWYG編輯器。 將CSS套用至最適化表單的各種元件是視覺化方法。 它提供更精細的控制項，以設定最適化表單的元件和面板的樣式。

主題是獨立的實體，例如最適化表單。 其中包含最適化表單的元件和面板的樣式(CSS)。 樣式包含CSS屬性，例如背景顏色、狀態顏色、透明度、對齊方式和大小。 套用主題時，指定的樣式會套用至最適化表單的對應元件。

在本教學課程中，您將對頁首和頁尾、文本和數字元件、附件元件和按鈕進行樣式設定。 讓我們從建立主題開始：

### 建立主題{#create-a-theme}

1. 登入AEM製作例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。 預設URL為[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)。
1. 點選&#x200B;**[!UICONTROL 建立]**&#x200B;並選取&#x200B;**[!UICONTROL 主題]**。 此時將顯示[!UICONTROL 建立主題]頁，其中包含建立主題所需的欄位。 **[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**&#x200B;欄位是必填欄位：

   * **標題：** 指定主題的標題。例如， **全域主題。** 標題可協助您從主題清單中識別主題。
   * **名稱：** 指定主題的名稱。例如， **Global-Theme。** 在儲存庫中建立具有指定名稱的節點。當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。

1. 點選&#x200B;**[!UICONTROL 建立]**。 會建立主題，並出現一個對話框以開啟表單進行編輯。 點選&#x200B;**[!UICONTROL 開啟]**&#x200B;以在新索引標籤中開啟新建立的主題。 主題編輯器開啟。 對於樣式，主題編輯器使用AEM [!DNL Forms]隨附的現成可用最適化表單。

   有關使用主題編輯器UI的資訊，請參閱[關於主題編輯器](/help/forms/using/themes.md#aboutthethemeeditor)。

1. 點選&#x200B;**[!UICONTROL 主題選項]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 設定]**。 在&#x200B;**[!UICONTROL 預覽表單]**&#x200B;欄位中，選取&#x200B;**shipping-address-add-update-form**&#x200B;適用性表單，點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，點選&#x200B;**[!UICONTROL Save]**。 現在，主題編輯器已設定為使用您自己的最適化表單，而非預設的最適化表單。 點選&#x200B;**[!UICONTROL 取消]**&#x200B;以返回主題編輯器。

   ![自訂主題](assets/custom-theme.png)

   **圖：** *主題編輯器，包含裝運地址 — add-update-form適用性表單*

   ![建立主題](assets/create-a-theme.png)

   **圖：** *具有預設表單的最適化表單*

### 樣式頁眉和頁腳{#style-header-and-footer}

頁首與頁尾為最適化表單提供一致且獨特的外觀。 一般而言，頁首包含組織的標誌和名稱，頁尾包含版權資訊，且這些資訊在組織的多種形式中保持不變。 要設定發運地址 — add-update-form適用性表單的頁眉和頁腳的樣式，請執行以下操作：

1. 導覽「選取器」面板中的&#x200B;**[!UICONTROL Header]** > **[!UICONTROL Text]**&#x200B;選項。 「選取器」面板位於主題編輯器的左側。 如果面板不可見，請點選「![切換側面板](assets/toggle-side-panel.png)切換側面板」。

1. 在&#x200B;**[!UICONTROL Text]**&#x200B;折疊式功能表中設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 字型系列 | Arial |
   | 字型色彩 | FFFFFF |
   | 字型大小 | 54px |

1. 點選[!UICONTROL 標題]介面工具集，然後點選&#x200B;**[!UICONTROL 標題]**。 設定標題Widget樣式的選項會顯示在左側。 展開&#x200B;**[!UICONTROL 「Dimension與位置」]**&#x200B;折疊式功能表，將&#x200B;**[!UICONTROL Height]**&#x200B;設為`120px`，然後點選![aem6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 展開標題Widget的&#x200B;**[!UICONTROL Background]**&#x200B;折疊式功能表，將&#x200B;**[!UICONTROL Background Color]**&#x200B;設定為`F6921E.`

   暫留在「**[!UICONTROL 影像和漸層」上，點選「**[!UICONTROL &#x200B;影像&#x200B;]**」>「**[!UICONTROL +新增」，點選「]**影像]**」。 設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 影像 | 上傳header-style.png。 影像下載於[開始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start)區段。 |
   | 位置 | 右下 |
   | 並排顯示 | 不重複 |

1. 在主題編輯器中，點選標題中的標誌，然後點選&#x200B;**[!UICONTROL 標題標誌]**。 展開「Dimension與位置」設定追蹤器，設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
        <li>排名在前：1.5rem</li> 
        <li>底部：-35px</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>提示：</strong> 點選連 <img src="assets/link.png"> 結圖示，為每個欄位提供不同值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. 點選頁尾介面工具集，然後點選&#x200B;**[!UICONTROL 頁尾]**。 展開&#x200B;**[!UICONTROL Background]**&#x200B;折疊式功能表，將&#x200B;**[!UICONTROL Background Color]**&#x200B;設定為`F6921E`，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

### 設定資料捕獲元件的樣式，並將背景應用到自適應表單{#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在最適化表單中使用多個元件來擷取資料。 例如，文字方塊和數值方塊。 您可以提供與所有資料捕獲元件相同的樣式，或為每個元件提供不同的樣式。 在本教學課程中，數值方塊（客戶ID、郵遞區號）和文字方塊（客戶ID、名稱、運送地址、狀態、電子郵件）會套用相同的樣式。 設定資料捕獲元件的樣式：

1. 點選「 **[!UICONTROL 客戶ID]**」欄位，然後點選「**[!UICONTROL 欄位Widget]**」選項。 設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
        <li>排名在前：7px<br /> </li> 
        <li>對：7px<br /> </li> 
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
      <td>Dimension和位置</td> 
      <td>寬度</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>左：10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 點選&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位上方的空白區域，然後點選&#x200B;**[!UICONTROL 回應式面板容器]**。 將&#x200B;**[!UICONTROL Background]** > **[!UICONTROL Background Color]**&#x200B;設定為F1F2F2。 點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   ![](do-not-localize/responsive-panel-container.png)

### 設定按鈕的樣式{#style-the-buttons}

您可以使用自訂主題將相同樣式套用至最適化表單的所有按鈕，並使用[內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md)將樣式套用至特定按鈕。 要設定按鈕的樣式：

1. 點選&#x200B;**[!UICONTROL 提交]**&#x200B;按鈕，然後點選&#x200B;**[!UICONTROL 按鈕]**&#x200B;選項。 設定下列屬性，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
        <li>排名在前：7px<br /> </li> 
        <li>對：7px<br /> </li> 
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

1. [將自訂主題](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)（全域主題）套用至最適化表單。如果樣式未反映在最適化表單上，請清除瀏覽器快取，然後再試一次。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 步驟4:設定單個元件的樣式{#step-style-individual-components}

某些樣式僅適用於特定元件。 這些元件在最適化表單編輯器中設定樣式。

1. 開啟最適化表單以進行編輯。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在頂端列上，選取&#x200B;**[!UICONTROL 樣式]**&#x200B;選項。

   ![樣式選項](assets/style-option.png)

1. 點選&#x200B;**[!UICONTROL Attach]**&#x200B;按鈕，然後點選![aem_6_3_edit](assets/aem_6_3_edit.png)圖示。 在&#x200B;**[!UICONTROL Dimension和位置]**&#x200B;折疊式功能表中設定以下屬性：

   | 屬性 | 值 |
   |---|---|
   | 浮點數 | 左 |
   | 寬度 | 10% |

1. 點選&#x200B;**[!UICONTROL 政府核准的位址校樣]**&#x200B;選項，然後點選![aem_6_3_edit](assets/aem_6_3_edit.png)圖示。 設定下列屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>浮點數</td> 
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
        <li>對：2rem</li> 
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

1. 點選&#x200B;**[!UICONTROL Submit]**&#x200B;按鈕，然後點選![aem_6_3_edit](assets/aem_6_3_edit.png)圖示。 設定下列屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>浮點數</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>排名在前：5rem</li> 
        <li>對：14rem</li> 
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

   ![stleed-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 步驟5:附加部分：在自定義主題{#step-bonus-section-using-web-fonts-in-a-custom-theme}中使用Web字型

您可以使用各種字型來設計最適化表單。 在檢視最適化表單的所有裝置，都可能沒有設計最適化表單時使用的字型。 您可以使用Web字型服務將所需字型傳送至目標裝置。

[!DNL Adobe Fonts] 是網頁字型服務。您可以透過最適化表單來設定及使用服務。 若要在最適化表單中使用[!DNL Adobe Fonts]:

>[!NOTE]
>
>![typekit-to-adobe-fontsis現](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] 在稱為Adobe Fonts，並隨附於Creative Cloud和其他訂閱。[了解更多](https://fonts.adobe.com/).

1. 建立[Adobe Fonts](https://typekit.com/)帳戶、建立套件、將字型Myriad Pro新增至套件、發佈套件並取得套件ID。 需要在最適化表單中使用[!DNL Adobe Fonts]（Web字型）。
1. 在AEM [!DNL Forms]伺服器中，導覽至![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** ![ hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**。 現在，開啟設定資料夾。 如果配置已可用，請按一下&#x200B;**[!UICONTROL Create]**&#x200B;按鈕以建立新實例。

   在「建立配置」對話框中，為配置指定&#x200B;**標題**，然後按一下&#x200B;**[!UICONTROL 建立]**。 系統會將您重新導向至設定頁面。 在顯示的[!UICONTROL 編輯元件]對話框中，提供您的&#x200B;**套件ID**，然後按一下&#x200B;**[!UICONTROL 確定]**。

1. 配置主題以使用[!DNL Adobe Fonts]配置。 在製作例項上，開啟主題編輯器中的&#x200B;**[!UICONTROL 全域主題]**。 在主題編輯器中，導覽至「**[!UICONTROL 主題選項]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 設定]**」。 在「**[!UICONTROL Adobe Fonts配置]**」欄位中，選擇套件，然後按一下「**[!UICONTROL 保存]**」。

   新增至&#x200B;**[!UICONTROL Adobe Fonts]**&#x200B;的字型可供所有元件的&#x200B;**[!UICONTROL Text]**&#x200B;折疊式功能表中選取。
