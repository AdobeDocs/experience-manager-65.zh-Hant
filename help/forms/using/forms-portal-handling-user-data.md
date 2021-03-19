---
title: Forms門戶 |處理使用者資料
seo-title: Forms門戶 |處理使用者資料
description: Forms門戶 |處理使用者資料
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---


# Forms門戶 |處理用戶資料{#forms-portal-handling-user-data}

[!DNL AEM Forms] portal提供您可用來列出頁面上最適化表單、HTML5表單和其他Forms資產的 [!DNL AEM Sites] 元件。此外，您也可以設定它，以顯示已登入使用者的草稿並提交最適化表單和HTML5表單。 如需表單入口網站的詳細資訊，請參閱[在入口網站上發佈表單的簡介](/help/forms/using/introduction-publishing-forms.md)。

當登入使用者將最適化表單儲存為草稿或提交時，這些表單會顯示在表單入口網站的「草稿」和「提交」標籤中。 草稿或提交表單的資料會儲存在設定為部署的資料AEM儲存區。 匿名用戶的草稿和提交不顯示在表單門戶頁面上；但是，該資料儲存在配置的資料儲存中。 有關詳細資訊，請參閱[為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)。

## 用戶資料和資料儲存{#user-data-and-data-stores}

Forms門戶網站在以下情況下儲存草稿和提交表單的資料：

* 在最適化表單中設定的提交動作為&#x200B;**Forms入口網站提交動作**。
* 對於&#x200B;**Forms門戶提交操作**&#x200B;以外的提交操作，在自適應表單容器的&#x200B;**[!UICONTROL 提交]**&#x200B;屬性中啟用了&#x200B;**[!UICONTROL 將資料儲存在表單門戶中的選項。]**

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
   <td><p>作者AEM和發佈實例的儲存庫</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>作者AEM和遠程實例的儲存庫AEM</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>資料庫</p> </td>
   <td><p>AEM作者實例和資料庫表儲存庫</p> </td>
   <td>資料庫表<code>data</code>、<code>metadata</code>和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料{#access-and-delete-user-data}

您可以存取已設定資料存放區中登入和匿名使用者的草稿和已提交表單資料，並視需要加以刪除。

### AEM實例{#aem-instances}

登入和匿名使用者的所AEM有草稿和已提交表單資料（作者、發佈或遠端）都會儲存在適用儲存庫的`/content/forms/fp/`節AEM點中。 每次登入或匿名使用者儲存草稿或提交表格時，就會產生每個附件的`draft ID`或`submission ID`、`user data ID`和隨機`ID`（如果適用），這些附件與各自的草稿或提交相關聯。

#### 訪問用戶資料{#access-user-data}

當登入使用者儲存草稿或提交表單時，會使用其使用者ID來建立子節點。 例如，用戶ID為`srose`的Sarah Rose的草稿和提交資料儲存在儲存庫的`/content/forms/fp/srose/`節AEM點中。 在用戶ID節點內，資料以分層結構組織。

下表說明`srose`所有草稿的資料如何儲存在儲存AEM庫中。

>[!NOTE]
>
>在`/content/forms/fp/srose/submit/`節點下，為`srose`提交的表單複製精確結構，如`drafts`。
>
>`anonymous`使用者的所有草稿和提交都儲存在`/content/forms/fp/anonymous/`節點下，該節點會組織`draft`和`submit`節點下所有匿名使用者的草稿和提交。

| 節點 | 說明 |
|---|---|
| `/content/forms/fp/srose/drafts` | 使用者所有草稿的容器節點資料 |
| `/content/forms/fp/srose/drafts/attachments/` | 根據草稿ID組織使用者的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含選定ID的二進位格式附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根據草稿ID組織使用者的表單中繼資料 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含所選草稿ID的表單中繼資料 |
| `/content/forms/fp/srose/drafts/data/` | 根據使用者資料ID組織使用者的表單資料 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所選用戶資料ID的二進位格式表單資料 |

#### 刪除用戶資料{#delete-user-data}

要從系統中完全刪除登錄用戶的草稿和提交中AEM的用戶資料，必須從作者節點中刪除特定用戶的`user ID`節點。 您必須從所有適用例項手動刪除AEM資料。

所有匿名用戶的草稿和提交資料都儲存在`/content/forms/fp/anonymous`下的公共`drafts`和`submit`節點中。 除非已知某些可識別資訊，否則無法找到特定匿名使用者的資料。 在這種情況下，您可以搜索在儲存庫中標識匿名用戶的資訊，並從AEM所有適用實例中手動刪除包含該用戶的節AEM點，以從系統中刪除AEM資料。 不過，若要刪除所有匿名使用者的資料，您可以刪除`anonymous`節點，以移除所有匿名使用者的草稿和提交資料。

### 資料庫 {#database}

將AEM表單門戶草稿和提交資料配置為將資料儲存在資料庫中時，會將表單門戶草稿和提交資料儲存在以下資料庫表中，供登錄用戶和匿名用戶使用：

* 資料
* 中繼資料
* 其他中繼資料

#### 訪問用戶資料{#access-user-data-1}

要訪問資料庫表中登錄用戶和匿名用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，將`logged-in user`替換為要訪問其資料的用戶ID，或用`anonymous`替換匿名用戶。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 刪除用戶資料{#delete-user-data-1}

要從資料庫表中刪除登錄用戶的草稿和提交資料，請運行以下資料庫命令。 在查詢中，將`logged-in user`替換為要刪除其資料的用戶ID，或用`anonymous`替換匿名用戶。 請注意，要從資料庫中刪除特定匿名用戶的資料，您需要使用一些可識別資訊查找該資料，並從包含該資訊的資料庫表中刪除該資料。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

