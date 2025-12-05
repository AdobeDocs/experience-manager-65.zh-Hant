---
title: ' [!DNL Adobe Experience Manager] 6.5的發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5的版本資訊、新增功能、安裝操作說明和詳細變更清單。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: ae66b28497bfb12686152b324e1758ad2d8592ee
workflow-type: tm+mt
source-wordcount: '9451'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 版本資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2025年11月26日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## [!DNL Experience Manager] 6.5.24.0包含的內容 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0包含新功能、客戶要求的重要增強功能和錯誤修正。 此外，還包含自2019年4月6.5首次推出以來的效能、穩定性和安全性改善專案。 在[&#x200B; 6.5上](#install)安裝此Service Pack[!DNL Experience Manager]。

<!-- UPDATE FOR EACH NEW RELEASE -->


## 主要功能和增強功能

### Forms

* **傳遞自訂XCI的支援：**&#x200B;新增在指令行應用程式xmlformcmd的引數中傳遞自訂XCI的支援。 這可讓使用者指定要用於測試的自訂XCI檔案，增強測試流程的彈性和控制力。 (LC-3923248)


## 已修正Service Pack 24中的問題 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* 更新至版本6.5.23.0後，在卡片檢視中依修改日期排序資料夾會造成尋找最近修改的資產以進行內部部署的困難。 (ASSETS-56946)
* 排程器執行期間會產生重複的警告日誌專案。 (ASSETS-52554)
* 標題排序在清單檢視中無法運作。 (ASSETS-50716)
* 即使按一下「取消」按鈕，「集合屬性」視窗也不會關閉。 (ASSETS-48504)

* 嘗試在AEM 6.5.22中為資產加上註解時發生&#x200B;*無效的URL*&#x200B;錯誤。 (NPR-42684)
* Assets中繼資料編輯器表單在執行相關或取消相關動作後未重新初始化。 (ASSETS-52207)
* 當資產從遠端DAM重新同步至本機Sites時，資產的已發佈狀態錯誤地更新為`Not published`。 (ASSETS-48958)
* 從SP23升級至6.5 LTS版本時發生問題。 (ASSETS-50541)

### [!DNL Sites]{#sites-6524}

#### 無障礙功能 {#sites-accessibility-6524}

* **切換顯示格式**&#x200B;對話方塊現在支援全鍵盤操作。 焦點不再略過&#x200B;**檢視設定**&#x200B;按鈕，標準金鑰(`Tab`、`Enter`、`Space`)會一致運作。 (SITES-24306)
* 鍵盤使用者無需滑鼠即可移除已發佈的狀態標籤。 焦點位於每個標籤上，並且啟動可搭配`Enter`/`Space`和Backspace/Delete運作。 標籤控制的行為現在類似按鈕，可改善熒幕助讀程式的意見反應，並符合WCAG 2.1.1鍵盤。 (SITES-24491)
* 篩選器邊欄在狹窄的檢視區中會回應式地重排。 選取範圍控制項和結果會以400%縮放保留在檢視區內，消除水準捲動和內容剪斷。 (SITES-24708)
* AEM會還原對ContextHub「重設」、「角色」和「裝置」按鈕的完整鍵盤存取權。 Tab鍵和方向鍵可觸及每個控制項、顯示可見的焦點指示器，以及使用`Enter`或`Space`啟動動作。 熒幕助讀程式會朗讀清楚的標籤。 (SITES-24939)
* 日期輸入和選取器在320畫素處仍完全可見。 Timewarp強制回應式調整大小，因此控制項不再在最小檢視區上裁剪或消失。 (SITES-24962)
* 「引用」邊欄現在支援400%瀏覽器縮放，而不會失去對其內容的存取權。 邊欄使用回應式大小調整而非固定寬度，因此專案在1280×1024處仍可見且可選取。 (SITES-24972)
* 篩選器邊欄現在能以400%縮放運作。 邊欄會以相對單位調整大小，不再封鎖或隱藏篩選控制項。 使用者可以檢視及選取每個篩選器選項，而不需要水準捲動或剪裁的點選目標。 (SITES-24981)
* 鍵盤使用者可以在Teaser強制回應視窗中操作格式功能表。 按`Enter`清單`Space`或&#x200B;**段落格式**&#x200B;上的&#x200B;**或**&#x200B;會開啟快顯視窗、方向鍵導覽選項，而`Enter`會套用選取專案。 `Escape`關閉功能表並將焦點還原到觸發控制項，產生一致的工具列工作流程。 (SITES-25235)
* 「色票檢色器」彈出視窗現在會保留在檢視區內320畫素。 彈出視窗會顯示所有顏色列並支援捲動，讓作者能在小熒幕上選取任何色票。 (SITES-25274)
* 人口統計工具列下拉式功能表現在可以使用鍵盤來完整運作。 開啟功能表會將焦點移至第一個選項、方向鍵導覽清單，以及Esc/Tab關閉或前進而不將焦點傾印至工具列。 互動式專案會使用正確的語意，以便NVDA和其他閱讀器能正確宣告選項。 (SITES-25310)
* 內容樹狀結構中的「新增元件」運作方式與AEM 6.5 SP24上的設計一致。 錯誤初始錯誤來自本機設定中缺少作者許可權，而非來自AEM。 擁有編輯許可權的作者可以透過鍵盤或滑鼠啟動按鈕及新增元件。 (SITES-25312)
* 人口統計工具列中的鍵盤和熒幕助讀程式存取現在能以可靠的方式運作。 使用NVDA的作者可以使用箭頭遍歷&#x200B;**Commerce**、**角色**&#x200B;和88，觀察清晰的焦點回饋，並瞭解哪個索引標籤作用中。 (SITES-25326)

* **跳至內容**&#x200B;連結現在將鍵盤焦點移至主要內容標題。 焦點會顯示在唯一識別的目標上，因此熒幕助讀程式會朗讀正確的區段。 此變更符合WCAG 2.4.1和2.4.3。 (SITES-24061)
* 使用&#x200B;**全選**&#x200B;後，Sites首頁樹狀結構中的鍵盤導覽會遵循邏輯順序。 焦點從&#x200B;**全選**&#x200B;移至下一個控制項（開啟左側邊欄），而非跳回到頁面開頭。 (SITES-24307)
* Sites編輯器中的區段標題和編輯控制項會回應鍵盤焦點與啟動。 鍵盤使用者會顯示與先前僅於暫留時顯示的相同標題和動作。 (SITES-24479)
* Sites編輯器中的按鈕會顯示描述性名稱，而不是通用或遺漏標籤。 輔助型技術會宣告正確的動作，提高清晰度並減少誤點。 (SITES-24480)
* 當Sites檢視重新整理時，熒幕助讀程式會收到口語「正在載入」訊息。 更新會新增專用狀態即時區域，並以程式設計方式將訊息寫入其中，這樣可確認進度而不移動焦點。 (SITES-24481)
* Assets側邊欄現在包含清除&#x200B;**關閉**&#x200B;控制項，並將焦點傳回切換按鈕。 鍵盤和熒幕助讀程式的使用者會立即關閉面板，而非在每個控制項之間使用Tab鍵。 此變更可減少按鍵次數，並符合預期的面板行為。 (SITES-24489)
* 網站頁面編輯器中的ARIA標籤清單包括描述性名稱。 熒幕助讀程式現在會將控制項識別為索引標籤清單，並閱讀正確的標籤，讓使用者找到正確的索引標籤集，並可靠地在這些索引標籤之間移動。 (SITES-24492)
* 在編輯器側邊欄中搜尋，現在會向熒幕朗讀程式宣告結果。 當使用者輸入時，即時狀態訊息會報告符合和更新的數量，而不會移動焦點。 鍵盤使用者會立即發現結果。 (SITES-24506)
* 針對輔助技術使用者，可改善「清單檢視」中的列選取範圍。 核取方塊會顯示衍生自列「標題」的有意義名稱，以便公告保持簡短並正確說明動作。 (SITES-24514)
* 更正清單檢視協助工具名稱。 表格會從非互動式元素中移除`aria-label`，並將標籤指派給可操作的連結或按鈕。 熒幕助讀程式的使用者現在可在整欄聽到準確、不重複的標籤。 (SITES-24515)
* 在高縮放使用期間，粘性標頭停止遮住Teaser模型對話方塊。 200%和400%縮放下內容仍可讀取和使用，具有垂直流量且沒有剪裁區段。 (SITES-24523)
* 在搜尋欄位中輸入不再觸發提前宣告第一個結果或意外啟用。 體驗現在會朗讀含有結果計數的簡潔狀態訊息，而焦點會保留在欄位中，直到使用者導覽至清單為止。 (SITES-24658)
* 文字編輯器的超連結對話方塊中的「替代文字」欄位現在會顯示程式設計標籤。 熒幕助讀程式會朗讀欄位的「替代文字」，並聚焦於正確命名的控制項。 此修正可改善鍵盤和語音使用者的導覽功能。 (SITES-24675)
* 在參考邊欄中新增即時狀態訊息，以便輔助技術立即宣佈變更。 選取多個專案會觸發有關參考可用性的明確訊息，以防止無訊息狀態變更並減少重複動作。 (SITES-24678)
* 「影像」對話方塊現在會透過ARIA即時區域宣佈其載入狀態。 熒幕助讀程式在旋轉圖顯示時聽到「正在載入，請稍候」訊息。 此外，內容完成時可立即更新，以便使用者知道何時可以互動。 (SITES-24697)
* 連結選取對話方塊現在會顯示可宣告搜尋結果的即時區域。 熒幕助讀程式會在每次搜尋後聽到「結果已更新」狀態，而不會移動焦點，因此使用者可獲得已完成搜尋的明確確認。 (SITES-24700)
* 現在，「連結選取」對話方塊會以320畫素重排。 所有欄位和動作保持可見且可用，且水準卷軸不再出現。 (SITES-24709)
* 現在，「連結選取」對話方塊會針對每個樹狀結構專案上的熒幕文字和存取許可權名稱使用相同的標籤。 熒幕助讀程式會在使用方向鍵移動時朗讀每個專案，包括最後一個層級，消除無訊息節點和不相符的名稱。 (SITES-24710)
* 變更篩選器現在會將其狀態報告為展開或摺疊。 按鈕會以與篩選器面板同步的方式切換`aria-expanded`，並公開單一清除名稱（「變更篩選器」），移除令人困惑的「篩選器？」 公告。 熒幕助讀程式的使用者可以預測啟動控制的結果。 (SITES-24713)
* 模組標題不再涵蓋320畫素寬度的內容。 標題會從粘性狀態中釋放，而對話方塊本文會捲動，因此所有欄位和動作按鈕都維持可見且可使用。 鍵盤使用者可觸及每個控制項，而不會失去焦點。 (SITES-24718)
* 應用程式導覽連結現在會顯示適當的連結語意。 熒幕助讀程式會將每個專案宣告為連結，而非清單專案，這可改善鍵盤導覽和語音控制。 清單容器會保留清單語意，而連結則會保持可聚焦的目標。 (SITES-24719)
* 篩選器變更時，結果狀態現在會向熒幕助讀程式宣佈。 NVDA會讀取「Y個結果中的X」計數和「沒有結果」訊息。 分頁狀態會使用就地更新的即時區域，讓使用者無需移動焦點即可聽到確認。 (SITES-24720)
* 「轉盤」對話方塊中的迴轉按鈕現在會向熒幕朗讀程式朗讀單一精簡的名稱。 控制項不再重複群組標籤和輸入標籤，這會減少NVDA使用者的詳細程度和混淆。 (SITES-24725)
* 「說明」功能表搜尋清單會顯示適當的語意。 容器會顯示清單，而每個結果都會維持連結，而不會有衝突的角色。 NVDA和JAWS會準確宣告連結，且導覽維持一致。 (SITES-24729)
* Adobe已修正「使用者偏好設定」中的顏色色票快顯視窗，因此NVDA會朗讀焦點中的色票，而非先前選取的色票。 鍵盤使用者在瀏覽清單時聽到精確的顏色名稱，並可確認正確的選擇。 (SITES-24739)
* NVDA現在會讀取樹狀目錄中的完整說明。 詳細資訊面板會將多行文字顯示為單一值，並將其連結至欄位標籤。 鍵盤使用者在Tab鍵瀏覽唯讀欄位時聽到完整的文字。 (SITES-24780)
* 樹狀目錄現在會朗讀修改日期。 NVDA會讀取焦點移至「已修改」欄的日期。 格線會將每個日期與專案名稱繫結，讓使用者同時聽到檔案及其上次更新。 (SITES-24782)
* 預覽模式現在會遵循使用者文字間距偏好設定。 畫布會反映所有預覽內容中的字母、單字和行高變更。 當間距增加時，文字不再保持固定或剪輯。 鍵盤和視力缺佳的使用者讀取內容時不會出現斷版問題。 (SITES-24936)
* AEM會更正Assets編輯器頁面上的標籤順序。 Tab鍵現在會從頁首控制項移至連絡人中樞按鈕，最後會以清晰的順序移至畫布工具。 熒幕助讀程式遵循相同的順序，可消除混淆並加快鍵盤導覽。 (SITES-24937)
* AEM會將程式化名稱新增至「卡片動作」功能表列。 熒幕助讀程式會正確宣告控制項，語音使用者可以依名稱鎖定控制項。 鍵盤導覽與焦點維持不變。 (SITES-24938)
* 卡片檢視功能表採用增加的文字間距。 「更多動作」專案會成長，且不再截斷標籤，包括「快速發佈」。 提出字母、單字或行距的使用者可保留完整的標籤和鍵盤存取權。 (SITES-24941)
* 移除隱藏網站首頁表格的「簡報」角色（從協助工具樹狀結構中）。 表格會再次正確讀取。 NVDA和JAWS會在列和欄導覽期間偵測表格、識別標題並宣告標題關係。 (SITES-24942)
* 在清單檢視中排序意見是明確且一致的。 排序之後，標題會透過`aria-sort`公開順序。 它會宣告變更，而未排序的標題則不再宣告狀態，協助熒幕助讀程式使用者追蹤哪一欄控制排序。 (SITES-24943)
* Edit Layout標題不再顯示非運作中的&#x200B;**Edit**&#x200B;按鈕。 控制項現在可作為靜態狀態標籤，且不會進入Tab鍵順序，因此鍵盤使用者不會浪費按鍵動作。 使用&#x200B;**選取其他模式**&#x200B;以變更模式，並取得熒幕助讀程式的清晰回饋。 (SITES-24950)
* 依預設，模擬器工具列會顯示完整的裝置名稱。 標籤在載入時不再截斷，因此使用者不需猜測即可讀取和選取裝置。 文字會整齊地縮放顯示層級並縮小寬度。 (SITES-24952)
* 模擬器工具列適合小型檢視區。 在320畫素處，裝置會列出並控制顯示而不進行剪裁，讓使用者可以選擇Galaxy S7和更新的型號。 版面會縮放和換行，以避免水準捲動，即使縮放比例為400%也是如此。 (SITES-24953)
* 熒幕朗讀程式會朗讀在模擬器中選取的裝置及其測量。 NVDA會停止讀取尺標資料流；裝置按鈕會使用工具提示文字的附加說明，以減少雜訊並指引導覽。 (SITES-24955)
* 篩選列現在會將每個選取的標籤視為動作按鈕。 清楚易存取的名稱和焦點處理可改善公告和鍵盤控制。 (SITES-24980)
* 網站管理員篩選器檢視中的狀態更新會向熒幕朗讀程式宣告。 當使用者在專案載入時切換卡片/清單時，NVDA現在會透過即時區域說「請稍候」訊息。 本指南可防止額外點按和混淆。 (SITES-24992)
* 現在，當使用者展開左側邊欄時，鍵盤焦點會依邏輯順序移動。 焦點會直接從左側邊欄按鈕移至展開的內容，消除回溯或略過元素的必要性。 這項變更改善了熒幕助讀程式和鍵盤使用者的協助工具。 (SITES-24998)
* **Edit**&#x200B;按鈕的熒幕助讀程式回饋現在符合控制項。 啟動按鈕會朗讀「編輯」動作而不是預覽訊息，這樣可提高清晰度，並減少非滑鼠使用者的輸入錯誤。 (SITES-25208)
* Teaser對話方塊中的確認動作會正確向熒幕朗讀程式宣告。 控制項會報告「確認」，而非圖示說明，為鍵盤和熒幕助讀程式的使用者提供明確的指引。 (SITES-25223)
* 「說明」按鈕現在會顯示清楚的存取名稱。 熒幕助讀程式會朗讀「說明」，而不是冗長的圖示說明。 使用者可瞭解動作，並更快找到協助。 (SITES-25224)
* Timewarp強制回應在&#x200B;**`Set Date`**&#x200B;和&#x200B;**退出Timewarp**&#x200B;連結上顯示明確的焦點回圈。 使用標籤的使用者可看到焦點確切登陸的位置，並避免意外動作。 該鈴聲在背景中至少保持3:1的對比。 (SITES-25232)
* 熒幕助讀程式現在會在「註解」工具列中準確朗讀「註解」和「關閉註解」控制項。 NVDA不再顯示「預覽按鈕已按下」，這會誤導作者並建議錯誤的動作。 宣告符合按下的按鈕，並保持工作流程清晰。 (SITES-25234)
* 註釋工具列中的鍵盤導覽運作方式一致。 開啟模式時，焦點不再跳至「退出」，而是移至開始控制項以新增註解。 使用者可依序導覽控制項，而不需反向Tab鍵。 (SITES-25241)
* 小熒幕檢視可在Teaser強制回應視窗中如預期般運作。 此對話方塊不再以320畫素建立水準卷軸，而且工具列在不橫向平移的情況下保持可存取性。 此更新可幫助縮放頁面的弱視使用者。 (SITES-25242)
* 小熒幕檢視在影像模式中如預期般運作。 此對話方塊不再以320畫素建立水準卷軸，且影像工具仍可存取，不會橫向移動。 此更新可改善縮放頁面的弱視使用者的導覽。 (SITES-25244)
* 「搜尋」模式會遵循使用者文字間距設定。 提高行高、段落間距、字母間距或字間距不再截斷文字或重疊樹狀結構。 內容在WCAG 1.4.12中重新排程，並保持完全可讀。 (SITES-25245)
* 搜尋強制回應現在可容納小型熒幕，而不會與樹狀目錄（320畫素）重疊。 內容在對話方塊內重排，僅保持垂直捲動，並保持控制項可見。 此修正可改善可讀性和鍵盤導覽，並符合WCAG Reflow。 (SITES-25246)
* 輪播模式溢位不再強制以電話大小的寬度水準捲動。 元件可調整為320畫素、保留垂直流量，並讓控制項保持在檢視畫面中。 這項變更改善了撰寫期間的可讀性和鍵盤存取權。 (SITES-25254)
* 註解工作流程不再失焦。 強制回應視窗會將初始焦點置於有意義的標題上，避免焦點跳到對話方塊外，並在移除後恢復焦點至觸發程式。 熒幕助讀程式的輸出仍保持簡潔且相關。 (SITES-25257)
* **刪除註解**&#x200B;對話方塊現在可以正確處理鍵盤焦點。 開啟對話方塊會將焦點移至熒幕朗讀程式內容的標題，關閉對話方塊會將焦點傳回啟動對話方塊的&#x200B;**刪除註解**&#x200B;按鈕。 使用者不再登陸於不相關的控制項或強制回應視窗之後。 (SITES-25258)
* Timewarp日期選擇器現在可以正確管理焦點。 按`Esc`會將焦點傳回&#x200B;**日期選擇器**&#x200B;按鈕，而選擇日期會將焦點移至連結的輸入欄位。 鍵盤和熒幕助讀程式的使用者會保留上下文，不會落在強制回應視窗後面。 (SITES-25264)
* 熒幕助讀程式會朗讀&#x200B;**註釋**&#x200B;和&#x200B;**關閉註釋**&#x200B;按鈕的正確動作。 NVDA不再顯示「預覽按鈕已按下」；它會朗讀按鈕名稱，讓使用者知道註釋模式何時開始或結束。 (SITES-25268)
* 註解強制回應現在會顯示清除&#x200B;**提交**&#x200B;動作。 作者可以新增註解，並使用鋼筆圖示按鈕提交，或使用`Esc`關閉強制回應視窗，而不需要猜測流量。 (SITES-25269)
* 註解專案包含明確的動作按鈕。 此對話方塊會顯示&#x200B;**Submit**&#x200B;以儲存筆記，並顯示&#x200B;**Cancel**&#x200B;以關閉它，鍵盤皆可存取並由輔助技術宣告。 作者不再需要依賴按一下對話方塊外部或僅按下`Esc`即可完成。 (SITES-25281)
* 註解模式現在將鍵盤焦點保持在覆蓋圖及其工具列上。 當作者按下Tab鍵時，覆蓋圖後面的頁面不再受到焦點，因此使用者保持定向且可以導覽註解而不跳到基礎內容。 (SITES-25282)
* 「編輯配置」中的裝置選擇器可如預期運作。 當兩個裝置選項具有相似的寬度(例如，Galaxy 7旁邊的iPhone 8 Plus)時，選取的按鈕會顯示工具提示以顯示完整標籤，而兩個按鈕仍可見且可存取。 (SITES-25285)
* 在200%縮放時，「編輯配置」不再超出頁面。 工具列會完全轉譯，並在需要時顯示水準捲動，讓視力不佳的使用者恢復對先前隱藏控制項的存取。 (SITES-25288)
* 「版面配置預覽」中的Tab鍵順序現在會從主要工具列直接移至「人口統計」工具列。 鍵盤和熒幕助讀程式的使用者可以按照可預測的順序周遊控制項，而不必跳至次要工具列。 此變更與WCAG 2.4.3焦點順序一致。 (SITES-25305)
* 將頁面縮放至200%不再隱藏「人口統計」工具列的一部分。 工具列區段可管理溢位並在其區域提供捲動，讓每個控制項都能以高放大率顯示和操作。 (SITES-25309)
* 「人口統計」工具列中的文字輸入現在會顯示正確的存取名稱。 每個欄位都包含唯一ID和程式設計標籤，因此熒幕助讀程式會朗讀欄位的用途，而使用者可以依標籤導覽。 可見標籤位於控制項附近，以改善低視力可讀性。 (SITES-25316)
* 現在，編輯按鈕在次要工具列中向熒幕朗讀程式宣告正確的動作。 啟用它時會顯示「編輯」，而不是相關的「按下預覽按鈕」，這可消除鍵盤導覽期間的混淆。 (SITES-25320)
* 「人口統計」工具列「購物車」滑桿現在會顯示適當的存取名稱。 熒幕助讀程式會朗讀「購物車總計」，而語音輸入工具可以依名稱鎖定控制項，改善對WCAG 4.1.2 （名稱、角色、值）的合規性。 (SITES-25322)
* 現在，當作者使用方向鍵變更值時，人口統計工具列滑桿會保持焦點。 焦點不再跳至「購物車」按鈕，因此鍵盤使用者會持續調整值，而熒幕助讀程式會朗讀每次變更。 (SITES-25324)
* 搜尋Assets現在會以320畫素（大約400%縮放）完全重排。 強制回應視窗可讓標題、欄位和動作保持可讀性和不重疊，讓作者無須水準捲動即可搜尋。 (SITES-25330)
* 編輯器中的Assets面板遵循邏輯焦點順序。 每個縮圖上的鍵盤使用者索引標籤都能存取面板退出控制項。 此變更移除略過並改善與WCAG 2.4.3的相容性。 (SITES-25360)
* AEM會更新Teaser強制回應視窗之RTF編輯器中的&#x200B;**清單**&#x200B;和&#x200B;**段落**&#x200B;按鈕，以公開其展開和收合狀態。 按鈕現在會切換`aria-expanded`並宣告熒幕朗讀程式的狀態變更。 作者在開啟或關閉格式功能表前，可獲得清楚的意見反應並避免猜測。 (SITES-25365)
* AEM會在Teaser強制回應中宣佈載入狀態。 強制回應現在會在內容載入時顯示即時狀態訊息，因此NVDA和JAWS會說「正在載入，請稍候」。 作者應會收到清楚的意見反應，並避免在對話方塊準備就緒前與其互動。 (SITES-25366)
* 改善連結選取對話方塊之資產索引標籤中的狀態訊息。 發生錯誤時，元件會注入可讀取的狀態更新並保持鍵盤焦點穩定，讓NVDA/JAWS立即通知使用者。 (SITES-25368)
* 修正極窄檢視區之「附註」面板中的UI行為。 在320畫素，標題和新增控制項先前發生衝突；工具列現在重新對齊並保留元素之間的明確分離。 作者可以在不遺失資訊或功能的情況下操作控制項。 (SITES-25376)
* 修正&#x200B;**Teaser**&#x200B;對話方塊的&#x200B;**連結與動作**&#x200B;索引標籤中的延遲錯誤狀態。 在作者啟用&#x200B;**Call to action**&#x200B;並修正空白或無效的欄位後，索引標籤會清除其錯誤樣式和圖示並移除`aria-invalid`。 欄位驗證後，熒幕助讀程式不再宣告錯誤。 (SITES-25527)
* 網站管理員表單中的錯誤處理現在符合協助工具的期望。 驗證失敗時，頁面會立即顯示錯誤、將焦點移至可用的訊息目標，並向熒幕閱讀程式（例如JAWS）公開文字。 (SITES-27138)
* 在Sites中建立資料夾時，現在會顯示清除的確認快顯通知。 JAWS會透過即時區域公告訊息，讓作者在動作後立即收到可存取的意見回饋。 (SITES-27141)
* 修正編寫對話方塊中的影像在轉譯時不含替代文字的協助工具間隙。 此對話方塊現在會視需要提供描述性替代文字，而純視覺化元素則提供空白替代文字，藉此還原JAWS和其他熒幕朗讀程式的相容行為。 (SITES-27153)
* 改善編寫對話方塊中的錯誤處理。 發生設定錯誤時，UI會顯示明確文字，並透過警示區域觸發熒幕朗讀程式宣告。 作者會立即收到意見反應，且可在不失去內容的情況下修正問題。 (SITES-27155)
* 修正Sites Admin中的Reflow協助工具缺陷。 在400%的瀏覽器縮放比例下，工具列和格線控制項會重疊並在熒幕外推播按鍵動作，因此會封鎖鍵盤導覽和熒幕助讀程式的使用。 版面現在會正確重排，使搜尋、篩選和動作按鈕保持可見，並可在400%縮放下操作。 (SITES-27238)
* 修正頁面鎖定/解鎖工作流程中所顯示鎖定狀態訊息中的低對比度。 訊息現在符合4.5:1比例，提高作者的可讀性和ADA合規性。 (SITES-27270)
* 在&#x200B;**有效許可權**&#x200B;對話方塊中的核取記號圖示中新增可存取的名稱。 JAWS現在會朗讀圖示及其含義，改善鍵盤導覽和ADA合規性。 (SITES-27272)
* 隱藏的頁首導覽可接受焦點，並使視力正常的使用者和熒幕助讀程式使用者感到困惑。 更新會停用摺疊控制項的焦點，並只公開可見的專案。 導覽維持可預測且符合WCAG 2.4.3。 (SITES-35224)

* 修正網站管理員中的資料夾縮圖圖示，以做為裝飾性影像。 更新會移除影像角色並套用空白替代文字，因此輔助技術會忽略圖示並只讀取有意義的標籤。 (SITES-2852)
* Adobe增加網站首頁參考文字的色彩對比。 文字現在符合WCAG 2.1 AA，比例至少為4.5:1，並在淺色主題和明亮的熒幕上清楚閱讀。 (SITES-24755)
* 參考邊欄地標現在會向熒幕朗讀程式宣告其名稱。 區域會顯示唯一的`aria-label` （「參考邊欄」），以改進地標式導覽，並將其與其他區域區分開。 (SITES-24973)
* 說明RTE封鎖了前進索引標籤導覽，並中斷了對話方塊流程。 此修正可恢復標準鍵盤移動。 作者使用單一標籤繼續通過欄位，並保持選擇順序可預測。 (SITES-35228)
* 製作控制項缺少可存取的名稱和公開的原始圖示文字，這會讓JAWS感到困惑。 此修正新增明確的ARIA標籤和標準角色。 公告內容正確無誤，符合協助工具的期望。 (SITES-35227)
* 「類別」下拉式清單缺少特定標籤，因此JAWS會以一般「影像按鈕選單」發聲。 更新會將控制項命名為「類別」並定義其角色。 熒幕助讀程式的使用者可聽到正確的標籤，並瞭解可用的選擇。 (SITES-35226)
* 「屬性」對話方塊會顯示資料格線，將熒幕閱讀程式視為純文字。 JAWS和NVDA錯過了焦點，並且無法宣告列和欄。 此修正會新增真正的表格語意和ARIA角色。 熒幕助讀程式現在可辨識表格並正確追蹤焦點。 (SITES-35225)
* 內容片段文字編輯器已載入截斷的動作列。 圖示被剪裁，溢位功能表無法連線。 更新會修正版面，使完整工具列保持可見且可存取。 (SITES-33005)
* 基本索引標籤表單欄位無法顯示有用的錯誤文字。 表單現在會顯示清楚的內嵌訊息，並將其連結至欄位，以供熒幕助讀程式使用。 鍵盤和輔助技術使用者可獲得立即的指引來修正輸入。 (SITES-32480)
* 自訂元件中使用的多欄位會顯示未標籤的圖示按鈕和不一致的Tab順序。 JAWS/NVDA只會宣佈「按鈕」或略過控制項，這會封鎖鍵盤操作。 此更新提供新增、移除和移動的描述性名稱，標準化定位停駐點，並宣佈清單更新以符合ADA的期望。 (SITES-30660)
* 「快速發佈」現在會傳回明確的成功通知。 對話方塊關閉，快顯通知確認動作，熒幕朗讀程式會朗讀訊息，讓作者不會錯過結果。 (SITES-26912)
* 不需要變更。 Adobe已檢閱搜尋圖示與附近文字重疊的宣告。 標題含有客戶新增的標籤；vanilla AEM只會呈現圖示。 乾淨的執行個體以100%縮放顯示正確的版面，因此錯誤會因超出範圍而關閉。 (SITES-26910)
* 建立頁面主題不再隱藏焦點狀態。 在鍵盤導覽期間，**基本**&#x200B;索引標籤和相鄰的索引標籤上會呈現一致的醒目提示。 此變更可讓低視力使用者恢復可預測、可感知的焦點回饋。 (SITES-26907)



#### 管理員使用者介面{#sites-adminui-6524}

熒幕助讀程式的使用者在&#x200B;**目錄系統Blueprint**&#x200B;格線中未收到任何導覽說明。 JAWS只宣佈了牢房的位置，然後就陷入了沈默。 此版本新增了可存取的指南和角色，使JAWS能夠讀取清單內容、選取的專案和必要的箭頭/空格控制項。 (SITES-30661)

#### 傳統 UI{#sites-classicui-6524}

傳統UI核取方塊遺失其標籤，並顯示空白選項。 對話方塊也會顯示編碼的HTML，例如`<br>`。 更新會還原核取方塊標籤並解碼標示，讓對話方塊可正確讀取。 (SITES-31822)

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments] — 管理員{#sites-admin-6524}

內容片段名稱中的括弧導致「參考」面板誤報使用情形。 即使其他片段參考了0，作者也看見。 此修正修正「（」和「）」的路徑剖析，並呈現適當的非零計數和專案。 (SITES-35078)


#### [!DNL Content Fragments] — 片段編輯器{#sites-fragments-editor-6524}

* DAM路徑包含括弧的內容片段取消發佈失敗。 管理發布精靈重新寫入「（」和「）」並中斷資產路徑。 此修正會保留字元並解析正確的專案，以便完成取消發佈動作。 (SITES-35077)
* 編輯內容片段並返回Assets清單會隱藏片段或整個資料夾。 關閉編輯器後，無法重新整理清單。 此修正現在會可靠地重新整理清單，並保持編輯後的片段可見，不會進行硬式重新載入。 (SITES-35374)

* 內容片段編輯器無法開啟Polaris資產選擇器，因為已刪除必要的IMS範圍。 此修正會還原最小範圍，並重新建立傳遞連線。 資產瀏覽和選取功能可再次運作，且沒有HTTP 500錯誤。 (SITES-35837)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6524}

每次部署後，有效的GraphQL查詢開始傳回`GraphQL_QueryValidationError`。 端點保留過時的結構描述，直到團隊清除快取或重新啟動為止。 此修正會在部署期間重新整理GraphQL結構描述和持續查詢登入，並立即還原正常回應。 (SITES-34301)

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

ContextHub不再在發佈頁面上插入第二個jQuery副本。 區段引擎使用者端程式庫捨棄了提取jQuery 1.12.4的cq.shared相依性，因此網站載入一致的jQuery且前端程式碼能以可靠的方式運作。 (SITES-30404)

#### 體驗片段{#sites-experiencefragments-6524}

* 體驗片段現在會將不存在Adobe Target設定時顯示的警告內容當地語系化。 訊息會以作者的地區設定顯示，而非英文，因此匯出和啟用步驟可正確為全域團隊讀取。 (SITES-11868)
* 發佈體驗片段變數現在會在雲端服務未附加至變數時顯示當地語系化的錯誤訊息。 訊息會以使用者的語言顯示在UI中，而非僅英文字串。 (SITES-20293)
* 將體驗片段匯出至目標時因`Attempt to modify attribute at illegal index: -1`而當機。 Web Vitals檢測與匯出程式和損毀的屬性處理衝突。 此修正會強化屬性處理，並移除該衝突。 匯出成功，片段在Target中呈現。 (SITES-31891)

* 體驗片段屬性現在會將&#x200B;**參考**&#x200B;索引標籤當地語系化。 標籤和欄標題，例如「頁面」、「頁面路徑」和「變化標題」，會以作者的語言顯示。 此變更會移除僅英文字串，並讓全域團隊的屬性檢視保持一致。 (SITES-11203)
* **變數** > **建立工作流程**&#x200B;現在會顯示完整的翻譯文字。 此對話方塊可正確包裝內容並調整內容大小，以處理較長的語言環境字串，消除剪裁或截斷標籤。 (SITES-19304)
* 體驗片段屬性現在會將社群媒體狀態標籤本地化。 作者可在所有地區設定中，以選取的語言檢視狀態值，例如「已發佈」和「未發佈」。 此變更會移除在稽核期間導致混淆的純英文字串。 (SITES-20014)

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### 啟動{#sites-launches-6524}

* 刪除非常大的Launch會凍結存放庫。 此工作佇列太多移除作業，導致其他請求無法運作。 此修正現在會批次刪除並在區塊之間產生，因此清理會在系統保持回應狀態時完成。 (SITES-32004)

* 啟動設定>屬性顯示運作中的公司和屬性下拉式清單。 **儲存**&#x200B;和&#x200B;**關閉**&#x200B;會遵循已完成的欄位，而且標題驗證不再觸發公司或屬性上的錯誤。 (CQ-4359853)
* IMS設定中的必要檢查在更新時執行，而不只是在建立時。 使用者端ID或使用者端密碼等欄位中的空白值會顯示錯誤，並暫停儲存，直到輸入有效值為止，以防止重複使用先前的值。 (CQ-4359938)
* Launch建立會顯示轉譯的驗證和錯誤字串。 建立失敗和遺失來源頁面的英文訊息將不再出現。 在Launch設定期間，作者會看到清晰、地區設定正確的意見反應。 (SITES-13085)
* 啟動項促銷活動更新來源頁面上的頁面屬性`jcr:title`、`jcr:description`和`cq:redirectTarget`。 此變更會移除MSM轉出設定和工作流程邏輯中的屬性排除。 行銷活動、翻譯和SEO會維持標題、說明和重新導向的一致性。 (SITES-34509)
* Launch動作忽略範圍，並包含與目標區段共用相同父項的頁面。 更新會強制子樹邊界，並只升級所選頁面及其子系。 不相關的頁面會保留其現有內容。 (SITES-34344)
* 修正巢狀Launch自動促銷活動停止在Author並略過Publishing層級的問題。 子啟動的自動促銷會將更新的頁面發佈至已設定的發佈者，並依排程完成完整啟動。 (SITES-30420)

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM - Live Copies{#sites-msm-live-copies-6524}

* 資料夾層級轉出無法在該資料夾下建立體驗片段的即時副本。 個別轉出已運作，這會中斷大量工作流程。 此變更會將資料夾轉出與頁面行為對齊，並在子樹狀結構中傳播關係和參照。 (SITES-35161)
* 刪除即時副本中的元件後，**啟用繼承**&#x200B;因JavaScript錯誤而中斷，元件一直遺失，直到第二次嘗試為止。 此更新修正已刪除的重新載入以攜帶正確的引數，並取代過時的警報呼叫。 對話方塊會乾淨地開啟，且繼承會在第一次嘗試時還原。 (SITES-31387)
* 轉出精靈接受沒有日期的&#x200B;**稍後**。 作者已進階並建立轉出，但沒有排程。 更新會強制進行日期選取並顯示清除提示。 **繼續**&#x200B;動作會一直停用，直到日期存在為止。 (SITES-31374)


#### 頁面編輯器{#sites-pageeditor-6524}

* 在具有Personalization容器的頁面上開啟內容樹狀結構時，傳回空白面板和控制檯null參照錯誤。 作者無法挑選或設定元件。 更新會移除錯誤，並重新啟用樹狀結構和元件互動。 (SITES-34336)
* AEM 6.5 SP23中斷頁面編輯器中的模式切換。 按一下「**配置**」、「**開發人員**」或「**鎖定目標**」時，編輯器卡在「**編輯**」模式中，並擲回主控台`TypeError`。 更新會還原工具列模式變更並清除錯誤。 (SITES-34536)
* 當作者在長容器中新增元件時，「頁面編輯器」會從插入點跳離。 更新音調覆蓋時間和捲動處理。 檢視保持原位，新元件保持可見狀態並準備設定。 (SITES-32621)
* 自訂標籤標籤在頁面編輯器中失敗，且UI一律顯示「標籤」。 述詞現在會先評估`fieldLabel`和`labelText`秒，然後套用預設值。 作者會看到他們設定的標籤。 (SITES-32278)
* 取消Sites中的「位置」篩選器時，會使OmniSearch圖示未對齊，並與預留位置文字重疊。 圖示變成無法點按。 此修正會重新對齊圖示並還原點選區域，因此滑鼠和鍵盤都會觸發搜尋。 (SITES-30946)
* 選擇「開發人員」會使頁面處於不良狀態，並封鎖該頁面的撰寫作業。 面板消失且UI停止回應。 此更新會修復模式切換邏輯和快取處理，讓頁面可編輯，並立即顯示開發人員資料。 (SITES-30922)
* 在&#x200B;**插入新元件**&#x200B;中按一下&#x200B;**清除**&#x200B;並未移除搜尋查詢，並保留篩選為單一專案(Accordion)的清單。 此修正會重設查詢並重新整理清單。 所有允許的元件會再次出現。 (SITES-30921)

<!--
#### Replication{#sites-replication-6524}
-->

#### RTF 編輯器{#sites-rte-6524}

* 在全熒幕中，RTF編輯器會在沒有錯誤存在時，將「拼字檢查」結果隱藏在對話方塊後面。 更新將結果面板置於最前面，並使訊息和建議保持可見。 作者可在不離開全熒幕的情況下檢閱並接受更正。 (SITES-32366)
* RTF編輯器影像現在會遵循所選的對齊方式。 作者在影像對話方塊中設定左、中或右，編輯器在輸出中一致地套用該選擇。 此變更也會使「替代文字」對話方塊穩定，因此替代文字和對齊會儲存並在重新編輯時持續存在。 (SITES-30634)

#### 通用編輯器 {#sites-universal-editor-6524}

設定查詢權杖驗證處理常式會混淆使用者，因為標籤不符合欄位。 UI從路徑中擷取文字，並顯示錯誤的名稱。 此修正可還原服務排名和查詢權杖選項的清晰、準確標籤。 (SITES-31305)


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* 視訊的&#x200B;**選取縮圖**&#x200B;選項現在在AEM Assets - Dynamic Media中運作正常。 按一下會開啟對話方塊，並允許從Assets中選取縮圖，消除先前的無法使用滑鼠操作行為，並移除僅限視訊影格擷取的限制。 (ASSETS-58926)


### [!DNL Forms]{#forms-6524}

<!--
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, December 4, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

#### Forms Designer

* 使用者遇到在特定測試案例中無法點選超連結的問題，這影響了他們在應用程式中導覽和驗證連結的能力。 (LC-3923505)
* 使用者在使用AEM Forms Designer 6.5.23為非拉丁語言產生的PDF中，遇到協助工具問題。 路徑標籤未放置在成品容器內，導致PAC和熒幕閱讀器檢查失敗。 (LC-3923295)
* 使用者在使用輸出服務從6.5.21版修補到6.5.23版後，在可攜式檔案格式(PDF)文字方塊中遇到超連結中斷的問題。 (LC-3923290)
* 使用者遇到記錄檔案(DoR)表單的協助工具問題。 當輸入欄位空白時，熒幕助讀程式僅會讀取欄位標題，而非值，導致身心障礙使用者難以有效導覽表單。 (LC-3923234)
* 使用者在DoR PDF forms中遇到協助工具問題，其中NVDA錯誤讀取核取方塊、選項按鈕和文字欄位的「無法使用」，通常會重複訊息並為熒幕助讀程式使用者造成混淆。 (LC-3923201)
* 使用者在新增欄位時遇到XDP中的分頁簿訂單不一致。 現有的索引標籤順序意外變更，影響表單導覽。 (LC-3923183、LC-3922630)
* 使用者遇到HTML轉譯問題。 使用`docReady`事件時，未在HTML中正確觸發，導致指令碼無法如預期執行。 (LC-3923118)
* 使用者遇到PDF轉譯指令碼無法在AEM Forms Cloud生產環境中運作的問題。 (LC-3923082 )
* 使用者遇到表單中浮動欄位的問題。 使用不同的資料檔案時，浮動欄位會正確由一個檔案呈現，但無法與另一個檔案呈現，儘管與欄位無關的細微差異。 (LC-3923056)
* 在有多個主版頁面的XDP (XML Data Package)中只選取英文內容時，使用者遇到空白的西班牙主版頁面。 (LC-3923009)
* 使用者在AEM Designer中觀察到過時的著作權年份資訊。 此問題發生在啟動時的快顯方塊、「關於」區段和「法律注意事項」區段，顯示「2003-2024」而不是「2003-2025」。 (LC-3923005)
* 使用者在AEM Forms Designer中使用分頁時遇到空白的PDF頁面。 為WireAdviceHeader選取「下一頁頂端/頁面頂端」時發生問題，這會中斷資料疊代的版面配置。 (LC-3922997、LC-3922830)
* 使用者遇到可延伸標籤語言(XML)結構描述定義(XSD)的檔案摘要值未儲存在64位元版本的AEM Forms Designer中的問題。 (LC-3922924)
* 使用者在AEM Designer 6.5.19中遇到不穩定的超連結格式，其中文字方塊內的超連結錯誤地採用來自周圍文字的樣式，例如第一個字元的格式。 (LC-3922376)
* 使用者透過HTML OSGI v6.5.22在MAC上透過行動轉譯來轉譯AEM Forms表單時遇到問題。 (LC-3923058)
* 當使用者在使用Designer 6.5.23建立並透過PAC 2024分析的XDP範本中使用邊界或背景欄位時，可攜式檔案格式(PDF)檔案中遇到「路徑物件未標籤」錯誤。 (LC-3923013)
* 使用者在接收訊息「路徑物件未標籤」時，遇到可攜式應用程式元件(PAC)中標題「Dati Richiedente」的背景顏色錯誤。 (LC-3922912)
* 使用者遇到特定範本以壓縮字型取代預期字型的問題。 (LC-3922330)

#### 自適應表單

* 使用者在規則編輯器中遇到缺少選項的問題。 當作者撰寫有關數字輸入的規則時，無法使用查詢、UTM和瀏覽器詳細資料選項。 (FORMS-21660)
* 使用者在與OdataResponse互動時，由於Null指標例外狀況，導致應用程式當機。 (FORMS-20344)
* 使用者在建立規則以顯示面板並將焦點設定在面板內的元素時發生問題。 在可見度更新之前執行的setFocus規則會導致焦點動作失敗。 (FORMS-19563)
* 使用者在AEM Forms Author中選擇元件時遇到問題。 在編輯模式下的標籤之間導覽時，某些容器會變成無法選取，導致無法輕鬆識別和互動。 (FORMS-18525)
* 使用者嘗試在AEM 6.5.22中為資產加上註解時遇到「無效的URL」錯誤。 (NPR-42684)

### 基礎 {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

更新Felix網頁主控台套件組合以包含FELIX-6747。 此修補程式會修正先前中斷OSGi Web主控台中頁面轉譯和驗證的回應處理。 主控台會一致地載入，且不再在記錄中擲回IllegalStateException專案。 (NPR-42730)

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granite{#foundation-granite-6524}

* 原始或僅英文字串不再出現在&#x200B;**移除存取控制**&#x200B;對話方塊中。 此對話方塊會針對支援的語言顯示完全當地語系化的內容，以提供一致的協助工具。 (GRANITE-48479)
* 「說明」圖示現在會顯示輔助技術的簡要標籤。 JAWS閱讀「說明按鈕」，不再新增多餘的「選單」措辭。 此更新將控制項帶入WCAG 4.1.2中，並簡化鍵盤和熒幕助讀程式的使用。 (GRANITE-55360)
* 消除OSGi服務中的相依性回圈後，還原HTL指令碼引擎原廠。 環境啟動整齊，HTL轉譯可在創作Pod間運作，管理員不再遇到啟動失敗或缺少指令碼服務。 (GRANITE-58276)

* 頁首「搜尋」方塊不再覆蓋預留位置文字上的放大鏡圖示。 預留位置會以適當的邊框間距顯示，而且各個瀏覽器都能完整讀取。 (GRANITE-54391)
* 作者可在自動完成欄位中看到可讀標籤，而非對話方塊中的原始值。 實作可讓值儲存在JCR中，並改善以動態方式取得選項的單選與多選設定的清晰度。 (GRANITE-57615)
* htmlLibraryManager.debug設為true時，編輯模式仍可運作。 這項變更會還原適當的clientlib解析度和載入作業，讓開發人員在編寫期間能夠使用HTML Library Manager的偵錯工具。 (GRANITE-58002)
* 復寫代理程式編輯頁面不會再在傳統UI中擲回JavaScript錯誤。 頁面會開啟、顯示所有標籤，並儲存代理程式設定，不會出現主控台錯誤。 (GRANITE-58302)
* 修正了「系統概覽」中的健康狀態彙總。 現在，個別檢查執行後，檢視會更新，並顯示正確的計數。 當安全性與維護檢查通過時，操作員會看到「確定」，而不是錯誤的「2錯誤」橫幅。 (GRANITE-61482)
* 在AEM 6.5 LTS （長期支援）升級期間停止`CodeUpgradeTasks`執行。 升級現在無需作業觸發的存放庫變更或重新設定。 此修正可減少升級風險，並防止可避免的停機時間。 (GRANITE-61486)
* 在製作對話方塊中，必填欄位現在會顯示單一、精確的驗證錯誤。 出現時，訊息會使用欄位自己的標籤，而當不存在標籤時，會退回一般提示。 跨欄位的重複和不相符訊息不再出現。 (GRANITE-59531)
* 頁面建立精靈對話方塊現在會在每次互動中重新驗證必要欄位，包括索引標籤變更和多欄位編輯。 **建立**&#x200B;按鈕在作者完成所有必要的輸入之前會保持停用，精靈會顯示遺失值的內嵌錯誤。 (GRANITE-58826)

#### 整合{#foundation-integrations-6524}

當作者設定開始和結束日期時，發佈AEM Target活動不再失敗。 此整合會傳送包含時區的符合標準時間戳記，因此Target會處理活動裝載，並如預期完成同步。 (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### 本地化{#foundation-localization-6524}

* zh-CN的本地化會移除在資產作業（例如「移動」）期間所顯示的參考資料收集狀態中模糊的片語。 UI現在顯示`正在获取对 [[0]] 项的引用`，提供準確的含義和一致的術語。 (CQ-4354648)
* 建立智慧型集合時，重新整理時不再轉譯儲存的搜尋關鍵字。 輸入英文辭彙的作者會看到這些相同的辭彙會被保留，且系列會繼續傳回一致的結果。 (NPR-43158)
* 修正「影像」面板中截斷的工具提示文字。 「以快顯視窗顯示註解」說明在所有支援的區域設定中完全呈現，改善非英文作者的指南。 (SITES-10490)
* 網站管理欄檢視截斷的法文和西班牙文本地化標籤。 「結束時間」和「關閉時間」似乎已截斷，沒有顯示工具提示。 Adobe已修正翻譯，並在暫留時還原工具提示，因此標籤會完整閱讀。 (SITES-31318)
* Sites中的&#x200B;**移動**&#x200B;對話方塊顯示原始i18n金鑰而非可讀取的標籤。 「參考頁面」、「建立時間」、「建立者」和「路徑」等專案看起來會亂碼。 此修正會將對話方塊連結至正確的字典，並提供翻譯（含英文備援）。 (SITES-30881)

<!--
#### Oak {#foundation-oak-6524}
-->

#### Platform{#foundation-platform-6524}

* 驗證錯誤現在會顯示清楚的描述性文字，而非只有圖示。 熒幕助讀程式會在訊息出現時自動朗讀訊息，因此使用者不需要導覽至圖示即可瞭解問題。 (CQ-4359152)


* 游標離開控制項後，導覽列中的暫留標籤不再停留在熒幕上。 UI會在模糊或滑鼠移出時立即隱藏這些工具提示，避免視覺雜亂和誤按。 (CQ-4360030)
* 在Sites中，工具列動作會停止在重複點按時建立第二個快顯視窗。 按第二下會關閉現有的快顯視窗，只留下一個可見的實體，消除重疊和分散注意力的情況。 (CQ-4360038)
* 過時的2024年版權文字不再出現。 登入頁面和&#x200B;**說明** > **關於AEM**&#x200B;快顯視窗2025年顯示，而AEM會以程式設計方式讀取年度以避免手動編輯。 (CQ-4360042)
* 按一下AEM標題列中的工具提示時，不再觸發基礎動作。 快顯視窗僅在使用者按一下實際按鈕時開啟，以防止在與工具提示文字互動時意外出現對話方塊。 (CQ-4360105)
* 年份變換不再保留過時的版權文字。 登入畫面和&#x200B;**說明** > **關於AEM**&#x200B;對話方塊會從系統時鐘衍生年度，並在每次UI載入時呈現最新值。 (CQ-4360173)
* 標題列快顯視窗現在可以正確切換。 按一下相同的動作（例如，**搜尋**&#x200B;或&#x200B;**篩選器**）會關閉開啟的快顯視窗，而非開啟另一個覆蓋圖。 這項變更可避免棧疊快顯視窗，並將焦點傳回頁首控制項。 (NPR-42891)
* 專案和收件匣行事曆檢視會正確轉譯。 切換檢視不會再遮蔽頁面；行事曆會載入並顯示排程專案。 (NPR-42968)

<!--
#### Security{#foundation-security-6524}
-->

#### Sling{#foundation-sling-6524}

* 修正`org.apache.sling.scripting.jsp:2.6.0`套件組合發生未預期的JSP編譯錯誤。 (SLING-12442)
* 該平台將核心Sling Engine從2.16.2升級至2.16.6。較新的引擎可強化輸入驗證，並穩定負載下的請求處理。 (NPR-43105)

#### SPA編輯器 {#foundation-spa-editor-6524}

開啟Sling主要Servlet **檢查Content-Type**&#x200B;覆寫中斷AEM 6.5 SP21/22中的`.model.json`匯出。 由於匯出工具反向了型別中間鏈，因此要求傳回HTML或錯誤。 此修正從一開始便會以正確的型別傳送JSON，因此`.model.json`適用於作者和發佈環境。 (SITES-32634)


#### 翻譯{#foundation-translation-6524}

* 已新增翻譯專案狀態的重新索引操作。 當狀態檢視不同步時，管理員可以重建支援索引、還原結果，並消除Oak周遊警告。 頁面載入速度更快，並顯示目前的作業狀態。 (NPR-42699)
* 修正XLIFF匯入回報成功，但JSON字典檔案未變更的回歸。 匯入現在會鎖定正確的i18n路徑並持續翻譯，因此本地化往返無需手動編輯即可完成。 (NPR-42989)


* 翻譯規則XML現在會如設定般運作。 轉譯架構遵循例外狀況規則，並在工作建立期間正確套用至`include`和`exclude`模式。 翻譯請求不再傳送已排除的內容。 (NPR-42761)



#### 使用者介面{#foundation-ui-6524}

* 修正停用「Adobe Stock授權」對話方塊中輸入內容的UI回歸。 此對話方塊現在會正常運作，接受必填欄位中的文字，並從「資產詳細資訊」檢視中完成Stock資產授權流程。 (NPR-42748)

* 已修正作者環境中的群組可見性。 「群組」主控台不再止步於約41個結果，並會為每位使用者傳回完整的成員資格集。 此修正可恢復累積修正後的一致行為，並保持目前的安全性強化。 (NPR-42749)


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## 安裝[!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0需要[!DNL Experience Manager] 6.5。如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用封裝管理員在其中一個作者執行個體上安裝[!DNL Experience Manager] 6.5.24.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝[!DNL Experience Manager] 6.5.24.0套件。 因此，在安裝套件之前，您應該建立`crx-repository`的備份，以備您必須復原它時使用。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在[!DNL Experience Manager] 6.5上安裝Service Pack{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip)下載Service Sack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。

1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 請參閱[Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>Service Pack安裝期間，Package Manager UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在[!DNL Safari]瀏覽器中，但可能間歇性地發生在任何瀏覽器中。

**自動安裝**

您可以使用兩種不同的方法來安裝[!DNL Experience Manager] 6.5.24.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。 套件會自動安裝。
* 使用封裝管理員[的](/help/sites-administering/package-manager.md#package-share)HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

>[!NOTE]
>
>Experience Manager 6.5.24.0不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁(`/system/console/productinfo`)會在`Adobe Experience Manager (6.5.24.0)`已安裝產品[!UICONTROL 下顯示更新的版本字串]。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi主控台中，所有OSGi套件組合均為&#x200B;**[!UICONTROL 作用中]**&#x200B;或&#x200B;**[!UICONTROL 片段]** （使用Web主控台： `/system/console/bundles`）。

1. OSGi套件`org.apache.jackrabbit.oak-core`是1.22.20或更新版本（使用Web主控台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安裝[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱[Experience Manager Forms Service Pack安裝說明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝適用於Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝[Experience Manager內容片段搭配GraphQL索引套件1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.24.0的UberJar可在[Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.24/)中使用。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`classifier`標籤沒有`apis`，其值為`dependency`。



## 已棄用和已移除的功能{#removed-deprecated-features}

如需AEM 6.5已棄用或移除之所有功能的詳細清單，請參閱[已棄用和移除的功能](/help/release-notes/deprecated-removed-features.md)。

### SPA 編輯器 {#spa-editor}

[從AEM 6.5版本6.5.24開始的新專案已棄用SPA編輯器](/help/sites-developing/spa-overview.md)。SPA Editor仍支援現有專案，但不應用於新專案。

目前，AEM 中用於管理 Headless 內容的首選編輯器為：

* [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。
* [內容片段編輯器](/help/sites-developing/universal-editor/introduction.md)，用於表單型編輯。

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **與Oak相關**
從Service Pack 13及更高版本開始，下列錯誤記錄檔開始出現，這會影響持續性快取：

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  或

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  若要解決此例外狀況，請執行下列動作：

   1. 從`crx-quickstart/repository/`中刪除以下兩個資料夾

      * `cache`
      * `diff-cache`

   1. 安裝Service Pack，或重新啟動Experience Manager as a Cloud Service。
`cache`和`diff-cache`的新資料夾會自動建立，而您在`mvstore`中不會再遇到與`error.log`相關的例外狀況。

* 更新可能已使用您內容模型的自訂API名稱的GraphQL查詢，以改用內容模型的預設名稱。

* GraphQL查詢可以使用`damAssetLucene`索引，而不是`fragments`索引。 此動作可能會導致GraphQL查詢失敗或需要很長時間才能執行。

  若要修正問題，`damAssetLucene`必須設定為在`/indexRules/dam:Asset/properties`下包含下列兩個屬性：

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  在變更索引定義之後，需要重新索引(`reindex` = `true`)。

  執行這些步驟後，GraphQL查詢應該可以更快執行。

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，在擷取內容片段參考時出現問題。 背景查詢失敗。 也就是說，功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點`/oak:index/damAssetLucene` （不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您將[!DNL Experience Manager]執行個體從6.5.0 - 6.5.4升級至Java™ 11上的最新Service Pack，您會在`RRD4JReporter`檔案中看到`error.log`例外狀況。 若要停止例外狀況，請重新啟動[!DNL Experience Manager]的執行個體。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在[!DNL Assets]中重新命名階層中的資料夾，並將巢狀資料夾發佈至[!DNL Brand Portal]。 但是，在重新發佈根資料夾之前，[!DNL Brand Portal]中的資料夾標題不會更新。

* 安裝[!DNL Experience Manager] 6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「當使用Adobe Target API （IMS驗證）在[!DNL Experience Manager]中設定Target Standard整合時，將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target會建立多個型別為「HTML」/來源「Adobe Target Classic」的選件，而非「體驗片段」/來源「Adobe Experience Manager」型別。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`找不到維護期間。
   * 使用彙總函式(例如SUM、MAX和MIN)時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`找不到維護期間。
   * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，```org.apache.servicemix.bundles.rhino```套件提供的Rhino JavaScript Engine有新的提升行為。 使用嚴格模式(```use strict;```)的指令碼必須宣告其正確的變數。 否則，它們不會執行，並最終擲回執行階段錯誤。

* 透過正式更新套件安裝標籤相關的現成可用內容會將`/content/cq:tags`節點的languages屬性重設為預設值。 此動作適用於Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等。 因此，在安裝之前，必須從屬性新增它。

### AEM Sites的已知問題 {#known-issues-aem-sites-6524}

內容片段 — 預覽失敗，因為大型片段樹受到DoS保護。 請參閱有關預設GraphQL查詢執行器組態選項[的](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)KB文章(SITES-17934)

### AEM Forms的已知問題 {#known-issues-aem-forms-6524}

>[!NOTE]
>
>在沒有可用的Hotfix時，請避免升級至Service Pack 6.5.24.0以解決問題。 這可能會導致意外的錯誤。 只有在發行必要的Hotfix之後，才能升級至Service Pack 6.5.24.0。

#### 可用的Hotfix問題 {#aem-forms-issues-with-hotfixes}

下列問題有可供下載和安裝的Hotfix。 您可以[下載並安裝Hotfix](/help/release-notes/aem-forms-hotfix.md)以解決下列問題：

* **FORMS-20203**：當使用者將Struts架構從2.5.x版升級為6.x版時，AEM Forms中的原則UI無法顯示所有設定，例如新增浮水印的選項。

* **FORMS-20360**：升級至AEM Forms Service Pack 6.5.24.0後，ImageToPDF轉換服務會失敗，並出現錯誤：
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478**：嘗試將型別7/8 TIFF檔案轉換成PDF時，轉換程式會失敗，錯誤為「ALC-PDG-001-000-Image2Pdf轉換失敗，原因為：com/sun/image/codec/jpeg/JPEGCodec」和「ALC-PDG-016-003-PDF後處理期間發生未知/未預期的錯誤」。 系統會嘗試使用TM ImageIO TIFF解碼器重試，但最終無法完成工作。

* **FORMS-14521**：如果使用者嘗試預覽含有已儲存XML資料的草稿信件，某些特定信件的草稿信件會卡在`Loading`狀態。

* AEM Forms現在包含表單元件的Struts版本從2.5.33升級至6.x。 此升級提供先前未包含在SP24中的Struts變更。 已透過[Hotfix](/help/release-notes/aem-forms-hotfix.md)新增支援，您可以下載並安裝該支援，以新增對最新版Struts的支援。

#### 其他已知問題 {#aem-forms-other-known-issues}

* 安裝AEM Forms JEE Service Pack 21 (6.5.21.0)後，如果在`(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`資料夾(FORMS-14926)下找到Geode jar `<AEM_Forms_Installation>/lib/caching/lib`的重複專案，請執行以下步驟以解決問題：

   1. 停止儲位（如果它們正在執行）。
   2. 停止AEM伺服器。
   3. 移至`<AEM_Forms_Installation>/lib/caching/lib`。
   4. 移除除`geode-*-1.15.1.2.jar`以外的所有Geode修補程式檔案。 確認只有具有`version 1.15.1.2`的Geode jar存在。
   5. 在管理員模式中開啟命令提示字元。
   6. 使用`geode-*-1.15.1.2.jar`檔案安裝Geode修補程式。

* 當使用者從AEM 6.5 Forms Service Pack 18或19升級為Service Pack 20或21時，他們遇到JSP編譯錯誤。 此錯誤會阻止他們開啟或建立最適化表單。 它也會導致其他AEM介面發生問題。 這些介麵包含頁面編輯器、AEM Forms UI、工作流程編輯器和系統概覽UI。 (FORMS-15256)

  如果您遇到這類問題，請執行以下步驟來解決問題：
   1. 導覽至CRXDE中的目錄`/libs/fd/aemforms/install/`。
   2. 刪除名稱為`com.adobe.granite.ui.commons-5.10.26.jar`的組合。
   3. 重新啟動AEM伺服器。

* 在互動式通訊代理程式UI的列印預覽中，所有欄位值都會不一致地顯示貨幣符號（例如美元符號$）。 對於最多999的值會顯示它，但對於1000或以上的值則遺失。 (FORMS-16557)
* 互動式通訊中巢狀配置片段XDP的任何修改都不會反映在IC編輯器中。 (FORMS-16575)
* 在互動式通訊代理程式UI的列印預覽中，部分計算值無法正確顯示。 (FORMS-16603)
* 在「列印預覽」中檢視信函時，內容會變更。 也就是說，某些空格會消失，而某些字母會以`x`取代。 (FORMS-15681)
* **FORMS-15428**：使用Forms附加元件更新至AEM Forms Service Pack 20 (6.5.20.0)後，依賴舊版Adobe Analytics Cloud Service （使用認證型驗證）的設定停止運作。 此問題導致Analytics規則無法正確執行。

* 當使用者設定WebLogic 14c執行個體時，在JBoss®上執行的JEE上的AEM Forms Service Pack 21 (6.5.21.0)中的PDFG服務會失敗，因為類別載入器衝突涉及SLF4J程式庫。 錯誤顯示如下(CQDOC-22178)：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* Forms-21378：啟用伺服器端驗證(SSV)時，表單提交可能會失敗。 如果您遇到此問題，請聯絡Adobe支援以尋求協助。



## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出此[!DNL Experience Manager] 6.5 Service Pack發行版本中包含的OSGi套件組合和內容套件：

* [Experience Manager中包含的OSGi套件組合清單6.5.24.0](/help/release-notes/assets/65240-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager中包含的內容套件清單6.5.24.0](/help/release-notes/assets/65240-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/tw/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
