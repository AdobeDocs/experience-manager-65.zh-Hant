---
title: ' [!DNL Adobe Experience Manager Assets]的可存取功能與介面'
description: 瞭解 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 中的協助工具功能如何協助殘障使用者。
contentOwner: AG
feature: Asset Management
role: User, Developer, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
solution: Experience Manager, Experience Manager Assets
source-git-commit: 20d6c716b4ba799a7d4ae2858459f7c38cf3da02
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 1%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets]中的協助工具功能 {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager]可讓內容建立者和發佈者在網路上提供令人驚豔的體驗。 Adobe致力於改善[!DNL Experience Manager]的無障礙功能，以吸引身心障礙的創作者。 軟體持續強化，以符合各類使用者的需求。 它遵循全球標準，包括視覺、聽覺、行動力或其他障礙人士。

[!DNL Experience Manager]會發佈符合性資訊，說明其遵循的標準、概述產品中的協助工具功能，以及符合性等級。 協助工具符合性報告可協助[!DNL Experience Manager]使用者瞭解各項標準的遵守程度。 在[!DNL Assets]中完成的增強功能可讓所有使用者透過鍵盤、熒幕閱讀器、放大鏡和其他輔助技術輕鬆使用介面。

[!DNL Experience Manager]為下列標準提供不同等級的支援：

* [網頁內容可及性指引(WCAG) 2.1](https://www.w3.org/TR/wcag/)。
* [修訂修復法案的第508節](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [協助工具計畫 — 由W3C](https://www.w3.org/WAI/standards-guidelines/aria/)協助工具的Rich Internet Applications (WAI-ARIA)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

若要閱讀包含詳細相容性層級的報表，請參閱[協助工具相容性報表](https://www.adobe.com/accessibility/compliance.html) (ACR)頁面。

若要瞭解[!DNL Dynamic Media]的存取方式，請參閱 [!DNL Dynamic Media][&#128279;](/help/assets/accessibility-dm.md)中的存取功能。

## 輔助技術 {#at-support}

殘障使用者經常依賴硬體與軟體來存取網頁內容及使用軟體產品。 這些工具稱為輔助技術。 使用軟體的核心功能時，[!DNL Experience Manager Assets]可以使用下列型別的輔助技術(AT)：

* 熒幕助讀程式和熒幕放大鏡。
* 語音辨識軟體。
* 鍵盤使用方式 — 導覽和捷徑。
* 輔助硬體，包括開關控制項、可重新整理的點字顯示器，以及其他電腦輸入裝置。
* UI放大工具。

## [!DNL Experience Manager Assets]個可存取的使用案例 {#accessible-assets-use-cases}

在[!DNL Experience Manager]中，協助工具功能可滿足[!DNL Experience Manager]使用者及其客戶的兩個主要需求。

* 對於內容設計人員和建立者而言，有建立及發佈無障礙內容的功能，可依次供其客戶和網站訪客使用。 殘障人士可在輔助技術的協助下使用內容。 如需詳細資訊，請參閱[網頁協助工具准則](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager]也可讓身心障礙的使用者和管理員存取使用者介面和控制項，以建立和管理內容。 殘障人士可使用輔助技術瀏覽、使用及管理[!DNL Assets]功能。

[!DNL Assets]中的核心功能比以前更容易存取，並且會定期更新以符合全球標準。 [!DNL Assets]中的CRUD作業內建一定程度的協助工具。 DAM工作流程例如新增、管理、搜尋和分發資產，都可透過鍵盤快速鍵、熒幕助讀程式文字、顏色對比等協助進行存取。

## 支援使用鍵盤 {#keyboard-use}

許多可使用指標點選或操作的使用者介面元素，也可以使用鍵盤來配合。 使用鍵盤時，使用者可專注於UI元素並採取適當的動作。 使用者可以直接使用鍵盤快速鍵來觸發命令或動作，而無需專注於UI元素並使用鍵盤來觸發。 例如，使用者可在使用者介面的左側開啟資產的時間軸。 使用鍵盤瀏覽至使用者介面控制項，並選取`Return`，然後選取`Alt + 2`鍵盤快速鍵。

<!--
TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets]中的鍵盤快速鍵 {#keyboard-shortcuts}

[!DNL Assets]中的下列動作可搭配列出的鍵盤快速鍵使用。 大部分套用至[!DNL Experience Manager]主控台的鍵盤快速鍵也套用至[!DNL Assets]。 請參閱主控台[&#128279;](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)的鍵盤快速鍵。 瞭解如何[啟用或停用鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 使用者介面或情境 | 鍵盤快速鍵 | 動作 |
|---|---|---|
| [!DNL Assets]使用者介面中的資料行檢視 | 向上鍵與向下鍵 | 導覽至相同階層內的檔案和資料夾。 |
| [!DNL Assets]使用者介面中的資料行檢視 | 左右方向鍵 | 導覽至目前資料夾上方或下方的檔案和資料夾。 |
| 瀏覽[!DNL Assets]中的資料夾 | `/` | 開啟Omnisearch方塊以叫用搜尋。 |
| [!DNL Assets]主控台 | &amp;grave； | 切換邊欄 |
| [!DNL Assets]主控台 | `Alt + 1` | 開啟內容樹狀結構。 |
| [!DNL Assets]主控台 | `Alt + 2` | 開啟[!UICONTROL 導覽]左側邊欄。 |
| [!DNL Assets]主控台 | `Alt + 3` | 顯示選取資產的[!UICONTROL 時間表]。 |
| [!DNL Assets]主控台 | `Alt + 4` | 開啟所選資產的即時副本參考。 |
| [!DNL Assets]主控台 | `Alt + 5` | 在選取的資料夾中開始搜尋和搜尋。 |
| 已選取資產或資料夾 | 退格鍵 | 刪除選取的資產或資料夾。 |
| 已選取資產或資料夾 | `p` | 開啟所選資產的「屬性」頁面。 |
| 已選取資產或資料夾 | `e` | 編輯選取的資產。 |
| 已選取資產或資料夾 | `m` | 移動選取的資產。 |
| 已選取資產或資料夾 | `Ctrl + c` | 複製選取的資產。 |
| 已選取資產或資料夾 | `Esc` | 取消選取。 |
| 對話方塊開啟並成為焦點 | `Esc` | 關閉對話方塊。 |
| 在DAM的資料夾內 | `Ctrl + v` | 貼上複製的資產。 |
| [!DNL Assets]主控台 | `Ctrl + A` | 選取所有資產。 |
| 資產屬性頁面 | `Ctrl + S` | 儲存變更。 |
| [!DNL Assets]主控台 | `?` | 請參閱鍵盤快速鍵清單。 |

## 登入並導覽[!DNL Assets]使用者介面 {#login}

使用者可使用鍵盤導覽並填寫登入欄位以進行登入。 每次使用者輸入錯誤的使用者名稱和密碼組合時，熒幕助讀程式都會在登入頁面上朗讀錯誤訊息。

登入後，DAM使用者可以使用鍵盤在[!DNL Assets]使用者介面中導覽。 使用者介面元素（如左側邊欄、功能表、使用者設定檔、搜尋列、檔案和資料夾以及管理和組態設定）可使用鍵盤瀏覽。 鍵盤導覽順序為由左至右、由上至下。 When users navigate with a keyboard, the UI highlights the focused actionable option with improved color contrast and screen readers narrate it. Where appropriate, screen readers announce the state (for example, expanded, collapsed, or mixed) of the focused menu options. Also, the screen reader announces the purpose of the actionable option, instead of, say, the appearance or interface placement.

If a user expands the help or user profile option from the menu, the screen reader announces the appropriate option or status. If a user expands the user profile option, the available options can be selected using a keyboard. For example, an administrator can impersonate a different user. If a user searches for a string from the [!UICONTROL Help] option, a narrator announces &quot;Searching Help&quot; to indicate that a search is in progress.

<!--
TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Browse assets and view the related information {#browse}

In the [!DNL Assets] user interface, users can use the keyboard to browse digital assets in the DAM repository and preview or download an asset. Users can also view generated renditions, switch views, and review the timeline, version history, comments, and references. In addition, users can view and manage metadata.

<!--
TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

When browsing the assets repository, the following functionality improves accessibility:

* A screen reader announces text alternatives that depict the purpose or functionality of the icons instead of their names.
* Users can access and focus the interactive user interface options in the References list of assets using keyboard keys.
* The elements in each row in list view are announced as the elements of the same row by screen readers.
* When navigating using `Tab` key, the focus can move to the close option in the version preview.
* When using the keyboard to browse, the highlighted actionable user interface options have more prominent visual focus with enhanced contrast. It makes the focused area more identifiable to the user.
* Use of the `Esc` key to remove the quick action icons from thumbnail view does not remove the keyboard focus from the last focused item.
* With an asset selected, selecting `Alt + 4` keyboard shortcut opens the [!UICONTROL References] list in the left rail. Using `Tab` key, users can navigate through the non-zero reference entries. Browsing through only the non-zero reference entries saves effort and keystrokes as well.
* Comments on an asset are available in the asset timeline. It is accessible if the left rail is accessed using a keyboard or a keyboard shortcut.
* [!UICONTROL View Settings] in [!DNL Experience Manager] are accessible using a keyboard. Users can navigate through the available card sizes using the arrow keys and select and tab through to navigate through and set other elements in the existing View Settings view.

<!--
TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理數位資產 {#manage-assets}

Many asset management tasks such as CRUD operations, downloading an asset, adding metadata are accessible to various degrees. [!DNL Assets] let you accomplish the tasks using various assistive technologies such as a screen reader and a keyboard.

For metadata operations that are typically done by roles, such as marketers and administrators, the following features improve accessibility:

* The [!UICONTROL Save &amp; Close] option on the Asset [!UICONTROL Properties] page can now be accessed using the keyboard.
* Screen readers announce the options to delete the selected tags in the [!UICONTROL Basic] tab of Asset [!UICONTROL Properties].
* Users can use the Date picker pop-up dialog box with a keyboard. The Date picker user interface element is used to set on-times and off-times, and select date.
* The drag functionality using keyboard correctly functions in the [!UICONTROL Metadata Schema Editor] in the browse mode of the screen reader.
* A user can use the keyboard to move focus to the **Add User or Group** field.

## Search digital assets {#search-assets}

A quick and seamless asset search experience boosts content velocity. The content velocity use cases are part of core [!DNL Assets] functionality. To start a search from the Omnisearch bar, users can use keyboard shortcut `/` or use `Tab` along with screen readers to locate the search option quickly. The screen reader narrates the name of the option as &quot;Search Button&quot; when the focus is on the search option ![search option](assets/do-not-localize/search_icon.png). Users can select `Return` to open the Omnisearch box. The screen reader not only narrates the keyword typed in the search box but also narrates the suggestions offered by [!DNL Experience Manager Assets]. Users can use a combination of arrow keys, `Return`, and `Tab` to access the various options to trigger a search.

Search functionality is made accessible by the following functionality:

* Page title, available to a screen reader, helps to identify the page as an assets&#39; search page.
* Users search for assets from within the Omnisearch field. Users can open it using either the keyboard navigation or the keyboard shortcut `/`.
* Users can start typing the search keyword and then select the auto-suggestions using arrow keys. Highlighted suggestion can be selected using the `Return` key and assets are searched for the selected suggestion.
* Screen readers can identify and announce mixed-state checkboxes in the Filters panel when users filter search results. 在混合狀態下，第一層核取方塊會被點進，直到使用者選取所有巢狀述詞為止。
* 關閉Omnisearch方塊後，使用者焦點會移至搜尋選項。

篩選搜尋結果時：

* 搜尋結果頁面有一個資訊性的標題，可讓使用者更瞭解熒幕助讀程式。
* 熒幕助讀程式會朗讀搜尋篩選器中的選項，作為可展開的摺疊式功能表。
* 熒幕助讀程式會朗讀包含混合狀態選項的述詞。

## 共用資產 {#share-assets}

<!--
TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共用資產時，下列功能可改善協助工具：

* 使用者可以使用鍵盤在連結共用對話方塊的「搜尋並新增電子郵件地址」欄位中移動焦點。

* 在連結共用對話方塊中，以瀏覽模式導覽時，熒幕助讀程式會：

   * 載入對話方塊時，不要提供表格資訊的旁白。
   * 導覽至列出的所有建議。
   * 提供旁白來敘述新增電子郵件地址和搜尋欄位顯示的建議。

## 無障礙檔案 {#accessible-docs}

[!DNL Experience Manager]提供無障礙說明檔案，以供身心障礙人士使用。 以下內容有助於讓內容立即可供存取，同時Adobe會繼續改善範本和內容：

* 熒幕助讀程式可以閱讀文字。
* 影像和插圖有可用的替代文字。
* 可以使用鍵盤導覽。
* 對比率有助於強調說明檔案網站的某些部分。

## 提供回饋意見 {#a11y-feedback}

若要提供與協助工具相關的意見回饋、提出問題並請求產品增強功能，請使用下列方法，將電子郵件傳送至`access@adobe.com`。

>[!MORELIKETHIS]
>
>* [&#x200B; [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的協助工具功能。
>* [每個Service Pack版本](/help/release-notes/release-notes.md)中完成的增強功能的發行說明。
>* [[!DNL Adobe Experience Manager] 協助工具指引](/help/managing/web-accessibility.md)。
>* [Adobe解決方案的一致性報告(ACR)和VPAT清單](https://www.adobe.com/accessibility/compliance.html)。
