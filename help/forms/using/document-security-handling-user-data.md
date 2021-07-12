---
title: 檔案安全性 |處理用戶資料
seo-title: 檔案安全性 |處理用戶資料
description: 檔案安全性 |處理用戶資料
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
role: Admin
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# 檔案安全性 |處理用戶資料 {#document-security-handling-user-data}

AEM Forms檔案安全性可讓您建立、儲存預先定義的安全性設定，並將其套用至您的檔案。 它確保只有授權用戶才能使用文檔。 您可以使用策略保護文檔。 策略是資訊的集合，包括安全設定和授權用戶清單。 您可以將原則套用至一或多個檔案，並授權新增至AEM Forms JEE使用者管理的使用者。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## 使用者資料和資料儲存 {#user-data-and-data-stores}

文檔安全儲存與受保護文檔相關的策略和資料，包括資料庫中的用戶資料，如My Sql 、Oracle、MS SQL Server和IBM DB2。 此外，在用戶管理中儲存的策略中授權用戶的資料。 如需儲存在使用者管理中的資料相關資訊，請參閱[Forms使用者管理：處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。

下表映射了文檔安全性如何在資料庫表中組織資料。

<table>
 <tbody>
  <tr>
   <td>資料庫表</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>儲存使用者的主要金鑰相關資訊。 這些鍵用於離線文檔安全工作流。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>儲存有關審核事件（如用戶事件、文檔事件和策略事件）的資訊。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>儲存受保護文檔的記錄。 它儲存每個受保護文檔的許可證詳細資訊。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>儲存系統中建立的每個許可證的文檔名稱。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>儲存有關撤銷和恢復受保護文檔的資訊。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>儲存有關可以建立個人策略的用戶的資訊，這些策略顯示在「策略」頁的「我的策略」頁簽下。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>儲存有關原則的資訊。 每個策略都與此表中的一行對應。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>儲存活動策略的XML檔案。 策略XML<sup> </sup>包含對與該策略關聯的用戶的主ID的引用。 策略XML儲存為Blob對象。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>儲存有關已存檔策略的資訊。 歸檔策略包含其作為Blob對象儲存的策略XML。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存策略集和用戶之間的映射。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>儲存受邀使用者的相關資訊。</td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以訪問和導出資料庫中用戶的文檔安全資料，如果需要，可以永久刪除該資料。

要從資料庫導出或刪除用戶資料，您需要使用資料庫客戶端連接到資料庫，並根據用戶的某些個人身份資訊查找主ID。 例如，要使用登錄ID檢索用戶的主ID，請在資料庫上運行以下`select`命令。

在`select`命令中，將`<user_login_id>`替換為要從`EdcPrincipalUserEntity`資料庫表中檢索其主ID的用戶的登錄ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

知道主體ID後，即可匯出或刪除使用者資料。

### 匯出使用者資料 {#export-user-data}

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
>若要從`EdcAuditEntity`表格匯出資料，請使用以[EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)為參數的[EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API，以根據`principalId`、`policyId`或`licenseId`匯出稽核資料。

要獲取系統中某個用戶的完整資料，必須從用戶管理資料庫訪問和導出資料。 如需詳細資訊，請參閱[Forms使用者管理：處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。

### 刪除使用者資料 {#delete-user-data}

執行以下操作以從資料庫表中刪除主體ID的文檔安全資料。

1. 關閉AEM Forms伺服器。
1. 運行以下資料庫命令，從資料庫表中刪除主ID的資料以確保文檔安全。 在`Delete`命令中，將`<principal_id>`替換為要刪除其資料的用戶的主ID。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >若要從`EdcAuditEntity`表格刪除資料，請使用以[EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html)EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)為參數的[EventManager.deleteEvents API，以根據`principalId`、`policyId`或`licenseId`刪除稽核資料。

1. 活動策略和歸檔策略XML檔案分別儲存在`EdcPolicyXmlEntity`和`EdcPolicyArchiveEntity`資料庫表中。 要從這些表中刪除用戶的資料，請執行以下操作：

   1. 開啟`EdcPolicyXMLEntity`或`EdcPolicyArchiveEntity`表中每行的XML blob，並提取XML檔案。 XML檔案與下面所示的檔案類似。
   1. 編輯XML檔案以刪除主體ID的blob。
   1. 對另一個檔案重複步驟1和2。

   >[!NOTE]
   >
   >必須刪除`Principal`標籤中的完整blob，主體ID才能刪除，否則策略XML可能已損壞或無法使用。

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

   除了直接從`EdcPolicyXmlEntity`表格刪除資料外，您還可以透過下列兩種方式達成此目標：

   **使用管理控制台**

   1. 以管理員身分登入Forms JEE管理主控台，網址為https://[*server*]:[*port*]/adminui。
   1. 導航到&#x200B;**[!UICONTROL 服務>文檔安全>策略集]**。
   1. 開啟策略集，然後從策略中刪除用戶。

   **使用文檔安全網頁**

   具有建立個人策略權限的文檔安全用戶可以從其策略中刪除用戶資料。 若要這麼做：

   1. 擁有個人策略的用戶登錄到其文檔安全網頁：https://[*server*]:[*port*]/edc。
   1. 導覽至「**[!UICONTROL 服務>檔案安全性>我的原則]**」。
   1. 開啟原則，然後從原則中刪除使用者。

   >[!NOTE]
   >
   >管理員可以使用管理控制台，從&#x200B;**[!UICONTROL 服務>文檔安全性>我的策略]**&#x200B;中其他用戶的個人策略中搜索、訪問和刪除用戶資料。

1. 從用戶管理資料庫中刪除主體ID的資料。 如需詳細步驟，請參閱[Forms使用者管理 |處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。
1. 啟動AEM Forms伺服器。
