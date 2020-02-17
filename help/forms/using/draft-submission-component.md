---
title: 草稿和提交元件
seo-title: 草稿和提交元件
description: 草稿和提交元件列出處於草稿狀態並已提交的表單。 可定製元件的外觀和樣式。
seo-description: 草稿和提交元件列出處於草稿狀態並已提交的表單。 可定製元件的外觀和樣式。
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc

---


# 草稿和提交元件{#drafts-and-submissions-component}

「草稿和提交」元件列出處於草稿狀態的所有表單以及已提交的表單。 該元件具有用於草稿和提交表單的單獨部分（頁籤）。 使用者只能檢視其草稿和提交的表單。

## 配置元件 {#configuring-the-component}

「草稿與提交」元件有兩個標籤：草稿和提交。

若要啟用提交最適化表單以顯示在提交標籤中，請將「提交」動 **作設為****[表單入口網站提交動作](../../forms/using/configuring-submit-actions.md)。 或者，**啟用「表單入口網站提交」選項。 每當使用者提交表格時，表格就會新增至提交標籤。

草稿功能會立即啟用。 當使用者按一 **下最適化表單** 「儲存」時，表單會新增至草稿標籤。

執行下列步驟以新增及設定「草稿與提交」元件：

1. 將「草稿與提交」元 **** 件拖放至頁面上元件瀏覽器的「檔案服務」類別下方。
1. 點選元件，然後點選 ![settings_icon](assets/settings_icon.png) ，以開啟元件的「編輯」對話方塊。

   ![草稿與提交元件](assets/drafts-submissions-edit.png)

1. 在「編輯」對話方塊中，指定下列詳細資訊並點選「 **完成** 」以儲存設定。

<table>
 <tbody>
  <tr>
   <th>索引標籤</th>
   <th>設定</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>一般</td>
   <td>總結果</td>
   <td>指定要顯示的結果數上限。 如果結果計數增加了「總結果」限制，則 <strong>元 </strong>件底部會出現「更多」連結。 按一 <strong>下「 </strong>更多」會顯示所有表格。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式類型</td>
   <td>指定元件的樣式。 您可以指 <strong>定「無樣式</strong>」、「 <strong>預設樣式</strong>」或「 <strong>自訂樣式</strong> 」來列出表格。 對於「自訂樣式選項」，您可以在「自訂樣式路徑」欄位中指定自訂CSS <strong>檔案的 </strong>路徑<strong>。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您在「樣 <strong>式類型</strong> 」欄位中選擇「自訂樣式」選項 <strong>，請使用「自訂樣式路徑」欄</strong><strong></strong> 位來指定自訂CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的頁籤。 您可以選擇顯示草稿表單、提交表單或兩者。 </p> <p><strong></strong> 注意<em>:對於 <strong>顯示選項</strong>，如果您選擇「兩者」以外的選項 <strong>，則不</strong>會使用「預設標籤 <strong></strong> 」欄位選項。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設標籤</td>
   <td>指定在表單入口網頁載入時要顯示的標籤。 您可以選擇「草稿表 <strong>單」標籤</strong> , <strong>或「已提交表單」標籤</strong>。</td>
  </tr>
  <tr>
   <td>草稿表單標籤設定</td>
   <td>自訂標題</td>
   <td>指定「草稿表單」 <strong>標籤的標題</strong> 。 預設值為「草 <strong>稿表單」。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於「草稿表單」清單的佈局。</td>
  </tr>
  <tr>
   <td>已提交表單標籤配置</td>
   <td>自訂標題 </td>
   <td>指定「已提交表 <strong>單」標籤的 </strong>標題。 預設值為「已提 <strong>交表單」。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於「已提交表單」清單的<strong></strong>佈局。 </td>
  </tr>
 </tbody>
</table>

## 自定義儲存 {#customizing-the-storage}

當您使用Forms Portal提交動作或啟用以最適化表單形式在表單入口網站中儲存資料選項時，表單資料會儲存在AEM儲存庫中。 在生產環境中，建議您不要將草稿或提交的表單資料儲存在AEM儲存庫中。 您必須將草稿和提交元件與安全儲存（例如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms Portal可讓您將資料儲存在本機AEM存放庫、遠端AEM存放庫或資料庫。 AEM Forms可讓您自訂儲存草稿和提交之使用者資料的實作。 您可以覆寫預設方法，以指定草稿和提交資料儲存在您選擇儲存空間的方式。 例如，您可以將資料儲存在您組織中目前實作的資料儲存區。

Forms入口網站提供立即可用的服務(API)，可將資料儲存在本機和遠端AEM Forms發佈例項的crx儲存庫上。 您可以將預設實作(如為草稿和提交 [配置儲存服務文章中所述)替換為自訂實作](/help/forms/using/configuring-draft-submission-storage.md) ，以取代預設功能。 如需自訂實作在安全位置儲存內容所需方法的詳細資訊，請參閱自訂草稿和提交資料服務 [](/help/forms/using/custom-draft-submission-data-services.md)[和草稿和提交元件的自訂儲存。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms檔案提供將草稿和 [提交元件與資料庫整合的範例](integrate-draft-submission-database.md)。 您可以使用範例實作來開發您自己的自訂實作。

## 相關文章

* [啟用表單入口元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表格](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表格簡介](/help/forms/using/introduction-publishing-forms.md)
