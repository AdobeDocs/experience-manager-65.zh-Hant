---
title: Forms用戶管理 |處理用戶資料
seo-title: Forms user management | Handling user data
description: Forms用戶管理 |處理用戶資料
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Forms用戶管理 |處理用戶資料 {#forms-user-management-handling-user-data}

用戶管理是AEM FormsJEE元件，它允許建立、管理和授權AEM Forms用戶訪問AEM Forms。 用戶管理使用域作為獲取用戶資訊的目錄。 支援以下域類型：

**本地域**:此類型的域未連接到第三方儲存系統。 而是在本地建立用戶和組並駐留在用戶管理資料庫中。 密碼在本地儲存，並使用本地資料庫進行身份驗證。

**混合域**:此類型的域未連接到第三方儲存系統。 而是在本地建立用戶和組並駐留在用戶管理資料庫中。 與本地域不同，混合域使用外部身份驗證提供程式，該提供程式可以是LDAP、Kerberos、SAML或自定義身份驗證提供程式。

**企業域**:由駐留在第三方儲存系統（如LDAP目錄）中的用戶和組組成。 用戶管理不寫入第三方儲存系統。 相反，用戶管理會將用戶和組資訊與用戶管理資料庫同步。 企業域還使用外部身份驗證提供程式，該提供程式可以是LDAP、Kerberos、SAML或自定義身份驗證提供程式。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 用戶資料和資料儲存 {#user-data-and-data-stores}

用戶管理將用戶資料儲存在資料庫中，如My Sql 、Oracle、MS SQL Server和IBMDB2。 此外，任何在Forms應用程式中至少登錄一次的用戶，其AEM作者 `https://'[server]:[port]'lc`，用戶將在儲存庫中AEM建立。 因此，用戶管理被儲存在以下資料儲存中：

* 資料庫
* AEM儲存庫
* 第三方儲存（如LDAP目錄）

>[!NOTE]
>
>儲存在第三方儲存中的資料超出此文檔的範圍。 直接聯繫第三方供應商以管理此類儲存中的用戶資料。

### 資料庫 {#database}

用戶管理將用戶資料儲存在以下資料庫表中：

<table>
 <tbody>
  <tr>
   <td>資料庫表</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>儲存有關主體實體的資訊。 承擔者可以是用戶、組或角色。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>儲存用戶的個人身份資訊(PII)。 它包含本地、企業和混合域中每個用戶的條目。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>僅儲存本地用戶的資料。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>包含來自本地、企業和混合域的所有用戶的條目。 它包含用戶電子郵件ID。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存用戶和組之間的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>儲存用戶和組的角色和承擔者之間的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>儲存用戶和組的承擔者和權限之間的映射。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存與承擔者對應的舊屬性值和新屬性值。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM儲存庫 {#aem-repository}

至少曾訪問過Forms應用程式的用戶的用戶管理資料 `https://'[server]:[port]'lc` 也儲存AEM在儲存庫中。

## 訪問和刪除用戶資料 {#access-and-delete-user-data}

您可以訪問和導出用戶管理資料庫和儲存庫中用戶的用戶AEM管理資料，如果需要，可永久刪除它。

### 資料庫 {#database-1}

要從用戶管理資料庫中導出或刪除用戶資料，需要使用資料庫客戶端連接到資料庫並根據用戶的某些PII查找主ID。 例如，要使用登錄ID檢索用戶的主ID，請運行以下 `select` 命令。

在 `select` 命令，替換 `<user_login_id>` 具有要檢索其主體ID的用戶的登錄ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

一旦知道主體ID，就可以導出或刪除用戶資料。

#### 導出用戶資料 {#export-user-data}

運行以下資料庫命令以從資料庫表導出主體ID的用戶管理資料。 在 `select` 命令，替換 `<principal_id>` 具有要導出其資料的用戶的主體ID。

>[!NOTE]
>
>以下命令在My SQL和IBMDB2資料庫中使用資料庫表名。 在Oracle和MS SQL資料庫上運行這些命令時，請替換命令中的以下表名：
>
>* 替換 `EdcPrincipalLocalAccountEntity` 與 `EdcPrincipalLocalAccount`
>
>* 替換 `EdcPrincipalEmailAliasEntity` 與 `EdcPrincipalEmailAliasEn`
>
>* 替換 `EdcPrincipalMappingEntity` 與 `EdcPrincipalMappingEntit`
>
>* 替換 `EdcPrincipalGrpCtmntEntity` 與 `EdcPrincipalGrpCtmntEnti`
>


```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### 刪除用戶資料 {#delete-user-data}

執行以下操作以從資料庫表中刪除主體ID的用戶管理資料。

1. 從儲存庫中刪AEM除用戶資料（如果適用），如中所述 [刪除用戶資料](/help/forms/using/user-management-handling-user-data.md#delete-aem)。
1. 關閉AEM Forms伺服器。
1. 運行以下資料庫命令，從資料庫表中刪除主體ID的用戶管理資料。 在 `Delete` 命令，替換 `<principal_id>` 具有要刪除其資料的用戶的主體ID。

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. 啟動AEM Forms伺服器。

### AEM儲存庫 {#aem-repository-1}

FormsJEE用戶如果至少訪問AEM了AEM Forms作者實例，則其資料將儲存庫中。 您可以訪問和從儲存庫中刪除其用AEM戶資料。

#### 訪問用戶資料 {#access-user-data}

要查看在儲存庫中創AEM建的用戶，請登錄 `https://'[server]:[port]'/lc/useradmin` 具有管AEM理員憑據。 請注意 `server` 和 `port` 的上界AEM。 在此，您可以使用用戶名搜索用戶。 按兩下某個用戶以查看該用戶的屬性、權限和組等資訊。 的 `Path` 用戶的屬性指定在儲存庫中建立的用戶節點的路AEM徑。

#### 刪除用戶資料 {#delete-aem}

要刪除用戶：

1. 轉到 `https://'[server]:[port]'/lc/useradmin` 具有管AEM理員憑據。
1. 搜索用戶並按兩下用戶名以開啟用戶屬性。 複製 `Path` 屬性。
1. 轉到CRX AEM DELite，地址： `https://'[server]:[port]'/lc/crx/de/index.jsp` 導航或搜索用戶路徑。
1. 刪除路徑並按一下 **[!UICONTROL 全部保存]** 從儲存庫中永久刪AEM除用戶。
