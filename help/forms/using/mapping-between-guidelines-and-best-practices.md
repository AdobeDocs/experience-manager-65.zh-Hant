---
title: 在Forms Designer中建立表單的准則和最佳協助工具作法
description: 在Forms Designer中開發表單時，協助工具的最佳作法和准則。
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 082a705e25c8c9f17428daadb017d5ab55784994
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 1%

---

# 准則與最佳實務之間的對應

以下章節將508節和WCAG指南對應至本指南中描述的最佳實務。

## § 1194.21指引說明和最佳作法

### 第508節§1194.21：軟體應用程式與作業系統

| § 1194.21指引 | 指引說明 | 合規性所需LiveCycleDesigner最佳實務 | 附註 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | 當軟體設計為在具有鍵盤的系統上執行時，產品功能應該可以從鍵盤執行，其中功能本身或執行功能的結果可以從文字上辨識。 | <li> 2.7確保可使用鍵盤存取表單控制項 </li><li> 2.6確定閱讀和定位鍵順序正確</li> | |
| (b) | 應用程式不得干擾或停用已識別為協助工具功能之其他產品的已啟動功能，這些功能是根據業界標準開發和記錄的。 應用程式也不應中斷或停用任何作業系統的已啟動功能，這些作業系統識別為協助工具功能，且作業系統製造商已記錄這些協助工具功能的應用程式設計介面，可供產品開發人員使用。 | 沒有LiveCycle Designer特定技術 — 本指引由Adobe Reader處理，以供PDF forms使用。 | |
| (c) | 當輸入焦點變更時，在互動式介面元素之間移動時，應提供目前焦點的明確定義熒幕指示。 焦點應以程式設計方式公開，以便輔助技術可追蹤焦點並聚焦於變更。 | 2.3選擇正確的控制項若要以程式設計方式及視覺化方式顯示焦點，請一律使用標準控制項。 | |
| (d) | 對於輔助技術來說，使用者介面元素的足夠資訊，包括元素的身分、操作和狀態。 當影像代表方案元素時，由影像傳達的資訊也必須在文字中可用。 | <ul><li>2.1保持表單簡單易用</li> <li>2.1.1避免移動、閃爍或閃爍內容</li> <li>2.2設定表單屬性以產生協助工具資訊</li> <li>2.5為表單控制項提供適當的標籤</li></ul> | |
| (e) | 當使用點陣圖影像來識別控制項、狀態指標或其他程式化元素時，指派給這些影像的含義在應用程式的整個效能中應該是一致的。 | <ul><li>2.4提供影像的對等文字</li><li> 2.5為表單控制項提供適當的標籤此標準僅適用於您在表單上的多個位置使用相同影像時。 不建議使用影像型自訂控制項。 請僅使用LiveCycleDesigner提供的標準控制項。 如果您確實在控制項中使用影像，請一律確定使用方式一致。</li> | |
| (f) | 文字資訊應透過顯示文字的作業系統功能提供。 可取得的最少資訊為文字內容、文字輸入插入符號位置及文字屬性。 | 2.3選擇正確的控制項避免使用影像傳達文字資訊。 不要使用自訂輸入元件（這些元件可能無法正確地向作業系統公開文字屬性），請一律使用標準控制項。 | |
| (g) | 應用程式不得覆寫使用者選取的對比和顏色選取以及其他個別顯示屬性。 | 無LiveCycle Designer特定技術 | 儘可能使用基本預設的系統顏色。 |
| (h) | 當顯示動畫時，應至少在一個非動畫顯示模式中根據使用者的選擇顯示資訊。 | 2.1保持表單簡單且易於使用避免在表單中使用動畫，或提供以靜態影像取代動畫的個別版本。 | |
| (i) | 色彩編碼不得用作傳達資訊、表示動作、提示回應或區分視覺元素的唯一方式。 | 2.8負責任地使用顏色 | |
| (j) | 當產品允許使用者調整顏色和對比設定時，應提供能夠產生一系列對比等級的各種顏色選擇。 | 不適用 | 此功能通常由Adobe Reader提供，而非由表單開發人員提供。 |
| (k) | 軟體不得使用閃爍或閃爍的文字、物件，或其他閃光或閃爍頻率大於2Hz且小於55Hz的元素。 | 2.1.1避免移動、閃爍或閃爍內容 | |
| (l) | 使用電子錶單時，表單應可讓使用輔助技術的人員存取完成和提交表單所需的資訊、欄位元素和功能，包括所有指示和提示。 | 2.5為表單控制項提供適當的標籤 | |

### 第508款§11942：網路內部網路和網際網路資訊和應用程式

| §11942指引 | 指引說明 | 合規性所需LiveCycleDesigner最佳實務 | 附註 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | 應提供每個非文字元素的同等文字（例如，透過&quot;alt&quot;、&quot;longdesc&quot;或在元素內容中）。 | 2.4提供影像的對等文字 | |
| (b) | 任何多媒體簡報的同等替代方案應與簡報同步。 | 2.12確保所有多媒體內容都能存取 | |
| (c) | 網頁的設計應使所有以顏色傳達的資訊也能以無顏色顯示，例如上下文或標示。 | 2.8負責任地使用顏色 | |
| (d) | 檔案應妥善組織，不需相關樣式表即可讀取。 | 不適用 | |
| (e) | 伺服器端影像地圖的每個作用中區域都應提供備援文字連結。 | 不適用 | |
| (f) | 除非無法以可用的幾何形狀定義區域，否則應提供使用者端影像地圖，而非伺服器端影像地圖。 | 不適用 | |
| (g) | 資料表須識別列與欄標題。 | 2.9提供表格的標題儲存格 | |
| (h) | 對於具有兩個或多個列或欄標題邏輯層級的資料表，應使用標籤來關聯資料儲存格和標題儲存格。 | 2.9提供表格的標題儲存格 | |
| (i) | 框架標題應為文字，以便於框架識別和導覽。 | 不適用 | |
| (j) | 網頁的設計應避免熒幕以大於2Hz且小於55Hz的頻率閃爍。 | 2.1保持表單簡單易用 | |
| (k) | 若無法以任何其他方式達成規範遵循，則應提供具有同等資訊或功能的純文字頁面，使網站符合本部分的規定。 主要頁面變更時，純文字頁面的內容將會更新。 | 不適用 | |
| (l) | 當頁面使用指令碼語言顯示內容或建立介面元素時，指令碼提供的資訊應以可透過輔助技術讀取的功能文字來識別。 | 2.11避免中斷指令碼 | |
| (m) | 當網頁需要在使用者端系統上存在應用程式、外掛程式或其他應用程式來解譯頁面內容時，頁面必須提供連至符合§1194.21(a)到(l)的外掛程式或應用程式的連結。 | 不適用 | 連結至PDF forms的網頁應會提供Adobe Reader的連結。 |
| (n) | 當電子錶單設計為線上上完成時，表單應可讓使用輔助技術的人員存取完成和提交表單所需的資訊、欄位元素和功能，包括所有指示和提示。 | 2.5為表單控制項提供適當的標籤 | |
| (o) | 應提供允許使用者略過重複導覽連結的方法。 | 2.10提供可導覽的表單結構 | |
| (p) | 當需要計時回應時，系統會提醒使用者，並提供充足的時間來指示需要更多時間。 | 2.11避免中斷指令碼 | |

### WCAG 1.0優先順序1查核點

| 查核點 | 查核點說明 | 合規性所需LiveCycleDesigner最佳實務 | 附註 |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | 為每個非文字元素提供等同的文字（例如，透過&quot;alt&quot;、&quot;longdesc&quot;或在元素內容中）。 這包括：影像、文字的圖形表示（包括符號）、影像地圖區域、動畫(例如動畫GIF)、Applet和程式化物件、ASCII藝術、影格、指令碼、清單專案符號使用的影像、分隔符號、圖形按鈕、聲音（不論是否與使用者互動播放）、獨立音訊檔案、視訊的音訊曲目，以及視訊。 | <ul><li>2.4提供影像的對等文字</li> <li>2.12確保所有多媒體內容都能存取</li> | |
| [1.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | 為伺服器端影像地圖的每個作用中區域提供多餘的文字連結。 | 不適用 | |
| [1.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | 在使用者代理程式可以自動朗讀視覺音軌的文字等效之前，請為多媒體簡報的視覺音軌提供聽覺上的重要資訊描述。 | 2.12確保所有多媒體內容都能存取 | |
| [1.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | 對於任何以時間為基礎的多媒體簡報（例如，電影或動畫），請將對等替代方案（例如，視覺軌跡的註解或聽覺描述）與簡報同步化。 | 2.12確保所有多媒體內容都能存取 | |
| [2.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | 確定所有以顏色傳達的資訊也無顏色可供使用，例如上下文或標示。 | 2.8負責任地使用顏色 | |
| [4.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | 清楚識別檔案文字的自然語言和任何文字等同專案（例如註解）的變更。 | 2.13識別語言變更 | |
| [5.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | 對於資料表格，請識別列和欄標題。 | 2.9提供表格的標題儲存格 | |
| [5.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | 對於具有兩個或多個列或欄標題邏輯層級的資料表，請使用標籤來關聯資料儲存格與標題儲存格。 | 2.9提供表格的標題儲存格 | |
| [6.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | 組織檔案，使其不需要樣式表即可讀取。 例如，當HTML檔案在轉譯時沒有關聯的樣式表，仍必須可以讀取該檔案。 | 不適用 | |
| [6.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | 確保在動態內容變更時更新動態內容的等效專案。 | 2.11避免中斷指令碼 | |
| [6.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | 關閉或不支援指令碼、Applet或其他程式化物件時，請確定頁面可供使用。 如果無法這麼做，請在其他可存取的頁面上提供同等資訊。 | 2.11避免中斷指令碼 | |
| [7.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | 在使用者代理程式允許使用者控制閃爍之前，請避免造成畫面閃爍。 | 2.1保持表單簡單易用 | |
| [9.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | 提供使用者端影像地圖，而非伺服器端影像地圖，除非無法以可用的幾何形狀定義區域。 | 不適用 | |
| [11.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | 如果經過最大努力，您還是無法建立可存取的頁面、提供使用W3C技術之替代頁面的連結、可存取、具有同等資訊（或功能），且更新頻率與無法存取（原始）頁面的頻率相同。 | 不適用 | |
| [12.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | 為每個影格加上標題，以方便影格識別和導覽。 | 不適用 | |
| [14.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | 使用最清晰、最簡單的語言，以適用於網站內容。 | 2.1保持表單簡單易用 | |

### WCAG 1.0優先順序2查核點

| 優先順序2查核點 | 查核點說明 | 合規性所需LiveCycle最佳實務 | 附註 |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | 確保當有顏色缺陷的人檢視或在黑白熒幕上檢視時，前景和背景顏色的組合能提供足夠的對比度。 [影像的優先順序2，文字的優先順序3]. | 2.8負責任地使用顏色 | |
| [3.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | 如果有適當的標籤語言，請使用標籤而非影像來傳達資訊。 | <ul><li>2.1保持表單簡單易用</li><li> 2.1.1避免移動、閃爍或閃爍內容</li> <li>2.2設定表單屬性以產生協助工具資訊一律使用實際文字，而非文字影像。</li> | |
| [3.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | 建立可驗證已發佈正式文法的檔案。 | | PDF forms必須符合已發佈的PDF規格，才能在Adobe Reader中呈現。 |
| [3.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | 使用樣式表來控制版面配置與簡報。 | 不適用 | |
| [3.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | 在標籤語言屬性值和樣式表屬性值中使用相對單位而非絕對單位。 | 不適用 | |
| [3.5](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | 使用頁首元素來傳達檔案結構，並根據規格使用它們。 | 2.10提供可導覽的表單結構 | |
| [3.6](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | 正確標示清單和清單專案。 | 2.10.3標示清單使用「清單」和「清單專案」角色將清單型內容標示為清單。 | |
| [3.7](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | 標示報價單。 請勿使用引號標示格式效果，例如縮排。 | 不適用 | |
| [5.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | 請勿使用表格進行版面配置，除非將表格線性化是有意義的。 否則，如果表格沒有意義，請提供替代的同等專案（可能是線性化版本）。 | 無特定LiveCycle技術 | 沒有理由在LiveCycle表單中使用表格進行版面配置。 請改用「版面」浮動視窗，以格線模式來定位表單欄位。 只有在利用表格特定功能（例如表格標頭）時才使用表格。 |
| [5.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | 如果表格用於版面，請勿將任何結構標籤用於視覺格式化的目的。 | 無特定LiveCycle技術 | |
| [6.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | 對於指令碼和Applet，請確定事件處理常式與輸入裝置無關。 | 2.7確保可使用鍵盤存取表單控制項 | |
| [6.5](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | 確保可存取動態內容，或提供替代簡報或頁面。 | 2.11避免中斷指令碼 | |
| [7.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | 在使用者代理程式允許使用者控制閃爍之前，請避免造成內容閃爍（亦即定期變更簡報，例如開啟和關閉）。 | 2.1保持表單簡單易用 | |
| [7.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | 在使用者代理允許使用者凍結移動內容之前，請避免在頁面中移動。 | 2.1保持表單簡單易用 | |
| [7.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | 在使用者代理程式提供停止重新整理的功能之前，請勿定期建立自動重新整理頁面。 | 不適用 | |
| [7.5](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | 在使用者代理程式提供停止自動重新導向的功能之前，請勿使用標示自動重新導向頁面。 請改為設定伺服器以執行重新導向。 | 不適用 | |
| [8.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | 讓程式設計元素（例如指令碼和Applet）可直接存取或與輔助技術相容 [優先順序1 （如果功能很重要且沒有顯示於其他地方），否則優先順序2。] | 2.11避免中斷指令碼 | |
| [9.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | 請確定任何具有自己介面的元素都可以獨立裝置的方式操作。 | 2.7確保可使用鍵盤存取表單控制項 | |
| [9.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | 對於指令碼，請指定邏輯事件處理常式，而非裝置相依的事件處理常式。 | 2.7確保可使用鍵盤存取表單控制項 | |
| [10.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | 除非使用者代理程式允許使用者關閉衍生視窗，否則不要造成快顯視窗或其他視窗出現，也不要在未通知使用者的情況下變更目前視窗。 | 2.11避免中斷指令碼 | |
| [10.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | 在使用者代理程式支援標籤和表單控制項之間的明確關聯之前，對於所有具有隱含關聯標籤的表單控制項，請確定標籤的位置正確。 | 2.5為表單控制項提供適當的標籤 | |
| [11.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | 使用W3C技術（當有條件使用時）和適合工作使用，並在支援時使用最新版本。 | 不適用 | |
| [11.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | 避免W3C技術的過時功能。 | 不適用 | |
| [12.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | 說明影格的用途，以及如果單獨使用影格標題並不明顯時，影格如何彼此關聯。 | 不適用 | |
| [12.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | 將大型的資訊區塊分成更容易管理的群組，以符合需求且適當的方式加以管理。 | 2.10提供可導覽的表單結構 | |
| [12.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | 將標籤與其控制項明確關聯。 | 2.5為表單控制項提供適當的標籤 | |
| [13.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | 清楚識別每個連結的目標。 | 2.5為表單控制項提供適當的標籤2.5.6提供連結文字 | |
| [13.2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | 提供中繼資料，以將語意資訊新增至頁面和網站。 | 不適用 | |
| [13.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | 提供網站一般配置的相關資訊（例如網站地圖或目錄）。 | 2.10提供可導覽的表單結構 | |
| [13.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | 以一致的方式使用導覽機制。 | 2.10提供可導覽的表單結構 | 使用主版頁面來建立一致的導覽內容。 |

### WCAG 2.0成功標準

| 優先順序1 G 2查核點 | 合規性所需LiveCycle最佳實務 | 附註 |
| --- | --- | --- |
| 1.1 [替代文字](http://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [非文字內容](http://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4提供影像的對等文字 | |
| | 2.5為表單控制項提供適當的標籤 | |
| 1.2 [時間型媒體](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [純音訊和純視訊（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.2 [註解（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.3 [音訊說明或替代媒體（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.4 [註解（即時）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.5 [音訊說明（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.6 [手語（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.7 [延伸音訊描述（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.8 [替代媒體（預先錄製）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.2.9 [僅限音訊（即時）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12確保所有音訊與視訊內容都能存取 | |
| 1.3 [可調整](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [資訊和關係](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9提供表格的標題儲存格 | |
| 1.3.2 [有意義的順序](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6確定閱讀和定位鍵順序正確 | |
| | 2.10提供可導覽的表單結構 | |
| 1.3.3 [感官特性](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8負責任地使用顏色 | |
| 1.4 [可區分](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [使用顏色](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8負責任地使用顏色 | |
| 1.4.2 [音訊控制](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | 無特定LiveCycle技術 | |
| 1.4.3 [對比（最小）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8負責任地使用顏色 | |
| 1.4.4 [調整文字大小](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | 無特定LiveCycle技術 | |
| 1.4.5 [文字的影像](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | 無特定LiveCycle技術 | |
| 1.4.6 [對比（增強）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8負責任地使用顏色 | |
| 1.4.7 [低背景音訊或無背景音訊](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | 無特定LiveCycle技術 | |
| 1.4.9 [文字的影像（無例外）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | 無特定LiveCycle技術 | |
| 2.1 [無障礙鍵盤](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [鍵盤](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6確定閱讀和定位鍵順序正確 | |
| | 2.7確保可使用鍵盤存取表單控制項 | |
| 2.1.2 [無鍵盤陷阱](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7確保可使用鍵盤存取表單控制項 | |
| 2.1.3 [鍵盤（無例外）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6確定閱讀和定位鍵順序正確 | |
| | 2.7確保可使用鍵盤存取表單控制項 | |
| 2.2 [充足的時間](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [計時可調](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | 無特定LiveCycle技術 | |
| 2.2.2 [暫停、停止、隱藏](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1保持表單簡單易用 | |
| 2.2.3 [無時間](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | 無特定LiveCycle技術 | |
| 2.2.4 [插斷](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | 無特定LiveCycle技術 | |
| 2.2.5 [重新驗證](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | 無特定LiveCycle技術 | |
| 2.3 [癲癇發作] | | |
| 2.3.1 [三個Flash或低於臨界值](http://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1保持表單簡單易用 | |
| 2.3.2 [三個Flash](http://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1保持表單簡單易用 | |
| 2.4 [可導覽](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [略過區塊](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10提供可導覽的表單結構 | |
| 2.4.2 [頁面帶有標題](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | 無特定LiveCycle技術 | |
| 2.4.3 [焦點順序](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6確定閱讀和定位鍵順序正確 | |
| 2.4.4 [連結目的（在內容中）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | 無特定LiveCycle技術 | 連結目的取決於作者為連結的元素選擇有意義的文字。 |
| 2.4.5 [多種方式](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10提供可導覽的表單結構 | |
| 2.4.6 [標題和標籤](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5為表單控制項提供適當的標籤</li><li>2.10提供可導覽的表單結構</li> | |
| 2.4.7 [焦點可見](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | 無特定LiveCycle技術 | LiveCycle表單中的預設焦點為可見。 |
| 2.4.8 [位置](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | 無特定LiveCycle技術 | 不適用：LiveCycle表單不需要導覽系統。 |
| 2.4.9 [連結目的（僅限連結）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | 無特定LiveCycle技術 | 連結目的取決於作者為連結的元素選擇有意義的文字。 |
| 2.4.10 [章節標題](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10提供可導覽的表單結構 | |
| 3.1 [可讀](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [頁面語言](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13識別自然語言和語言的任何變更 | |
| 3.1.2 [部分語言](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13識別自然語言和語言的任何變更 | |
| 3.1.3 [不尋常字詞](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | 無特定LiveCycle技術 | |
| 3.1.4 [縮寫](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | 無特定LiveCycle技術 | |
| 3.1.5 [讀取層級](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | 無特定LiveCycle技術 | |
| 3.1.6 [發音](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | 無特定LiveCycle技術 | |
| 3.2 [可預測](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [聚焦](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11避免中斷指令碼 | |
| 3.2.2 [在輸入上](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11避免中斷指令碼 | |
| 3.2.3 [一致的導覽](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10提供可導覽的表單結構 | |
| 3.2.4 [一致的識別](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3選擇正確的控制項</li><li>2.5為表單控制項提供適當的標籤</li> | |
| 3.2.5 [依要求變更](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11避免中斷指令碼 | |
| 3.3 [輸入協助](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [錯誤識別](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycleDesigner提供必要工具來標籤表單欄位，以及執行表單輸入驗證。 |
| 3.3.2 [標籤或指示](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5為表單控制項提供適當的標籤 | |
| 3.3.3 [錯誤建議](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycleDesigner提供必要工具來標籤表單欄位，以及執行表單輸入驗證。 |
| 3.3.4 [錯誤預防（法律、金融、資料）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | 無特定LiveCycle技術 | |
| 3.3.5 [說明](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | 無特定LiveCycle技術 | |
| 3.3.6 [錯誤預防（全部）](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | 無特定LiveCycle技術 | |
| 4.1 [相容](http://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [剖析](http://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | 無特定LiveCycle技術 | |
| 4.1.2 [名稱、角色、值](http://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3選擇正確的控制項</li> <li>2.5為表單控制項提供適當的標籤</li> | |



