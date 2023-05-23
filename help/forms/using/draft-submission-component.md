---
title: 草稿和提交部分
seo-title: Drafts and submissions component
description: 草稿和提交元件列出處於草稿狀態並已提交的表單。 可定製元件的外觀和樣式。
seo-description: Drafts and submissions component lists forms that are in the draft state and are already submitted. You can customize appearance and style of the component.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# 草稿和提交部分{#drafts-and-submissions-component}

「草稿和提交」元件列出處於草稿狀態的所有表單以及已提交的表單。 該元件具有用於草稿和已提交表單的單獨部分（頁籤）。 用戶只能查看其草稿和已提交的表單。

## 配置元件 {#configuring-the-component}

「草稿和提交」元件有兩個頁籤：草稿和提交。

要啟用在提交頁籤中顯示的自適應表單提交，請設定 **提交操作** 至 **[Forms門戶提交操作](../../forms/using/configuring-submit-actions.md)。 或者，** 啟用Forms門戶提交選項。 每當用戶提交表單時，表單即添加到提交頁籤。

拔模功能在框外啟用。 當用戶按一下 **保存** 在自適應窗體中，窗體將添加到「草稿」頁籤。

執行以下步驟來添加和配置草稿和提交元件：

1. 拖放 **草稿和提交** 元件。
1. 點擊元件，然後點擊 ![設定表徵圖](assets/settings_icon.png) 開啟元件的「編輯」(Edit)對話框。

   ![草稿和提交元件](assets/drafts-submissions-edit.png)

1. 在「編輯」對話框中，指定以下詳細資訊並點擊 **完成** 按鈕。

<table>
 <tbody>
  <tr>
   <th>定位字元</th>
   <th>設定</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>一般</td>
   <td>總結果</td>
   <td>指定要顯示的最大結果數。 如果結果計數增加「總結果」限制，則 <strong>更多 </strong>連結出現在元件底部。 按一下 <strong>更多 </strong>顯示所有窗體。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式類型</td>
   <td>指定元件的樣式。 可以指定 <strong>無樣式</strong>。 <strong>預設樣式</strong>或 <strong>自定義樣式</strong> 清單。 對於「自定義樣式」選項，可以在 <strong>自定義樣式路徑 </strong>場<strong>。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自定義樣式路徑</td>
   <td>如果您選擇 <strong>自定義樣式</strong> 的上界 <strong>樣式類型</strong> 欄位，使用 <strong>自定義樣式路徑</strong> 欄位，以指定自定義CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的頁籤。 您可以選擇顯示草稿表單、已提交表單或兩者。 </p> <p><strong>注釋</strong>:<em> 對於 <strong>顯示選項</strong>，也請參見Wiki頁 <strong>兩者</strong>，也請參見Wiki頁。 <strong>預設頁籤</strong> 欄位選項。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設頁籤</td>
   <td>指定在載入表單門戶頁面時要顯示的頁籤。 您可以選擇 <strong>草稿Forms頁籤</strong> 和 <strong>已提交Forms頁籤</strong>。</td>
  </tr>
  <tr>
   <td>草稿Forms頁籤配置</td>
   <td>自定義標題</td>
   <td>指定 <strong>草稿Forms</strong> 頁籤。 預設值為 <strong>起草Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>佈局模板</td>
   <td>指定用於草稿Forms清單的佈局。</td>
  </tr>
  <tr>
   <td>已提交Forms頁籤配置</td>
   <td>自定義標題 </td>
   <td>指定 <strong>已提交Forms </strong>頁籤。 預設值為 <strong>已提交Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>佈局模板</td>
   <td>指定用於已提交的Forms的佈局<strong> </strong>清單框。 </td>
  </tr>
 </tbody>
</table>

## 自定義儲存 {#customizing-the-storage}

當您使用Forms門戶提交操作或以自適應形式啟用「在表單門戶中儲存資料」選項時，表單資料將儲存在儲存AEM庫中。 在生產環境中，建議不要將草稿或提交的表單資料儲存在儲存AEM庫中。 相反，您必須將草稿和提交元件與安全儲存（如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms門戶允許您將資料儲存AEM在本地存AEM儲庫、遠程儲存庫或資料庫中。 AEM Forms允許您自定義為草稿和提交儲存用戶資料的實現。 您可以覆蓋預設方法，以指定草稿和提交資料如何儲存在您選擇的儲存中。 例如，您可以將資料儲存在組織中當前實施的資料儲存中。

Forms門戶提供開箱即用服務(API)，將資料儲存在本地和遠程AEM Forms發佈實例的crx儲存庫上。 可以替換預設實現，如中所述 [為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md) 項目，使用自定義實現替換預設功能。 有關自定義實現中在安全位置儲存內容所需方法的詳細資訊，請參見 [自定義草稿和提交資料服務](/help/forms/using/custom-draft-submission-data-services.md) 和 [草稿和提交元件的自定義儲存。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms文檔提供 [將草稿和提交元件與資料庫整合的示例](integrate-draft-submission-database.md)。 您可以使用示例實現來開發您自己的自定義實現。

## 相關文章

* [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單門戶頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自定義草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定義表單門戶元件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
