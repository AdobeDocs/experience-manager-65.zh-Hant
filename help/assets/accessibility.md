---
title: ' [!DNL Experience Manager Assets]中的輔助功能'
description: 瞭解 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 中的協助功能如何協助殘障人士使用。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 863d1bd3f0f188153fcbbb7256d3ac2e3b247f59
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 1%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}中的協助功能

[!DNL Adobe Experience Manager] 可讓內容建立者和發佈者在網路上提供絕佳的體驗。Adobe致力於讓殘障人士也能參與其中，改善[!DNL Experience Manager]的協助功能。 本軟體不斷增強，以符合各種使用者的需求，並符合包括視覺、聽覺、行動或其他障礙者在內的全球標準。

[!DNL Experience Manager] 發佈符合性資訊，說明符合的標準、概述產品中的協助功能，並說明符合性等級。協助工具符合性報告可協助[!DNL Experience Manager]使用者瞭解各種標準的遵守程度。 [!DNL Assets]中的增強功能可讓所有使用者透過鍵盤、螢幕閱讀程式、放大鏡和其他輔助技術，輕鬆使用介面。

[!DNL Experience Manager] 提供不同等級的支援：

* [網頁內容可及性指引 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修訂後的《康復法》第508節](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [協助工具計畫- W3C提供的協助工具Rich Internet Applications(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

要閱讀包含法規遵從性級別詳細資訊的報告，請參閱[輔助功能符合性報告](https://www.adobe.com/accessibility/compliance.html)(ACR)頁。

要瞭解[!DNL Dynamic Media]如何訪問，請參閱 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[輔助功能。

## 輔助技術{#at-support}

行動不便的使用者通常依賴硬體和軟體來存取網頁內容和使用軟體產品。 這些工具被稱為輔助技術。 [!DNL Experience Manager Assets] 使用本軟體的核心功能時，可使用下列類型的輔助技術(AT):

* 螢幕閱讀程式和螢幕放大鏡。
* 語音識別軟體。
* 鍵盤使用——導覽和捷徑。
* 輔助硬體，包括開關控制項、可重新整理的盲文顯示器和其他電腦輸入裝置。
* UI放大工具。

## [!DNL Experience Manager Assets] 可存取的使用案例  {#accessible-assets-use-cases}

在[!DNL Experience Manager]中，協助功能可解決[!DNL Experience Manager]使用者及其客戶的兩項主要需求。

* 對於內容設計人員和創作者，有一些功能可用來建立和發佈客戶和網站訪客輪流使用的可存取內容。 殘障人士在協助技術的協助下使用內容。 如需詳細資訊，請參閱[網頁協助工具指南](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager] 也可讓殘障人士使用者和管理員存取使用者介面和控制項，以建立和管理內容。殘障人士可使用輔助技術導覽、使用和管理[!DNL Assets]功能。

[!DNL Assets]中的核心功能比以前更容易存取，並定期更新，以改善全球標準的合規性。 [!DNL Assets]中的CRUD操作在這些操作中具有一定程度的可訪問性。 您可透過鍵盤快速鍵、螢幕閱讀程式文字、色彩對比等，來存取新增、管理、搜尋和散布資產等DAM工作流程。

## 支援使用鍵盤{#keyboard-use}

使用鍵盤也可以參與許多可點選或可操作的使用者介面元素。 使用鍵盤，使用者可專注在UI元素上並採取適當的動作。 使用者可直接使用鍵盤快速鍵來觸發命令或動作，而不需專注在UI元素上，並使用鍵盤來觸發。 例如，使用者可以使用鍵盤瀏覽至使用者介面控制項，然後選取`Return`並選取`Alt + 2`鍵盤快速鍵，以開啟使用者介面左側資產的時間軸。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}中的鍵盤快速鍵

[!DNL Assets]中的下列動作可搭配列出的鍵盤快速鍵運作。 套用至[!DNL Experience Manager]控制台的大部分鍵盤快速鍵也套用至[!DNL Assets]。 請參閱[控制台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)。 瞭解如何[啟用或停用鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 使用者介面或藍本 | 鍵盤快速鍵 | 動作 |
|---|---|---|
| [!DNL Assets]使用者介面中的欄檢視 | 向上和向下鍵 | 導覽至相同階層中的檔案和檔案夾。 |
| [!DNL Assets]使用者介面中的欄檢視 | 向左和向右箭頭鍵 | 導覽至目前檔案夾上方或下方的檔案和檔案夾。 |
| 瀏覽[!DNL Assets]中的資料夾 | `/` | 開啟Omnisearch方塊以叫用搜尋。 |
| [!DNL Assets] 主控台 | 「 | 切換邊欄 |
| [!DNL Assets] 主控台 | `Alt + 1` | 開啟內容樹狀結構。 |
| [!DNL Assets] 主控台 | `Alt + 2` | 開啟[!UICONTROL Navigation]左側導軌。 |
| [!DNL Assets] 主控台 | `Alt + 3` | 顯示選定資產的[!UICONTROL 時間軸]。 |
| [!DNL Assets] 主控台 | `Alt + 4` | 開啟選取資產的即時副本參考。 |
| [!DNL Assets] 主控台 | `Alt + 5` | 在選定資料夾中開始搜索和搜索。 |
| 已選取資產或資料夾 | 回空格 | 刪除選定的資產或資料夾。 |
| 已選取資產或資料夾 | `p` | 開啟所選資產的「屬性」頁面。 |
| 已選取資產或資料夾 | `e` | 編輯選取的資產。 |
| 已選取資產或資料夾 | `m` | 移動選定資產。 |
| 已選取資產或資料夾 | `Ctrl + c` | 複製選取的資產。 |
| 已選取資產或資料夾 | `Esc` | 取消選取選取範圍。 |
| 對話框開啟並位於焦點中 | `Esc` | 關閉對話框。 |
| 在DAM的資料夾內 | `Ctrl + v` | 貼上複製的資產。 |
| [!DNL Assets] 主控台 | `Ctrl + A` | 選取所有資產。 |
| 資產屬性頁面 | `Ctrl + S` | 儲存變更。 |
| [!DNL Assets] 主控台 | `?` | 請參閱鍵盤快速鍵清單。 |

## 登入並導覽[!DNL Assets]使用者介面{#login}

使用者可使用鍵盤導覽並填寫登入欄位以登入。 每次發生錯誤時，螢幕閱讀程式都會宣佈因使用者名稱和密碼組合不正確而導致的錯誤訊息。

登入後，DAM使用者可使用鍵盤在[!DNL Assets]使用者介面中導覽。 使用者介面元素（例如左側導軌、選單、使用者描述檔、搜尋列、檔案和資料夾），以及管理和組態設定都可使用鍵盤導覽。 鍵盤導覽順序為從左至右和從上至下。 當使用鍵盤導覽時，聚焦時可操作的選項會以較佳的色彩對比反白顯示，並由螢幕閱讀器旁白。 視情況而定，螢幕閱讀程式會宣佈功能表中焦點選項的狀態，例如展開、收合和混合狀態。 此外，螢幕閱讀程式會宣佈可操作選項的用途，而不是說外觀或介面位置。

如果使用者從功能表展開說明或使用者描述檔選項，螢幕閱讀程式會宣佈適當的選項或狀態。 如果使用者展開使用者設定檔選項，則可使用鍵盤選取可用的選項。 例如，管理員可以模擬不同的使用者。 如果使用者從[!UICONTROL Help]選項搜尋字串，旁白者會宣佈「搜尋說明」以指出搜尋正在進行中。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 瀏覽資產並檢視相關資訊{#browse}

在[!DNL Assets]使用者介面中，使用者可使用鍵盤瀏覽DAM儲存庫中現有數位資產的清單、預覽或下載資產、查看產生的轉譯、切換檢視、查看產生的轉譯、查看時間軸和版本記錄、查看注釋和參考，以及檢視和管理中繼資料。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

瀏覽資產儲存庫時，下列功能可改善協助工具：

* 螢幕閱讀程式會發佈文字替代項目，說明圖示的用途或功能，而非其名稱。
* 使用者可使用鍵盤按鍵，存取並集中「參考」資產清單中的互動式使用者介面選項。
* 清單檢視中每一列的元素會由螢幕閱讀程式宣佈為同一列的元素。
* 使用`Tab`鍵導覽時，焦點可移至版本預覽中的關閉選項。
* 當使用鍵盤瀏覽時，反白顯示的可操作使用者介面選項會以增強的對比顯示更突出的視覺焦點。 它可讓使用者更容易辨識出焦點區域。
* 使用`Esc`鍵從縮圖檢視中移除快速動作圖示並不會移除鍵盤焦點最後一個焦點項目。
* 在選取資產後，選取`Alt + 4`鍵盤快速鍵會開啟左側導軌中的[!UICONTROL 參考]清單。 使用`Tab`鍵，用戶可以瀏覽非零引用條目。 只瀏覽非零參照項目也可節省心力和按鍵輸入。
* 資產時間軸中提供資產的注釋。 如果使用鍵盤或鍵盤快速鍵存取左側導軌，則可加以存取。
* [!UICONTROL 使用] 鍵盤可 [!DNL Experience Manager] 以訪問「查看設定」。使用者可使用方向鍵來瀏覽可用的卡片大小，並選取並切換，以在現有的「檢視設定」檢視中瀏覽及設定其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理數位資產{#manage-assets}

許多資產管理工作（例如CRUD作業、下載資產、新增中繼資料）都可以不同程度地存取。 [!DNL Assets] 可讓您使用螢幕閱讀器和鍵盤等各種輔助技術完成工作。

觀看如何使用鍵盤瀏覽儲存庫並下載資產](https://youtu.be/K3dgqMRQJys)的視頻演示。[

對於通常由行銷人員和管理員等角色執行的中繼資料作業，下列功能可改善協助工具：

* [!UICONTROL 現在，您可] 以使用鍵盤  存取資產屬性頁面上的儲存與關閉選項。
* 螢幕閱讀程式會宣佈在資產[!UICONTROL 屬性]的[!UICONTROL Basic]標籤中刪除選取標籤的選項。
* 使用者可搭配鍵盤使用「日期選擇器」彈出式對話方塊。 「日期選擇器」使用者介面元素可用來設定開機和關機，並選取日期。
* 使用鍵盤的拖曳功能可在螢幕閱讀程式的瀏覽模式下，在[!UICONTROL 中繼資料結構編輯器]中正常運作。
* 用戶可以使用鍵盤將焦點移動到資料夾[!UICONTROL 屬性]的[!UICONTROL 權限]標籤中[!UICONTROL 關閉用戶組]下的「添加用戶」或「組」欄位。

## 搜尋數位資產{#search-assets}

快速順暢的資產搜尋體驗可大幅提升內容速度。 內容速度使用案例是核心[!DNL Assets]功能的一部分。 若要從Omnisearch列開始搜尋，使用者可以使用鍵盤快速鍵`/`或搭配使用`Tab`和螢幕閱讀程式，以快速找到搜尋選項。 當焦點在搜尋選項![搜尋選項](assets/do-not-localize/search_icon.png)時，螢幕閱讀程式會將選項的名稱稱為「搜尋按鈕」。 用戶可以選擇`Return`以開啟Omnisearch框。 螢幕閱讀程式不僅會旁白搜尋方塊中輸入的關鍵字，也會旁白說明[!DNL Experience Manager Assets]所提供的建議。 使用者可以組合使用方向鍵、`Return`和`Tab`來存取各種選項以觸發搜尋。

搜尋功能可透過下列功能存取：

* 頁面標題（如螢幕閱讀程式所提供）有助於將頁面識別為資產的搜尋頁面。
* 使用者從Omnisearch欄位中搜尋資產。 使用者可以使用鍵盤導覽或鍵盤快速鍵`/`來開啟它。
* 使用者可以開始輸入搜尋關鍵字，然後使用方向鍵選取自動建議。 使用`Return`索引鍵可選取反白顯示的建議，並搜尋所選建議的資產。
* 螢幕閱讀程式可在篩選搜尋結果時，在「篩選」面板中識別並宣佈混合狀態核取方塊（除非您選取所有巢狀謂詞，否則不會選取並切換第一層核取方塊）。
* 在Omnisearch方塊關閉後，使用者焦點會移至搜尋選項。

篩選搜尋結果時：

* 搜尋結果頁面提供資訊標題，以進一步瞭解螢幕閱讀程式使用者。
* 螢幕閱讀器將搜索過濾器中的選項作為可擴展的收合器來宣佈。
* 具有混合狀態選項的謂詞由螢幕閱讀器宣佈。

## 共用資產 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共用資產時，下列功能可改善無障礙環境支援：

* 使用者可以在連結共用對話方塊中，使用鍵盤在搜尋和新增電子郵件地址欄位中移動焦點。

* 在連結共用對話方塊中，當在瀏覽模式中導覽時，螢幕閱讀程式、

   * 載入對話方塊時，請勿將表格資訊旁白化。
   * 可導覽至所有列出的建議。
   * 對顯示的「新增電子郵件地址」和「搜尋」欄位建議進行旁白。

## 可存取的檔案{#accessible-docs}

[!DNL Experience Manager] 提供協助工具的說明檔案供殘障人士使用。以下內容可讓您立即存取內容，而Adobe也會持續改善範本和內容：

* 螢幕閱讀程式可以閱讀文字。
* 影像和插圖有替代文字可供使用。
* 鍵盤導覽是可能的。
* 對比度有助於反白顯示說明檔案網站的部分部分。

## 提供反饋{#a11y-feedback}

若要提供與協助工具相關的意見回應、提出問題並要求產品增強功能，請使用下列方法：

* 填寫[www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)的表格。
* 請寄電子郵件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [中的輔助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)。
>* [每個Service Pack版本中增強功能的發行說明](/help/release-notes/new-features-latest-service-pack.md)。
>* [[!DNL Adobe Experience Manager] 協助工具指引](/help/managing/web-accessibility.md)。
>* [Adobe解決方案的符合性報告(ACR)和VPAT清單](https://www.adobe.com/accessibility/compliance.html)。

