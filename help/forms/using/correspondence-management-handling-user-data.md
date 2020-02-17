---
title: 信件管理|處理使用者資料
seo-title: 信件管理|處理使用者資料
description: 'null'
seo-description: 'null'
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 信件管理|處理使用者資料 {#correspondence-management-handling-user-data}

AEM Forms Commense Management可讓您建立、管理和簡化安全且個人化的客戶通訊。 它提供直覺式使用者介面，讓商業使用者使用預先核准的內容區塊和媒體元素來建立通訊。 如需建立通訊的詳細資訊，請參閱「建立 [通訊」](/help/forms/using/create-correspondence.md)。

當商業使用者或代理將信件儲存為草稿或提交時，信函例項會儲存在AEM儲存庫中。 字母實例包括對應資料和元資料。

>[!NOTE]
>
>在AEM 6.5 Forms中，無法立即使用通訊管理。 如果您要從舊版AEM Forms升級，請安裝相容性套件並移轉您的通訊管理資產，以繼續在AEM 6.5 Forms中使用這些資產。 有關詳細資訊，請參 [見Compatibility package](/help/forms/using/compatibility-package.md)。

## 使用者資料與資料儲存 {#data}

對應管理僅在將發佈例項設定為管理字母例項時，才會將草稿和已提交字母的資料儲存在AEM儲存庫中。 有關配置的詳細資訊，請參 [閱Correponse Management配置屬性](/help/forms/using/cm-configuration-properties.md)。

根據您AEM部署所設定的資料存放區永續性，草稿和提交的對應資料會儲存在下列位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>在反向複製設定中指定之發佈例項和作者例項的AEM儲存庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>遠端處理作者例項的AEM儲存庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在上述指定的AEM儲存庫位置：

* `[yyyy]/[mm]/[dd]` 是基於建立字母實例的日期的節點結構
* `[node-id]` 是指派給包含字母的資料夾的ID
* `[letter-instance-name]` 是儲存或送出信函時指定的名稱

在 [letter-instance-name節點下] ，會建立下列節點結構，並將每個letter實例的資料儲存在AEM儲存庫中：

| 節點 | 說明 |
|---|---|
| `extendedProperties` | 儲存字母實例的元資料屬性。 |
| `dataXML` | 以二進位格式儲存包含對應資料的可下載的dataXML檔案。 |
| `processedXDP` | 包含用於建立已提交信函的XDP模板的詳細資訊。 此節點僅為提交的通信建立。 |
| `submittedLetter` | 以可下載的二進位格式儲存提交的信函資料。 此節點僅為提交的通信建立。 |

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以存取已設定資料存放區中的草稿和已提交的對應資料，並視需要加以刪除。

### 存取使用者資料 {#access-user-data}

信件管理提供API，您可用來尋找及存取草稿和已提交的信件例項。 使用API，您可以使用字母實例ID或儲存或提交信件的使用者來尋找並開啟字母實例。 如需詳細資訊，請參 [閱API以存取字母例項](/help/forms/using/cm-apis-to-access-letter-instances.md)。

或者，您也可以使用CRX DELite導覽至AEM儲存庫中的字母例項。 有關 [儲存的資料和儲存庫位置的資訊](/help/forms/using/correspondence-management-handling-user-data.md#data) ，請參閱用戶資料和資料儲存。

### 刪除使用者資料 {#delete-user-data}

要查找包含特定用戶資料的字母實例，您可以：

* 如果信件實例名稱或保存草稿或提交信件的用戶已知，請使用信件管理API
* 使用個人識別資訊（例如電子郵件ID或名稱）使用AEM存放庫搜尋，以尋找儲存資訊的節點

若要從AEM系統完全刪除草稿和提交的通訊資料中的使用者資料，您必須從所有適用的AEM例項手動刪除字母例項節點。
