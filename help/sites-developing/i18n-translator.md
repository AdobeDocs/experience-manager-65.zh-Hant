---
title: 使用翻譯器管理詞典
seo-title: Using Translator to Manage Dictionaries
description: 提AEM供了用於管理元件UI中使用的文本的各種翻譯的控制台
seo-description: AEM provides a console for managing the various translations of texts used in component UI
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# 使用翻譯器管理詞典{#using-translator-to-manage-dictionaries}

提AEM供了用於管理元件UI中使用的文本的各種翻譯的控制台。 此控制台可在

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

使用翻譯工具管理英文字串及其翻譯。 字典是在儲存庫中建立的，例如/apps/myproject/i18n。

請注意，「翻譯器」工具和您管理的詞典用於以不同語言顯示元件UI。 如果要翻譯頁面或用戶生成的內容，請參閱 [翻譯多語言站點的內容](/help/sites-administering/translation.md) 和 [用戶生成內容的翻譯](/help/communities/translate-ugc.md)。

>[!CAUTION]
>
>僅編輯為項目建立並位於 `/apps`。
>
>此工AEM具中還提供系統詞典。 不要更改系AEM統詞典，因為這可能導致UIAEM問題。 此外，升級時更改可能丟失。 AEM系統詞典位於 `/libs`。

>[!NOTE]
>
>儘管「翻譯器」工具具有經典的UI介面，但它用於翻譯短語，而不管這些短語在哪個介面中找到。

譯者將各種語言AEM翻譯中使用的文本並列列出：

![chlimage_1-205](assets/chlimage_1-205.png)

您可以搜索、篩選和編輯英文和已翻譯文本。 您還可以將詞典導出為XLIFF格式進行翻譯，然後將翻譯導入回詞典。

也可以從此控制台將i18n字典添加到翻譯項目中。 您可以建立新項目或添加到現有項目。

1. 按一下 **翻譯詞典**。

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. 根據需要選擇「建立」或「添加」選項。 將開啟一個對話框。

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. 根據需要填寫欄位，然後按一下「確定」。 ![chlimage_1-208](assets/chlimage_1-208.png)

1. 您現在可以按一下 **確定** 或查看目標詞典。

   >[!NOTE]
   >
   >有關翻譯項目的詳細資訊，請閱讀 [管理翻譯項目](/help/sites-administering/tc-manage.md)。

## 建立字典 {#creating-a-dictionary}

建立用於管理本地化UI字串的字典。 建立字典後，可以使用翻譯工具管理字典。

1. 使用CRXDE Lite，添加根節點( `sling:Folder`)，作為保存語言定義的結構：

   ` /apps/<projectName>/i18n`

   例如 `/apps/myProject/i18n`

1. 在此根下添加所需的語言結構。 例如：

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >這是 [吊具i18n模組](https://sling.apache.org/site/internationalization-support.html)。

1. 重新載入轉換器和字典路徑(例如 `/apps/myProject/i18n`)將在工具欄的下拉選擇器中可用。 選擇此選項可開始添加字串及其翻譯。

   >[!NOTE]
   >
   >翻譯器將僅保存路徑下實際存在的語言的翻譯(例如， `/apps/myProject/i18n`)。
   >
   >確保這些語言與網格中顯示的語言對應。

## 管理字典字串 {#managing-dictionary-strings}

使用翻譯工具管理詞典中的字串。 您可以添加、修改和刪除英文字串，還可以提供已翻譯的字串。

>[!CAUTION]
>
>僅編輯為項目建立並位於 `/apps`。
>
>不要更改系AEM統詞典，因為這可能導致UIAEM問題。 此外，升級時更改可能丟失。 AEM系統詞典位於 `/libs`。

### 添加、更改和刪除字串 {#adding-changing-and-removing-strings}

將英文字串添加到您的元件已國際化的詞典。 只添加國際化的字串，這樣您就不會通過翻譯未使用的字串而浪費資源。

添加到字典的字串必須與在代碼中指定的字串完全匹配。 如果代碼中使用的預設英文字串與字典中的英文字串不匹配，則在需要時，翻譯後的字串不會出現在UI中。 字串區分大小寫。

**提供翻譯提示**

使用字典字串的Commentet屬性向轉換器提供資訊以澄清字串的含義。 通常，UI會幫助用戶確定模糊詞的含義。 但是，轉換器在UI的上下文中看不到字串。 翻譯提示可消除歧義。 例如，注釋有助於翻譯人員瞭解英文單詞Request是用作名詞而不是動詞。

翻譯提示還可區分相同且含義不同的字串。 例如，詞Search可以是名詞或動詞，需要詞典中兩個「Search」條目，其中有兩個不同的翻譯提示。 請求字串的代碼還包含轉換提示，以便在UI中使用正確的字串。

**包括索引變數**

在本地化字串中包括變數，以將上下文意義構建到句子中。 例如，登錄到Web應用程式後，首頁將顯示消息「歡迎返回管理員」。 您的收件箱中有2封留言。」 頁面上下文確定用戶名和消息數。

要在本地化字串中包括變數，請將帶括弧的索引置於get方法第一個參數中變數的位置。 使用本地化提示描述值。 翻譯者必須理解變數的含義，因為不同語言使用不同的句子結構。

請注意 [請求轉換後的字串的代碼](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) 根據上下文為索引變數提供值。

例如，當用戶登錄到網站並包含在詞典中時，將顯示以下字串：

`Welcome back {0}. You have {1} messages.`

以下注釋描述了變數：

`{0} = the user name, {1} = the number of items in the user's inbox`

**修改字串**

在代碼中更改或刪除英文字串時，請更改或刪除這些字串。 當更改字串時，原始字串將保留，並生成反映更改的新字串。 在刪除字串之前，請確保沒有代碼使用它。

請按下列步驟添加字串。

1. 在「詞典」下拉菜單中，選擇要添加字串的詞典。 在下拉菜單中，字典由它們在儲存庫中的路徑表示。
1. 在「字串和轉換」(Strings and Translations)表格上，按一下「添加」(Add)。

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 在「添加字串」對話框的「字串」框中，鍵入英文字串。 在「注釋」框中，鍵入翻譯員的翻譯提示（如有必要）。
1. 按一下「確定」。
1. 按一下「儲存」。

   ![chlimage_1-210](assets/chlimage_1-210.png)

請按下列步驟更改字典中的字串。

1. 在「詞典」下拉菜單中，選擇包含要更改的字串的詞典。
1. 按兩下要更改的字串。
1. 在「編輯字串」對話框中，選擇「修改字串」或「注釋」（建立副本）。

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. 修改字串或注釋，然後按一下確定。
1. 按一下「儲存」。

   ![chlimage_1-212](assets/chlimage_1-212.png)

請按下列步驟從字典中刪除字串。

1. 在「詞典」下拉菜單中，選擇要從中刪除字串的詞典。
1. 按一下移除。

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 按一下「儲存」。

   ![chlimage_1-214](assets/chlimage_1-214.png)

### 搜索字串 {#searching-for-strings}

「轉換器」工具底部的搜索欄提供了字串選擇選項：

* **按文本篩選：** 與英文字串、注釋或翻譯匹配的模式。 表中只顯示與陣列全部或部分匹配的項目。
* **更改：任意、已修改、新建、已刪除：** 顯示已更改且未保存的項目。

   * 任意：顯示已修改、添加或刪除的項。
   * 已修改：顯示已更改的項。
   * 新建：顯示添加的項。
   * 已刪除：顯示要刪除的項。
   * 多個選擇：顯示具有所有選定屬性的項。

* **有注釋**:顯示有翻譯員注釋的項目。
* **缺少翻譯：** 顯示至少一種語言沒有翻譯的項目。

![chlimage_1-215](assets/chlimage_1-215.png)

1. 在搜索欄上，選擇篩選選項。
1. 要使用選項進行篩選，請按一下「篩選」。
1. 要刪除過濾器並查看字典中的所有項，請按一下「清除」。

### 編輯已轉換字串 {#editing-translated-strings}

將英文字串添加到字典後，可以添加字串的翻譯。 您也可以 [導出字典](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) 由第三方翻譯。

1. 選擇 [您的項目特定詞典](#creating-a-dictionary) 指定儲存庫中保存翻譯的路徑。 例如，選擇 **詞典** 為：

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >僅編輯為項目建立並位於 `/apps`。
   >
   >此工AEM具中還提供系統詞典。 不要更改系AEM統詞典，因為這可能導致UIAEM問題。 此外，升級時更改可能丟失。 AEM系統詞典位於 `/libs`。

1. 要編輯某個字串的已翻譯文本，您可以執行以下任一操作：

   * 按兩下所需字串的相應語言以編輯該文本：

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * 按兩下 **字串** 或 **注釋** 用於開啟 **編輯字串** 對話框，根據需要編輯翻譯，然後按一下 **確定** 關閉對話框：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 按一下 **保存** 的子菜單。

   >[!NOTE]
   >
   >按一下 **重置和刷新** (而不是 **保存**)對以前的文本進行任何更改。

## 使用第三方翻譯員 {#using-third-party-translators}

為支援使用第三方翻譯服務，翻譯工具使您能夠導出和導入字典。

### 導出字典 {#exporting-a-dictionary}

將字典導出到XLIFF檔案，以便第三方服務可以翻譯字典字串。

* 導出字典，並包括語言的英語和已翻譯術語。
* 導出部分或全部英文字串。

導出XLIFF檔案並包括語言時，儲存庫中字典的節點結構必須包括該語言。 如果未包括該語言，則會出錯。 例如，要導出法文XLIFF檔案，字典資料夾必須包括 `mix:language` 子節點命名 `fr`。 (請參閱 [建立字典](/help/sites-developing/i18n-translator.md#creating-a-dictionary)。)

請按下列步驟為特定語言導出XLIFF檔案。

1. 開啟翻譯工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用「字典」下拉菜單選擇要導出的字典。
1. 按一下「導出」(Export)>「導出完整」(Export Full) *XX* Xliff選項，其中 *XX* 是雙字母語言代碼，如DE或FR。

   XLIFF檔案將在新頁籤或窗口中開啟。

1. 使用Web瀏覽器命令將頁面另存為檔案在檔案系統上，如「檔案」>「將頁面另存為」。

請按下列步驟導出全部或部分英文字串。

1. 開啟「翻譯」工具。 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用「字典」下拉菜單選擇要導出的字典。
1. 如果要導出字串的子集，請選擇要導出的詞典中的項。 選擇「無」項會導出所有項。
1. 按一下「導出」(Export)>「將所選內容導出為xliff（僅字串）」。
1. 在出現的對話框中，複製文本並將其貼上到文本檔案中。

### 導入字典 {#importing-a-dictionary}

將XLIFF檔案導入字典以填充字典。 當字典包括英文字串的翻譯，而XLIFF檔案包含同一字串的不同翻譯時，字典翻譯將被替換。

1. 開啟翻譯工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 按一下「導入」(Import)>「XLIFF翻譯」(XLIFF Translations)。
1. 選擇要導入的檔案，然後按一下「確定」。

## 管理支援的語言 {#managing-supported-lanuages}

添加或刪除翻譯工具支援並提供給網頁用戶的語言。

### 更改字典表中列出的語言 {#changing-languages-listed-in-the-dictionary-table}

「翻譯器」工具在字典表中包含以下語言：

* de — 德語
* fr — 法語
* 它 — 義大利
* es — 西班牙語
* ja — 日語
* pt-br — 巴西葡萄牙語
* zh-cn — 簡體中文
* zh-tw — 繁體中文（有限支援）
* ko-kr — 朝鮮語

請按下列步驟添加或刪除語言。

1. 使用CRXDE Lite建立新節點：

   `/etc/languages`

1. 在此節點上，建立一個屬性：

   * **名稱**: `languages`
   * **類型**: `Multi-String`
   * **值**:要顯示的語言清單。 例如：

      * fr
      * es

   >[!NOTE]
   >
   >語言代碼必須為小寫。

1. 按一下 **全部保存** CRXDE Lite並重新載入轉換器。 將更新網格以顯示定義的語言。

   >[!NOTE]
   >
   >翻譯器將只保存實際上 [在字典里](#creating-a-dictionary) (即字典路徑下，例如 `/apps/myProject/i18n`)。
   >
   >確保這些語言與網格中顯示的語言對應。

### 使語言可供作者使用 {#making-languages-available-to-authors}

在為實例中新的語言定義詞典AEM後，您需要使此詞典可供作者選擇(例如，在 **首選項**):

1. 更改中可用語言的清單 **首選項** 的 **安全** 控制台：

   1. 在應用程式碼中為以下項建立覆蓋：

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. 使語言在中可用 **首選項** 從 **網站** 控制台需要在應用程式中進行以下更改：

   1. 在下面為結構建立覆蓋：

      `/libs/cq/security/content/tools/userProperties`

   1. 在覆蓋內更新語言清單：

      `items/common/items /lang/options`

1. 保存所有內容並重新載入相應的控制台。

### 更改語言名稱和預設國家/地區 {#changing-language-names-and-default-countries}

各國都用同一種語言，比如美國，英國，澳大利亞都用英語。 這由代碼表示，該代碼同時指示語言和國家(如 `en_US`。 `en_GB` 和 `en_AU`。

在顯示標誌時（例如，在語言副本對話框中）使用預設國家（地區），它們用於解析語言代碼的國家（地區）。

>[!NOTE]
>
>對於由上面的翻譯器管理的本地化，只有準確的語言才起作用。 如果語言首選項下拉清單使用 `en_uk`，肯定有 `en_uk` 詞典。

要更改預設定義：

1. 語言清單儲存在：

   `/libs/wcm/core/resources/languages`

   將其複製到：

   `/apps/wcm/core/resources/languages`

   然後更改或擴展該清單。 屬性 `defaultCountry` 語言節點(例如 `ja`)必須包含完整代碼，如 `ja_jp`，定義 `jp` 作為語言的預設國家/地區 `ja`。

1. 更新 **CQ WCM語言管理器**。

   * **語言清單**:

      儲存庫中語言清單的路徑。 將此設定為用於覆蓋的位置：

      ```
             /apps/wcm/core/resources/languages
      ```
   您可以使用OSGi Web控制台執行此操作：

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## 發佈詞典 {#publishing-dictionaries}

將您的詞典納入應用程式的版本管AEM理流程。 例如，在應用程式的內容包中包含詞典，以便部署到發佈實例。 此策略具有以下優點：

* 詞典可用於其發佈環境中的元件。
* 對元件UI字串的更改與更新的轉換一起部署。

同樣，字典字串的測試應作為正常軟體開發生命週期的一部分執行。

>[!NOTE]
>
>定期發佈功能或複製不應用於字典。 相反，應將字典與代碼和配置相同地對待。 這包括使用原始碼管理跟蹤更改，以及使用內容包將更改應用於作者和發佈。

>[!NOTE]
>
>使用Dispatcher時，您需要 [無效快取頁](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) 在已呈現的元件字串中包含新的字典字串。
