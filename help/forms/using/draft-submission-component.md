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
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# 草稿和提交元件{#drafts-and-submissions-component}

「草稿和提交」元件列出處於草稿狀態的所有表單以及已提交的表單。 該元件具有用於草稿和提交表單的單獨部分（頁籤）。 使用者只能檢視其草稿和提交的表單。

## 配置元件{#configuring-the-component}

「草稿與提交」元件有兩個標籤：草稿和提交。

若要啟用提交最適化表單以顯示在提交標籤中，請將&#x200B;**提交動作**&#x200B;設為&#x200B;**[表單入口網站提交動作](../../forms/using/configuring-submit-actions.md)。 或者，**&#x200B;啟用「表單入口網站提交」選項。 每當使用者提交表格時，表格就會新增至提交標籤。

草稿功能會立即啟用。 當使用者按一下最適化表單上的&#x200B;**Save**&#x200B;時，表單會新增至草稿標籤。

執行下列步驟以新增及設定「草稿與提交」元件：

1. 將元件瀏覽器中「文檔服務」類別下的&#x200B;**草稿和提交**&#x200B;元件拖放到頁面上。
1. 點選元件，然後點選![settings_icon](assets/settings_icon.png)以開啟元件的「編輯」對話方塊。

   ![草稿與提交元件](assets/drafts-submissions-edit.png)

1. 在「編輯」對話方塊中，指定下列詳細資訊並點選「完成」以儲存設定。****

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
   <td>指定要顯示的結果數上限。 如果結果計數增加「總結果」限制，則元件底部會顯示<strong>更多</strong>連結。 按一下<strong>更多</strong>顯示所有表單。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式類型</td>
   <td>指定元件的樣式。 您可以指定「無樣式」(<strong>)、「預設樣式」(<strong>)或「自訂樣式」(<strong>)，以列出表單。 </strong></strong></strong>對於「自訂樣式選項」，您可以在<strong>「自訂樣式路徑</strong>」欄位<strong>中指定自訂CSS檔案的路徑。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您在<strong>樣式類型</strong>欄位中選擇<strong>自訂樣式</strong>選項，請使用<strong>自訂樣式路徑</strong>欄位來指定自訂CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的頁籤。 您可以選擇顯示草稿表單、提交表單或兩者。 </p> <p><strong>注意</strong>：對<em> 於「顯示」選項 <strong>，如果您選擇「兩者」以外的選項</strong>，則不使用「缺 <strong>省值</strong>：不使用」( <strong></strong> Both:Default)表欄位選項。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設標籤</td>
   <td>指定在表單入口網頁載入時要顯示的標籤。 您可以選擇<strong>草稿表單標籤</strong>和<strong>已提交表單標籤</strong>。</td>
  </tr>
  <tr>
   <td>草稿表單標籤設定</td>
   <td>自訂標題</td>
   <td>指定<strong>草稿表單</strong>標籤的標題。 預設值為<strong>草稿表單。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於「草稿表單」清單的佈局。</td>
  </tr>
  <tr>
   <td>已提交表單標籤配置</td>
   <td>自訂標題 </td>
   <td>指定<strong>已提交表單</strong>標籤的標題。 預設值為<strong>已提交表單。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面範本</td>
   <td>指定用於「已提交表單」清單的佈局。</strong><strong> </strong></td>
  </tr>
 </tbody>
</table>

## 自定義儲存{#customizing-the-storage}

當您使用Forms Portal提交動作或啟用以最適化表單形式在表單入口網站中儲存資料選項時，表單資料會儲存在AEM儲存庫中。 在生產環境中，建議您不要將草稿或提交的表單資料儲存在AEM儲存庫中。 您必須將草稿和提交元件與安全儲存（例如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms Portal可讓您將資料儲存在本機AEM存放庫、遠端AEM存放庫或資料庫。 AEM Forms可讓您自訂儲存草稿和提交之使用者資料的實作。 您可以覆寫預設方法，以指定草稿和提交資料儲存在您選擇儲存空間的方式。 例如，您可以將資料儲存在您組織中目前實作的資料儲存區。

Forms入口網站提供立即可用的服務(API)，可將資料儲存在本機和遠端AEM Forms發佈例項的crx儲存庫上。 您可以將[為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)文章中所述的預設實施替換為定制實施以替換預設功能。 如需將內容儲存在安全位置的自訂實作所需方法的詳細資訊，請參閱[自訂草稿與提交資料服務](/help/forms/using/custom-draft-submission-data-services.md)和[草稿與提交元件的自訂儲存。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms檔案提供[範例，以整合草稿和提交元件與資料庫](integrate-draft-submission-database.md)。 您可以使用範例實作來開發您自己的自訂實作。

## 相關文章

* [啟用表單入口元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網頁](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表格簡介](/help/forms/using/introduction-publishing-forms.md)
