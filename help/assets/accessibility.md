---
title: 可訪問 [!DNL Experience Manager Assets]的功能和介面
description: 了解 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 中的協助工具功能如何協助身心障礙的使用者。
contentOwner: AG
feature: 資產管理
role: Business Practitioner, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: a7a9a31364497ab67d805e45ba4fa03c927828ed
workflow-type: tm+mt
source-wordcount: '1924'
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

# [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}中的輔助功能

[!DNL Adobe Experience Manager] 可讓內容建立者和發佈者在網路上提供絕佳體驗。Adobe致力於通過改善[!DNL Experience Manager]的可訪問性，將殘疾創造者納入其中。 該軟體不斷得到增強，以滿足所有類型用戶的需求，並遵守包括視覺、聽覺、移動性或其他損傷個人在內的全球標準。

[!DNL Experience Manager] 發佈描述其遵守的標準的一致性資訊，概述產品中的輔助功能，並描述法規遵從性級別。協助工具合規性報告可協助[!DNL Experience Manager]使用者了解各種標準的遵守程度。 [!DNL Assets]中完成的增強功能讓所有使用者都能透過鍵盤、螢幕助讀程式、放大鏡和其他輔助技術輕鬆使用介面。

[!DNL Experience Manager] 對以下標準提供不同級別的支援：

* [網頁內容可及性指引 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修訂《康復法》第508條](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [協助工具計畫 — W3C提供無障礙的豐富網際網路應用程式(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

要閱讀包含合規性級別詳細資訊的報告，請參閱[輔助功能合規性報告](https://www.adobe.com/accessibility/compliance.html)(ACR)頁。

要了解[!DNL Dynamic Media]如何可訪問，請參閱 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[輔助功能。

## 輔助技術{#at-support}

殘疾用戶經常依賴硬體和軟體來訪問Web內容和使用軟體產品。 這些工具稱為輔助技術。 [!DNL Experience Manager Assets] 使用軟體的核心功能時，可以使用下列類型的輔助技術(AT):

* 螢幕助讀程式和螢幕放大鏡。
* 語音識別軟體。
* 鍵盤使用情況 — 導覽和快速鍵。
* 輔助硬體，包括交換機控制、可重新整理的盲文顯示器和其他電腦輸入設備。
* UI放大工具。

## [!DNL Experience Manager Assets] 可存取的使用案例  {#accessible-assets-use-cases}

在[!DNL Experience Manager]中，輔助功能滿足[!DNL Experience Manager]用戶及其客戶的兩個關鍵要求。

* 對於內容設計人員和建立者，有一些功能可建立和發佈客戶和網站訪客循序使用的無障礙內容。 殘疾人士透過輔助技術使用內容。 如需詳細資訊，請參閱[網頁協助工具指南](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager] 也可讓殘疾使用者和管理員存取使用者介面和控制項，以建立和管理內容。殘疾人可使用輔助技術來導覽、使用和管理[!DNL Assets]功能。

[!DNL Assets]中的核心功能比以往更容易訪問，並定期更新以改進對全球標準的遵守。 [!DNL Assets]中的CRUD操作具有一定程度的可訪問性。 您可以透過鍵盤快速鍵、螢幕助讀程式文字、顏色對比等協助，存取新增、管理、搜尋和發佈資產等DAM工作流程。

## 支援使用鍵盤{#keyboard-use}

許多可點按或可透過指標操作的使用者介面元素也可使用鍵盤來參與。 使用鍵盤時，使用者可以專注在UI元素上，並採取適當的動作。 使用者可以直接使用鍵盤快速鍵來觸發命令或動作，而無須聚焦於UI元素並使用鍵盤來觸發。 例如，用戶可以使用鍵盤瀏覽到用戶介面控制項，選擇`Return`，然後選擇`Alt + 2`鍵盤快捷鍵，以開啟用戶介面左側資產的時間軸。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}中的鍵盤快捷鍵

[!DNL Assets]中的以下操作與列出的鍵盤快捷鍵一起使用。 套用至[!DNL Experience Manager]控制台的大部分鍵盤快速鍵也套用至[!DNL Assets]。 請參閱[控制台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)。 請參閱如何[啟用或停用鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 使用者介面或案例 | 鍵盤快速鍵 | 動作 |
|---|---|---|
| [!DNL Assets]用戶介面中的列視圖 | 向上和向下鍵 | 導覽至相同階層中的檔案和資料夾。 |
| [!DNL Assets]用戶介面中的列視圖 | 向左和向右方向鍵 | 導航到當前資料夾上或下方的檔案和資料夾。 |
| 瀏覽[!DNL Assets]中的資料夾 | `/` | 開啟Omnisearch方塊叫用搜尋。 |
| [!DNL Assets] 主控台 | &#39; | 切換邊欄 |
| [!DNL Assets] 主控台 | `Alt + 1` | 開啟內容樹。 |
| [!DNL Assets] 主控台 | `Alt + 2` | 開啟左側邊欄的[!UICONTROL Navigation]。 |
| [!DNL Assets] 主控台 | `Alt + 3` | 顯示所選資產的[!UICONTROL 時間軸]。 |
| [!DNL Assets] 主控台 | `Alt + 4` | 開啟所選資產的即時副本參考。 |
| [!DNL Assets] 主控台 | `Alt + 5` | 在所選資料夾中開始搜索和搜索。 |
| 已選取資產或資料夾 | 空格 | 刪除選取的資產或資料夾。 |
| 已選取資產或資料夾 | `p` | 開啟所選資產的「屬性」頁面。 |
| 已選取資產或資料夾 | `e` | 編輯選取的資產。 |
| 已選取資產或資料夾 | `m` | 移動所選資產。 |
| 已選取資產或資料夾 | `Ctrl + c` | 複製選取的資產。 |
| 已選取資產或資料夾 | `Esc` | 取消選取。 |
| 對話框開啟，且在焦點中 | `Esc` | 關閉對話框。 |
| DAM中的資料夾內 | `Ctrl + v` | 貼上複製的資產。 |
| [!DNL Assets] 主控台 | `Ctrl + A` | 選取所有資產。 |
| 資產屬性頁面 | `Ctrl + S` | 儲存變更。 |
| [!DNL Assets] 主控台 | `?` | 請參閱鍵盤快速鍵清單。 |

## 登入並導覽[!DNL Assets]使用者介面 {#login}

使用者可使用鍵盤導覽至並填入登入欄位以登入。 每次發生錯誤時，螢幕助讀程式都會公告由於登錄頁面上的錯誤使用者名稱和密碼組合。

登入後，DAM使用者可以使用鍵盤在[!DNL Assets]使用者介面中導覽。 使用者介面元素（如左側邊欄、功能表、使用者設定檔、搜尋列、檔案和資料夾，以及管理和組態設定）可使用鍵盤導覽。 鍵盤導覽順序由左至右、由上至下。 使用鍵盤導覽時，聚焦時的可操作選項會以更好的顏色對比強調顯示，並由螢幕助讀程式提供旁白。 螢幕助讀程式會視情況宣佈功能表中重點選項的狀態（例如展開、收合和混合狀態）。 此外，螢幕助讀程式會朗讀可操作選項的用途，而非顯示外觀或介面位置。

如果使用者從功能表展開說明或使用者設定檔選項，螢幕助讀程式會朗讀適當的選項或狀態。 如果使用者展開使用者設定檔選項，可使用鍵盤選取可用選項。 例如，管理員可以模擬不同的使用者。 如果用戶從[!UICONTROL Help]選項中搜索字串，則講述人會宣佈「Searching Help」（搜索幫助）以指示正在進行搜索。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 瀏覽資產並檢視相關資訊 {#browse}

在[!DNL Assets]使用者介面中，使用者可以使用鍵盤瀏覽DAM存放庫中現有數位資產的清單、預覽或下載資產、查看產生的轉譯、切換檢視、查看產生的轉譯、查看時間軸和版本記錄、查看註解和參考，以及檢視和管理中繼資料。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

瀏覽資產存放庫時，下列功能可改善協助工具：

* 螢幕助讀程式會朗讀描述圖示用途或功能（而非其名稱）的替代文字。
* 使用者可使用鍵盤鍵存取「參考」清單中的互動式使用者介面選項，並加以聚焦。
* 螢幕助讀程式會將清單檢視中每一列的元素宣佈為同一列的元素。
* 使用`Tab`鍵導覽時，焦點可移至版本預覽中的關閉選項。
* 使用鍵盤瀏覽時，醒目提示的可操作使用者介面選項具有更突出的視覺焦點，並增強對比。 這可讓使用者更容易識別重點區域。
* 使用`Esc`鍵從縮圖檢視中移除快速動作圖示時，不會從最後一個聚焦項目移除鍵盤焦點。
* 選取資產後，選取`Alt + 4`鍵盤快速鍵會開啟左側邊欄中的[!UICONTROL 參考]清單。 使用`Tab`鍵，用戶可以瀏覽非零的引用條目。 僅瀏覽非零的引用條目也節省了工作和擊鍵。
* 資產時間軸中提供資產的註解。 如果使用鍵盤或鍵盤快速鍵存取左側邊欄，便可存取。
* [!UICONTROL 可] 使用 [!DNL Experience Manager] 鍵盤存取檢視設定。使用者可使用方向鍵導覽可用的卡片大小，並選取及索引標籤，以導覽及設定現有「檢視設定」檢視中的其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理數位資產{#manage-assets}

許多資產管理工作（例如CRUD作業、下載資產、新增中繼資料）皆可在不同程度上存取。 [!DNL Assets] 可讓您使用各種輔助技術（例如螢幕助讀程式和鍵盤）來完成工作。

請觀看影片示範，了解如何使用鍵盤來瀏覽存放庫並下載資產](https://youtu.be/K3dgqMRQJys)。[

對於通常由行銷人員和管理員等角色執行的中繼資料操作，下列功能可改善協助工具：

* [!UICONTROL 現在可] 以使用鍵盤  存取資產屬性頁面上的儲存與關閉選項。
* 螢幕助讀程式會朗讀資產[!UICONTROL 屬性]的[!UICONTROL Basic]標籤中刪除所選標籤的選項。
* 使用者可以使用鍵盤來使用「日期挑選器」彈出式對話方塊。 Datepicker用戶介面元素用於設定開啟時間和關閉時間，並選擇日期。
* 在螢幕助讀程式的瀏覽模式中，使用鍵盤的拖曳功能在[!UICONTROL 中繼資料結構編輯器]中可正常運作。
* 用戶可以使用鍵盤將焦點移動到資料夾[!UICONTROL 屬性]的[!UICONTROL 權限]標籤中[!UICONTROL 封閉用戶組]下的「添加用戶」或「組」欄位。

## 搜尋數位資產{#search-assets}

快速順暢的資產搜尋體驗可提升內容速度。 內容速度使用案例是核心[!DNL Assets]功能的一部分。 若要從Omnisearch列開始搜尋，使用者可以使用鍵盤快速鍵`/`，或搭配使用`Tab`和螢幕助讀程式來快速找到搜尋選項。 當焦點在搜尋選項![搜尋選項](assets/do-not-localize/search_icon.png)時，螢幕助讀程式會將選項的名稱敘述為「搜尋按鈕」。 使用者可以選取`Return`以開啟Omnisearch方塊。 螢幕助讀程式不僅會提供搜尋方塊中輸入之關鍵字的旁白，也會提供[!DNL Experience Manager Assets]所提供建議的旁白。 使用者可使用方向鍵、`Return`和`Tab`的組合來存取各種選項以觸發搜尋。

可透過下列功能存取搜尋功能：

* 螢幕助讀程式可用的頁面標題有助於將頁面識別為資產的搜尋頁面。
* 使用者從Omnisearch欄位內搜尋資產。 用戶可以使用鍵盤導航或鍵盤快捷鍵`/`開啟它。
* 使用者可以開始輸入搜尋關鍵字，然後使用方向鍵選取自動建議。 可使用`Return`索引鍵選取醒目提示的建議，並搜尋所選建議的資產。
* 螢幕助讀程式可在篩選搜尋結果時，識別並宣佈「篩選器」面板中的混合狀態核取方塊（除非您選取所有巢狀述詞，否則不會選取第一層核取方塊，並徹底清除）。
* 關閉Omnisearch方塊後，使用者焦點會移至搜尋選項。

篩選搜尋結果時：

* 搜尋結果頁面提供資訊標題，以便更清楚了解螢幕助讀程式的使用者。
* 螢幕助讀程式會將搜尋篩選器中的選項朗讀為可展開的折疊式訊息。
* 螢幕助讀程式會公佈具有混合狀態選項的謂語。

## 共用資產 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共用資產時，下列功能可改善協助工具：

* 使用者可以在連結共用對話方塊的「搜尋」和「新增電子郵件地址」欄位中使用鍵盤來移動焦點。

* 在連結共用對話方塊中，以瀏覽模式導覽時，螢幕助讀程式會

   * 載入對話方塊時，請勿提供表格資訊的旁白。
   * 可以導覽至所有列出的建議。
   * 提供旁白來敘述針對新增電子郵件地址和搜尋欄位所顯示的建議。

## 可訪問文檔{#accessible-docs}

[!DNL Experience Manager] 提供方便殘疾人士使用的檔案。下列項目有助於讓內容選件目前可供存取，而Adobe仍持續改善範本和內容：

* 螢幕助讀程式可以讀取文字。
* 影像和圖解有可用的替代文字。
* 鍵盤導航是可能的。
* 對比率有助於突顯檔案網站的某些部分。

## 提供反饋{#a11y-feedback}

若要提供與協助工具相關的意見反應、提出問題並要求產品增強功能，請使用下列方法：

* 在[www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)填寫表單。
* 請寄電子郵件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [ [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的協助工具功能。
>* [每個Service Pack版本中完成之增強功能的發行說明](/help/release-notes/new-features-latest-service-pack.md)。
>* [[!DNL Adobe Experience Manager] 無障礙指引](/help/managing/web-accessibility.md)。
>* [Adobe解決方案的符合性報表(ACR)和VPAT清單](https://www.adobe.com/accessibility/compliance.html)。

