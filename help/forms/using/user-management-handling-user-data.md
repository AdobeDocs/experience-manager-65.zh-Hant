---
title: Forms使用者管理 |處理用戶資料
seo-title: Forms user management | Handling user data
description: Forms使用者管理 |處理用戶資料
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

# Forms使用者管理 |處理用戶資料 {#forms-user-management-handling-user-data}

使用者管理是AEM Forms JEE元件，可讓AEM Forms使用者建立、管理及授權AEM Forms。 用戶管理使用域作為獲取用戶資訊的目錄。 支援下列網域類型：

**本機網域**:此類域未連接到第三方儲存系統。 而是會在本機建立使用者和群組，並位於使用者管理資料庫中。 密碼儲存在本機，並使用本機資料庫進行驗證。

**混合網域**:此類域未連接到第三方儲存系統。 而是會在本機建立使用者和群組，並位於使用者管理資料庫中。 與本地域不同，混合域使用外部身份驗證提供程式，該提供程式可以是LDAP、Kerberos、SAML或自定義身份驗證提供程式。

**企業網域**:由駐留在第三方儲存系統（如LDAP目錄）中的用戶和組組成。 用戶管理不寫入第三方儲存系統。 而是，「用戶管理」將用戶和組資訊與用戶管理資料庫同步。 企業域還使用外部身份驗證提供程式，該提供程式可以是LDAP、Kerberos、SAML或自定義身份驗證提供程式。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 使用者資料和資料儲存 {#user-data-and-data-stores}

用戶管理將用戶資料儲存在資料庫中，如My Sql、Oracle、MS SQL Server和IBM DB2。 此外，任何使用者只要至少在AEM作者的Forms應用程式中登入一次， `https://'[server]:[port]'lc`，則會在AEM存放庫中建立使用者。 因此，用戶管理儲存在以下資料儲存中：

* 資料庫
* AEM存放庫
* 第三方儲存，如LDAP目錄

>[!NOTE]
>
>儲存在第三方儲存中的資料不在本文檔中。 直接聯絡第三方供應商，以管理此類儲存中的使用者資料。

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
   <td><p>儲存有關主要實體的資訊。 主體可以是用戶、組或角色。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>儲存使用者的個人識別資訊(PII)。 它包含來自本機、企業和混合網域之每位使用者的項目。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>僅儲存本機使用者的資料。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>包含來自本機、企業和混合網域之所有使用者的項目。 它包含使用者電子郵件ID。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存使用者和群組之間的對應。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>儲存用戶和組的角色和主體之間的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>儲存用戶和組的主體和權限之間的映射。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存與主體對應的新舊屬性值。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM存放庫 {#aem-repository}

至少曾存取下列Forms應用程式一次的使用者的使用者管理資料 `https://'[server]:[port]'lc` 也會儲存在AEM存放庫中。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以存取和匯出使用者管理資料庫和AEM存放庫中使用者的使用者管理資料，並視需要將其永久刪除。

### 資料庫 {#database-1}

若要從使用者管理資料庫匯出或刪除使用者資料，您需使用資料庫用戶端連線至資料庫，並根據使用者的某些PII來找出主要ID。 例如，要使用登錄ID檢索用戶的主體ID，請運行以下 `select` 命令。

在 `select` 命令，替換 `<user_login_id>` 使用您要擷取其主體ID之使用者的登入ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

知道主體ID後，即可匯出或刪除使用者資料。

#### 匯出使用者資料 {#export-user-data}

運行以下資料庫命令，從資料庫表導出主ID的用戶管理資料。 在 `select` 命令，替換 `<principal_id>` 具有您要匯出其資料之使用者的主要ID。

>[!NOTE]
>
>以下命令在My SQL和IBM DB2資料庫中使用資料庫表名。 在Oracle和MS SQL資料庫上運行這些命令時，請在命令中替換以下表名：
>
>* 取代 `EdcPrincipalLocalAccountEntity` with `EdcPrincipalLocalAccount`
>
>* 取代 `EdcPrincipalEmailAliasEntity` with `EdcPrincipalEmailAliasEn`
>
>* 取代 `EdcPrincipalMappingEntity` with `EdcPrincipalMappingEntit`
>
>* 取代 `EdcPrincipalGrpCtmntEntity` with `EdcPrincipalGrpCtmntEnti`
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

#### 刪除使用者資料 {#delete-user-data}

執行以下操作，從資料庫表中刪除主體ID的用戶管理資料。

1. 從AEM存放庫刪除使用者資料（若適用），如 [刪除使用者資料](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. 關閉AEM Forms伺服器。
1. 運行以下資料庫命令，從資料庫表中刪除主體ID的用戶管理資料。 在 `Delete` 命令，替換 `<principal_id>` 具有您要刪除其資料之使用者的主體ID。

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

### AEM存放庫 {#aem-repository-1}

Forms JEE使用者若至少存取了一個AEM Forms製作例項，其資料會存放在AEM存放庫中。 您可以從AEM存放庫存取和刪除其使用者資料。

#### 存取使用者資料 {#access-user-data}

若要檢視在AEM存放庫中建立的使用者，請登入 `https://'[server]:[port]'/lc/useradmin` 具有AEM管理員憑證。 請注意 `server` 和 `port` 在URL中是AEM author例項的URL。 您可以在此使用使用者名稱搜尋使用者。 按兩下某個使用者，即可檢視該使用者的屬性、權限和群組等資訊。 此 `Path` 用戶的屬性指定在AEM儲存庫中建立的用戶節點的路徑。

#### 刪除使用者資料 {#delete-aem}

要刪除用戶：

1. 前往 `https://'[server]:[port]'/lc/useradmin` 具有AEM管理員憑證。
1. 搜尋使用者，然後按兩下使用者名稱以開啟使用者屬性。 複製 `Path` 屬性。
1. 前往AEM CRX DELite，網址為 `https://'[server]:[port]'/lc/crx/de/index.jsp` 和導覽或搜尋使用者路徑。
1. 刪除路徑，然後按一下 **[!UICONTROL 全部儲存]** 從AEM存放庫中永久刪除使用者。
