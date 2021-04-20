---
title: Forms用戶管理 |處理使用者資料
seo-title: Forms用戶管理 |處理使用者資料
description: Forms用戶管理 |處理使用者資料
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---


# Forms用戶管理 |處理用戶資料{#forms-user-management-handling-user-data}

用戶管理是AEM FormsJEE元件，它允許建立、管理和授權AEM Forms用戶訪問AEM Forms。 用戶管理使用域作為獲取用戶資訊的目錄。 支援下列網域類型：

**本機網域**:此類域未連接到第三方儲存系統。使用者和群組會建立在本機，並位於使用者管理資料庫中。 密碼會儲存在本機，驗證會使用本機資料庫完成。

**混合網域**:此類域未連接到第三方儲存系統。使用者和群組會建立在本機，並位於使用者管理資料庫中。 與本地域不同，混合域使用外部驗證提供程式，該提供程式可以是LDAP、Kerberos、SAML或自定義驗證提供程式。

**企業網域**:由駐留在第三方儲存系統（如LDAP目錄）中的用戶和組組成。用戶管理不寫入第三方儲存系統。 使用者管理會改為將使用者和群組資訊與使用者管理資料庫同步。 企業網域也使用外部驗證提供者，可以是LDAP、Kerberos、SAML或自訂驗證提供者。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 用戶資料和資料儲存{#user-data-and-data-stores}

用戶管理將用戶資料儲存在資料庫中，如My Sql 、Oracle、MS SQL Server和IBM DB2。 此外，任何已在作者`https://'[server]:[port]'lc`的Forms應用程式中至少登錄一次的用AEM戶，都會在儲存庫中建立AEM該用戶。 因此，用戶管理儲存在以下資料儲存中：

* 資料庫
* AEM儲存庫
* 第三方儲存，如LDAP目錄

>[!NOTE]
>
>儲存在第三方儲存中的資料不適用於此文檔。 請直接聯絡第三方廠商，以管理此類儲存中的使用者資料。

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
   <td><p>儲存有關主實體的資訊。 承擔者可以是用戶、組或角色。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>儲存使用者的個人識別資訊(PII)。 它包含本機、企業和混合網域的每位使用者的項目。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>僅儲存本地用戶的資料。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>包含來自本機、企業和混合網域的所有使用者項目。 它包含使用者電子郵件ID。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存使用者和群組之間的對應。</td>
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
   <td>儲存與主體對應的新舊屬性值。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM儲存庫{#aem-repository}

至少曾在`https://'[server]:[port]'lc`下訪問過Forms應用程式的用戶的用戶管理資料也儲存在AEM儲存庫中。

## 存取和刪除使用者資料{#access-and-delete-user-data}

您可以存取和匯出使用者管理資料庫和儲存庫中使用者的使用者AEM管理資料，並視需要永久刪除資料。

### 資料庫 {#database-1}

要從用戶管理資料庫中導出或刪除用戶資料，您需要使用資料庫客戶端連接到資料庫，並根據用戶的某些PII查找主ID。 例如，要使用登錄ID檢索用戶的主ID，請在資料庫上運行以下`select`命令。

在`select`命令中，將`<user_login_id>`替換為要檢索其主ID的用戶的登錄ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

一旦您知道承擔者ID，就可以匯出或刪除使用者資料。

#### 匯出使用者資料{#export-user-data}

運行以下資料庫命令，從資料庫表導出主ID的用戶管理資料。 在`select`命令中，將`<principal_id>`替換為要導出其資料的用戶的主ID。

>[!NOTE]
>
>以下命令在My SQL和IBM DB2資料庫中使用資料庫表名。 在Oracle和MS SQL資料庫上運行這些命令時，請在命令中替換以下表名：
>
>* 將`EdcPrincipalLocalAccountEntity`取代為`EdcPrincipalLocalAccount`
   >
   >
* 將`EdcPrincipalEmailAliasEntity`取代為`EdcPrincipalEmailAliasEn`
   >
   >
* 將`EdcPrincipalMappingEntity`取代為`EdcPrincipalMappingEntit`
   >
   >
* 將`EdcPrincipalGrpCtmntEntity`取代為`EdcPrincipalGrpCtmntEnti`

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

#### 刪除用戶資料{#delete-user-data}

執行下列操作，從資料庫表中刪除主ID的用戶管理資料。

1. 如果適用，請AEM按[刪除用戶資料](/help/forms/using/user-management-handling-user-data.md#delete-aem)中所述從儲存庫刪除用戶資料。
1. 關閉AEM Forms伺服器。
1. 運行以下資料庫命令，從資料庫表中刪除主ID的用戶管理資料。 在`Delete`命令中，將`<principal_id>`替換為要刪除其資料的用戶的主ID。

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

### AEM儲存庫{#aem-repository-1}

FormsJEE用戶如果至少訪問了一個AEMAEM Forms作者實例，則其資料會保存在儲存庫中。 您可以從儲存庫訪問和刪除其用AEM戶資料。

#### 訪問用戶資料{#access-user-data}

要查看在儲存庫中創AEM建的用戶，請使用管理員憑據登錄到&lt;a0/AEM>。 `https://'[server]:[port]'/lc/useradmin`請注意，URL中的`server`和`port`是作者例項的AEM。 您可以在這裡使用使用者名稱來搜尋使用者。 連按兩下使用者，即可檢視使用者的屬性、權限和群組等資訊。 用戶的`Path`屬性指定在儲存庫中建立的用戶節點的路AEM徑。

#### 刪除用戶資料{#delete-aem}

刪除用戶：

1. 使用管理員憑據轉至&lt;a0/AEM>。`https://'[server]:[port]'/lc/useradmin`
1. 搜尋使用者，然後按兩下使用者名稱以開啟使用者屬性。 複製`Path`屬性。
1. 前往位AEM於`https://'[server]:[port]'/lc/crx/de/index.jsp`的CRX DELite，並導覽或搜尋使用者路徑。
1. 刪除路徑，然後按一下&#x200B;**[!UICONTROL Save All]** ，從儲存庫中永久刪除用AEM戶。

