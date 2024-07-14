---
title: 草稿和提交元件
description: 草稿和提交元件會列出處於草稿狀態且已提交的表單。 您可以自訂元件的外觀和樣式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 草稿和提交元件{#drafts-and-submissions-component}

草稿和提交元件會列出處於草稿狀態的所有表單以及已提交的表單。 元件有用於草稿和已提交表單的單獨區段（標籤）。 使用者只能檢視其草稿和已提交的表單。

## 設定元件 {#configuring-the-component}

草稿和提交元件有兩個標籤：草稿和提交。

若要啟用最適化表單的提交功能以顯示於提交索引標籤，請將&#x200B;**提交動作**&#x200B;設定為&#x200B;**[Forms入口網站提交動作](../../forms/using/configuring-submit-actions.md)。 或者，**&#x200B;啟用Forms入口網站提交選項。 每當使用者提交表單時，該表單就會新增到提交索引標籤。

草稿功能是現成啟用的。 當使用者按一下最適化表單上的&#x200B;**儲存**&#x200B;時，該表單會新增到草稿索引標籤。

執行以下步驟來新增及設定草稿和提交元件：

1. 將元件瀏覽器中Document Services類別下的&#x200B;**草稿和提交**&#x200B;元件拖放到您的頁面上。
1. 選取元件，然後選取![settings_icon](assets/settings_icon.png)以開啟元件的[編輯]對話方塊。

   ![草稿與提交元件](assets/drafts-submissions-edit.png)

1. 在[編輯]對話方塊中，指定下列詳細資料，並選取&#x200B;**完成**&#x200B;以儲存設定。

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
   <td>指定要顯示的最大結果數量。 如果結果計數增加「結果總計」限制，元件底部會顯示<strong>更多</strong>連結。 按一下<strong>更多</strong>顯示所有表格。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>樣式型別</td>
   <td>指定元件的樣式。 您可以指定<strong>無樣式</strong>、<strong>預設樣式</strong>或<strong>自訂樣式</strong>來列出表單。 對於自訂樣式選項，您可以在<strong>自訂樣式路徑</strong>欄位<strong>.</strong>中指定自訂CSS檔案的路徑</td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您在<strong>樣式型別</strong>欄位中選擇<strong>自訂樣式</strong>選項，請使用<strong>自訂樣式路徑</strong>欄位來指定自訂CSS檔案的路徑。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>顯示選項</td>
   <td><p>指定要顯示的標籤。 您可以選擇顯示草稿表單、已提交表單或兩者。 </p> <p><strong>備註</strong>：<em>若為<strong>顯示選項</strong>，若您選取<strong>Both</strong>以外的選項，則不會使用<strong>預設標籤</strong>欄位選項。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>預設標籤</td>
   <td>指定載入表單入口網站頁面時顯示的標籤。 您可以選擇<strong>草稿Forms標籤</strong>和<strong>已提交的Forms標籤</strong>。</td>
  </tr>
  <tr>
   <td>草稿Forms索引標籤設定</td>
   <td>自訂標題</td>
   <td>指定<strong>草稿Forms</strong>索引標籤的標題。 預設值為<strong>草稿Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面配置範本</td>
   <td>指定用於草稿Forms清單的版面。</td>
  </tr>
  <tr>
   <td>已提交Forms索引標籤設定</td>
   <td>自訂標題 </td>
   <td>指定<strong>已提交的Forms </strong>索引標籤的標題。 預設值為<strong>已提交的Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面配置範本</td>
   <td>指定用於已提交Forms<strong> </strong>清單的配置。 </td>
  </tr>
 </tbody>
</table>

## 自訂儲存 {#customizing-the-storage}

當您使用Forms Portal提交動作或啟用最適化表單中的將資料儲存在Forms Portal選項時，表單資料會儲存在AEM存放庫中。 在生產環境中，建議不要將草稿或提交的表單資料儲存在AEM存放庫中。 相反地，您必須將草稿和提交元件與安全的儲存裝置（例如企業資料庫）整合，以儲存草稿和提交的表單資料。

Forms入口網站可讓您將資料儲存在本機AEM存放庫、遠端AEM存放庫或資料庫。 AEM Forms可讓您自訂儲存草稿及提交之使用者資料的實作。 您可以覆寫預設方法，以指定草稿和提交資料如何儲存在您選擇的儲存體中。 例如，您可以將資料儲存在組織目前實作的資料存放區中。

Forms入口網站提供立即可用的服務(API)，將資料儲存在本機與遠端AEM Forms發佈執行個體的crx存放庫上。 您可以用自訂實作來取代預設功能，如[為草稿和提交設定儲存服務](/help/forms/using/configuring-draft-submission-storage.md)文章中所述。 如需自訂實作中所需方法在安全位置儲存內容的詳細資訊，請參閱[自訂草稿和提交資料服務](/help/forms/using/custom-draft-submission-data-services.md)以及[草稿和提交元件的自訂儲存](/help/forms/using/adding-custom-storage-provider-forms.md)。

AEM Forms檔案提供將草稿與提交元件與資料庫](integrate-draft-submission-database.md)整合的[範例。 您可以使用範例實作來開發自己的自訂實作。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂Forms Portal元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
