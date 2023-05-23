---
title: 建立表單門戶頁
seo-title: Creating a forms portal page
description: Forms門戶為Web開發人員提供元件，以在使用Adobe Experience Manager()創作的網站上建立和自定義表AEM單門戶。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 1%

---

# 建立表單門戶頁{#creating-a-forms-portal-page}

Forms門戶元件為Web開發人員提供元件，以在使用Adobe Experience Manager(AEM)創作的網站上建立和自定義表單門戶。 有關表單門戶的快速概述，請參閱 [門戶上發佈表單簡介](../../forms/using/introduction-publishing-forms.md)。

## 必備條件 {#prerequisites}

Forms門戶元件預設不可用。 確保按中所述啟用以下表單門戶元件類別 [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)。

**文檔服務** 包括Search &amp; Lister、Link、Drafts和Submissions元件。

**文檔服務謂語** 包括日期謂詞、全文謂詞、屬性謂詞和標籤謂詞元件。 這些元件用於配置Search &amp; Lister元件中的搜索。

在站點頁面上啟AEM用這些元件類別後，這些元件類別便可在元件瀏覽器中使用。

![AEM Forms門戶元件瀏覽器](assets/component-categories.png)

Forms門戶元件類別

## 搜索和Lister元件 {#search-amp-lister-component}

「文檔服務」元件類別下提供的Search &amp; Lister元件用於列出頁面上的表單，並對列出的表單執行搜索。 該元件包括兩個窗格：

* 列出表單的清單窗格。
* 添加搜索功能的搜索窗格。

可將Search &amp; Lister元件從元件瀏覽器中的Document Services元件類別拖放到頁面上。 添加時，該元件與下列內容類似。

![在頁面中搜索和Lister元件](assets/fp-grid-viw.png)

在具有網格佈局的頁面中搜索和Lister元件

### 清單窗格 {#list-pane}

「清單」窗格是列出表單的區域。 Search &amp; Lister元件提供了各種配置選項，可用於控制「清單」窗格中表單的顯示。

要配置「清單」窗格，請按一下「搜索」和「Lister」元件，然後按一下 ![設定表徵圖](assets/settings_icon.png)。 的 **[!UICONTROL 編輯元件]** 對話框。

![清單窗格處於編輯模式](assets/edit-list.png)

清單窗格處於編輯模式

的 **編輯** 對話框包括幾個頁籤，它們提供了下表中所述的配置選項。 點擊 **確定** 以保存配置。

<table>
 <tbody>
  <tr>
   <th>定位字元</th>
   <th>設定</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>資產檔案夾</strong></code></td>
   <td>新增項目</td>
   <td>配置使用AEM FormsUI上載資產的資料夾。 預設情況下，它會列出所有上載的資產。 有關AEM FormsUI的詳細資訊，請參見 <a href="../../forms/using/introduction-managing-forms.md" target="_blank">管理表單簡介</a>。</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>顯示</strong></code></p> </td>
   <td>標題文字</td>
   <td>Search &amp; Lister元件的標題。 預設標題為 <strong>Forms門戶。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>佈局模板</td>
   <td>資產的佈局。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用高級搜索</td>
   <td>啟用後，隱藏高級搜索表徵圖。</td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用文本搜索</td>
   <td>啟用後，隱藏全文搜索欄。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>結果</strong></code></td>
   <td>每頁結果數</td>
   <td>配置要在頁面上顯示的表單的最大數量。</td>
  </tr>
  <tr>
   <td> </td>
   <td>結果文字</td>
   <td><p>配置結果文本（例如，601的1-12） <strong>結果</strong>)。 預設值為 <strong>結果</strong>。</p> <p>例如，如果 <strong>Forms </strong>在此欄位中，共有601個表單，結果文本更改為601的1-12個 <strong>Forms。</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>頁面文字</td>
   <td><p>配置頁面文本(例如， <strong>頁面 </strong>51人中有1人)。 預設值為 <strong>頁面</strong>。</p> <p>例如，如果 <strong>申請表 </strong>在此欄位中，有51頁，頁面文本將更改為 <strong>申請表 </strong>51人中有1人。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Of 文字</td>
   <td><p>替換單詞 <strong>共</strong> （第1頁） <strong>共 </strong>51)。 預設值為 <strong>共</strong>。</p> <p>例如，如果 <strong>外 </strong>在此欄位中，文本將更改為第1頁 <strong>外 </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>窗體連結</strong></code></td>
   <td>呈現類型</td>
   <td>根據指定的呈現類型控制表單清單。 可用選項包括PDF和HTML。 例如，如果只選擇HTML作為渲染類型，則會過濾掉PDF forms。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML配置檔案</td>
   <td>配置用於呈現的HTML配置檔案。 所有可用配置檔案都列在下拉清單中。</td>
  </tr>
  <tr>
   <td> </td>
   <td>提交URL</td>
   <td><p>配置提交表單資料的servlet。</p> <p><strong>注：</strong> <em>表單的提交URL可以在多個位置指定，其優先順序如下：</em></p>
    <ol>
     <li><em>在表單中嵌入的提交URL（在「提交」按鈕中）具有最高優先順序。</em></li>
     <li><em>在AEM FormsUI中提到的提交URL具有第二高優先順序。</em></li>
     <li><em>表單門戶中提及的提交URL優先順序最低。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML渲染操作工具提示</td>
   <td>配置工具提示的文本，該文本在指針懸停時顯示 <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML5表徵圖)。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF渲染操作工具提示</td>
   <td>配置工具提示的文本，該文本在指針懸停時顯示 <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDF表徵圖)。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>樣式</strong></code></td>
   <td>樣式類型</td>
   <td>允許您指定 <strong>無樣式，預設樣式</strong>或 <strong>自定義樣式 </strong>清單。</td>
  </tr>
  <tr>
   <td> </td>
   <td>自定義樣式路徑</td>
   <td>如果選擇「自定義」作為「樣式類型」，請瀏覽以指定自定義CSS的路徑，否則選擇「預設」。</td>
  </tr>
 </tbody>
</table>

### 搜索窗格 {#search-pane}

使用「搜索」窗格可以在Sidek中添加Document Services謂語類別中的「日期謂語」、「全文謂語」、「屬性謂語」和「標籤謂AEM語」元件。 這些元件實現了用戶對列出的表單執行搜索的搜索功能。

**提示：** *您可以根據預設條件控制表單門戶上顯示的表單清單，並隱藏最終用戶的搜索功能。 要控制表單清單，請使用謂詞元件應用搜索篩選器。 也可以從「編輯元件」(Edit Component)對話框的「顯示」(Display)頁籤中指定預設篩選器值並禁用搜索。*

![包含日期、全文、屬性和標籤謂詞的搜索面板](assets/search-with-predicates.png)

包含日期、全文、屬性和標籤謂詞的搜索面板

#### 日期述詞 {#date-predicate}

添加「日期謂詞」元件時，可以搜索在指定持續時間內修改的列出表單。

要配置「日期謂詞」元件，請執行以下操作：

1. 點擊元件，然後點擊 ![設定表徵圖](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 指定以下內容：

   * **類型：** 唯一可用的選項是 **上次修改日期**

   * **文本：** 日期謂詞元件的標籤或標題。 預設值為 **上次修改日期。**

   * **開始日期標籤：** 開始日期欄位的標籤或標題
   * **結束日期標籤：** 結束日期欄位的標籤或標題
   * **隱藏：** 要強制使用預設日期篩選器來列出表單

1. 點擊 **確定**

#### 全文謂詞 {#full-text-predicate}

全文謂詞元件對表單資料（如名稱和說明）實現全文搜索。 用戶可以搜索任何文本字串以返回包含其名稱或說明中的文本的表單。

要配置全文謂詞元件，請執行以下操作：

1. 點擊元件，然後點擊 ![設定表徵圖](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 在 **主標題** 的子菜單。
1. 點擊 **確定**

#### 屬性謂詞 {#properties-predicate}

「屬性謂詞」元件實現基於表單屬性（如標題、作者和說明）的表單搜索。

要配置「屬性謂詞」元件：

1. 點擊元件，然後點擊 ![設定表徵圖](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 在「常規」頁籤中，指定搜索標籤。 預設值為 **屬性**

1. 在「Options（選項）」頁籤中，按一下 **添加項目。**
1. 從下拉清單中選擇一個屬性，並在下拉清單下的欄位中為其指定搜索標籤。
1. 重複步驟4以添加更多屬性。 您還可以指定預設篩選器值，以便根據指定的條件列出表單，並隱藏該屬性供最終用戶搜索。 選中屬性的「隱藏」複選框並指定預設篩選器值。
例如，如果要顯示其標題中包含「Travel」的表單，請選擇「Title」屬性旁邊的「隱藏」。 此外，在預設篩選器值文本框中指定行程。

1. 點擊 **確定**

#### 標記述詞 {#tags-predicate}

「標籤謂詞」元件實現基於在Forms管理器中定義的標籤搜索表單。

要配置「標籤謂語」元件，請執行以下操作：

1. 點擊元件，然後點擊 ![設定表徵圖](assets/settings_icon.png)。 「編輯」(Edit)對話框開啟。
1. 按一下「Tags（標籤）」欄位旁邊的下箭頭按鈕。
1. 選擇適當的標籤
1. 點擊 **確定**

選定標籤將與選定內容的複選框一起出現在「搜索」窗格中。 用戶現在可以根據標籤縮小搜索範圍。

## 在頁面上列出表單 {#list-forms-on-a-page-br}

要列出頁面上的表單，請添加 **[!UICONTROL 搜索與李斯特]** 頁面元件並配置 **[!UICONTROL 清單窗格]**。 要使最終用戶能夠搜索包含日期、文本和標籤的表單，請添加 **[!UICONTROL 搜索窗格]** 元件。

要從頁面上的任何位置連結表單，請使用「連結」元件。 有關連結元件的詳細資訊，請參見 [在頁面中嵌入連結元件](../../forms/using/embedding-link-component-page.md)。

要列出處於草稿狀態的表單和已提交的表單，請使用 **[!UICONTROL 草稿和提交]** 元件。 有關詳細資訊，請參見 [自定義草稿和提交元件](../../forms/using/draft-submission-component.md)。

## 移動設備友好性 {#mobile-device-friendliness}

FormsPortal Search &amp; Lister元件對移動設備友好，並相應地進行調整。 所有三個預設視圖：網格、卡、面板根據開啟網站的設備進行重新連接，其中提供網頁也適應的事實。 簡單的事實是，Search &amp; Lister僅是一個元件，不控制頁面級別樣式。

在移動設備上開啟時，下面的影像將顯示Search &amp; Lister元件：

![Search和Lister元件的螢幕快照](assets/search_lister.png)

Search &amp; Lister元件

## 自定義表單門戶頁 {#customizing-a-forms-portal-page-br}

您可以自定義表單門戶頁面，以為頁面提供不同的外觀。 您還可以添加元資料以改進搜索體驗、更改頁面佈局和添加自定義CSS樣式。 有關詳細資訊，請參見 [自定義Forms門戶元件模板](../../forms/using/customizing-templates-forms-portal-components.md)。

AEM FormsUI允許您向表單添加自定義元資料。 自定義元資料在向最終用戶提供清單和搜索表單體驗方面非常有用。 有關自定義元資料的詳細資訊，請參見 [自定義Forms門戶元件模板](../../forms/using/customizing-templates-forms-portal-components.md)。

現成的表單門戶提供了呈現操作。 您可以自定義表單門戶以添加更多操作。 有關詳細資訊，請參見 [添加窗體線程表項的自定義操作。](../../forms/using/add-custom-action-form-lister.md)

## 相關文章

* [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單門戶頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自定義草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定義表單門戶元件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
