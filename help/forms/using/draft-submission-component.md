---
title: 草稿和提交元件
seo-title: Drafts and submissions component
description: 草稿和提交元件列出處於草稿狀態且已提交的表單。 您可以自訂元件的外觀和樣式。
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

# 草稿和提交元件{#drafts-and-submissions-component}

「草稿與提交」元件會列出處於草稿狀態的所有表單以及已提交的表單。 元件有個別的草稿和已提交表單區段（索引標籤）。 使用者只能檢視其草稿和已提交的表單。

## 設定元件 {#configuring-the-component}

「草稿與提交」元件有兩個標籤：草稿和提交。

若要啟用提交最適化表單以顯示在提交索引標籤中，請設定 **提交動作** to **[Forms Portal提交動作](../../forms/using/configuring-submit-actions.md). 或者，** 啟用Forms Portal提交選項。 每當使用者提交表單時，表單就會新增至提交索引標籤。

草稿功能會立即啟用。 使用者點按 **儲存** 在最適化表單中，表單會新增至「草稿」索引標籤。

執行下列步驟來新增和設定「草稿與提交」元件：

1. 拖放 **草稿和提交** 元件（在頁面的元件瀏覽器中）。
1. 點選元件，然後點選 ![settings_icon](assets/settings_icon.png) 開啟元件的「編輯」(Edit)對話框。

   ![草稿和提交元件](assets/drafts-submissions-edit.png)

1. 在「編輯」對話方塊中，指定下列詳細資訊並點選 **完成** 以儲存設定。

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
   <td>指定要顯示的結果數目上限。 如果結果計數增加「總結果」限制，則 <strong>更多 </strong>連結會顯示在元件底部。 按一下 <strong>更多 </strong>顯示所有表單。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式類型</td>
   <td>指定元件的樣式。 您可以指定 <strong>無樣式</strong>, <strong>預設樣式</strong>，或 <strong>自訂樣式</strong> 列出表格。 對於「自訂樣式」選項，您可以在 <strong>自訂樣式路徑 </strong>欄位<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您選擇 <strong>自訂樣式</strong> 選項 <strong>樣式類型</strong> 欄位，使用 <strong>自訂樣式路徑</strong> 欄位來指定自訂CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的頁簽。 您可以選擇顯示草稿表單、已提交表單或兩者。 </p> <p><strong>附註</strong>:<em> 針對 <strong>顯示選項</strong>，若您選取 <strong>兩者</strong>, <strong>預設標籤</strong> 欄位選項未使用。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設標籤</td>
   <td>指定在表單入口網站頁面載入時要顯示的索引標籤。 您可以選擇 <strong>草稿Forms標籤</strong> 和 <strong>已提交Forms標籤</strong>.</td>
  </tr>
  <tr>
   <td>草稿Forms標籤設定</td>
   <td>自訂標題</td>
   <td>指定 <strong>草稿Forms</strong> 標籤。 預設值為 <strong>Forms草稿。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於草稿Forms清單的佈局。</td>
  </tr>
  <tr>
   <td>已提交Forms標籤設定</td>
   <td>自訂標題 </td>
   <td>指定 <strong>已提交Forms </strong>標籤。 預設值為 <strong>已提交Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定要用於已提交Forms的版面<strong> </strong>清單。 </td>
  </tr>
 </tbody>
</table>

## 自訂儲存 {#customizing-the-storage}

當您使用Forms Portal提交動作或啟用適用性表單中的「在表單入口網站中儲存資料」選項時，表單資料會儲存在AEM存放庫。 在生產環境中，建議不要將草稿或已提交的表單資料儲存在AEM存放庫中。 相反地，您必須將草稿和提交元件與安全的儲存體（如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms入口網站可讓您將資料儲存在本機AEM存放庫、遠端AEM存放庫或資料庫。 AEM Forms可讓您自訂為草稿和提交儲存使用者資料的實作。 您可以覆寫預設方法，以指定草稿和提交資料儲存在您選擇的儲存空間的方式。 例如，您可以將資料儲存在貴組織目前實作的資料存放區中。

Forms入口網站提供立即可用的服務(API)，可將資料儲存在本機和遠端AEM Forms發佈執行個體的crx存放庫上。 您可以取代預設實施，如 [配置草稿和提交的儲存服務](/help/forms/using/configuring-draft-submission-storage.md) 文章，以取代預設功能。 如需自訂實施中儲存安全位置內容所需方法的詳細資訊，請參閱 [自訂草稿和提交資料服務](/help/forms/using/custom-draft-submission-data-services.md) 和 [草稿和提交元件的自訂儲存。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms檔案提供 [將草稿和提交元件與資料庫整合的範例](integrate-draft-submission-database.md). 您可以使用範例實作，開發您自己的自訂實作。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
