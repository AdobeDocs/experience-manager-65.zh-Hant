---
title: Forms入口網站 | 處理使用者資料
description: 瞭解如何管理AEM Forms Portal上的使用者資料，例如存取、刪除和資料存放區。
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Forms入口網站 | 處理使用者資料 {#forms-portal-handling-user-data}

[!DNL AEM Forms] Portal提供的元件可用於列出最適化表單、HTML5表單以及上的其他Forms資產 [!DNL AEM Sites] 頁面。 此外，您可以將其設定為顯示草稿並向登入使用者提交最適化表單和HTML5表單。 如需Forms入口網站的詳細資訊，請參閱 [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md).

當登入的使用者將最適化表單儲存為草稿或提交時，他們會顯示在Forms入口網站上的草稿和提交索引標籤中。 草擬或提交表單的資料會儲存在為AEM部署設定的資料存放區中。 匿名使用者的草稿和提交內容不會顯示在Forms入口網站頁面上，但資料會儲存在已設定的資料存放區中。 另請參閱 [為草稿和提交設定儲存服務](/help/forms/using/configuring-draft-submission-storage.md).

## 使用者資料和資料存放區 {#user-data-and-data-stores}

Forms入口網站會在下列情況下儲存草稿與已提交表單的資料：

* 在最適化表單中設定的提交動作為 **Forms Portal提交動作**.
* 用於提交動作，而不是 **Forms Portal提交動作**，則 **[!UICONTROL 在Forms入口網站中儲存資料]** 選項已啟用於 **[!UICONTROL 提交]** 最適化表單容器的屬性。

對於登入和匿名使用者的每個草稿和提交表單，Forms入口網站都會儲存下列資料：

* 表單中繼資料，例如，表單名稱、表單路徑、草稿或提交ID、附件路徑和使用者資料ID
* 表單附件為資料位元組
* 以資料位元組形式呈現表單資料

根據設定的資料存放區持續性，草稿和提交的表單資料會儲存在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持續性型別</strong></p> </td>
   <td><p><strong>資料存放區</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>製作和發佈執行個體的AEM存放庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>作者和遠端AEM例項的AEM存放庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>資料庫</p> </td>
   <td><p>製作執行個體和資料庫表格的AEM儲存庫</p> </td>
   <td>資料庫表格 <code>data</code>， <code>metadata</code>、和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以在設定的資料存放區中存取已登入和匿名使用者的草稿和已提交表單資料，並在必要時將其刪除。

### AEM執行個體 {#aem-instances}

AEM例項（作者、發佈或遠端）中針對已登入及匿名使用者的所有草稿及已提交表單資料都會儲存在 `/content/forms/fp/` AEM存放庫的節點。 每次登入或匿名使用者儲存草稿或提交表單時， `draft ID` 或 `submission ID`， a `user data ID`和隨機 `ID` 會針對每個附件產生（如果適用）。 它與個別草稿或提交內容相關聯。

#### 存取使用者資料 {#access-user-data}

當登入的使用者儲存草稿或提交表單時，會使用其使用者ID建立子節點。 例如，使用者ID為「 」的Sarah Rose的草稿和提交資料 `srose` 儲存在 `/content/forms/fp/srose/` AEM存放庫中的節點。 在使用者ID節點中，資料會以階層結構組織。

下表說明所有草稿的資料如何依據於 `srose` 儲存在AEM存放庫中。

>[!NOTE]
>
>完全相同的結構，例如 `drafts` 針對提交的表單進行復寫 `srose` 在 `/content/forms/fp/srose/submit/` 節點。
>
>所有草稿及提交者為 `anonymous` 使用者會儲存在 `/content/forms/fp/anonymous/` 節點，這會在「 」下為所有匿名使用者組織草稿和提交 `draft` 和 `submit` 節點。

| 節點 | 說明 |
|---|---|
| `/content/forms/fp/srose/drafts` | 使用者所有草稿的容器節點資料 |
| `/content/forms/fp/srose/drafts/attachments/` | 根據草稿識別碼組織使用者的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含選取之識別碼的附件，採用二進位格式 |
| `/content/forms/fp/srose/drafts/metadata/` | 根據草稿ID組織使用者的表單中繼資料 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含所選草稿ID的表單中繼資料 |
| `/content/forms/fp/srose/drafts/data/` | 根據使用者資料ID組織使用者的表單資料 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所選使用者資料ID的表單資料（二進位格式） |

#### 刪除使用者資料 {#delete-user-data}

若要從AEM系統的已登入使用者之草稿和提交中完全刪除使用者資料，您必須刪除 `user ID` 作者節點中特定使用者的節點。 從所有適用的AEM執行個體手動刪除資料。

所有匿名使用者的草稿和提交資料都會儲存在通用中， `drafts` 和 `submit` 節點在 `/content/forms/fp/anonymous`. 除非某些可識別的資訊是已知的，否則沒有方法可以尋找特定匿名使用者的資料。 在這種情況下，您可以搜尋可識別AEM存放庫中匿名使用者的資訊，並從所有適用的AEM執行個體中手動刪除包含該資訊的節點，以從AEM系統中移除資料。 不過，若要刪除所有匿名使用者的資料，您可以刪除 `anonymous` 節點，移除所有匿名使用者的草稿和提交資料。

### 資料庫 {#database}

當AEM設定為將資料儲存在資料庫時，Forms Portal草稿和提交資料會儲存在下列資料庫表格中，以供登入和匿名使用者使用：

* 資料
* 中繼資料
* 其他中繼資料

#### 存取使用者資料 {#access-user-data-1}

若要存取資料庫表格中登入和匿名使用者的草稿和提交資料，請執行以下資料庫命令。 在查詢中，取代 `logged-in user` ，並使用您要存取其資料的使用者ID或 `anonymous` 匿名使用者的許可權。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 刪除使用者資料 {#delete-user-data-1}

若要從資料庫表格中刪除登入使用者的草稿與提交資料，請執行以下資料庫命令。 在查詢中，取代 `logged-in user` ，並使用您要刪除其資料的使用者ID或 `anonymous` 匿名使用者的許可權。 若要從資料庫中刪除特定匿名使用者的資料，您必須使用某些可識別資訊找到該資料，並從包含該資訊的資料庫表格中刪除該資料。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
