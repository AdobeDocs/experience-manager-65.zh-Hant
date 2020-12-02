---
title: Document Security |處理使用者資料
seo-title: Document Security |處理使用者資料
description: Document Security |處理用戶資料
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Document Security |處理用戶資料{#document-security-handling-user-data}

AEM Forms檔案安全性可讓您建立、儲存並套用預先定義的保全設定至檔案。 它可確保只有授權的使用者才能使用檔案。 您可以使用原則來保護檔案。 原則是包含安全性設定和授權使用者清單的資訊集合。 您可以套用原則至一或多份檔案，並授權在AEM Forms JEE使用者管理中新增的使用者。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## 用戶資料和資料儲存{#user-data-and-data-stores}

Document Security會將與受保護檔案相關的原則和資料儲存在資料庫中，包括使用者資料，例如My Sql、Oracle、MS SQL Server和IBM DB2。 此外，在用戶管理中儲存的策略中授權用戶的資料。 如需有關儲存在使用者管理中的資料，請參閱[表單使用者管理：處理用戶資料](/help/forms/using/user-management-handling-user-data.md)。

下表映射了文檔安全性在資料庫表中組織資料的方式。

<table>
 <tbody>
  <tr>
   <td>資料庫表</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>儲存有關用戶的主鍵的資訊。 這些金鑰用於離線檔案保全工作流程中。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>儲存有關審核事件的資訊，例如使用者事件、檔案事件和原則事件。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>儲存受保護檔案的記錄。 它會儲存每個受保護檔案的授權詳細資訊。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>儲存系統中建立之每個授權的檔案名稱。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>儲存有關撤銷和恢復受保護檔案的資訊。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>儲存有關可建立個人策略的用戶的資訊，這些策略顯示在「策略」頁的「我的策略」頁籤下。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>儲存有關策略的資訊。 每個策略都與此表中的一行相對應。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>儲存活動策略的XML檔案。 策略XML<sup> </sup>包含對與策略關聯的用戶的主ID的引用。 策略XML儲存為Blob對象。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>儲存有關歸檔策略的資訊。 歸檔策略包含其作為Blob對象儲存的策略XML。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> （Oracle和MS SQL資料庫）</p> </td>
   <td>儲存策略集和用戶之間的映射。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>儲存有關已邀請使用者的資訊。</td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料{#access-and-delete-user-data}

您可以存取和匯出資料庫中使用者的檔案安全性資料，並視需要永久刪除。

要從資料庫導出或刪除用戶資料，您需要使用資料庫客戶端連接到資料庫，並根據用戶的某些個人身份資訊查找主ID。 例如，要使用登錄ID檢索用戶的主ID，請在資料庫上運行以下`select`命令。

在`select`命令中，將`<user_login_id>`替換為要從`EdcPrincipalUserEntity`資料庫表中檢索其主ID的用戶的登錄ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

一旦您知道承擔者ID，就可以匯出或刪除使用者資料。

### 匯出使用者資料{#export-user-data}

運行以下資料庫命令，從資料庫表導出主ID的用戶資料。 在`select`命令中，將`<principal_id>`替換為要導出其資料的用戶的主ID。

>[!NOTE]
>
>以下命令在My SQL和IBM DB2資料庫中使用資料庫表名。 在Oracle和MS SQL資料庫上運行這些命令時，請在命令中將`EdcPolicySetPrincipalEntity`替換為`EdcPolicySetPrincipalEnt`。

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>若要從`EdcAuditEntity`表格匯出資料，請使用[EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API，此API會以[EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)為參數，以根據`principalId`、`policyId`或`licenseId`匯出稽核資料。

要獲取系統中用戶的完整資料，必須訪問用戶管理資料庫並從中導出資料。 如需詳細資訊，請參閱[Forms使用者管理：處理用戶資料](/help/forms/using/user-management-handling-user-data.md)。

### 刪除用戶資料{#delete-user-data}

執行下列操作，從資料庫表中刪除承擔者ID的文檔安全資料。

1. 關閉AEM Forms伺服器。
1. 運行以下資料庫命令，從資料庫表中刪除主ID的資料，以確保文檔安全。 在`Delete`命令中，將`<principal_id>`替換為要刪除其資料的用戶的主ID。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >若要刪除`EdcAuditEntity`表格中的資料，請使用[EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API，此API會以[EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)為參數，以根據`principalId`、`policyId`或`licenseId`刪除稽核資料。

1. 活動策略和歸檔策略XML檔案分別儲存在`EdcPolicyXmlEntity`和`EdcPolicyArchiveEntity`資料庫表中。 要從這些表中刪除用戶的資料，請執行以下操作：

   1. 在`EdcPolicyXMLEntity`或`EdcPolicyArchiveEntity`表格中開啟每一列的XML Blob，並擷取XML檔案。 XML檔案類似於下方所示的檔案。
   1. 編輯XML檔案以刪除主ID的blob。
   1. 對另一個檔案重複步驟1和2。

   >[!NOTE]
   >
   >您必須為主ID刪除`Principal`標籤中的完整blob，否則策略XML可能會損壞或不可用。

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   除了直接從`EdcPolicyXmlEntity`表格刪除資料外，您還有另外兩種方式可以做到：

   **使用管理控制台**

   1. 以管理員身份登錄Forms JEE管理控制台，網址為https://[*server*]:[*port*]/adminui。
   1. 導覽至&#x200B;**[!UICONTROL 服務> Document Security >原則集]**。
   1. 開啟策略集並從策略中刪除用戶。

   **使用檔案安全性網頁**

   具有建立個人原則權限的檔案安全性使用者可從其原則中刪除使用者資料。 若要這麼做：

   1. 擁有個人原則的使用者可登入其檔案安全網頁https://[*server*]:[*port*]/edc。
   1. 導覽至「**[!UICONTROL 服務> Document Security >我的原則]**」。
   1. 開啟原則，並從原則中刪除使用者。

   >[!NOTE]
   >
   >管理員可以使用管理控制台，從&#x200B;**[!UICONTROL 服務> Document Security > My Policys]**&#x200B;中其他使用者的個人原則搜尋、存取和刪除使用者資料。

1. 從用戶管理資料庫中刪除承擔者ID的資料。 如需詳細步驟，請參閱[Forms使用者管理 |處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。
1. 啟動AEM Forms伺服器。

