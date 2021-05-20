---
title: 草稿和提交元件
seo-title: 草稿和提交元件
description: 草稿和提交元件列出處於草稿狀態且已提交的表單。 您可以自訂元件的外觀和樣式。
seo-description: 草稿和提交元件列出處於草稿狀態且已提交的表單。 您可以自訂元件的外觀和樣式。
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# 草稿和提交元件{#drafts-and-submissions-component}

「草稿與提交」元件會列出處於草稿狀態的所有表單以及已提交的表單。 元件有個別的草稿和已提交表單區段（索引標籤）。 使用者只能檢視其草稿和已提交的表單。

## 配置元件{#configuring-the-component}

「草稿與提交」元件有兩個標籤：草稿和提交。

若要讓提交最適化表單顯示在提交索引標籤中，請將&#x200B;**Submit action**&#x200B;設為&#x200B;**[Forms Portal Submit Action](../../forms/using/configuring-submit-actions.md)。 或者，**&#x200B;啟用Forms Portal提交選項。 每當使用者提交表單時，表單就會新增至提交索引標籤。

草稿功能會立即啟用。 當使用者按一下最適化表單上的&#x200B;**儲存**&#x200B;時，表單會新增至草稿索引標籤。

執行下列步驟來新增和設定「草稿與提交」元件：

1. 將&#x200B;**草稿與提交**&#x200B;元件拖放至頁面上「檔案服務」類別下的元件瀏覽器。
1. 點選元件，然後點選![settings_icon](assets/settings_icon.png)以開啟元件的「編輯」對話方塊。

   ![草稿和提交元件](assets/drafts-submissions-edit.png)

1. 在「編輯」對話方塊中，指定下列詳細資訊，然後點選&#x200B;**Done**&#x200B;以儲存設定。

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
   <td>指定要顯示的結果數目上限。 如果結果計數增加「總結果」限制，則元件底部會出現<strong>更多</strong>連結。 按一下「<strong>更多</strong>」會顯示所有表單。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式類型</td>
   <td>指定元件的樣式。 您可以指定<strong>無樣式</strong>、<strong>預設樣式</strong>或<strong>自訂樣式</strong>來列出表單。 對於「自定義樣式」選項，您可以在<strong>「自定義樣式路徑</strong>欄位<strong>.</strong>中指定自定義CSS檔案的路徑</td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您在<strong>樣式類型</strong>欄位中選擇<strong>自訂樣式</strong>選項，請使用<strong>自訂樣式路徑</strong>欄位來指定自訂CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的頁簽。 您可以選擇顯示草稿表單、已提交表單或兩者。 </p> <p><strong>注意</strong>:<em> 若為 <strong>「顯示」選項</strong>，如果您選取「兩者」以外的 <strong>選項</strong>，則不會使 <strong>用「預設」</strong> 表格欄位選項。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設標籤</td>
   <td>指定在表單入口網站頁面載入時要顯示的索引標籤。 您可以在<strong>草稿Forms標籤</strong>和<strong>已提交Forms標籤</strong>之間進行選擇。</td>
  </tr>
  <tr>
   <td>草稿Forms標籤設定</td>
   <td>自訂標題</td>
   <td>指定<strong>草稿Forms</strong>標籤的標題。 預設值為<strong>草稿Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於草稿Forms清單的佈局。</td>
  </tr>
  <tr>
   <td>已提交Forms標籤設定</td>
   <td>自訂標題 </td>
   <td>指定<strong>已提交Forms </strong>標籤的標題。 預設值為<strong>Submitted Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於已提交Forms<strong> </strong>清單的版面。 </td>
  </tr>
 </tbody>
</table>

## 自定義儲存{#customizing-the-storage}

當您使用Forms Portal提交動作或啟用適用性表單中的「在表單入口網站中儲存資料」選項時，表單資料會儲存在AEM存放庫。 在生產環境中，建議不要將草稿或已提交的表單資料儲存在AEM存放庫中。 相反地，您必須將草稿和提交元件與安全的儲存體（如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms入口網站可讓您將資料儲存在本機AEM存放庫、遠端AEM存放庫或資料庫。 AEM Forms可讓您自訂為草稿和提交儲存使用者資料的實作。 您可以覆寫預設方法，以指定草稿和提交資料儲存在您選擇的儲存空間的方式。 例如，您可以將資料儲存在貴組織目前實作的資料存放區中。

Forms入口網站提供立即可用的服務(API)，可將資料儲存在本機和遠端AEM Forms發佈執行個體的crx存放庫上。 您可以將[為草稿和提交設定儲存服務](/help/forms/using/configuring-draft-submission-storage.md)文章中所述的預設實作取代為自訂實作，以取代預設功能。 有關在安全位置儲存內容的自定義實施所需方法的詳細資訊，請參閱[自定義草稿和提交資料服務](/help/forms/using/custom-draft-submission-data-services.md)和[草稿和提交元件的自定義儲存。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms檔案提供[範例，用於整合草稿和提交元件與資料庫](integrate-draft-submission-database.md)。 您可以使用範例實作，開發您自己的自訂實作。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
