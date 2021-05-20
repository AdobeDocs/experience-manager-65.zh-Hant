---
title: 建立表單入口網站頁面
seo-title: 建立表單入口網站頁面
description: Forms入口網站為網頁開發人員提供元件，以便在使用Adobe Experience Manager(AEM)製作的網站上建立和自訂表單入口網站。
seo-description: Forms入口網站為網頁開發人員提供元件，以便在使用Adobe Experience Manager(AEM)製作的網站上建立和自訂表單入口網站。
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: 表單入口網站
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---


# 建立表單入口網頁{#creating-a-forms-portal-page}

Forms入口網站元件為網頁開發人員提供元件，以便在使用Adobe Experience Manager(AEM)製作的網站上建立和自訂表單入口網站。 如需表單入口網站的快速概覽，請參閱[在入口網站上發佈表單的簡介](../../forms/using/introduction-publishing-forms.md)。

## 必備條件 {#prerequisites}

Forms入口網站元件預設無法使用。 確保以下表單門戶元件類別已啟用，如[啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)中所述。

**文檔** 服務包括Search &amp; Lister、Link、Drafts和Submissions元件。

**文檔服** 務謂詞包括日期謂詞、全文謂詞、屬性謂詞和標籤謂詞元件。這些元件用於在Search &amp; Lister元件中配置搜索。

在AEM網站頁面上啟用後，這些元件類別即可在元件瀏覽器中使用。

![元件瀏覽器中的AEM Forms入口網站元件](assets/component-categories.png)

Forms入口網站元件類別

## Search &amp; Lister元件{#search-amp-lister-component}

「文檔服務」元件類別下提供的Search &amp; Lister元件用於列出頁面上的表單，以及對列出的表單實施搜索。 元件包含兩個窗格：

* 列出表單的清單窗格。
* 添加搜索功能的搜索窗格。

您可以將「Search &amp; Lister」元件從元件瀏覽器的「Document Services」元件類別拖放到頁面上。 新增元件後，看起來類似下列。

![頁面中的搜尋與清單元件](assets/fp-grid-viw.png)

在具有網格佈局的頁面中搜索和清單元件

### 清單窗格{#list-pane}

「清單」窗格是列出表單的區域。 Search &amp; Lister元件提供了各種配置選項，可用於控制「清單」窗格中表單的顯示。

若要設定「清單」窗格，請點選「搜尋」和「清單」元件，然後點選![settings_icon](assets/settings_icon.png)。 將開啟「編輯元件」對話框。****

![以編輯模式顯示的清單窗格](assets/edit-list.png)

以編輯模式顯示的清單窗格

**Edit**&#x200B;對話框包括幾個頁簽，這些頁簽提供下表中描述的配置選項。 點選&#x200B;**OK**&#x200B;以儲存設定，完成時。

<table>
 <tbody>
  <tr>
   <th>索引標籤</th>
   <th>設定</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>資產資料夾</strong></code></td>
   <td>新增項目</td>
   <td>設定使用AEM Forms UI上傳資產的資料夾。 依預設，會列出所有上傳的資產。 如需AEM Forms UI的詳細資訊，請參閱<a href="../../forms/using/introduction-managing-forms.md" target="_blank">管理表單簡介</a>。</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>顯示</strong></code></p> </td>
   <td>標題文字</td>
   <td>Search &amp; Lister元件的標題。 預設標題為<strong>Forms Portal。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>資產的配置。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用高級搜索</td>
   <td>啟用後，會隱藏進階搜尋圖示。</td>
  </tr>
  <tr>
   <td> </td>
   <td>停用文字搜尋</td>
   <td>啟用後，會隱藏全文搜索欄。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>結果</strong></code></td>
   <td>每頁結果數</td>
   <td>設定您要在頁面上顯示的表單數量上限。</td>
  </tr>
  <tr>
   <td> </td>
   <td>結果文字</td>
   <td><p>配置結果文本（例如，601 <strong>Results</strong>的1-12）。 預設值為<strong>Results</strong>。</p> <p>例如，如果您在此欄位中指定<strong>Forms </strong>，且總共有601個表單，則結果文字會變更為601 <strong>Forms的1-12。</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>頁面文字</td>
   <td><p>配置頁面文本（例如，<strong>頁面</strong>1，共51頁）。 預設值為<strong>Page</strong>。</p> <p>例如，如果在此欄位中指定<strong>「應用表單</strong>」，且有51頁，則頁面文本將更改為<strong>「應用表單</strong>1/51」。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Of 文字</td>
   <td><p>將</strong>的<strong>取代為指定的文字（</strong>51的第1頁<strong>）。 預設值為<strong>of</strong>。</strong></strong></p> <p>例如，如果您在此欄位中指定<strong>out of </strong>，則文字會變更為</strong>out <strong>out 51頁。</strong></p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>表單連結</strong></code></td>
   <td>呈現類型</td>
   <td>根據指定的呈現類型控制表單清單。 可用的選項有PDF和HTML。 例如，如果僅選擇HTML作為渲染類型，則會過濾掉PDF forms。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML設定檔</td>
   <td>設定用於呈現的HTML設定檔。 下拉式清單中會列出所有可用的設定檔。</td>
  </tr>
  <tr>
   <td> </td>
   <td>提交URL</td>
   <td><p>配置提交表單資料的Servlet。</p> <p><strong>注意：</strong> <em>表單的提交URL可在數個位置指定，其優先順序如下：</em></p>
    <ol>
     <li><em>表單中內嵌的提交URL（在「提交」按鈕中）具有最高優先順序。</em></li>
     <li><em>AEM Forms UI中提及的提交URL具有第二高的優先順序。</em></li>
     <li><em>表單入口網站中提及的提交URL優先順序最低。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML呈現操作工具提示</td>
   <td>配置工具提示的文本，該文本顯示在將指針懸停在<img height="16" src="assets/aem6forms_panel-html.png" width="13" />上（HTML5表徵圖）上。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF轉譯動作工具提示</td>
   <td>配置工具提示的文本，該文本顯示在將指針懸停在<img height="16" src="assets/aem6forms_panel-pdf.png" width="14" />上（PDF表徵圖）上。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>樣式</strong></code></td>
   <td>樣式類型</td>
   <td>可指定<strong>無樣式、預設樣式</strong>或<strong>自訂樣式</strong>以列出表單。</td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果選擇「自定義」作為「樣式類型」，請瀏覽以指定自定義CSS的路徑，否則選擇「預設」。</td>
  </tr>
 </tbody>
</table>

### 搜索窗格{#search-pane}

「搜尋」窗格可讓您從AEM Sidekick的「檔案服務述詞」類別中新增「日期述詞」、「全文述詞」、「屬性述詞」和「標籤述詞」元件。 這些元件為使用者實作搜尋功能，以便在列出的表單上執行搜尋。

**提示：** *您可以根據預設條件控制表單入口網站上顯示的表單清單，並隱藏使用者的搜尋功能。若要控制表單清單，請使用述詞元件來套用搜尋篩選器。 您也可以指定預設篩選值，並從「編輯元件」對話框的「顯示」頁簽中禁用搜索。*

![含有日期、全文、屬性和標籤述詞的搜尋面板](assets/search-with-predicates.png)

含有日期、全文、屬性和標籤述詞的搜尋面板

#### 日期述詞 {#date-predicate}

新增「日期述詞」元件後，即可搜尋在指定期間修改的清單。

要配置「日期謂詞」元件，請執行以下操作：

1. 點選元件，然後點選![settings_icon](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 指定下列項目：

   * **類型：** 唯一可用的選項是「上次 **修改日期」**

   * **文字：** 日期述詞元件的標籤或註解。預設值為&#x200B;**上次修改日期。**

   * **開始日期標籤：** 標籤或開始日期欄位的標題
   * **結束日期標籤：** 結束日期欄位的標籤或註解
   * **隱藏：** 若要強制執行預設日期篩選以列出表單

1. 點選&#x200B;**確定**

#### 全文謂詞{#full-text-predicate}

全文述詞元件會對表單資料（例如名稱和說明）實作全文搜尋。 使用者可以搜尋任何文字字串，以傳回名稱或說明中包含文字的表單。

配置全文謂詞元件：

1. 點選元件，然後點選![settings_icon](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 在&#x200B;**主標題**&#x200B;欄位中指定標題。
1. 點選&#x200B;**確定**

#### 屬性謂詞{#properties-predicate}

「屬性述詞」元件會實作根據表單屬性（例如標題、作者和說明）來搜尋表單。

要配置屬性謂詞元件：

1. 點選元件，然後點選![settings_icon](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 在「常規」頁簽中，指定搜索標籤。 預設值為&#x200B;**Properties**

1. 在「選項」標籤中，點選「**新增項目」。**
1. 從下拉式清單中選取屬性，並在下拉式清單下方的欄位中指定其搜尋標籤。
1. 重複步驟4以新增更多屬性。 您也可以指定預設篩選值，以根據指定的條件列出表單，並隱藏屬性以供一般使用者搜尋。 選取屬性的「隱藏」核取方塊並指定預設篩選值。
例如，如果要顯示標題中包含&quot;Travel&quot;的表單，請選擇Title屬性旁的隱藏。 此外，指定預設篩選值文本框中的差旅。

1. 點選&#x200B;**確定**

#### 標記述詞 {#tags-predicate}

「標籤述詞」元件會實作根據Forms Manager中定義的標籤來搜尋表單。

若要設定「標籤述詞」元件：

1. 點選元件，然後點選![settings_icon](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 點選「標籤」欄位旁的向下箭頭按鈕。
1. 選擇適當的標籤
1. 點選&#x200B;**確定**

所選標籤與選中的複選框一起顯示在「搜索」窗格中。 使用者現在可以根據標籤縮小搜尋範圍。

## 列出頁面{#list-forms-on-a-page-br}上的表單

要在頁面上列出表單，請將&#x200B;**[!UICONTROL Search &amp; Lister]**&#x200B;元件添加到頁面，並配置&#x200B;**[!UICONTROL List Pane]**。 要使最終用戶能夠搜索包含日期、文本和標籤的表單，請添加&#x200B;**[!UICONTROL 搜索窗格]**&#x200B;元件。

若要從頁面上的任何位置連結表單，請使用連結元件。 如需連結元件的詳細資訊，請參閱頁面](../../forms/using/embedding-link-component-page.md)中的內嵌連結元件。[

要列出處於草稿狀態的表單以及已提交的表單，請使用&#x200B;**[!UICONTROL 草稿和提交]**&#x200B;元件。 如需詳細資訊，請參閱[自訂草稿和提交元件](../../forms/using/draft-submission-component.md)。

## 移動設備友好性{#mobile-device-friendliness}

Forms Portal Search &amp; Lister元件適合行動裝置，並據此進行調整。 所有三個預設視圖：網格、卡、面板根據開啟網站的裝置重新發佈，但網頁也隨之調整。 簡單的事實是，Search &amp; Lister僅是元件，不控管頁面層級樣式。

下列影像描述在行動裝置上開啟Search &amp; Lister元件時：

![Search和Lister元件的螢幕截圖](assets/search_lister.png)

Search&amp;Lister元件

## 自訂表單入口網頁{#customizing-a-forms-portal-page-br}

您可以自訂表單入口網頁，為頁面提供不同的外觀。 您也可以新增中繼資料以改善搜尋體驗、變更頁面版面，以及新增自訂CSS樣式。 如需詳細資訊，請參閱[自訂Forms入口網站元件的範本](../../forms/using/customizing-templates-forms-portal-components.md)。

AEM Forms UI可讓您將自訂中繼資料新增至表單。 自訂中繼資料對於提供清單和搜尋表單體驗給使用者很實用。 如需自訂中繼資料的詳細資訊，請參閱[自訂Forms入口網站元件的範本](../../forms/using/customizing-templates-forms-portal-components.md)。

表單入口網站可立即提供演算動作。 您可以自訂表單入口網站，以新增更多動作。 有關詳細資訊，請參閱[添加對表單清單項的自定義操作。](../../forms/using/add-custom-action-form-lister.md)

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
