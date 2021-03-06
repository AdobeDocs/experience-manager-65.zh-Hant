---
title: 建立無障礙的最適化表單
seo-title: 建立無障礙的最適化表單
description: AEM Forms提供工具，並協助您建立無障礙的最適化表單，並符合無障礙標準。
seo-description: AEM Forms提供工具，並協助您建立無障礙的最適化表單，並符合無障礙標準。
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
feature: 適用性表單
exl-id: e755159f-374f-42b8-b28b-e8864df44f9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2078'
ht-degree: 0%

---

# 建立可存取的最適化表單{#creating-accessible-adaptive-forms}

## 簡介 {#introduction}

無障礙表單是每個人都能使用的表單，包括有特殊需求的使用者。 適用性Forms包含許多增強不同功能使用者可用性的功能。 將協助工具建置至最適化表單中，不僅可讓內容的受眾盡可能廣泛，而且在必須符合協助工具標準的地理位置提供檔案時，也需要這麼做。 AEM Forms可協助表單開發人員遵守無障礙標準。

編寫最適化表單時，作者應考量下列幾點，以建立無障礙的最適化表單：

* 使用無障礙名稱和說明檢查工具(ANDI)無障礙測試工具檢查表單
* 為表單控制項提供適當標籤
* 為影像提供等效文字
* 提供足夠的顏色對比度
* 確保窗體控制項可鍵盤訪問

## 必備條件

您需要輔助工具，例如&#x200B;**可存取名稱和說明檢查器(ANDI)**，以及為修正協助工具相關問題而開發的&#x200B;**適用性表單主題**，以建立可存取的適用性表單。

### 下載並安裝協助工具測試工具

無障礙名稱和說明檢查工具(ANDI)可協助您識別及修正網頁內容中與無障礙規範相關的問題。 這是根據國土安全部Trusted Tester v5准則推薦的工具。 由美國社會保障管理部&#x200B;制定，以檢查Section 508是否符合Web內容。 工具：

* 幫助檢測網頁上&#x200B;的輔助功能問題
* 提供改善協助工具的建議&#x200B;。
* 偵測鍵盤協助工具和顏色對比問題
* 清楚識別符合標準的螢幕助讀程式內容

ANDI可與所有主要網際網路瀏覽器搭配使用。 有關配置和使用工具的詳細說明，請參閱[ANDI的文檔](https://www.ssa.gov/accessibility/andi/help/install.html)。

### 下載並安裝超便攜主題

超級海洋無障礙主題是參考主題。 有助於示範如何以最適化表單修正顏色對比和其他協助工具的相關問題。 Adobe建議根據貴組織核准的樣式，為生產環境建立自訂主題。 執行下列步驟將主題上傳至您的AEM例項：

1. 下載主題套件。
1. 在您的AEM例項上導覽至&#x200B;**[!UICONTROL Experience Manager]** > **[!UICONTROL 導覽![導覽](assets/Smock_Compass_18_N.svg) >**[!UICONTROL  Forms ]**。]**
1. 點選「**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**」。 選取並上傳x Ultramarine-Accessible-Theme.zip檔案。 它會將主題上傳至您的AEM例項。

## 讓最適化表單可供存取

您應著重於四個關鍵方面：鍵盤導覽、顏色對比、影像的有意義替代文字，以及表單控制項的適當標籤，讓最適化表單可供存取。 執行下列步驟，讓您現有的最適化表單可供存取：

### 1.套用可存取的主題並執行其他修正

將「超海洋無障礙」主題應用於現有的最適化表單。 要應用主題：

1. 開啟最適化表單以進行編輯。
1. 選取元件並點選上層圖示。 在內容功能表中，點選&#x200B;**[!UICONTROL 適用性表單容器]**，然後點選設定圖示。
1. 在屬性瀏覽器中，選擇「超海洋可訪問」主題，然後點選&#x200B;**[!UICONTROL Save]**&#x200B;表徵圖。
1. 刷新瀏覽器窗口。 主題會套用至最適化表單。

套用可存取的主題後，請執行下列其他修正。 除了無障礙主題涵蓋的協助工具修正外，這些修正也包括：

1. 在最適化表單中為標誌影像新增有意義的替代文字。

   為最適化表單範本的頁首與頁尾元件中的影像提供有意義的替代文字。 修正範本並使用它建立最適化表單時，適用性表單會繼承套用至範本頁首和頁尾的所有協助工具相關修正。  對於現有的最適化表單，請在最適化表單層級進行變更。 對最適化表單範本所做的變更不會自動流向現有的最適化表單。

1. 將包含表單名稱的標題元件新增至最適化表單。 如果您的表單設計指定了公司名稱，請為公司名稱新增個別的標題元件。

   大部分的協助工具都會通知使用者內容的階層，協助他們了解網頁的結構。 在最適化表單上為組織名稱和表單名稱文字設定不同的標題層，為這些文字提供階層結構。 此外，在每個面板和區域前面使用具有適當標題級別的文本元件來建立層次結構。

   ![如何套用標題樣式](assets/apply-style.gif)

1. 變更頁尾背景顏色，以根據協助工具標準使用適當的對比，以改善文字的可見性和可讀性。 您可以使用ANDI來尋找表單中的顏色對比問題。 此外，請勿使用非常小的字型。 小字型很難讀。

1. 將現有最適化表單中的開關和影像選擇元件更換為選擇（無線電）元件。

1. 將現有適用性表單中的數值步進器元件替換為數值盒元件。

1. 將日期輸入欄位取代為日期選擇器欄位。

1. 設定日期選擇器元件的顯示、驗證和編輯模式。 此外，還設定自訂驗證錯誤訊息。 例如，您指定了無效日期。 日期的正確格式為YYYY-MM-DD。

1. 設定日期選擇器元件的自訂協助工具文字。 例如，輸入您的出生日期。 螢幕助讀程式會閱讀這些自訂協助工具文字。

1. 最適化表單元件請使用簡短說明，而非長篇說明。 詳細說明添加幫助按鈕。 確認適用性表單沒有任何說明按鈕。

1. 將自訂協助工具文字新增至表格的所有唯讀儲存格。 同時，禁用表的所有只讀單元格。

1. 移除手寫簽名欄位（如果有的話）。 設定最適化表單以使用Adobe Sign提供順暢的數位簽署體驗。

### 2.為表單控制項提供正確的標籤{#provide-proper-labels-for-form-controls}

元件的標籤或標題可識別表單元件代表的內容。 例如，文字「名字」會告訴使用者，他們必須在文字欄位中輸入名字。 為了供螢幕閱讀器訪問，標籤以寫程式方式與表單元件相關聯。 或者，表單控制項配置有附加的輔助資訊。

螢幕助讀程式感知的標籤不一定與視覺標題相同。 在某些情況下，您可能會想要更明確地說明控制項的用途。 對於表單中的每個欄位物件，協助工具選項可用來指定螢幕助讀程式要朗讀的內容，以識別特定的表單欄位。

若要使用協助工具選項，請遵循下列步驟：

1. 選取元件，然後點選![cmppr](assets/cmppr.png)。
1. 按一下側欄中的&#x200B;**[!UICONTROL 協助工具]**&#x200B;以選擇所需的協助工具選項。

### 表單元件{#accessibility-options-in-form-components}中的協助工具選項

![表單元件中的協助工具選項](assets/accessibility-options.png)

**自訂** TextForm作者可在協助工具選項自訂文字欄位中提供內容。輔助技術（例如螢幕閱讀器）會使用此自訂文字。 在大多數情況下，使用標題設定是最佳選項。 請考慮僅在無法使用標題或簡短說明時建立自訂螢幕Reader文字。

**簡短** 說明對於大多數元件，當用戶將指針暫留在元件上時，運行時將顯示簡短說明。您可以在說明內容選項下的簡短說明欄位中設定此選項。

**** 標題使用此選項，讓AEM Forms將與表單欄位相關聯的視覺標籤作為螢幕助讀程式文字。

**** 名稱您可以在「綁定」頁簽的「名稱」欄位中指定值。名稱不能包含任何空格。

**** 無選擇無會導致已發佈表單中的表單對象沒有名稱。表單控制項不建議使用「無」設定。

>[!NOTE]
>
>* 選項按鈕和核取方塊只能有兩個協助工具選項，即自訂文字和標題。
>* 針對XFA型適用性表單，協助工具選項繼承自XDP中設定的協助工具選項。 XDP提供的工具提示會對應至「簡短說明」，而「註解」會對應至「標題」。 其他選項的運作方式。


### 3.為影像{#provide-text-equivalents-for-images}提供等效文字

影像有助於改善某些使用者的理解。 不過，對於使用螢幕助讀程式的使用者，影像會降低表單的協助工具。 如果您選擇使用影像，請為所有影像提供文字說明。

請確定文字以表單說明物件及其用途。 螢幕助讀程式在遇到影像時會讀取此替代文字。 影像必須一律指定替代文字。

選取影像元件，然後點選![cmppr](assets/cmppr.png)。 在側欄的「屬性」下，指定影像的替代文字。

![影像的替代文字](assets/image-properties.png)

### 4.提供足夠的顏色對比度{#provide-sufficient-color-contrast}

協助工具設計需要考慮其他色彩使用准則。 表單作者可以強調顯示各種表單元件，借此使用顏色來改善表單的外觀。 然而，不當使用顏色可能使不同能力的人很難或無法閱讀一種形式。

視力障礙的使用者需要文字與背景之間的高對比度來閱讀數位內容。 如果沒有足夠的對比，某個表單可能會變得很困難，甚至是不可能，讓某些使用者閱讀。

建議您使用預設的字型和背景顏色，即白色背景中的黑色內容。 如果更改預設顏色，請選擇淺色背景顏色的深色前景顏色，或者反之亦然。

請參閱[建立最適化表單的自訂主題](/help/forms/using/creating-custom-adaptive-form-themes.md) ，以取得關於變更最適化表單的顏色對比和主題的詳細資訊。

### 5.確保窗體控制項是鍵盤可訪問的{#ensure-that-form-controls-are-keyboard-accessible}

只能使用鍵盤或等效的輸入設備來完全填充可訪問的表單。 移動性降低或視力受損的用戶可能別無選擇，只能使用鍵盤，而許多可以使用滑鼠的用戶更喜歡鍵盤輸入。 通過允許使用各種輸入方法，您不僅可以建立可訪問的表單，還可以建立更適合所有用戶偏好的表單。

下列鍵盤快速鍵可在AEM Forms中使用。

| 動作 | 鍵盤快速鍵 |
|---|---|
| 通過表單向前移動游標 | 索引標籤 |
| 將游標向後移動到窗體中 | Shift+Tab鍵 |
| 移至下一個面板 | Alt+向右箭頭 |
| 移至上一個面板 | Alt+向左箭頭 |
| 重設表單中填入的資料 | Alt+R |
| 提交表單 | Alt+S |

此外，適用性Forms中的&#x200B;**[!UICONTROL 日期選擇器]**&#x200B;元件也提供各種鍵盤快速鍵。 若要啟用快捷鍵，請點選&#x200B;**[!UICONTROL 日期選擇器]**&#x200B;元件，然後點選![設定](assets/configure-icon.svg)以開啟屬性。 在&#x200B;**[!UICONTROL 模式]**&#x200B;部分，使用&#x200B;**[!UICONTROL Type]**&#x200B;和&#x200B;**[!UICONTROL 模式]**&#x200B;下拉清單選擇顯示模式。 保存屬性以啟用&#x200B;**[!UICONTROL 日期選擇器]**&#x200B;元件的快捷鍵的使用。

下列鍵盤快速鍵適用於適用性Forms中的日期選取器元件：

| 動作 | 鍵盤快速鍵 |
|---|---|
| <ul><li>當索引標籤焦點反白標示日曆圖示時，顯示「日期選取器」元件選項</li><li>當索引標籤焦點反白標示選項時，執行點按事件</li> | 空格或Enter |
| 隱藏日期選擇器元件選項 | Esc |
| <ul><li>在「日期選擇器」元件中可用的選項中將游標向前移動。</li><li>日期輸入欄位生效時，將索引標籤焦點設定在日曆圖示上</li> | 索引標籤 |
| 在日期選擇器元件中可用的選項中向後移動游標 | Shift+Tab鍵 |
| <ul><li>當索引標籤焦點反白標示日期輸入欄位時，顯示日期選擇器元件選項</li><li>在日期選擇器元件中可用的日曆中向下移動游標</li> | 向下箭頭 |
| 在「日期選擇器」元件中可用的日曆中，將游標上移 | 向上鍵 |
| 在「日期選擇器」元件中可用的日曆中向後移動游標 | 左箭頭 |
| 在日期選擇器元件中可用的日曆中將游標向前移動 | 向右鍵 |
| 對日曆中右和左導航箭頭之間的可用標題執行操作 | Shift +向上鍵 |
| 對日曆中可用的右導航箭頭表徵圖![右箭頭](assets/right-navigation-icon.svg)執行操作 | Shift +向左鍵 |
| 對日曆中可用的左導航箭頭表徵圖![左箭頭](assets/left-navigation-icon.svg)執行操作 | Shift +向右鍵 |

## 使用協助工具來尋找剩餘的協助工具問題

無障礙名稱和說明檢查工具(ANDI)可協助您以最適化表單識別及修正無障礙法規遵循問題。 若要使用ANDI工具在最適化表單中找出協助工具問題：

1. 在預覽模式中開啟最適化表單。
1. 按一下已建立書籤的ANDI工具圖示。 ANDI工具會分析最適化表單並顯示協助工具問題。 如需如何使用工具的詳細資訊，請參閱[ANDI的檔案](https://www.ssa.gov/accessibility/andi/help/howtouse.html)。
1. 檢閱並修正ANDI回報的問題。
