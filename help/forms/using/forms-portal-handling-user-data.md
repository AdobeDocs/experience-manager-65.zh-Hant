---
title: Forms門戶 |處理用戶資料
seo-title: Forms Portal | Handling user data
description: Forms門戶 |處理用戶資料
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Forms門戶 |處理用戶資料 {#forms-portal-handling-user-data}

[!DNL AEM Forms] 門戶提供了可用於列出自適應表單、HTML5表單和Forms其他資產的元件 [!DNL AEM Sites] 的子菜單。 此外，您還可以配置它，以顯示已登錄用戶的草稿和已提交的自適應表單以及HTML5表單。 有關表單門戶的詳細資訊，請參見 [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)。

當登錄用戶將自適應表單保存為草稿或提交時，它們會顯示在表單門戶的「草稿」和「提交」頁籤中。 草稿或已提交表單的資料儲存在配置為部署的資料儲存AEM中。 匿名用戶的草稿和提交不顯示在表單門戶頁面上；但是，該資料被儲存在配置的資料儲存中。 有關詳細資訊，請參見 [為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)。

## 用戶資料和資料儲存 {#user-data-and-data-stores}

Forms門戶網站將草稿和提交的表格資料儲存在以下情形中：

* 在自適應表單中配置的提交操作是 **Forms門戶提交操作**。
* 提交除 **Forms門戶提交操作**，也請參見Wiki頁。 **[!UICONTROL 在表單門戶中儲存資料]** 選項 **[!UICONTROL 提交]** 自適應窗體容器的屬性。

對於登錄用戶和匿名用戶的每個草稿和提交的表單，表單門戶儲存以下資料：

* 表單元資料，如表單名稱、表單路徑、草稿或提交ID、附件路徑和用戶資料ID
* 表單附件作為資料位元組
* 以資料位元組形式表單資料

根據配置的資料儲存持久性，草稿和提交的表單資料儲存在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>作AEM者和發佈實例儲存庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>AEM作者和遠程實例庫AEM</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>資料庫</p> </td>
   <td><p>作者AEM實例和資料庫表的儲存庫</p> </td>
   <td>資料庫表 <code>data</code>。 <code>metadata</code>, <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 訪問和刪除用戶資料 {#access-and-delete-user-data}

您可以訪問配置資料儲存中登錄用戶和匿名用戶的草稿和提交的表單資料，如果需要，可將其刪除。

### AEM實例 {#aem-instances}

已登錄和匿名用戶AEM的所有草稿和已提交表單資料（作者、發佈或遠程）都儲存在 `/content/forms/fp/` 的子AEM目錄。 每次登錄或匿名用戶保存草稿或提交表單時， `draft ID` 或 `submission ID`的 `user data ID`和隨機 `ID` 生成與各份草案或提交書關聯的附件（如果適用）。

#### 訪問用戶資料 {#access-user-data}

當登錄用戶保存草稿或提交表單時，將使用其用戶ID建立子節點。 例如，為用戶ID為Sarah Rose草稿和提交資料 `srose` 儲存 `/content/forms/fp/srose/` 儲存庫中AEM的節點。 在用戶ID節點內，資料以分層結構組織。

下表說明了所有草稿的資料 `srose` 儲存在存AEM儲庫中。

>[!NOTE]
>
>一個精確的結構 `drafts` 複製為 `srose` 下 `/content/forms/fp/srose/submit/` 的下界。
>
>所有草稿和提交者 `anonymous` 用戶儲存在 `/content/forms/fp/anonymous/` 節點，該節點為以下所有匿名用戶組織草稿和提交 `draft` 和 `submit` 節點。

| 節點 | 說明 |
|---|---|
| `/content/forms/fp/srose/drafts` | 用戶所有草稿的容器節點資料 |
| `/content/forms/fp/srose/drafts/attachments/` | 根據草稿ID組織用戶的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含二進位格式的所選ID的附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根據草稿ID組織用戶的表單元資料 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含所選草稿ID的表單元資料 |
| `/content/forms/fp/srose/drafts/data/` | 根據用戶資料ID為用戶組織表單資料 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所選用戶資料ID的二進位格式的表單資料 |

#### 刪除用戶資料 {#delete-user-data}

要從系統中刪除已登錄用戶的草稿和提交的AEM用戶資料，必須刪除 `user ID` 從作者節點中指定用戶的節點。 必須手動從所有適用實例中刪AEM除資料。

所有匿名用戶的草稿和提交資料都儲存在公共 `drafts` 和 `submit` 節點 `/content/forms/fp/anonymous`。 除非已知某些可識別資訊，否則找不到特定匿名用戶的資料。 在這種情況下，您可以搜索在儲存庫中標識匿名用戶的資訊AEM，然後從所有適用實例中手動刪除包含該用戶的AEM節點，以從系統中AEM刪除資料。 但是，要刪除所有匿名用戶的資料，可以刪除 `anonymous` 節點，以刪除所有匿名用戶的草稿和提交資料。

### 資料庫 {#database}

當AEM配置為將資料儲存在資料庫中時，表單門戶草稿和提交資料將儲存在以下資料庫表中，供登錄用戶和匿名用戶使用：

* 資料
* 中繼資料
* 附加元資料

#### 訪問用戶資料 {#access-user-data-1}

要訪問資料庫表中登錄用戶和匿名用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，替換 `logged-in user` 具有要訪問其資料的用戶ID或 `anonymous` 匿名用戶。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 刪除用戶資料 {#delete-user-data-1}

要從資料庫表中刪除已登錄用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，替換 `logged-in user` 具有要刪除其資料的用戶ID或 `anonymous` 匿名用戶。 請注意，要從資料庫中刪除特定匿名用戶的資料，您需要使用一些可識別資訊找到它，然後從包含該資訊的資料庫表中刪除它。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
