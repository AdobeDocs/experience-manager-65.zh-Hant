---
title: 表單入口網站|處理使用者資料
seo-title: 表單入口網站|處理使用者資料
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 表單入口網站|處理使用者資料 {#forms-portal-handling-user-data}

AEM Forms入口網站提供您可用來在AEM Sites頁面上列出最適化表單、HTML5表單和其他表單資產的元件。 此外，您也可以設定它，以顯示已登入使用者的草稿並提交最適化表單和HTML5表單。 如需表單入口網站的詳細資訊，請參 [閱Portal上發佈表單的簡介](/help/forms/using/introduction-publishing-forms.md)。

當登入使用者將最適化表單儲存為草稿或提交時，這些表單會顯示在表單入口網站的「草稿」和「提交」標籤中。 草稿或提交表單的資料會儲存在為AEM部署所設定的資料儲存區中。 匿名用戶的草稿和提交不顯示在表單門戶頁面上；但是，該資料儲存在配置的資料儲存中。 有關詳細資訊，請參 [閱為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)。

## 使用者資料與資料儲存 {#user-data-and-data-stores}

表單入口網站會在下列情況下儲存草稿和提交表單的資料：

* 在最適化表單中設定的提交動作為 **Forms Portal Submit Action**。
* 對於提交動作( **Forms Portal Submit Action除外)**，在最適化表單容器的「提交」屬性中啟用「將資料儲存在表單portal ******** 」選項。

對於每個登入和匿名使用者的草稿和提交表單，表單入口網站會儲存下列資料：

* 表單中繼資料，例如表單名稱、表單路徑、草稿或提交ID、附件路徑和使用者資料ID
* 表單附件作為資料位元組
* 以資料位元組形式表示資料

根據設定的資料儲存永續性，草稿和提交的表單資料會儲存在下列位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>AEM作者和發佈例項的儲存庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>作者和遠端AEM例項的AEM儲存庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>資料庫</p> </td>
   <td><p>作者實例和資料庫表的AEM儲存庫</p> </td>
   <td>資料庫 <code>data</code>表 <code>metadata</code>和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以存取已設定資料存放區中登入和匿名使用者的草稿和已提交表單資料，並視需要加以刪除。

### AEM例項 {#aem-instances}

登入和匿名使用者的AEM例項（作者、發佈或遠端）中所有草稿和提交的表單資料都會儲存在適用的AEM `/content/forms/fp/` 儲存庫的節點中。 每次登入或匿名使用者儲存草稿或提交表格時，就會針對每個附件（如果適用）產生 `draft ID` a或 `submission ID``user data ID`、a和隨機 `ID` 表格，這些表格會與各自的草稿或提交相關聯。

#### 存取使用者資料 {#access-user-data}

當登入使用者儲存草稿或提交表單時，會使用其使用者ID來建立子節點。 例如，其使用者ID儲存在AEM儲存庫節點中的Sarah rose的草稿 `srose` 和提交 `/content/forms/fp/srose/` 資料。 在用戶ID節點內，資料以分層結構組織。

下表說明如何將所有草稿的資料儲 `srose` 存在AEM儲存庫中。

>[!NOTE]
>
>在節點下，會為 `drafts` 提交的表單複製一 `srose` 個精確 `/content/forms/fp/srose/submit/` 結構。
>
>使用者的所有草稿和 `anonymous` 提交都會儲存在節點下， `/content/forms/fp/anonymous/` 節點會組織所有匿名使用者在節點和節點下的 `draft` 草稿和提 `submit` 交。

| 節點 | 說明 |
|---|---|
| `/content/forms/fp/srose/drafts` | 使用者所有草稿的容器節點資料 |
| `/content/forms/fp/srose/drafts/attachments/` | 根據草稿ID組織使用者的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含選定ID的二進位格式附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根據草稿ID組織使用者的表單中繼資料 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含所選草稿ID的表單中繼資料 |
| `/content/forms/fp/srose/drafts/data/` | 根據使用者資料ID組織使用者的表單資料 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所選用戶資料ID的二進位格式表單資料 |

#### 刪除使用者資料 {#delete-user-data}

若要從AEM系統的已登入使用者的草稿和提交中完全刪除使用者資料，您必須從作者節 `user ID` 點刪除特定使用者的節點。 您必須從所有適用的AEM例項手動刪除資料。

所有匿名使用者的草稿和提交資料會儲存在下方的公 `drafts` 用 `submit` 和節點 `/content/forms/fp/anonymous`中。 除非已知某些可識別資訊，否則無法尋找特定匿名使用者的資料。在此案例中，您可以搜尋AEM儲存庫中識別匿名使用者的資訊，並從所有適用的AEM例項手動刪除包含該資訊的節點，以從AEM系統移除資料。 不過，若要刪除所有匿名使用者的資料，您可以刪除節 `anonymous` 點，以移除所有匿名使用者的草稿和提交資料。

### 資料庫 {#database}

當AEM設定為將資料儲存在資料庫中時，表單入口網站草稿和提交資料會儲存在下列資料庫表格中，供登入和匿名使用者使用：

* 資料
* 中繼資料
* 其他中繼資料

#### 存取使用者資料 {#access-user-data-1}

要訪問資料庫表中登錄用戶和匿名用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，請 `logged-in user` 以您要存取其資料的使用者ID取代，或以匿名使用者 `anonymous` 的使用者ID取代。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 刪除使用者資料 {#delete-user-data-1}

要從資料庫表中刪除登錄用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，請 `logged-in user` 以您要刪除其資料的使用者ID取代，或以匿名使用者 `anonymous` 的使用者ID取代。 請注意，要從資料庫中刪除特定匿名用戶的資料，您需要使用一些可識別資訊查找該資料，並從包含該資訊的資料庫表中刪除該資料。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

