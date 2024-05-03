---
title: 草稿和提交元件
description: 草稿和提交元件會列出處於草稿狀態且已提交的表單。 您可以自訂元件的外觀和樣式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 草稿和提交元件{#drafts-and-submissions-component}

草稿和提交元件會列出處於草稿狀態的所有表單以及已提交的表單。 元件有用於草稿和已提交表單的單獨區段（標籤）。 使用者只能檢視其草稿和已提交的表單。

## 設定元件 {#configuring-the-component}

草稿和提交元件有兩個標籤：草稿和提交。

若要啟用最適化表單的提交功能，使其顯示在提交索引標籤中，請設定 **提交動作** 至 **[Forms Portal提交動作](../../forms/using/configuring-submit-actions.md). 或者，** 啟用Forms入口網站提交選項。 每當使用者提交表單時，該表單就會新增到提交索引標籤。

草稿功能是現成啟用的。 當使用者按一下 **儲存** 在最適化表單上，該表單會新增到草稿索引標籤中。

執行以下步驟來新增及設定草稿和提交元件：

1. 拖放 **草稿和提交** 在頁面上元件瀏覽器中的「檔案服務」類別下的元件。
1. 選取元件，然後選取 ![settings_icon](assets/settings_icon.png) 以開啟元件的「編輯」對話方塊。

   ![草稿和提交元件](assets/drafts-submissions-edit.png)

1. 在「編輯」對話方塊中，指定下列詳細資料並選取 **完成** 以儲存設定。

<table>
 <tbody>
  <tr>
   <th>標籤</th>
   <th>設定</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>一般</td>
   <td>總結果</td>
   <td>指定要顯示的最大結果數量。 如果結果計數增加「結果總計」限制，則 <strong>更多 </strong>連結會出現在元件底部。 按一下 <strong>更多 </strong>顯示所有表格。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式型別</td>
   <td>指定元件的樣式。 您可以指定 <strong>無樣式</strong>， <strong>預設樣式</strong>，或 <strong>自訂樣式</strong> 以列出表格。 對於「自訂樣式選項」，您可以在下列位置指定自訂CSS檔案的路徑： <strong>自訂樣式路徑 </strong>欄位<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您選擇 <strong>自訂樣式</strong> 中的選項 <strong>樣式型別</strong> 欄位，使用 <strong>自訂樣式路徑</strong> 欄位以指定自訂CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的標籤。 您可以選擇顯示草稿表單、已提交表單或兩者。 </p> <p><strong>注意</strong>：<em> 的 <strong>顯示選項</strong>，如果您選取 <strong>兩者</strong>，則 <strong>預設標籤</strong> 未使用欄位選項。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設標籤</td>
   <td>指定載入表單入口網站頁面時顯示的標籤。 您可以選擇 <strong>草稿Forms索引標籤</strong> 和 <strong>已提交Forms索引標籤</strong>.</td>
  </tr>
  <tr>
   <td>草稿Forms索引標籤設定</td>
   <td>自訂標題</td>
   <td>指定標題 <strong>草稿Forms</strong> 標籤。 預設值為 <strong>草稿Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面配置範本</td>
   <td>指定用於草稿Forms清單的版面。</td>
  </tr>
  <tr>
   <td>已提交Forms索引標籤設定</td>
   <td>自訂標題 </td>
   <td>指定標題 <strong>已提交Forms </strong>標籤。 預設值為 <strong>已提交Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面配置範本</td>
   <td>指定用於已提交Forms的版面<strong> </strong>清單。 </td>
  </tr>
 </tbody>
</table>

## 自訂儲存 {#customizing-the-storage}

當您使用Forms Portal提交動作或啟用最適化表單中的將資料儲存在Forms Portal選項時，表單資料會儲存在AEM存放庫中。 在生產環境中，建議不要將草稿或提交的表單資料儲存在AEM存放庫中。 相反地，您必須將草稿和提交元件與安全的儲存裝置（例如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms入口網站可讓您將資料儲存在本機AEM存放庫、遠端AEM存放庫或資料庫。 AEM Forms可讓您自訂儲存草稿及提交之使用者資料的實作。 您可以覆寫預設方法，以指定草稿和提交資料如何儲存在您選擇的儲存體中。 例如，您可以將資料儲存在組織目前實作的資料存放區中。

Forms入口網站提供立即可用的服務(API)，將資料儲存在本機與遠端AEM Forms發佈執行個體的crx存放庫上。 您可以取代預設實施，如所述 [為草稿和提交設定儲存服務](/help/forms/using/configuring-draft-submission-storage.md) 文章，使用自訂實施來取代預設功能。 如需自訂實施中所需方法在安全位置儲存內容的詳細資訊，請參閱 [自訂草稿和提交資料服務](/help/forms/using/custom-draft-submission-data-services.md) 和 [草稿和提交元件的自訂儲存空間。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms檔案提供 [將草稿和提交元件與資料庫整合的範例](integrate-draft-submission-database.md). 您可以使用範例實作來開發自己的自訂實作。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂Forms Portal元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
