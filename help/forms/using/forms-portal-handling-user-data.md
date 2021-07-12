---
title: Forms入口網站 |處理用戶資料
seo-title: Forms入口網站 |處理用戶資料
description: Forms入口網站 |處理用戶資料
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# Forms入口網站 |處理用戶資料 {#forms-portal-handling-user-data}

[!DNL AEM Forms] portal提供可在頁面上列出最適化表單、HTML5表單和其他Forms資產的元 [!DNL AEM Sites] 件。此外，您也可以設定它，以顯示登入使用者的草稿和已提交的最適化表單及HTML5表單。 如需表單入口網站的詳細資訊，請參閱[在入口網站上發佈表單的簡介](/help/forms/using/introduction-publishing-forms.md)。

登入的使用者將最適化表單儲存為草稿或提交時，表單會顯示在表單入口網站的「草稿」和「提交」索引標籤中。 草稿或已提交表單的資料會儲存在為AEM部署設定的資料存放區中。 匿名用戶的草稿和提交不會顯示在表單門戶頁面上；但是，資料儲存在配置的資料儲存中。 有關詳細資訊，請參閱[為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)。

## 使用者資料和資料儲存 {#user-data-and-data-stores}

Forms入口網站會在下列情況下儲存草稿和已提交表單的資料：

* 在最適化表單中設定的提交動作為&#x200B;**Forms Portal Submit Action**。
* 對於「**Forms Portal提交操作**」以外的提交操作，在最適化表單容器的&#x200B;**[!UICONTROL 提交]**&#x200B;屬性中啟用「**[!UICONTROL 在表單入口]**&#x200B;中儲存資料」選項。

針對登入和匿名使用者的每份草稿和提交表單，表單入口網站會儲存下列資料：

* 表單中繼資料，例如表單名稱、表單路徑、草稿或提交ID、附件路徑和使用者資料ID
* 表單附件作為資料位元組
* 表單資料作為資料位元組

根據已設定的資料存放區持續性，草稿和提交的表單資料會儲存在下列位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>AEM製作和發佈例項的存放庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>AEM author和遠端AEM例項存放庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>資料庫</p> </td>
   <td><p>AEM author例項和資料庫表存放庫</p> </td>
   <td>資料庫表<code>data</code>、<code>metadata</code>和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以在設定的資料存放區中存取登入和匿名使用者的草稿和已提交表單資料，並視需要刪除它。

### AEM例項 {#aem-instances}

登入與匿名使用者的AEM例項（製作、發佈或遠端）中，所有草稿與提交的表單資料都會儲存在適用AEM存放庫的`/content/forms/fp/`節點中。 每次登入或匿名的使用者儲存草稿或提交表單時，都會產生每個附件的`draft ID`或`submission ID`、`user data ID`和隨機`ID`（若適用），且會與個別草稿或提交相關聯。

#### 存取使用者資料 {#access-user-data}

登入的使用者儲存草稿或提交表單時，會以其使用者ID建立子節點。 例如，使用者ID為`srose`的Sarah Rose的草稿和提交資料會儲存在AEM存放庫的`/content/forms/fp/srose/`節點中。 在使用者ID節點內，資料以階層結構組織。

下表說明`srose`所有草稿的資料如何儲存在AEM存放庫中。

>[!NOTE]
>
>在`/content/forms/fp/srose/submit/`節點下，針對`srose`提交的表單複製了`drafts`之類的確切結構。
>
>`anonymous`使用者提交的所有草稿和提交都儲存在`/content/forms/fp/anonymous/`節點下，該節點會為`draft`和`submit`節點下的所有匿名使用者組織草稿和提交。

| 節點 | 說明 |
|---|---|
| `/content/forms/fp/srose/drafts` | 使用者所有草稿的容器節點資料 |
| `/content/forms/fp/srose/drafts/attachments/` | 根據草稿ID組織使用者的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含二進位格式的所選ID附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根據草稿ID組織使用者的表單中繼資料 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含所選草稿ID的表單中繼資料 |
| `/content/forms/fp/srose/drafts/data/` | 根據使用者資料ID組織使用者的表單資料 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所選用戶資料ID的表單資料，採用二進位格式 |

#### 刪除使用者資料 {#delete-user-data}

若要從AEM系統的登入使用者草稿和提交中完全刪除使用者資料，您必須從製作節點中刪除特定使用者的`user ID`節點。 您必須從所有適用的AEM例項手動刪除資料。

所有匿名使用者的草稿和提交資料都儲存在`/content/forms/fp/anonymous`下的公用`drafts`和`submit`節點中。 除非已知某些可識別資訊，否則無法尋找特定匿名使用者的資料。 在此情況下，您可以在AEM存放庫中搜尋可識別匿名使用者的資訊，並從所有適用的AEM例項手動刪除包含該使用者的節點，以從AEM系統中移除資料。 但是，要刪除所有匿名用戶的資料，可以刪除`anonymous`節點，以刪除所有匿名用戶的草稿和提交資料。

### 資料庫 {#database}

將AEM設定為將資料儲存在資料庫中時，表單入口網站草稿和提交資料會儲存在以下資料庫表格中，供登入和匿名使用者使用：

* 資料
* 中繼資料
* 其他中繼資料

#### 存取使用者資料 {#access-user-data-1}

要訪問資料庫表中登錄用戶和匿名用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，將`logged-in user`替換為要訪問其資料的用戶ID，或將`anonymous`替換為匿名用戶。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 刪除使用者資料 {#delete-user-data-1}

要從資料庫表中刪除登錄用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，將`logged-in user`替換為要刪除其資料的用戶ID，或將`anonymous`替換為匿名用戶。 請注意，要從資料庫中刪除特定匿名用戶的資料，需要使用一些可識別資訊找到該資料，並從包含該資訊的資料庫表中刪除該資料。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
