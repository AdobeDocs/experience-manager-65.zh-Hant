---
title: ' [!DNL Adobe Experience Manager] 6.5的發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5的版本資訊、新增功能、安裝操作說明和詳細變更清單。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 87e11d37b9aa14ee3d4e47ae30eaa25f151a9b5b
workflow-type: tm+mt
source-wordcount: '7373'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 發行摘要 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2026年5月21日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

Experience Manager 6.5.25.0包含新功能、客戶要求的重要增強功能和錯誤修正。 此外，也包含自2019年4月起以6.5為基礎所建置的效能、穩定性和安全性改善專案。

此Service Pack發行版本提供Sites、Assets和Foundation的275個後端連線埠，包括關鍵錯誤修正和安全性強化。 此版本也透過廣泛的鍵盤導覽、焦點管理、ARIA語意、色彩對比改良以及符合WCAG標準的觸控目標大小調整，來提升網站撰寫的協助工具。

此發行版本預設提供交叉通道，不需要在安裝後另外安裝套件或組態。

安全性後端連線埠可解決XSS弱點並改善共用資產中繼資料的處理方式。

內容片段和GraphQL API也獲得可靠性改善，包括內嵌影像參考、持續查詢處理和編輯器本地化。


<!-- UPDATE FOR EACH NEW RELEASE -->

### Forms的主要功能和增強功能

* [多執行緒PDF Generator轉換](/help/forms/using/install-configure-document-services.md#windows-only-enable-multi-threaded-pdf-generator-conversions)：新增支援，當AEM Forms在單一設定的使用者帳戶下以Windows服務形式執行時，可同時執行Microsoft Word (doc/docx)和Excel (xls/xlsx)轉換。

* [XFA型PDF的階層式書籤](https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：輸出服務和AEM Forms Designer現在會在靜態互動和平坦的XFA型PDF中產生結構化的書籤階層。 書籤會依照在文字方塊的「協助工具」屬性中設定的標題層級(H1-H6)顯示，因此H1-H6專案會巢狀內嵌在正確的父項下，而非平行顯示。

* [&#x200B; JEE交易記錄中的表單層級詳細資料](/help/forms/using/transaction-report-overview-jee.md#form-level-details-transaction-log-jee)： JEE上的AEM Forms現在會將每個交易的表單層級詳細資料記錄在`transaction_log.log`中，以及現有的服務和操作資訊。 管理員可在分析提交、轉譯和轉換時，將交易報告資料與特定表單建立關聯。 (FORMS-21574)

* [已更新支援的平台矩陣](/help/forms/using/aem-forms-jee-supported-platforms.md)： JEE Service Pack上的AEM Forms 6.5.25.0新增支援與下列較新技術的相容性：
   * JBoss® Enterprise Application Platform (EAP) 7.4.23
   * ® Content Manager Client 8.7
   * ® Windows Terminal Server 2025上的AEM Forms Designer

  >[!NOTE]
  >
  > 若要將JBoss EAP從7.4.10升級至7.4.23，請參閱：
  > * [針對獨立環境，將JEE版AEM Forms的JBoss EAP從7.4.10升級至7.4.23](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md)。
  > * [針對叢集環境，將JEE上的AEM Forms的JBoss EAP叢集從7.4.10升級至7.4.23。](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md)

## 已修正Service Pack 25中的問題 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### 協助工具 {#sites-accessibility-6525}

* 網站清單檢視中的表格列拖放控制項現在可用於鍵盤導覽。 熒幕助讀程式和鍵盤使用者可在動作期間重新排序資料列並接收回饋。 (SITES-24946)

* 「編輯版面」工具列現在會在有意義的熒幕助讀程式序列中顯示較小的熒幕和Tablet標籤。 使用者會聽到具有相關尺標測量值的標籤，而非聽見標籤順序不正。 (SITES-25291)
* 「色票彈出視窗」強制回應視窗現在會從註解強制回應視窗開啟時，正確管理焦點。 焦點從模組標題開始，而不是直接移至選取的色票按鈕。 (SITES-25275)
* Teaser強制回應視窗現在提供使用鍵盤移動對話方塊的協助工具。 使用者不再需要滑鼠來重新定位頁面上的強制回應視窗。 (SITES-25226)
* 卡片檢視可移除不必要的ARIA格線行為，進而改善協助工具。 熒幕助讀程式的使用者會收到較清楚的卡片資訊，且不會收到不符合視覺版面的格線導覽控制項。 (SITES-24933)
* 重複暫留動作後，「刪除」強制回應視窗中的工具提示現在會一致顯示。 使用者可以將指標移開並返回圖示以再次閱讀工具提示。 (SITES-24778)
* 現在，使用者從Sites首頁開啟左側邊欄後，左側邊欄會依預期順序收到焦點。 鍵盤和熒幕助讀程式的使用者可從設定按鈕移至邊欄內容，無需略過擴充區域。 (SITES-24754)
* 「焦點」管理現在可在輪播模式對話方塊中一致運作。 鍵盤和熒幕助讀程式的使用者可以從模組標題開始，並在關閉對話方塊後返回原始控制項。 (SITES-24716)
* 現在，「連結選取」對話方塊會將焦點傳回至使用者關閉對話方塊後開啟該對話方塊的控制項。 關閉對話方塊後，鍵盤和熒幕助讀程式的使用者不再失去位置。 (SITES-24707)
* 當作者開啟或關閉對話方塊時，「影像」強制回應視窗不再將焦點移至第一個索引標籤或首頁面地標。 焦點會先移至對話方塊標題，然後回到開啟對話方塊的控制。 (SITES-24693)
* 現在，當強制回應對話方塊開啟時，「參考邊欄」可正確管理焦點。 鍵盤和熒幕助讀程式的使用者會保留在對話方塊內，直到關閉為止，然後繼續導覽，而不會失去內容。 (SITES-24683)
* 當作者開啟或關閉超連結路徑選擇模式時，該模式不再將焦點移至錯誤的欄位或控制項。 焦點從強制回應視窗標題開始，然後返回到開啟強制回應視窗的按鈕。 (SITES-24672)
* 作者開啟或關閉Teaser強制回應視窗時，不會將焦點移至第一個標籤或頁面頂端。 焦點現在會遵循預期的對話方塊流程，並減少不必要的熒幕助讀程式宣告。 (SITES-24522)

* 頁面編輯器鎖定按鈕現在可提供更精確的熒幕助讀程式意見反應。 熒幕助讀程式會在有空時使用title屬性，以減少使用輔助技術的作者的詳細公告。 (SITES-41431)
* 鍵盤導覽現在會略過隱藏的內容。 使用者可以在可見的介面元素中移動，而不會將焦點移至他們看不到的內容。 (SITES-41430)
* 現在，使用者關閉覆蓋後，鍵盤焦點會回到觸發元素。 頁面編輯器不再將焦點傳回覆蓋圖，這會改善鍵盤使用者的導覽功能。 (SITES-40819)
* 當使用者使用鍵盤導覽工具列專案時，頁面編輯器工具列現在會顯示標籤，例如工具提示。 當焦點在不同專案間移動時，使用者可以瞭解每個工具列動作。 (SITES-40751)
* 將滑鼠懸停在元件瀏覽器專案上，不再移除使用中文字元件的焦點。 作者可以編輯文字而不會中斷，鍵盤焦點仍可預測。 (SITES-35370)
* 熒幕助讀程式現在會更清楚宣告搜尋模組排序方向按鈕。 按鈕標籤不再重複相同的方向，能更妥善地描述切換行為。 (SITES-25534)
* 「搜尋強制回應視窗」現在會在「變更檔案」或「資料夾」清單方塊中顯示所選選項的視覺指示器。 使用者可識別目前的階層連結選項，而不需單獨依賴焦點。 (SITES-25532)
* 「搜尋強制回應視窗」現在會增加「排序依據」標籤的對比。 文字元合協助工具要求，並改善視力缺佳使用者的可讀性。 (SITES-25531)
* 裝置選取按鈕現在會在「編輯配置」工具列中顯示正確的目前狀態資訊。 熒幕助讀程式的使用者可識別作用中裝置，而不會聽到誤導的切換狀態。 (SITES-25524)
* 當焦點離開時，鍵盤和熒幕助讀程式導覽現在會關閉「收件匣」功能表。 使用者可避免當焦點移至其他位置時，功能表保持開啟狀態的混亂狀態。 (SITES-25518)
* 當焦點離開時，鍵盤和熒幕助讀程式導覽現在會關閉「說明」功能表。 當選單保持開啟時，焦點不再移動到選單之外的內容。 (SITES-25517)
* 內容片段首頁現在為側邊欄標籤提供了一致的存取標籤。 使用者導覽標籤控制項時，NVDA會正確宣告標籤標籤。 (SITES-25509)
* 「頁面資訊」功能表中的「焦點」選項現在符合最低對比需求。 改善的對比可協助視力缺佳的使用者識別使用中的功能表專案。 (SITES-25321)
* 鍵盤導覽現在會略過摺疊的人口統計工具列中的隱藏控制項。 焦點會停留在可見的互動元素上，這會改善版面預覽中的導覽順序。 (SITES-25304)
* 「旋轉裝置」按鈕現在可在「編輯版面」工具列中提供更清晰的熒幕助讀程式意見反應。 熒幕助讀程式會朗讀目前的方向以及變更方向的動作。 (SITES-25292)
* 「編輯版面」工具列現在會顯示「案頭」按鈕的清除選取狀態。 「案頭」選項與其他裝置按鈕相符，讓使用中的檢視更容易識別。 (SITES-25290)
* 「編輯版面」工具列現在會標籤輔助技術的尺標區域。 熒幕助讀程式的使用者在版面編輯期間不會再遇到未標籤的測量值。 (SITES-25287)
* 「編輯版面」工具列現在會以未勾選的狀態顯示完整的iPhone 8 Plus按鈕標籤。 當按鈕周圍有足夠的空間時，標籤不再截斷。 (SITES-25284)
* 報告的問題說明「編輯配置」工具列中有一個焦點指示器，似乎涵蓋多個裝置控制項。 當焦點外框包含相鄰按鈕時，可能會失去作用中控制項追蹤的鍵盤使用者會成為關注的焦點。 問題按預期運作。 (SITES-25283)
* 所報告的問題描述了在每個按鈕標籤之前宣佈註解的註解模式按鈕。 令人擔心的焦點在於不清楚的熒幕助讀程式輸出，以執行如註釋、色票和刪除等動作。 (SITES-25277)
* 註解按鈕文字現在在註解強制回應視窗中使用足夠的對比。 此更新可改善視力缺佳使用者的可讀性，並支援WCAG對比度要求。 (SITES-25267)
* 熒幕助讀程式現在會在使用者篩選「插入新元件」清單時收到狀態更新。 強制回應會朗讀結果變更，讓使用者瞭解清單在他們輸入時發生了變更。 (SITES-25251)
* 記錄的問題說明註釋模組標題缺少標題語意。 問題是熒幕助讀程式導覽和瞭解模組結構的能力。 (SITES-25248)
* 頁面編輯器側邊欄中的標題層級，現在會遵循更清楚的內容階層。 左側欄區段不再顯示為輔助技術的主要頁面標題。 (SITES-25222)
* Assets左側邊欄中的「編輯」按鈕現在擁有較大的觸控目標。 具有行動需求的使用者可以更輕鬆地啟動按鈕，並避免附近的控制項。 (SITES-25221)
* Assets左側邊欄現在會在「編輯」按鈕開啟新的瀏覽器標籤時識別。 使用者可以預期導覽變更，而非意外遺失內容。 (SITES-25220)
* 現在，使用者套用增加文字間距時，元件標題可正確顯示。 側邊欄會保留可讀的標籤，並支援WCAG文字間距要求。 (SITES-25219)
* 側邊欄元件中的篩選器欄位現在會顯示適當的存取名稱。 此更新可協助熒幕助讀程式的使用者識別欄位，而不需依賴預留位置文字。 (SITES-25212)
* 報告的問題說明註釋模式中存在不邏輯的焦點順序。 據報導，鍵盤使用者錯過了註釋工具列，除非他們在啟動模式後使用Shift+Tab。 (SITES-24996)
* 編輯器畫布會顯示其頂端列標題為標題。 熒幕助讀程式可用正確的結構朗讀標題，以改善導覽和頁面理解。 (SITES-24993)
* 協助工具報告指出，當使用者切換檢視時，載入狀態訊息的對比度不足。 重點在於視力缺佳或色盲的使用者的可讀性。 (SITES-24991)
* 協助工具報告指出卡片連結包含非描述性文字。 重點在於協助熒幕助讀程式的使用者瞭解每個連結目的地，而不需要額外的內容。 (SITES-24975)
* 「網站」清單檢視現在會顯示對比較強的即時副本文字。 這項更新改善了視力缺佳的作者以及在明亮熒幕條件下工作的使用者的可讀性。 (SITES-24956)
* 現在，鍵盤導覽在使用者展開模擬器選單後，焦點會移至該選單。 此行為可協助熒幕助讀程式和鍵盤使用者以預期順序存取功能表選項。 (SITES-24954)
* 網站清單檢視現在可改善表格列中拖放按鈕的可見度。 當作者重新排序內容時，可以更輕鬆地識別控制項。 (SITES-24951)
* 當影像連結和標題連結共用相同目的地時，卡片不會再同時公開為個別連結。 此更新可降低熒幕助讀程式的詳細程度，並提升導覽效率。 (SITES-24947)
* 頁首功能表按鈕現在會使用更精確的協助工具屬性。 熒幕助讀程式會朗讀按鈕作為可展開的控制項，而非開啟對話方塊的控制項。 (SITES-24742)
* 收件匣現在會以語意清單標籤來標籤相關連結。 熒幕助讀程式的使用者可更輕鬆瞭解收件匣連結的數量和分組。 (SITES-24730)
* 頁首按鈕標籤現在可避免詳細的可存取名稱。 熒幕助讀程式的使用者會收到更清楚的公告，圖示文字不會顯示重複的角色資訊。 (SITES-24715)
* CSV報表按鈕現在提供有關新標籤行為的更清楚意見反應。 使用者可以瞭解，選取按鈕會在啟動前開啟新的瀏覽器索引標籤。 (SITES-24704)
* 模型對話方塊現在會針對標題控制項使用更精確的協助工具標示。 說明和切換全熒幕按鈕仍為互動式控制項，不再顯示為熒幕助讀程式的標題。 (SITES-24696)
* 「篩選器邊欄」地標現在會使用不同的標籤來識別其用途。 熒幕助讀程式的使用者可以更自信地導覽具有多個類似地標的頁面。 (SITES-24686)
* 參考邊欄訊息現在為依賴足夠文字對比的使用者提供更好的可讀性。 報告的問題涉及選擇範圍和多重選擇訊息，在背景中看起來太淺。 (SITES-24666)
* 「搜尋」強制回應視窗現在會為「移除位置」和「關閉」按鈕提供較大的觸控目標。 這項變更可協助手部顫動、痙攣或視力缺佳的使用者啟動預期的控制項。 (SITES-24530)
* Adobe Experience Manager標題連結報告為使用不正確的ARIA屬性。 測試確認連結控制可擴充內容，因此現有的存取狀態仍然適當。 (SITES-24528)
* 「元件」清單中「署名」按鈕的焦點指示器不再顯示為截斷。 可見的大綱可協助鍵盤使用者追蹤其在編輯器中的位置。 (SITES-24503)
* 一個回報問題說明「元件」面板中資訊工具提示圖示遺漏替代文字。 問題並未重現，但檢閱確認資訊圖示必須公開清楚的存取名稱。 (SITES-24500)
* 頁面編輯器不再使用相同標籤公開多個區域地標。 現在，每個地標都有一個唯一的可存取名稱，讓熒幕助讀程式的使用者可以識別目前的區域。 (SITES-24497)
* 「變更」檔案或資料夾控制項現在會將控制項標籤與其狀態資訊分開。 熒幕助讀程式的使用者在導覽頁首控制項時，會聽到較短、更清楚的名稱。 (SITES-24496)
* 內容片段管理員表格中的互動式控制項現在支援標準鍵盤導覽。 鍵盤使用者可以Tab鍵跳至按鈕和連結，而非僅透過方向鍵導覽來探索。 (SITES-24285)
* 網站管理員UI現在可正確處理熒幕助讀程式的裝飾性地球圖示。 這些圖示使用空白的替代文字，讓使用者只聽到有意義的介面內容。 (SITES-3057)

#### 管理員使用者介面{#sites-adminui-6525}

Sites主控台現在可正確顯示儲存的&#x200B;**清單檢視**&#x200B;欄設定。 當作者重新開啟設定對話方塊時，選取的欄會保持核取狀態，而作用中的欄計數則保持正確。 (SITES-38576)

#### 傳統 UI{#sites-classicui-6525}

傳統UI文字元件對話方塊現在會將RTF編輯器(RTE)內容顯示為格式化文字，而非原始HTML。 作者無須切換至Source模式或手動移除標示，即可編輯現有文字。 (SITES-38709)

#### 元件主控台{#sites-component-console-6525}

* 使用者現在可以使用當地語系化或多位元組字元來搜尋「元件」主控台。 主控台也顯示當地語系化的&#x200B;**Remove**&#x200B;標籤，而非未翻譯的英文字串。 (SITES-39747)
* 元件屬性頁面現在會將「工具>元件>元件屬性」中的字串當地語系化。 使用者在本地化撰寫介面中不會再看到未翻譯的英文標籤。 (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

Assets搜尋現在會在使用者選取或變更篩選器時正確回應。 篩選的結果集會如預期更新，還原Assets主控台中的可靠搜尋細分。 (SITES-38686)

#### [!DNL Content Fragments] - 管理員{#sites-admin-6525}

* Assets清單檢視現在會顯示已鎖定內容片段的本地化「取出者」工具提示。 此修正可改善作者檢閱工作流程列時的本地化一致性。 (SITES-42531)

* AEM現在會在內容片段下載對話方塊中將主要標籤當地語系化。 此修正可讓下載工作流程在非英文地區設定中保持一致。 (SITES-42534)
* 當作者從Assets排程內容片段發佈時，AEM現在會翻譯`Later`狀態標籤。 此修正會保持本地化介面中「已發佈」欄的一致性。 (SITES-42532)
* 現在，當作者在「標題」欄位中輸入無效字元時，內容片段建立會顯示當地語系化的驗證訊息。 對話方塊不再顯示未當地語系化的「提供的名稱無效」字串。 (SITES-19796)
* 編輯內容片段頁面現在為標籤和集合使用本地化的標籤。 作者會看到翻譯的欄位名稱，而非未本地化的英文字串。 (SITES-977)

#### [!DNL Content Fragments] - 片段編輯器{#sites-fragments-editor-6525}

* 現在，當作者從集合中移除內容時，內容片段編輯器中的關聯內容會顯示正確的當地語系化字串。 對話方塊不再以未定義取代內容名稱。 (SITES-33675)
* 內容片段編輯器現在會顯示已翻譯的一般標籤，以供沒有設定預留位置的索引標籤使用。 本地化的介面不再在該編輯器區域顯示未翻譯的英文字串。 (SITES-30715)
* 內容片段編輯器中的內容參考選擇器現在會顯示允許之資產型別的本地化標籤。 當地語系化的介面不再顯示支援資產類別的英文型別名稱。 (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6525}

* 當DAM檔案名稱包含空格或非ASCII字元時，GraphQL JSON回應現在包含內容片段RTF欄位中的內嵌影像參考。 此修正可協助應用程式呈現參照的影像，而不需要作者重新命名資產。 (SITES-42191)
* 內容片段的GraphQL回應現在可以更可靠地處理持續查詢。 更新會更正重複的快取標題、改善編碼變數的處理方式，並針對缺少內容或失敗的查詢傳回更清楚的回應。 (SITES-40159)
* GraphQL持續查詢現在會在紀錄中執行而不會出現不必要的ERROR和WARN訊息。 AEM可正確處理編碼變數，因此成功的查詢不會再產生誤導性的`PersistedQueryServlet`專案。 (SITES-39354)

* 編輯GraphQL端點對話方塊現在會將其介面字串當地語系化。 使用者不會再看到未翻譯的GraphQL結構描述是從本地化介面的設定訊息中取得。 (SITES-34018)

#### [!DNL Content Fragments] - GraphQL 查詢編輯器{#sites-graphql-query-editor-6525}

當選取的設定瀏覽器名稱包含CJK或斯拉夫文字字元時，使用者現在可以開啟GraphQL查詢編輯器。 編輯器顯示端點的持續查詢，而不是顯示錯誤。 (SITES-31616)

#### [!DNL Content Fragments] — 模型與模型編輯器{#sites-models-model-editor-6525}

* 當選取的值需要有效的模型型別時，使用者現在會在內容片段模型編輯器中看到當地語系化的驗證訊息。 編輯器不再於本地化介面中顯示未翻譯的英文訊息。 (SITES-41117)
* 內容片段模型篩選器面板現在會將其狀態和標題字串當地語系化。 使用者不會再看到未翻譯的標籤，例如模型標題、狀態、草稿、已啟用和已停用。 (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

ContextHub現在載入時不會出現JavaScript錯誤，並會中斷個人化。 Teaser和其他個人化體驗可以在受影響的頁面上正確呈現。 (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### 核心元件{#sites-core-components-6525}

* 當請求鎖定缺少的DAM資源時，AEM不再產生重複的ThumbnailServlet錯誤。 此servlet會在重新導向後停止處理，以防止NullPointerException專案淹沒錯誤記錄。 (SITES-41238)
* 當作者重新開啟元件對話方塊時，AEM不再將選用對話方塊欄位標示為必填。 對話方塊會持續讓驗證集中在實際需要輸入的欄位上，以避免誤導性的索引標籤層級錯誤。 (SITES-40449)

* AEM包含數個反向移植安全性修正，可加強Sites和相關雲端服務元件。 這些修正可減少跨網站指令碼風險，並改善受影響編寫路徑的請求處理方式。 (SITES-38314)
* 影像v3元件設定對話方塊現在會在頁面編輯器中本地化字串。 作者在本地化介面中設定影像元件時，不會再看到未翻譯的標籤。 (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### 行人穿越道 {#sites-crosswalk-6525}

* 交叉通路在安裝後不再需要個別的套件和組態設定。 AEM包含現成可用套件的必要套件組合、內容套件、系統使用者、服務使用者對應及功能切換。 (SITES-41417)
* 行人穿越道工作流程現在可以在AEM 6.5中使用必要的cq-wcm-core支援。 作者可使用「建立範本」和「開啟Universal Editor」動作，而不需個別更新核心套件。 (SITES-37666)

#### 體驗片段{#sites-experiencefragments-6525}

AEM現在會在作者建立體驗片段變數並捲動通過前40個結果時載入正確的範本。 範本選擇器在分頁期間會保留所選的體驗片段路徑。 (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### 啟動{#sites-launches-6525}

* 網站時間軸現在會將AEM在提升啟動項前建立版本時顯示的訊息內容當地語系化。 使用者在本地化介面中不會再看到未翻譯的英文字串。 (SITES-39157)
* 「啟動」清單現在會顯示沒有範本或即時副本繼承的建立之啟動項的正確說明。 使用者不再看到誤導性的「已覆寫」範本標籤。 (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### 本地化{#sites-localization-6525}

* 體驗片段中的文字元件屬性現在使用當地語系化標籤。 格式功能表不再顯示段落、標題、引號或預設格式文字選擇之未當地語系化字串。 (SITES-15091)

* 範本狀態文字現在在&#x200B;**工具** > **一般** > **範本**&#x200B;中正確對齊。 更新、啟用和發佈的狀態標籤會顯示在水平線上。 (SITES-36797)
* 「移動頁面」對話方塊現在會顯示完整的「選取日期與時間」標籤。 標籤不再截斷當地語系化介面，例如法文。 (SITES-36795)
* 範本編輯器中的Assets區段現在會顯示翻譯的標籤標籤。 在範本設定期間，本地化的編寫介面會顯示一致的標籤。 (SITES-33770)
* 頁面原則說明現在可在範本編輯器中正確轉譯。 使用者可以閱讀完整的預設CSS類別指引，而不會截斷樣式索引標籤中的文字。 (SITES-29724)
* 現在，當作者嘗試將元件拖曳到已刪除的範本時，範本編輯器會顯示本地化錯誤。 訊息不再顯示為未翻譯的「處理時」字串。 (SITES-19313)
* 「Teaser設定」視窗中的「目標」標籤現在會以當地語系化的文字顯示。 「超連結」區段不再以非英文地區設定顯示英文字串。 (SITES-18622)
* 頁面編輯器中的「開始工作流程」對話方塊現在會顯示當地語系化的工作流程動作標籤。 作者不會再看到工作流程選項的英文字串。 選項包括核准、發佈、請求和取消發佈動作。 (SITES-18103)
* 「分隔符號」編輯面板中的「上層」下拉式功能表，現在會顯示不含截斷的當地語系化字串。 作者可在設定元件時檢閱完整標籤。 (SITES-17480)
* 頁面編輯器現在會在容器元件樣式選單中顯示「完整寬度」和「固定寬度」的本地化標籤。 使用支援地區設定的作者不會再看到英文字串。 (SITES-17478)
* 作者現在可以在範本控制檯的導覽屬性區域中閱讀完整的工具提示。 UI會保持工具提示對齊，並防止在範本編輯期間截斷文字。 (SITES-15480)
* 作者現在可以在「參考」側面板中閱讀完整的「使用範本的Forms和檔案」標籤。 範本主控台不再針對支援的地區設定切斷字串。 (SITES-13167)
* 「參考」檢視現在會針對重新整理錯誤訊息使用當地語系化文字。 當AEM無法更新參考清單時，作者會看到已翻譯訊息。 (SITES-13102)
* 表單驗證現在會識別包含無效時間值的欄位。 時間扭曲強制回應會顯示更清楚的錯誤訊息，讓作者可以更正受影響的時數或分鐘欄位。 (SITES-10980)
* 「範本」主控台現在會在「選取影像」對話方塊中顯示本地化的Assets標籤。 當作者從範本屬性瀏覽資產時，標籤會正確顯示。 (SITES-8113)

#### MSM - Live Copies{#sites-msm-live-copies-6525}

* 即時副本概述現在會將「關係狀態」檢視中的日期格式當地語系化。 L **即時副本Source上次修改時間**、**即時副本上次修改時間**&#x200B;及&#x200B;**上次轉出時間**&#x200B;欄位會顯示符合使用者地區設定的日期。 (SITES-40756)
* MSM現在會記錄推播修改事件的更多詳細資料。 新增的事件資訊可協助團隊追蹤轉出活動，並識別非預期頁面變更的來源。 (SITES-38029)

#### 頁面編輯器{#sites-pageeditor-6525}

* 作者現在可以建立包含大寫字母或空格的標籤，並在儲存第一個「頁面屬性」時套用這些標籤。 AEM會建立標籤，並在相同作業期間將正確的值寫入頁面中繼資料。 (SITES-42550)

* 作者現在可以在名稱包含撇號的DAM資料夾中建立內容片段。 AEM會正確處理編碼的資料夾路徑，在建立期間不再觸發NullPointerException。 (SITES-38653)

* AEM現在支援在頁面編輯器中對已設定的內容片段元件執行複製和貼上動作。 元件會保留其內容片段參考，讓作者可以複製內容而不需要手動重新編寫。 (SITES-41586)
* 頁面編輯器現在會在元件對話方塊中正確顯示第一欄位說明工具提示。 較長的說明仍會顯示，讓作者可以檢閱欄位指示，而不會遺失工具提示頂端的文字。 (SITES-39937)
* 作者現在透過HTTP使用AEM時，可以開啟RTF編輯器連結對話方塊。 此修正會針對不使用HTTPS的內部部署環境還原連結編輯。 (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### 通用編輯器 {#sites-universal-editor-6525}

* Universal Editor預設不再在「預覽」模式中開啟。 AEM會將使用者傳送至生產環境通用編輯器環境，除非他們明確要求預覽行為。 (SITES-37193)
* Universal Editor現在會在預覽模式下開啟，以用於AEM開發、快速開發和預備環境。 「開啟」指令會對非生產執行個體使用正確的預覽行為。 (SITES-33839)

### [!DNL Assets] {#assets-6525}

* 「我的共用」使用者端程式庫現在會在將共用資產標題資料新增至頁面標籤之前，安全地處理該資料。 產生的共用頁面不再讓使用者透過操控的資產中繼資料接受指令碼插入。 (ASSETS-60898)

* Adobe Stock授權現在可在Assets使用者介面中正常運作。 AEM載入股票資產設定檔和權益資料後，授權按鈕不再保持停用。 (ASSETS-62610)
* 現成可用的資產到期通知現在可正確處理接近到期日期。 當剩餘時間達到設定的臨界值時，會執行提醒電子郵件，而非略過八天過期的資產。 (ASSETS-57857)

* AEM Assets現在會在使用者選擇儲存的搜尋後，還原鍵盤導覽。 介面可讓使用者離開下拉式清單，而不需重新整理或重新啟動Assets檢視。 (ASSETS-52061)

* 「管理員檢視」下載工作流程現在會正確保留ZIP檔案名稱。 下載ZIP資產不再產生副檔名為.zip的檔案名稱。 (ASSETS-62207)
* Assets參考工作流程現在可以正確處理檔案名稱中的空格。 當選取的檔案名稱包含一個或多個空格時，相關的資產更新不再失敗。 (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

Subtitles and Audio Tracks下拉式清單現在會將阿拉伯語顯示為Dynamic Media支援的語言。 此更新可讓使用者新增阿拉伯文字標題曲目，而不需要自訂因應措施。 (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

* 互動式通訊預覽現在會在AEM Forms Service Pack 6.5.24.0之後正確載入內容。 文字不再緩慢地載入遺失的空格，因此預覽會比對編寫的內容且更容易閱讀。 (FORMS-25346)
* 設定驗證模式並儲存表單後，最適化Forms核心元件中現在會顯示驗證詳細資料。 該圖樣在製作介面中仍保持可見。 (FORMS-25236)
* 檔案產生現在可以在AEM Forms 6.5 Service Pack 23和AEM Forms Service Pack 6.5.24.0環境中正確處理巢狀可擴充Forms描述語言(XDP)片段。 (FORMS-25234)
* 使用Rhino引擎在Adaptive Forms伺服器端重新驗證期間，表單片段外的當地語系化文字現在會以正確語言顯示。 文字在提交後不再回覆為預設語言。 (FORMS-25224)
* 升級至AEM Forms Service Pack 6.5.24.0後，Red Hat Enterprise Linux (RHEL) 8上的輸出服務不再當機，並出現不合法的指令錯誤。 檔案產生和表單輸出處理完成，不會突然停止服務。 (FORMS-25192)
* 當初始例項數設為0時，在Adaptive Forms中使用addInstance()函式動態新增的面板和內容現在會出現。 (FORMS-25169， FORMS-25124)
* 升級至AEM Forms Service Pack 6.5.24.0後，繁體中文（香港）翻譯現在可在製作和發佈環境中正確顯示。 本地化的zh-HK內容不再以錯誤的語言出現，或是意外地回覆為預設字串。 (FORMS-25042)
* 現在，在最適化Forms中，鍵盤導覽在手寫簽名欄位中的焦點會一致地移入和移出簽名區域，同時在表單中按Tab鍵。 (FORMS-25011)
* Web服務描述語言(WSDL)檔案現在會在組態和更新作業期間，在叫用Web服務步驟中正確載入。 (FORMS-24992、FORMS-24789、FORMS-24188)
* 現在，將條件套用至文字片段時，字母草稿會保留分行符號。 多行內容不再顯示為單一連續行。 (FORMS-24602)
* 到達Adobe Sign步驟後未傳回簽署狀態回應時，Adobe Managed Services (AMS)上AEM Forms中的Adobe Sign工作流程不再停滯。 (FORMS-24514)
* HTML至可攜式檔案格式(PDF)轉換在AEM Forms Service Pack 6.5.24.0中不再斷斷續續逾時，包括較大或複雜的轉換工作。 (FORMS-23978)
* 安裝修補程式AEMForms-6.5.0-0112後，在管理員使用者介面中管理安全備份模式現在可正常運作。 當選項可用時，使用者可以停用或關閉安全備份模式。 (FORMS-23976， FORMS-23718)
* 表單資料模型資料來源搜尋不再失敗，或在搜尋結果中顯示原始HyperText標籤語言(HTML)標籤。 結果會顯示可讀文字。 (FORMS-23875)
* 使用AEM Forms Service Pack 6.5.24.0中支援的核心元件版本將Adaptive Forms內嵌於網站頁面時，自訂函式現在會在執行階段載入。 (FORMS-23802)
* 透過更新的Sling Commons JavaScript物件標籤法(JSON)程式庫進行剖析時，互動式通訊數值規則現在能正確評估值。 數值欄位會一致地處理BigDecimal剖析變更。 (FORMS-23733)
* 現在，處理6.5.0版和更新版本時，記錄檔案的行為是一致的。 表單輸出和相關處理符合較新環境的預期行為。 (FORMS-23338)

#### FORMS JEE {#forms-jee-6525}

* 載入記錄元件時，若找不到org.owasp.esapi.reference.JavaLogFactory錯誤的類別，應用程式啟動不會再失敗。 受影響的環境可正確初始化，不需要重新啟動服務或重新設定組態。 (FORMS-25348)
* 套用Service Pack 25後，啟動成功完成。 初始化完成之前，系統啟動程式程式不會再失敗。 (FORMS-25347)
* Core Portable Document Format (PDF) (CPDF)元件現在能在Linux環境中正確建置和執行，執行期間不會意外停止。 (FORMS-25115)
* 在條碼擷取期間處理特定可攜式檔案格式(PDF)檔案時，條碼解碼不再因DecodingException錯誤而失敗。 (FORMS-23534， FORMS-23449)

#### Forms Designer {#forms-designer-6525}

* 在6.5版中使用ExportData時，ExportData輸出現在與表單資料相符。 匯出的可延伸標籤語言(XML)欄位與原始表單中顯示的值一致。 (LC-3922791)
* Output Service現在會在AEM Forms Service Pack 6.5.22.0中建立的Portable Document Format (PDF)檔案中，產生正確的協助工具標籤。 輔助式技術會以正確順序讀取內容，而不會略過元素。 (LC-3922756)
* 現在當平面化可攜式檔案格式(PDF)表單並啟用標籤時，輸出服務可正確反映隱藏或停用的欄位狀態。 (LC-3922708)
* Workbench中有底部標題的欄位現在會收到正確的標籤，這有助於改善產生檔案的一致性和協助工具。 (LC-3922619)
* 升級至AEM Forms Service Pack 6.5.20.0後，表單上的QR碼仍可掃描。 標準掃描器能可靠讀取產生的QR碼。 (LC-3922551)
* 現在，跨不同的Service Pack使用相同的輸入時，Forms Service轉譯器會產生一致的輸出。 AEM Forms Service Pack 6.5.17.0與AEM Forms Service Pack 6.5.18.0之間的轉譯值不再不同。 (LC-3922461)
* 從XML Data Package (XDP)範本產生的PDF/A檔案現在可以正確轉譯下沈方形邊框樣式。 表單欄位外觀符合設計的版面。 (LC-3922180)
* 平面化的可攜式檔案格式(PDF)提交現在會保留所有區段中的資料。 輸入的值會保留在最終平面化檔案中。 (LC-3922008)
* 轉換後的靜態可攜式檔案格式(PDF)檔案不再從原始XDP範本中的單一連結產生多個連結標籤。 (LC-3921997)
* 從AEM Forms匯出提交內容時，匯出的輸出檔案現在包含所有欄位。 (LC-3921983)


### 基礎 {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

啟動程式現在會正確連線CredentialsSupport服務，以進行Felix型驗證。 這可防止在AEM啟動期間發生可能影響權杖驗證的相依性錯誤。 (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

AEM 6.5升級後，JSP檔案編輯現在可在CRXDE Lite中如預期般運作。 CodeMirror編輯器會載入檔案內容，而不是將JSP標籤保留為空白。 (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### 本地化{#foundation-localization-6525}

* 「安全性>信任存放區」中的憑證上傳對話方塊現在會顯示本地化的資料格式標籤。 使用者新增憑證時，不會再看到未本地化的英文標籤。 (NPR-43412)

* 「建立KeyStore」對話方塊現在會將「取消」按鈕與其他對話方塊按鈕對齊。 按鈕版面配置會維持一致，且不再移動至不對齊。 (NPR-43291)
* **安全性** > A **Adobe IMS設定**&#x200B;中的「核取」對話方塊現在會顯示當地語系化的確認文字。 檢查和刪除訊息不再顯示為未本地化的英文字串。 (NPR-43289)
* 本地化的UI標籤現在會正確顯示在受影響的對話方塊和「金鑰儲存庫」標籤中。 Aria標籤值會使用翻譯的字串，而密碼欄位標籤會顯示且不會遭到截斷。 (NPR-43285)
* 「建立新使用者」工作流程現在會顯示無效字元的本地化驗證錯誤。 使用者會收到清楚的翻譯訊息，而非未當地語系化的IllegalArgumentException字串。 (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### Platform{#foundation-platform-6525}

* 「顯示標籤參照」按鈕現在會顯示所選標籤的參照數目。 此更新可協助使用者瞭解標籤的使用方式，而不需要額外的導覽。 (CQ-4355509)
* 「標籤」中的「移動」對話方塊現在可正確放置驗證訊息。 當使用者提交具有空白必填欄位的對話方塊時，錯誤文字不再涵蓋搜尋路徑圖示。 (CQ-4353009)

#### 安全性{#foundation-security-6525}

AEM現在允許列出包含client-secret的其他關鍵字。 當受支援的整合使用這些使用者端密碼命名模式時，設定建立不會再失敗。 (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### 翻譯{#foundation-translation-6525}

升級後，翻譯專案狀態計數現在會正確更新。 作者可以檢閱草稿、進行中和完整的值，而不需依賴早期Service Pack行為中過時的中繼資料。 (NPR-43418)

#### 使用者介面{#foundation-ui-6525}

* 手動輸入的網站主控台URL現在會解析為預期的頁面或資料夾路徑。 內容階層在重新整理後會維持一致，不會再回覆為基底URL。 (NPR-43688)
* AEM 6.5 LTS SP1執行個體升級為LTS SP2後，Adobe CRX Package Manager測試套件不再失敗。 縮圖清單servlet測試現在會如預期般完成。 (NPR-43534)

* 現在，每次瀏覽器重新整理後，網站主控台內容樹都會以一致方式載入。 內容存在時，作者不會再看到空白的左側邊欄或「沒有專案」訊息。 (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### 工作流程{#foundation-workflow-6525}

* 工作流程模型編輯器現在會正確驗證租使用者特定工作流程模型路徑。 將工作流程模型儲存在租使用者層級/conf路徑下的客戶可以編輯這些模型，而無需將其移動到全域設定路徑。 (GRANITE-65376)

* 工作流程模型編輯器現在會在路徑驗證期間標準化Windows檔案路徑。 作者可以在Windows伺服器上編輯工作流程模型，而不會發生封鎖模型更新的存取錯誤。 (GRANITE-63692)
* 任務建立現在包含到期日的伺服器端驗證。 使用者無法建立到期日早於開始日期的工作，這可保持收件匣工作資料的一致性。 (CQ-4362253)
* 名稱空間建立現在可以正確處理當地語系化的文字。 使用者可以在「標題」欄位中輸入非拉丁字元，並建立名稱空間，而不會發生驗證錯誤。 (CQ-4355587)

## 安裝[!DNL Experience Manager] 6.5.25.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0需要[!DNL Experience Manager] 6.5。 如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用封裝管理員在其中一個作者執行個體上安裝[!DNL Experience Manager] 6.5.25.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝[!DNL Experience Manager] 6.5.25.0套件。 因此，在安裝套件之前，您應該建立`crx-repository`的備份，以備您必須復原它時使用。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在[!DNL Experience Manager] 6.5上安裝Service Pack{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)下載Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。

1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 請參閱[Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>Service Pack安裝期間，Package Manager UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在[!DNL Safari]瀏覽器中，但可能間歇性地發生在任何瀏覽器中。

**自動安裝**

您可以使用兩種不同的方法來安裝[!DNL Experience Manager] 6.5.25.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。 套件會自動安裝。
* 使用封裝管理員[&#128279;](/help/sites-administering/package-manager.md#package-share)的HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

>[!NOTE]
>
>Experience Manager 6.5.25.0不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁(`/system/console/productinfo`)會在[!UICONTROL 已安裝產品]下顯示更新的版本字串`Adobe Experience Manager (6.5.25.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi主控台中，所有OSGi套件組合均為&#x200B;**[!UICONTROL 作用中]**&#x200B;或&#x200B;**[!UICONTROL 片段]** （使用Web主控台： `/system/console/bundles`）。

1. OSGi套件`org.apache.jackrabbit.oak-core`是1.22.20或更新版本（使用Web主控台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安裝[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱[Experience Manager Forms Service Pack安裝說明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)) 僅用於探索和評估目的。 若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝適用於Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝[Experience Manager內容片段搭配GraphQL索引套件1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.25.0的UberJar可在[Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/)中使用。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`dependency`標籤沒有`classifier`，其值為`apis`。



## 已棄用和已移除的功能{#removed-deprecated-features}

如需AEM 6.5已棄用或移除之所有功能的詳細清單，請參閱[已棄用和移除的功能](/help/release-notes/deprecated-removed-features.md)。

### AEM Assets REST API 中的內容片段支援 {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 為內容片段和模型管理提供現代化的 OpenAPI，因此 AEM Assets REST API 中較舊的內容片段支援端點現已棄用。

Adobe打算在產品生命週期結束前保留這些較舊的端點。 Adobe 未計劃針對已棄用的端點提供進一步的增強功能。

### SPA 編輯器 {#spa-editor}

[從AEM 6.5.25版開始的新專案已棄用SPA編輯器](/help/sites-developing/spa-overview.md)。 SPA Editor仍支援現有專案，但不應用於新專案。

目前，AEM 中用於管理 Headless 內容的首選編輯器為：

* [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。
* [內容片段編輯器](/help/sites-developing/universal-editor/introduction.md)，用於表單型編輯。

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* 與Oak相關的&#x200B;**&#x200B;**
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
`cache`和`diff-cache`的新資料夾會自動建立，而您在`error.log`中不會再遇到與`mvstore`相關的例外狀況。

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

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，在擷取內容片段參考時出現問題。背景查詢失敗；功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點`/oak:index/damAssetLucene` （不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您將[!DNL Experience Manager]執行個體從6.5.0 - 6.5.4升級至Java™ 11上的最新Service Pack，您會在`error.log`檔案中看到`RRD4JReporter`例外狀況。 若要停止例外狀況，請重新啟動[!DNL Experience Manager]的執行個體。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在[!DNL Assets]中重新命名階層中的資料夾，並將巢狀資料夾發佈至[!DNL Brand Portal]。 但是，在重新發佈根資料夾之前，[!DNL Brand Portal]中的資料夾標題不會更新。

* 安裝[!DNL Experience Manager] 6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「當使用Adobe Target API （IMS驗證）在[!DNL Experience Manager]中設定Target Standard整合時，將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target會建立多個型別為「HTML」/來源「Adobe Target Classic」的選件，而非「體驗片段」/來源「Adobe Experience Manager」型別。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`找不到維護期間。
   * 使用彙總函式（例如SUM、MAX和MIN）時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`找不到維護期間。
   * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，`org.apache.servicemix.bundles.rhino`套件提供的Rhino JavaScript Engine有新的提升行為。 使用嚴格模式(`use strict;`)的指令碼必須宣告其正確的變數。 否則，它們不會執行，並最終擲回執行階段錯誤。

* 透過正式更新套件安裝標籤相關的現成可用內容會將`/content/cq:tags`節點的languages屬性重設為預設值。 此動作適用於Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等。 因此，在安裝之前，必須從屬性新增它。

### AEM Sites的已知問題 {#known-issues-aem-sites-6525}

內容片段 — 預覽失敗，因為大型片段樹受到DoS保護。 請參閱有關預設GraphQL查詢執行器組態選項[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)的KB文章(SITES-17934)

### AEM Forms的已知問題 {#known-issues-aem-forms-6525}

* **FORMS-23722**&#x200B;當包含使用`bindref`的&#x200B;**檔案附件**&#x200B;欄位的表單提交給具有&#x200B;**指派任務**&#x200B;步驟的AEM工作流程時，附件未顯示。 因此，當從「收件匣」開啟任務時，它們不會出現。 檔案會正確儲存至存放庫，但指派工作步驟UI無法顯示附件。

#### 可用Hotfix的已知問題 {#aem-forms-issues-with-hotfixes}

下列問題有可供下載和安裝的Hotfix。 您可以[下載並安裝Hotfix](/help/release-notes/aem-forms-hotfix.md)以解決下列問題：

* **NPR-44100**&#x200B;在WAR/JEE部署（包括JEE上的AEM Forms）上安裝AEM 6.5 Service Pack 25後，`com.adobe.cq.screens.sessions`套件組合會維持在「已安裝」狀態，而不會變成「作用中」。 若要解決此問題，請[下載並安裝AEM Service Pack 6.5.25.0的Hotfix](/help/release-notes/aem-forms-hotfix.md)。
* **FORMS-14926**&#x200B;安裝AEM Forms JEE Service Pack 21 (6.5.21.0)後，如果在`<AEM_Forms_Installation>/lib/caching/lib`資料夾下發現重複的Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`專案，請執行以下步驟以解決問題：

   1. 停止儲位（如果它們正在執行）。
   2. 停止AEM伺服器。
   3. 移至`<AEM_Forms_Installation>/lib/caching/lib`。
   4. 移除除`geode-*-1.15.1.2.jar`以外的所有Geode修補程式檔案。 確認只有具有`version 1.15.1.2`的Geode jar存在。
   5. 在管理員模式中開啟命令提示字元。
   6. 使用`geode-*-1.15.1.2.jar`檔案安裝Geode修補程式。

   * AEM Forms現在包含表單元件的Struts版本從2.5.33升級至6.x。 此升級提供先前未包含在SP24中的Struts變更。 已透過[Hotfix](/help/release-notes/aem-forms-hotfix.md)新增支援，您可以下載並安裝該支援，以新增對最新版Struts的支援。

## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

下列zip檔案包含列出此[!DNL Experience Manager] 6.5 Service Pack發行版本中包含的OSGi套件組合和內容套件的文字檔案：

* [Experience Manager 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)中包含的OSGi套件組合清單
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.25.0](/help/release-notes/assets/65250-packages.zip)中包含的內容套件清單
<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/tw/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)




