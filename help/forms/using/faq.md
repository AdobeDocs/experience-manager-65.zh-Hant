---
title: HTML5表單的常見問題(FAQ)
seo-title: HTML5表單的常見問題(FAQ)
description: 關於HTML5表單版面配置、指令碼支援和範圍的常見問題(FAQ)。
seo-description: 關於HTML5表單版面配置、指令碼支援和範圍的常見問題(FAQ)。
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# HTML5表單的常見問題(FAQ){#frequently-asked-questions-faq-for-html-forms}

HTML5表格的版面配置、指令碼支援和範圍有一些常見問題(FAQ)。

## 配置 {#layout}

1. 為什麼條碼和簽名欄位不會出現在我的表單中？

   答案：條碼和簽名欄位與HTML或行動藍本無關。 這些欄位會顯示為非互動區域。 不過，AEM Forms Designer提供新的簽名塗鴉欄位，可供使用，而非簽名欄位。 您也可以新增條碼的 [自訂介面工具集](../../forms/using/custom-widgets.md) ，並加以整合。

1. XFA文字欄位是否支援豐富式文字？

   答案：XFA欄位不支援AEM Forms Designer中的多樣化內容，會呈現為一般文字，而不支援從使用者介面設定文字樣式。 同時，具有梳狀屬性的XFA欄位顯示為正常欄位，儘管根據梳狀數字的值仍然對允許的字元數有限制。

1. 使用可重複的子表單是否有任何限制？

   答案：可重複的子表單的初始計數應為1或更多。 不支援初始計數為零的可重複子表單。 您也可以選擇使用可重複的子表單，而不是在表單載入時顯示。 要實現使用案例：

   1. 將可重複子表單的初始計數設定為1。

      ![初計](assets/intial-count.png)

   1. 使用表單的initialize事件隱藏子表單的主實例。 例如，以下代碼在表單初始化時隱藏子表單的主實例。 此外，它還會驗證應用程式類型，以確保指令碼僅在用戶端執行：

      ```
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 開啟指令碼以新增子表單的例項以進行編輯。 新增程式碼（如下），以新增子表單指令碼的例項。

      下面的代碼檢查子表單的隱藏實例。 如果找到子表單的隱藏實例，請刪除子表單的隱藏實例，並插入新的子表單實例。 如果找不到子表單的隱藏實例，則只需插入子表單的新實例。

      ```
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

   1. 開啟用於刪除子表單實例以進行編輯的指令碼。 將下列程式碼新增至移除子表單指令碼的例項。

      程式碼會檢查子表單的計數。 如果子表單的計數達到1，程式碼會隱藏子表單，而非刪除子表單。

      ```
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 開啟表單的預先提交事件以進行編輯。 將下列指令碼新增至事件，以在編輯前移除指令碼的隱藏例項。 它可防止在提交時傳送隱藏子表單的資料。

      ```
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 使用隱藏子表單有任何限制嗎？

   答案：具有複雜階層的隱藏子表單會跨頁分割，造成版面配置問題。 因應措施是將子表單標示為一開始可見，然後根據某些邏輯或資料，在初始化指令碼中隱藏子表單。

1. 為什麼HTML5中有些文字會截斷或顯示不正確？

   答案：如果未為「繪圖」或「標題」文字元素提供足夠空間來顯示內容，則行動表單轉譯中會出現截斷的文字。 AEM Forms Designer的「設計」檢視中也會顯示此截斷。 雖然此截斷可在PDF中處理，但無法在HTML5表格中處理。 為避免此問題，請為「繪圖」或「標題文字」提供足夠的空間，以免在AEM Forms Designer的設計模式中截斷。

1. 我正在觀察與遺失內容或內容重疊相關的版面問題。 原因何在？

   答案：如果在相同位置有「繪製文字」或「繪製影像」元素以及另一個重疊元素（例如矩形），則如果「繪製文字」內容稍後以檔案順序出現（在「AEM Forms設計器階層」檢視中），則不會顯示。 PDF支援透明分層，但HTML/瀏覽器不支援透明分層。

1. 為何HTML表格中顯示的某些字型與設計表格時使用的字型不同？

   答案：HTML5表格不嵌入字型（與將字型內嵌在表格中的PDF表格不同）。 若要如預期般呈現HTML版表單，請確定XDP中指定的字型可在伺服器和用戶端機器上使用。 如果伺服器上未提供所需的字型，則會使用回傳字型。 此外，如果您在「表單範本」中使用用戶端裝置上無法使用的字型，則會使用瀏覽器的預設字型來轉換文字。

1. vAlign和hAlign屬性是否支援HTML表單？

   是的，支援vAlign和hAlign屬性。 vAlign屬性不受Internet explorer和多行欄位的支援。

1. HTML5表格是否支援希伯來文字元？

   HTML5表單支援除Microsoft Internet explorer外的所有瀏覽器中的希伯來文字元。

1. HTML5表單對數值欄位有任何限制嗎？

   答案：是的，HTML5表格有一些限制。 如果數字數大於picture子句中指定的計數，則數字不本地化，並以英語地區顯示。

1. 為什麼HTML表格大小比PDF表格大？

   將XDP轉換為HTML表單時，需要許多中介資料結構和物件，例如表單dom、資料dom和版面dom。

   對於PDF表格，Adobe Acrobat有內建的XTG引擎，可建立中介資料結構和物件。 Acrobat也會處理版面配置和指令碼。

   對於HTML5表單，瀏覽器沒有內建的XTG引擎來建立中介資料結構，也沒有來自原始XDP位元組的物件。 因此，對於HTML5表單，會在伺服器上產生中介結構並傳送至用戶端。 在用戶端，Javascript架構的指令碼和版面引擎會使用這些中介結構。

   中間結構的大小取決於原始XDP和與XDP合併的資料的大小。

1. 在xdp中使用表有任何限制嗎？

   答案：複雜的表格會在轉換時產生問題。

   * 不支援表內的Section（子表單集）。
   * 某些表格中的頁首或頁尾行會標籤為重複。 將這些表格分割為多個頁面可能會遇到一些問題。

1. 可存取的表格有任何限制嗎？

   答案：是的，可訪問的表具有以下限制：

   * 不支援表內的嵌套表和子表單。
   * 表格頂端列或左側列僅支援標題。 中間表格元素不支援標題。 您可以將標題套用至多列，而且支援欄標題，但是所有這些列和欄都必須與表格的最上方列或最左側的欄一起使用。
   * `Rowspan`不 `colspan`支援從表格內的隨機位置。

   * 您無法動態新增或移除包含行範圍值大於1之元素之列的例項。

1. 螢幕閱讀程式的工具提示和標題閱讀順序為何？

   * 當字幕和工具提示同時存在時，會讀取唯一的字幕。 如果標題不可用，則會讀取工具提示。 您也可以使用表單設計工具指定XDP中的讀取優先順序
   * 當您暫留元素時，會顯示工具提示。 如果工具提示不可用，則會顯示語音文字。 如果語音文字不可用，則顯示欄位名稱。

1. 當您暫留欄位時，會顯示工具提示。 如何禁用它？

   若要停用暫留時的工具提示，請在設計工具的協助工具面板中選取「無」。

1. 在Designer中，用戶可以配置單選按鈕和複選框的自定義外觀屬性。 在轉譯表單時，HTML5表單會考量到這些自訂外觀屬性嗎？

   答案：HTML5表單會忽略選項按鈕和核取方塊的自訂外觀屬性。 選項按鈕和核取方塊會根據基礎瀏覽器的規格顯示。

1. 在支援的瀏覽器中開啟HTML5表格時，相鄰放置的欄位邊框無法正確對齊，或子表格會重疊。 當在Forms Designer中預覽相同的HTML5表單時，欄位和版面不會顯示未對齊，子表單會顯示在正確的位置。 如何修正此問題？

   將子表單設定為流內容且子表單具有隱藏的邊框元素時，相鄰放置的欄位的邊界不正確對齊或子表單顯示重疊。 要解決此問題，可以從相應的XDP中刪除或注釋隱藏的&lt;border>元素。 例如，下列&lt;border>元素會標示為備注：

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 為什麼螢幕閱讀程式無法正確處理日期／時間欄位物件？

   螢幕閱讀程式不支援日期／時間欄位。 不過，您可以手動輸入欄位的日期／時間，讓螢幕閱讀程式加以閱讀。 使用工具提示或螢幕閱讀器文字，指示使用者手動選取欄位的日期／時間。

### 指令碼 {#scripting}

1. HTML Forms的JavaScript實作有任何限制嗎？

   答案:

   * xfa.connectionSet指令碼的支援有限。 對於connectionSet，僅支援伺服器端調用web服務。 如需詳細資訊，請參閱指 [令碼支援](/help/forms/using/scripting-support.md)。
   * 用戶端指令碼中不支援$record和$data。 不過，如果指令碼是以formReady、layoutReady區塊編寫，則指令碼仍然有效，因為這些事件會在伺服器端執行。
   * 不支援XFA Draw元素特定的指令碼，例如變更Draw文字（或欄位中的標題文字）。

1. 使用formCalc有任何限制嗎？

   答案：當前只實施formCalc指令碼的子集。 如需詳細資訊，請參閱指 [令碼支援](/help/forms/using/scripting-support.md)。

1. 是否有建議的命名慣例，以及是否有要避免的保留關鍵字？

   * 在AEM Forms Designer中，建議您不要以底線(_)開頭顯示物件（例如子表單或文字欄位）的名稱。 要在名稱的開頭使用下划線，請在下划線_&lt;prefix>&lt;objectname>後面添加前置詞。
   * 所有HTML5表格API都是保留關鍵字。 對於自訂API/函式，請使用與 [HTML5表單API不相同的名稱](/help/forms/using/scripting-support.md)。

1. HTML5表格是否支援浮動欄位？

   是的，HTML5 Forms支援浮動欄位。 若要啟用浮動欄位，請新增下列屬性至演算描述檔：

   >[!NOTE]
   >
   >依預設，這些欄位不會啟用浮動。 您可以使用Forms Designer來設定欄位的浮動屬性。

   1. 開啟CRXde lite並導覽至節 `/content/xfaforms/profiles/default` 點。
   1. 新增String `mfDataDependentFloatingField`類型的屬性，並將屬性的值設為 `true`。
   1. 按一下「 **全部儲存**」。 現在，使用更新的轉換設定檔，HTML表格會啟用浮動欄位。

      >[!NOTE]
      >
      >若要為特定表單啟用浮動欄位而不更新轉換描述檔，請將mfDataDependentFloatingField=true屬性作為URL參數傳遞。

1. HTML5表單是否會多次執行初始化指令碼和表單就緒事件？

   是的，初始化指令碼和表單就緒事件會執行多次，至少在伺服器上執行一次，在客戶端執行一次。 建議根據某些業務邏輯（表單或欄位資料）編寫諸如initialize或form:ready事件之類的指令碼，以便根據資料狀態和冪等元（如果資料相同）執行操作。

### 設計XDP {#designing-xdp}

1. HTML5表單中是否有保留的關鍵字？

   答案：所有HTML5表格API都是保留關鍵字。 對於自訂API/函式，請使用與 [HTML5表單API不相同的名稱](/help/forms/using/scripting-support.md)。 除保留關鍵字外，如果您使用以底線(_)開頭的物件名稱，建議在底線後面加入唯一首碼。 新增首碼有助於避免與HTML5表單內部API產生任何可能的衝突。 例如， `_fpField1`

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
