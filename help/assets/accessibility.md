---
title: 可訪問的功能和介面 [!DNL Experience Manager Assets]
description: 瞭解中的輔助功能 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 幫助殘疾用戶。
contentOwner: AG
feature: Asset Management
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: 399ae241593b5cc14ef1c2efd090f0d1fae7c2df
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

# 中的輔助功能 [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] 允許內容建立者和發佈者在網路上提供驚人體驗。 Adobe努力通過改善殘疾人的無障礙性 [!DNL Experience Manager]。 軟體不斷得到增強，以滿足所有類型用戶的需要，並遵守包括視覺、聽覺、移動性或其他缺陷的個人在內的全球標準。

[!DNL Experience Manager] 發佈符合性資訊，描述其遵守的標準，概述產品中的輔助功能，並描述法規遵從性級別。 輔助功能一致性報告幫助 [!DNL Experience Manager] 用戶瞭解各種標準的遵守程度。 在 [!DNL Assets] 讓所有用戶通過鍵盤、螢幕閱讀器、放大鏡和其他輔助技術輕鬆使用介面。

[!DNL Experience Manager] 為以下標準提供不同級別的支援：

* [網頁內容可及性指引 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [《康復法》第508條修訂](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [輔助功能計畫 — W3C提供的可訪問的富網際網路應用程式(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

要閱讀包含符合性級別詳細資訊的報告，請參閱 [輔助功能符合性報表](https://www.adobe.com/accessibility/compliance.html) (ACR)頁。

要知道 [!DNL Dynamic Media] 可訪問，請參閱 [輔助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)。

## 輔助技術 {#at-support}

殘疾用戶經常依靠硬體和軟體來訪問網路內容和使用軟體產品。 這些工具被稱為輔助技術。 [!DNL Experience Manager Assets] 使用軟體的核心功能時，可以使用以下類型的輔助技術(AT):

* 螢幕閱讀器和螢幕放大鏡。
* 語音識別軟體。
* 鍵盤用法 — 導航和快捷方式。
* 輔助硬體，包括開關控制、可刷新的盲文顯示器和其他電腦輸入設備。
* UI放大工具。

## [!DNL Experience Manager Assets] 可訪問的使用案例 {#accessible-assets-use-cases}

在 [!DNL Experience Manager]，輔助功能可滿足以下兩個關鍵要求： [!DNL Experience Manager] 用戶及其客戶。

* 對於內容設計者和建立者，有建立和發佈可供其客戶和網站訪問者依次使用的可訪問內容的功能。 殘疾人在輔助技術的幫助下使用內容。 有關詳細資訊，請參閱 [Web輔助指南](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager] 還允許其用戶和管理員訪問用戶介面和控制項來建立和管理內容。 殘疾人可以使用輔助技術導航、使用和管理 [!DNL Assets] 功能。

中的核心功能 [!DNL Assets] 比以前更容易獲得，並定期更新，以改進對全球標準的遵守。 CRUD操作 [!DNL Assets] 有一定程度的可訪問性。 通過鍵盤快捷鍵、螢幕閱讀器文本、顏色對比度等，可以訪問DAM工作流，如添加、管理、搜索和分發資產。

## 支援使用鍵盤 {#keyboard-use}

使用鍵盤還可以使用可點擊或可操作的許多用戶介面元素。 使用鍵盤，用戶可以專注於UI元素並採取適當的操作。 用戶可以直接使用鍵盤快捷鍵來觸發命令或操作，而無需關注UI元素並使用鍵盤來觸發它。 例如，用戶可以通過使用鍵盤瀏覽到用戶介面控制項並選擇 `Return`，選擇 `Alt + 2` 鍵盤快捷鍵。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### 鍵盤快捷鍵 [!DNL Assets] {#keyboard-shortcuts}

以下操作 [!DNL Assets] 使用列出的鍵盤快捷鍵。 適用於的大多數鍵盤快捷鍵 [!DNL Experience Manager] 控制台也適用於 [!DNL Assets]。 請參閱 [控制台的鍵盤快捷鍵](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)。 瞭解如何 [啟用或禁用鍵盤快捷鍵](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 用戶介面或方案 | 鍵盤快捷鍵 | 動作 |
|---|---|---|
| 列視圖 [!DNL Assets] 用戶介面 | 上箭頭和下箭頭鍵 | 導航到同一層次結構中的檔案和資料夾。 |
| 列視圖 [!DNL Assets] 用戶介面 | 左箭頭和右箭頭鍵 | 導航到當前資料夾上方或下方的檔案和資料夾。 |
| 瀏覽資料夾 [!DNL Assets] | `/` | 通過開啟Omnisearch框調用搜索。 |
| [!DNL Assets] 主控台 | &grave; | 切換邊欄 |
| [!DNL Assets] 主控台 | `Alt + 1` | 開啟內容樹。 |
| [!DNL Assets] 主控台 | `Alt + 2` | 開啟 [!UICONTROL 導航] 左欄。 |
| [!DNL Assets] 主控台 | `Alt + 3` | 顯示 [!UICONTROL 時間軸] 的子菜單。 |
| [!DNL Assets] 主控台 | `Alt + 4` | 開啟所選資產的Live Copy引用。 |
| [!DNL Assets] 主控台 | `Alt + 5` | 開始在所選資料夾中搜索和搜索。 |
| 已選擇資產或資料夾 | 退格字元 | 刪除所選資產或資料夾。 |
| 已選擇資產或資料夾 | `p` | 開啟所選資產的「屬性」頁。 |
| 已選擇資產或資料夾 | `e` | 編輯所選資產。 |
| 已選擇資產或資料夾 | `m` | 移動所選資產。 |
| 已選擇資產或資料夾 | `Ctrl + c` | 複製所選資產。 |
| 已選擇資產或資料夾 | `Esc` | 取消選擇。 |
| 對話框開啟，並位於焦點中 | `Esc` | 關閉對話框。 |
| 在DAM中的資料夾內 | `Ctrl + v` | 貼上複製的資產。 |
| [!DNL Assets] 主控台 | `Ctrl + A` | 選擇所有資產。 |
| 資產屬性頁 | `Ctrl + S` | 保存更改。 |
| [!DNL Assets] 主控台 | `?` | 請參閱鍵盤快捷鍵清單。 |

## 登錄並導航 [!DNL Assets] 用戶介面 {#login}

用戶可以使用鍵盤導航並填寫登錄欄位以登錄。 每次出現錯誤時，螢幕閱讀器都會宣佈由於登錄頁上的用戶名和密碼組合不正確而導致的錯誤消息。

登錄後，DAM用戶可以在 [!DNL Assets] 使用鍵盤的用戶介面。 用戶介面元素（如左滑軌、菜單、用戶配置檔案、搜索欄、檔案和資料夾）以及管理和配置設定可使用鍵盤導航。 鍵盤導航順序為從左到右和從上到下。 當使用鍵盤導航時，聚焦時可操作的選項會以更好的顏色對比度突出顯示，並由螢幕閱讀器敘述。 在適當的情況下，螢幕閱讀器會宣佈菜單中的聚焦選項的狀態，例如，展開、折疊和混合狀態。 此外，螢幕閱讀器還會宣佈可操作選項的用途，而不是說外觀或介面放置。

如果用戶從菜單中展開幫助或用戶配置檔案選項，螢幕閱讀器會宣佈相應的選項或狀態。 如果用戶展開用戶配置檔案選項，則可以使用鍵盤選擇可用選項。 例如，管理員可以模擬其他用戶。 如果用戶從 [!UICONTROL 幫助] 的子菜單。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 瀏覽資產並查看相關資訊 {#browse}

在 [!DNL Assets] 用戶介面，用戶可以使用鍵盤瀏覽DAM儲存庫中現有數字資產的清單，預覽或下載資產，查看生成的格式副本，切換視圖，查看生成的格式副本，查看時間軸和版本歷史記錄，查看注釋和引用，以及查看和管理元資料。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

瀏覽資產儲存庫時，以下功能可提高可訪問性：

* 螢幕閱讀器會發佈描述表徵圖的用途或功能而不是其名稱的文本替代選項。
* 用戶可以使用鍵盤鍵訪問和集中「引用」資產清單中的互動式用戶介面選項。
* 清單視圖中每行中的元素都由螢幕閱讀器作為同一行的元素來宣佈。
* 導航時使用 `Tab` 鍵，焦點可移到版本預覽中的「關閉」選項。
* 當使用鍵盤進行瀏覽時，突出顯示的可操作用戶介面選項具有更突出的視覺焦點，對比度增強。 它使聚焦區域對用戶更加可辨認。
* 使用 `Esc` 從縮略圖視圖中刪除快速操作表徵圖的鍵不會從最後一個聚焦項目中刪除鍵盤焦點。
* 選擇資產後，選擇 `Alt + 4` 鍵盤快捷鍵開啟 [!UICONTROL 引用] 清單。 使用 `Tab` 鍵，用戶可以瀏覽非零引用條目。 僅瀏覽非零引用條目也節省了工作和擊鍵。
* 資產時間表中提供了對資產的注釋。 如果使用鍵盤或鍵盤快捷鍵訪問左滑軌，則可訪問該滑軌。
* [!UICONTROL 查看設定] 在 [!DNL Experience Manager] 可使用鍵盤訪問。 用戶可以使用箭頭鍵瀏覽可用的卡大小，並選擇和選中標籤，以瀏覽和設定現有「視圖設定」視圖中的其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理數位資產 {#manage-assets}

許多資產管理任務（如CRUD操作、下載資產、添加元資料）都可在不同程度上訪問。 [!DNL Assets] 讓您使用螢幕閱讀器和鍵盤等各種輔助技術完成任務。

查看如何使用鍵盤進行 [瀏覽儲存庫並下載資產](https://youtu.be/K3dgqMRQJys)。

對於通常由營銷人員和管理員等角色執行的元資料操作，以下功能可提高可訪問性：

* [!UICONTROL 保存並關閉] 資產期權 [!UICONTROL 屬性] 現在可以使用鍵盤訪問頁面。
* 螢幕閱讀器宣佈刪除中選定標籤的選項 [!UICONTROL 基本] 頁籤 [!UICONTROL 屬性]。
* 用戶可以使用鍵盤上的Datepicker彈出對話框。 Datepicker用戶介面元素用於設定開機時間和關機時間，並選擇日期。
* 使用鍵盤的拖動功能在 [!UICONTROL 元資料架構編輯器] 在螢幕閱讀器的瀏覽模式下。
* 用戶可以使用鍵盤將焦點移動到下面的「添加用戶」或「組」欄位 [!UICONTROL 已關閉用戶組] 的 [!UICONTROL 權限] 資料夾頁籤 [!UICONTROL 屬性]。

## 搜索數字資產 {#search-assets}

快速、無縫的資產搜索體驗可提高內容速度。 內容速度使用案例是核心部分 [!DNL Assets] 功能。 要從Omnisearch欄開始搜索，用戶可以使用鍵盤快捷鍵 `/` 或 `Tab` 與螢幕閱讀器一起快速查找搜索選項。 當焦點在搜索選項上時，螢幕閱讀器會將選項的名稱描述為「搜索按鈕」 ![搜索選項](assets/do-not-localize/search_icon.png)。 用戶可以選擇 `Return` 開啟Omnisearch。 螢幕閱讀器不僅敘述在搜索框中鍵入的關鍵字，還敘述由 [!DNL Experience Manager Assets]。 用戶可以使用箭頭鍵的組合， `Return`, `Tab` 來觸發搜索。

搜索功能可通過以下功能訪問：

* 頁面標題（如螢幕閱讀器可用）有助於將頁面標識為資產的搜索頁面。
* 用戶從Omnisearch欄位中搜索資產。 用戶可以使用鍵盤導航或鍵盤快捷鍵開啟它 `/`。
* 用戶可以開始鍵入搜索關鍵字，然後使用箭頭鍵選擇自動建議。 可以使用 `Return` 搜索鍵和資產以查找所選建議。
* 篩選器面板中篩選搜索結果時，螢幕閱讀器可以識別並宣佈混合狀態複選框（除非選擇所有嵌套的謂詞，否則第一級複選框不會被選中並衝透）。
* 關閉Omnisearch框後，用戶焦點將移到搜索選項。

篩選搜索結果時：

* 搜索結果頁面具有資訊標題，可更好地瞭解螢幕閱讀器用戶。
* 螢幕閱讀器將搜索過濾器中的選項作為可擴展的手風琴來宣佈。
* 具有混合狀態選項的謂詞由螢幕閱讀器宣佈。

## 共用資產 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共用資產時，以下功能可提高可訪問性：

* 用戶可以使用鍵盤在連結共用對話框中的「搜索」和「添加電子郵件地址」欄位中移動焦點。

* 在連結共用對話框中，在瀏覽模式下導航時，螢幕閱讀器，

   * 載入對話框時，不說明表資訊。
   * 可以導航到所有列出的建議。
   * 說明「添加電子郵件地址」和「搜索」欄位的顯示建議。

## 可訪問的文檔 {#accessible-docs}

[!DNL Experience Manager] 提供供殘疾人使用的輔助文檔。 以下內容有助於立即訪問內容，同時Adobe繼續改進模板和內容：

* 螢幕閱讀器可以讀取文本。
* 影像和插圖具有可用的替代文字。
* 鍵盤導航是可能的。
* 對比度有助於突出顯示文檔網站的某些部分。

## 提供反饋 {#a11y-feedback}

要提供與輔助功能相關的反饋、提問和請求產品增強功能，請使用以下方法：

* 在以下位置填寫表單 [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)。
* 請發送電子郵件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [中的輔助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)。
>* [發佈說明，說明在每個Service Pack版本中都做了增強](/help/release-notes/release-notes.md)。
>* [[!DNL Adobe Experience Manager] 輔助指導](/help/managing/web-accessibility.md)。
>* [Adobe解決方ACR案的符合性報告()和VPAT清單](https://www.adobe.com/accessibility/compliance.html)。

