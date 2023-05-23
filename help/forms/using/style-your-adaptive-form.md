---
title: 設定自適應窗體的樣式
seo-title: Style your adaptive form
description: 學習建立自定義主題、設定單個元件的樣式，以及在主題中使用Web字型
seo-description: Learn to create a custom theme, style individual components, and use web fonts in a theme
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 8%

---

# 設定自適應窗體的樣式 {#do-not-publish-style-your-adaptive-form}

學習建立自定義主題、設定單個元件的樣式，以及在主題中使用Web字型

![](do-not-localize/08-style_your_adaptiveformmain.png)

本教程是 [建立第一個自適應窗體](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

## 關於教程  {#about-the-tutorial}

可以使用主題為自適應表單提供獨特的外觀和樣式。 您可以應用自適應表單編輯器提供的框外主題，或建立自己的自定義主題。 AEM [!DNL Forms] 提供 [主題編輯器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) 的子菜單。 單個主題可以為在移動、平板或案頭上開啟的相同自適應表單提供不同的外觀。 使用主題編輯器不需要任何有關CSS或LESS的先前知識，但是需要它。

在本教程結束時，您將學習：

* 將現成主題應用於自適應窗體
* 使用主題編輯器為自適應窗體建立主題
* 設定單個元件的樣式
* 附加部分：在自定義主題中使用Web字型

完成本教程後，該表單將如下所示：

![具有自定義主題的窗體](assets/styled-adaptive-form.png)

## 開始之前 {#before-you-start}

下載本地電腦上的標題樣式和徽標影像（如下所示）。 標題 `shipping-address-add-update-form` 自適應表單使用頁眉樣式和徽標影像。 頁眉樣式影像顯示在頁眉的右側。

[取得檔案](assets/header-style.png)

[取得檔案](assets/logo-1.png)

## 步驟1:將主題應用於自適應窗體 {#step-apply-a-theme-to-your-adaptive-form}

自適應表單編輯器提供多個現成主題。 如果您計畫不為自適應表單使用自定義樣式，您還可以發佈具有現成主題的自適應表單。 主題與自適應形式無關。 可以將同一主題應用於多個自適應表單。 要將主題應用於自適應表單，請執行以下操作：

1. 開啟自適應表單進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 開啟屬性 **[!UICONTROL 自適應窗體容器]**。 在屬性瀏覽器中，導航到 **[!UICONTROL 基本]** > **[!UICONTROL 自適應窗體主題]**。 的 **[!UICONTROL 自適應窗體主題]** 欄位列出了所有預置主題和自定義主題。 預設情況下，將應用畫布主題。
1. 從 **[!UICONTROL 自適應窗體主題]** 的子菜單。 比如說， **調查主題**。 點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 按鈕。

   ![具有預設主題的自適應窗體](assets/default-adaptive-form.png)

   **圖：** *具有預設主題的自適應窗體*

   ![具有調查主題的自適應窗體](assets/adaptive-form-with-survey-theme.png)

   **圖：** *具有調查主題的自適應窗體*

## 步驟2:更新自適應表單 {#step-update-your-adaptive-form}

上面顯示的設計要求更改現有自適應表單的佔位符文本和徽標。 執行以下步驟進行所需的更改：

1. 更改頁眉的現有徽標和文本。 要刪除徽標：

   1. 在窗體編輯器中開啟窗體。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 點擊中的徽標影像 [!UICONTROL 標題] 元件和抽頭 ![招商](assets/cmppr.png) **[!UICONTROL 屬性]**。 在 [!UICONTROL 影像] 屬性，按一下X刪除現有徽標影像。
   1. 點擊 **[!UICONTROL 上載]**，選擇logo.png，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 的子菜單。 映像已下載到 [開始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start) 的子菜單。
   1. 點擊標題文本， `We.Retail`，然後點擊 ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL 編輯]**。 將標題文本更改為 `we retail`。 僅將粗體格式應用於 `we`在 `we retail`。

      ![我們零售 — 標識 — 文本](assets/we-retail-logo-text.png)

1. 刪除標題並添加佔位符文本：

   1. 按一下「Customer ID（客戶ID）」欄位，然後按一下 ![招商](assets/cmppr.png) 屬性。
   1. 複製 **[!UICONTROL 標題]** 的 **[!UICONTROL 佔位符文本]** 的子菜單。
   1. 刪除 **[!UICONTROL 標題]** 欄位和攻擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
   1. 對表單中的所有文本框、數字框和電子郵件欄位重複前三步。

      ![更新自適應形式](assets/updated-adaptive-form.png)

## 第3步：為自適應表單建立自定義主題 {#step-create-a-custom-theme-for-your-adaptive-form}

您可以使用 [主題編輯器](/help/forms/using/themes.md) 的子菜單。 主題編輯器是功能強大的WYSIWYG編輯器。 將CSS應用於自適應表單的各個元件是一種可視化方法。 它為自適應形式的樣式元件和面板提供了更精細的控制項。

主題是獨立的實體，如自適應表單。 它包含自適應窗體元件和面板的樣式(CSS)。 樣式包括CSS屬性，如背景顏色、狀態顏色、透明度、對齊方式和大小。 應用主題時，指定的樣式將應用於自適應表單的相應元件。

在本教程中，您將設定頁眉和頁腳、文本和數字元件、附件元件和按鈕的樣式。 讓我們從建立主題開始：

### 建立主題 {#create-a-theme}

1. 登錄到作AEM者實例並導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。 預設URL為 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)。
1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 主題]**。 的 [!UICONTROL 建立主題] 的子菜單。 的 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]** 欄位為必填項：

   * **標題：** 指定主題的標題。 比如說， **全球主題。** 標題可幫助您從主題清單中確定主題。
   * **名稱：** 指定主題的名稱。 比如說， **全球主題。** 在儲存庫中建立具有指定名稱的節點。 開始鍵入標題時，將自動生成名稱欄位的值。 您可以更改建議的值。 名稱欄位只能包含字母數字字元、連字元和下划線。 所有無效輸入都用連字元替換。

1. 點擊 **[!UICONTROL 建立]**。 將建立主題，並出現一個對話框以開啟表單進行編輯。 點擊 **[!UICONTROL 開啟]** 的子菜單。 主題在主題編輯器中開啟。 對於樣式，主題編輯器使用隨附的現成自適應表AEM單 [!DNL Forms]。

   有關使用主題編輯器UI的資訊，請參見 [關於主題編輯器](/help/forms/using/themes.md#aboutthethemeeditor)。

1. 點擊 **[!UICONTROL 主題選項]** ![主題選項](assets/theme-options.png) > **[!UICONTROL 配置]**。 在 **[!UICONTROL 預覽窗體]** ，選擇 **裝運地址 — 添加 — 更新 — 表單** 自適應窗體，點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)按一下 **[!UICONTROL 保存]**。 現在，主題編輯器已配置為使用您自己的自適應窗體，而不是預設的自適應窗體。 點擊 **[!UICONTROL 取消]** 按鈕。

   ![自定義主題](assets/custom-theme.png)

   **圖：** *帶有shipping-address-add-update-form自適應表單的主題編輯器*

   ![建立主題](assets/create-a-theme.png)

   **圖：** *具有預設窗體的自適應窗體*

### 樣式頁眉和頁腳 {#style-header-and-footer}

頁眉和頁腳為自適應表單提供了一致且獨特的外觀。 通常，頁眉包含組織的徽標和名稱，頁腳包含版權資訊，並且這些資訊在組織的多種形式中保持不變。 要設定shipping-address-add-update-form自適應表單的頁眉和頁腳的樣式，請執行以下操作：

1. 導航 **[!UICONTROL 標題]** > **[!UICONTROL 文本]** 選項。 「選擇器」面板位於主題編輯器的左側。 如果面板不可見，請點擊 ![切換側面板](assets/toggle-side-panel.png) 切換側面板。

1. 在 **[!UICONTROL 文本]** 手風琴和點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 字型系列 | Arial |
   | 字型色彩 | FFFFFF |
   | 字型大小 | 54px |

1. 點擊 [!UICONTROL 標題] 小部件和點擊 **[!UICONTROL 標題]**。 標題小部件的樣式選項顯示在左側。 展開 **[!UICONTROL Dimension和職位]** 手風琴，設定 **[!UICONTROL 高度]** 至 `120px`，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 展開 **[!UICONTROL 背景]** 標題小部件的折疊面，設定 **[!UICONTROL 背景顏色]** 至 `F6921E.`

   懸停於 **[!UICONTROL 影像和漸變]** > **[!UICONTROL +添加]**&#x200B;按一下 **[!UICONTROL 影像]**。 設定以下屬性並點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 影像 | 上載header-style.png。 映像已下載到 [開始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start) 的子菜單。 |
   | 位置 | 右下 |
   | 並排顯示 | 不重複 |

1. 在主題編輯器中，點擊標題中的徽標，然後點擊 **[!UICONTROL 標題徽標]**。 展開Dimension和位置折疊面板，設定以下屬性並點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
       </ul> <p><strong>提示：</strong> 點擊 <img src="assets/link.png"> 連結表徵圖，為每個欄位提供不同的值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. 點擊頁腳構件並點擊 **[!UICONTROL 頁腳]**。 展開 **[!UICONTROL 背景]** 手風琴，設定 **[!UICONTROL 背景顏色]** 至 `F6921E`，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

### 設定資料捕獲元件的樣式，並將背景應用於自適應窗體 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在自適應表單中使用多個元件來捕獲資料。 例如，文本框和數字框。 可以為所有資料捕獲元件提供相同的樣式，或為每個元件提供單獨的樣式。 在本教程中，相同的樣式應用於數字框（客戶ID、郵遞區號）和文本框（客戶ID、名稱、發運地址、狀態、電子郵件）。 要設定資料捕獲元件的樣式：

1. 點擊 **[!UICONTROL 客戶ID]** 點擊 **[!UICONTROL 域小部件]** 的雙曲餘切值。 設定以下屬性並點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
      <td>Dimension和職位</td> 
      <td>寬度</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension和職位</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>左：10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 點擊上方的空區域 **[!UICONTROL 客戶ID]** 欄位和攻擊 **[!UICONTROL 響應面板容器]**。 設定 **[!UICONTROL 背景]** > **[!UICONTROL 背景顏色]** 到F1F2F2。 點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   ![](do-not-localize/responsive-panel-container.png)

### 設定按鈕的樣式 {#style-the-buttons}

可以使用自定義主題將相同的樣式應用於自適應窗體和 [內聯樣式](/help/forms/using/inline-style-adaptive-forms.md) 按鈕。 要設定按鈕的樣式：

1. 點擊 **[!UICONTROL 提交]** 按鈕 **[!UICONTROL 按鈕]** 的雙曲餘切值。 設定以下屬性並點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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

1. [應用自定義主題](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)的子菜單。 如果樣式未反映在自適應表單上，請清除瀏覽器快取，然後重試。

   ![樣式資料捕獲元件](assets/style-data-capture-components.png)

## 第4步：設定單個元件的樣式 {#step-style-individual-components}

某些樣式只適用於特定元件。 這些元件在自適應表單編輯器中設定樣式。

1. 開啟自適應表單進行編輯。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在頂欄上，選擇 **[!UICONTROL 樣式]** 的雙曲餘切值。

   ![樣式選項](assets/style-option.png)

1. 點擊 **[!UICONTROL 附加]** 按鈕 ![aem_6_3_edit](assets/aem_6_3_edit.png)表徵圖 在 **[!UICONTROL Dimension和職位]** 手風琴：

   | 屬性 | 值 |
   |---|---|
   | 浮動 | 左 |
   | 寬度 | 10% |

1. 點擊 **[!UICONTROL 政府批准的地址證明]** 選項並點擊 ![aem_6_3_edit](assets/aem_6_3_edit.png)表徵圖 設定以下屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>浮動</td> 
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

1. 點擊 **[!UICONTROL 提交]** 按鈕 ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖 設定以下屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊式面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>Dimension和職位</td> 
      <td>浮動</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>Dimension和職位</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>頂部：5rem</li> 
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

   ![自適應形式–1](assets/styled-adaptive-form-1.png)

## 第5步：附加部分：在自定義主題中使用Web字型 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

可以使用各種字型來設計自適應表單。 查看自適應表單的所有設備可能沒有用於設計自適應表單的字型。 您可以使用Web字型服務將所需字型傳送到目標設備。

[!DNL Adobe Fonts] 是web字型服務。 可以配置和使用具有自適應表單的服務。 要使用 [!DNL Adobe Fonts] 格式：

>[!NOTE]
>
>![typekit到adobe字型](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] 現在稱為Adobe Fonts，並包含在Creative Cloud和其他訂閱中。 [深入了解](https://fonts.adobe.com/).

1. 建立 [Adobe Fonts](https://typekit.com/) 帳戶、建立套件、將字型MyriadPro添加到套件、發佈套件並獲取套件ID。 需要使用 [!DNL Adobe Fonts] （Web字型）。
1. 在AEM [!DNL Forms] 伺服器，導航至 ![adobeexperience manager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**。 現在，開啟配置資料夾。 如果配置已可用，請按一下 **[!UICONTROL 建立]** 的子菜單。

   在「建立配置」對話框中，指定 **標題** ，然後按一下 **[!UICONTROL 建立]**。 您被重定向到配置頁面。 在 [!UICONTROL 編輯元件] 對話框，提供 **套件ID** 按一下 **[!UICONTROL 確定]**。

1. 配置主題以使用 [!DNL Adobe Fonts] 配置。 在作者案例上，開啟 **[!UICONTROL 全球主題]** 的子菜單。 在主題編輯器中，導航到 **[!UICONTROL 主題選項]** ![主題選項](assets/theme-options.png) > **[!UICONTROL 配置]**。 在 **[!UICONTROL Adobe Fonts配置]** ，選擇工具包，然後按一下 **[!UICONTROL 保存]**。

   添加到 **[!UICONTROL Adobe Fonts]** 可供選擇 **[!UICONTROL 文本]** 所有部件的手風琴。
