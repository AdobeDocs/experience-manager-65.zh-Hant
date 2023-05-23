---
title: HTML5表單的常見問題(FAQ)
seo-title: Frequently asked questions (FAQ) for HTML5 forms
description: 有關HTML5表單的佈局、指令碼支援和範圍的常見問題(FAQ)。
seo-description: Frequently Asked Questions (FAQ) about layout, scripting support, and scope of HTML5 forms.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: Mobile Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: 99c9eddad7a2ec7eb23b3c374a1c0e65e141da20
workflow-type: tm+mt
source-wordcount: '2005'
ht-degree: 0%

---


# HTML5表單的常見問題(FAQ){#frequently-asked-questions-faq-for-html-forms}

有關HTML5表單的佈局、指令碼支援和範圍的常見問題(FAQ)。

## 配置 {#layout}

1. 為什麼條形碼和簽名欄位不出現在我的表單中？

   答案：條形碼和簽名欄位與HTML或移動方案無關。 這些欄位顯示為非交互區域。 但是，AEM Forms設計器提供了一個新的簽名Scribble欄位，可以使用該欄位代替簽名欄位。 也可以添加 [自定義小部件](../../forms/using/custom-widgets.md) 條形碼並整合。

1. XFA文本欄位是否支援RTF?

   答案：XFA欄位不支援在AEM Forms設計器中允許豐富內容，它以普通文本形式呈現，而不支援通過用戶介面設定文本的樣式。 同時，具有梳狀屬性的XFA欄位被顯示為正常欄位，儘管基於梳狀數字的值仍對允許的字元數有限制。

1. 使用可重複子表單是否存在任何限制？

   答案：可重複子表單的初始計數應為1或更多。 不支援初始計數為零的可重複子表單。 您也可以選擇使用可重複的子表單，並且在載入表單時不顯示它。 要實現使用案例：

   1. 將可重複子窗體的初始計數設定為1。

      ![初數](assets/intial-count.png)

   1. 使用表單的初始化事件隱藏子表單的主實例。 例如，下面的代碼在表單初始化時隱藏子表單的主實例。 它還驗證應用類型以確保指令碼僅在客戶端執行：

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 開啟用於添加子表單實例以進行編輯的指令碼。 添加如下代碼以添加子表單指令碼的實例。

      下面的代碼檢查子窗體的隱藏實例。 如果找到子表單的隱藏實例，請刪除子表單的隱藏實例並插入子表單的新實例。 如果找不到子表單的隱藏實例，則只需插入子表單的新實例即可。

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. 開啟用於刪除子表單實例以進行編輯的指令碼。 添加如下代碼以刪除子表單指令碼的實例。

      代碼檢查子表單的計數。 如果子表單的計數達到1，則代碼將隱藏子表單，而不是刪除子表單。

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 開啟表單的預提交事件進行編輯。 將以下指令碼添加到事件中，以便在編輯前刪除指令碼的隱藏實例。 它防止在提交時發送隱藏子窗體的資料。

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 使用隱藏子表單是否存在任何限制？

   答案：具有跨頁拆分的複雜層次結構的隱藏子窗體會導致佈局問題。 解決方法是將子表單標籤為初始可見，然後根據某些邏輯或資料在初始化指令碼中隱藏。

1. 為什麼某些文本被截斷或在HTML5中顯示不正確？

   答案：如果未給「繪圖」或「字幕」文本元素足夠的空間來顯示內容，則文本將以移動表單格式副本顯示為截斷。 此截斷在AEM Forms設計器的「設計」視圖中也可見。 雖然此截斷可以在PDF中處理，但不能在HTML5窗體中處理。 為避免此問題，請提供足夠的空間來繪製或字幕文本，以便它不會在AEM Forms設計器的設計模式中截斷。

1. 我正在觀察與缺少內容或內容重疊相關的佈局問題。 原因何在？

   答案：如果在同一位置有「繪製文本」或「繪製影像」元素以及另一個重疊元素（如「矩形」），則如果「繪製文本」內容稍後以文檔順序出現(在「AEM Forms設計器層次結構」視圖中)，則不可見。 PDF支援透明分層，但HTML/瀏覽器不支援透明分層。

1. 為什麼HTML窗體中顯示的某些字型與設計窗體時使用的字型不同？

   答案：HTML5Forms不允許嵌入字型(與字型嵌入表單中的PDF forms形式相反)。 對於要按預期呈現的表單的HTML版本，請確保字型在AEM Forms伺服器的CRX儲存庫(AEM內容儲存庫)和安裝了設計器的電腦AEM中可用。 當字型在AEM Forms伺服器的CRX資料庫或安裝設計器的位AEM置不可用時，將使用回退字型呈現表單。

1. vAlign和hAlign屬性是否在HTML表單中受支援？

   答案：是，支援vAlign和hAlign屬性。 Internet Explorer和多行欄位中不支援vAlign屬性。

1. HTML5表單是否支援希伯來文字元？

   答案：HTML5表單支援除MicrosoftInternet Explorer外的所有瀏覽器中的希伯來字元。

1. HTML5表單對數字欄位有任何限制嗎？

   答案：是的，HTML5表格有一些限制。 如果數字數大於圖片子句中指定的計數，則數字不會本地化，並以英語區域設定顯示。

1. 為什麼HTML形式比PDF forms大？

   答案：要將XDP呈現到HTML窗體，需要許多中間資料結構和對象，如窗體dom、資料dom和佈局dom。

   對於PDF forms,Adobe Acrobat有一個內置的XTG引擎來建立中間資料結構和對象。 Acrobat還負責佈局和指令碼。

   對於HTML5表單，瀏覽器沒有內置的XTG引擎來建立中間資料結構和來自原始XDP位元組的對象。 因此，對於HTML5表單，在伺服器上生成中間結構併發送到客戶端。 在客戶端，基於JavaScript的指令碼和佈局引擎使用這些中間結構。

   中間結構的大小取決於原始XDP的大小以及與XDP合併的資料。

1. 在我的xdp中使用表有任何限制嗎？

   答案：複雜表在呈現中導致問題。

   * 不支援表內的Section(SubformSet)。
   * 某些表中的頁眉或頁腳行被標籤為重複。 跨多頁拆分此類表可能會遇到一些問題。

1. 可訪問的表有任何限制嗎？

   答案：是，可訪問的表具有以下限制：

   * 不支援表內的嵌套表和子表單。
   * 表的頂行或左列僅支援標題。 中間表元素不支援標頭。 如果所有此類行和列都與表的最頂部行或最左側列一起，則可以將標題應用於多個行和列標題。
   * `Rowspan`和 `colspan`不支援從表內的隨機位置。

   * 不能動態添加或刪除包含行範圍值大於1的元素的行實例。

1. 螢幕閱讀器的工具提示和標題的閱讀順序是什麼？

   答案:
   * 如果同時存在標題和工具提示，則只讀取標題。 如果標題不可用，則讀取工具提示。 也可以使用表單設計器指定XDP中讀取的優先順序
   * 懸停元素時，將顯示工具提示。 如果工具提示不可用，則顯示語音文本。 如果語音文本不可用，則顯示欄位名稱。

1. 懸停欄位時，將顯示工具提示。 如何禁用它？

   答案：要在懸停時禁用工具提示，請在設計器的輔助功能面板中選擇「無」。

1. 在設計器中，用戶可以配置單選按鈕和複選框的自定義外觀屬性。 是否，在呈現表單時，HTML5表單會考慮此類自定義外觀屬性？

   答案：HTML5表單忽略單選按鈕和複選框的自定義外觀屬性。 單選按鈕和複選框按基礎瀏覽器的規範顯示。

1. 當在支援的瀏覽器中開啟HTML5窗體時，相鄰放置的域的邊界不正確對齊，或子窗體出現重疊。 當在Forms設計器中預覽同一HTML5窗體時，欄位和佈局不會出現不對齊，子窗體出現在正確的位置。 如何解決問題？

   答案：當子窗體設定為流內容且該子窗體具有隱藏的邊框元素時，相鄰放置的域的邊框不正確對齊或子窗體出現重疊。 要解決此問題，可刪除或注釋隱藏 &lt;border> 元素。 例如，以下 &lt;border> 元素標籤為注釋：

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 為什麼螢幕閱讀器不能正確處理日期/時間欄位對象？

   答案：螢幕閱讀器不支援日期/時間欄位。 但是，您可以手動在欄位中輸入日期/時間，以使螢幕閱讀器讀取。 使用工具提示或螢幕閱讀器文本指示用戶手動選擇欄位的日期/時間。

1. HTML5是否支援浮動欄位的顯示模式？

   答案：HTML5窗體不支援浮動欄位的顯示圖案。

1. FormsHTML5中「日期」欄位的格式是什麼？

答案：「日期」欄位接受ISO格式YYYY-MM-DD。 如果以其他格式指定日期，則「日期欄位」在用戶頁籤離開該欄位之前不接受格式設定。

### 指令碼 {#scripting}

1. JavaScript實現中對HTMLForms有任何限制嗎？

   答案:

   * 對xfa.connectionSet指令碼的支援有限。 對於connectionSet，僅支援Web服務的伺服器端調用。 有關詳細資訊，請參見 [指令碼支援](/help/forms/using/scripting-support.md)。
   * 客戶端指令碼中不支援$record和$data。 但是，如果指令碼以formReady、layoutReady塊編寫，則指令碼仍然有效，因為這些事件在伺服器端運行。
   * 不支援XFA繪圖元素特定的指令碼，如更改繪圖文本（或欄位情況下的標題文本）。

1. 使用formCalc有任何限制嗎？

   答案：當前僅實現formCalc指令碼的子集。 有關詳細資訊，請參見 [指令碼支援](/help/forms/using/scripting-support.md)。

1. 是否存在任何推薦的命名約定，以及是否存在任何要避免的保留關鍵字？

   答案:
   * 在AEM Forms設計器中，建議不要以下划線(_)。 要在名稱的開頭使用下划線，請在下划線後面添加前置詞，_&lt;prefix>&lt;objectname>。
   * 所有HTML5表單API都是保留關鍵字。 對於自定義API/函式，請使用與 [HTML5表單API](/help/forms/using/scripting-support.md)。

1. HTML5是否支援浮動欄位？

   答案：是的，HTML5號Forms支援浮地。 要啟用浮動欄位，請將以下屬性添加到渲染配置檔案：

   >[!NOTE]
   >
   >預設情況下，不為浮動啟用欄位。 可以使用Forms設計器設定欄位的浮動屬性。

   1. 開啟CRXde lite並導航到 `/content/xfaforms/profiles/default` 的下界。
   1. 添加屬性 `mfDataDependentFloatingField`類型字串，並將屬性值設定為 `true`。
   1. 按一下 **全部保存**。 現在，使用更新的渲染配置檔案為HTMLForms啟用浮動欄位。

      >[!NOTE]
      >
      >要在不更新呈現配置檔案的情況下為特定表單啟用浮動欄位，請將mfDataDependentFloatingField=true屬性作為URL參數傳遞。

1. HTML5表單是否多次執行初始化指令碼和表單就緒事件？

   答案：可以，初始化指令碼和表單就緒事件將多次執行，至少一次在伺服器上執行，一次在客戶端執行。 建議根據某些業務邏輯（表單或欄位資料）編寫諸如初始化或表單：就緒事件之類的指令碼，以便根據資料和冪等元的狀態（如果資料相同）執行該操作。

### 設計XDP {#designing-xdp}

1. HTML5窗體中是否有保留的關鍵字？

   答案：所有HTML5表單API都是保留關鍵字。 對於自定義API/函式，請使用與 [HTML5表單API](/help/forms/using/scripting-support.md)。 除保留關鍵字外，如果使用以下划線(_)開頭的對象名稱，建議在下划線之後添加唯一前置詞。 添加前置詞有助於避免與HTML5表單內部API發生任何可能的衝突。 例如 `_fpField1`
