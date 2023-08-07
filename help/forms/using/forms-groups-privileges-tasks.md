---
title: OSGi群組和許可權上的AEM Forms
seo-title: AEM Forms on OSGi Groups and Privileges
description: 將使用者指派給群組，以便在OSGi上管理AEM Forms
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: 3bc61e56d2fcd9f32c37a7ea04b0ffc6728bfc56
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 6%

---

# OSGi群組和許可權上的AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html) |
| AEM 6.5 | 本文章 |

您可以 [建立群組](/help/sites-administering/user-group-ac-admin.md#group-administration) 並指派原則和 [使用者](/help/sites-administering/user-group-ac-admin.md#user-administration) 到AEM中的群組。 這些原則控制屬於群組之使用者的許可權。

安裝之後 [AEM Forms附加元件套件](../../forms/using/installing-configuring-aem-forms-osgi.md)，本文中提到的群組（例如forms-users和forms-power-user）可自動用於指派。 下表列出使用者可以根據群組指派在OSGi上為AEM Forms執行的工作：

<table>
 <tbody>
  <tr>
   <td>群組</td> 
   <td>任務</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈及提交最適化表單</li> 
     <li>建立、預覽和發佈互動式通訊和檔案片段</li> 
     <li>將資產上傳至AEM執行個體</li> 
     <li>建立主題</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈及提交最適化表單</li> 
     <li>建立、預覽和發佈互動式通訊和檔案片段</li> 
     <li>使用程式碼編輯器建立最適化表單的指令碼</li> 
     <li>上傳資產，包括指令碼</li> 
     <li>建立主題</li> 
     <li>匯入包含XDP的套件</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表單 — 提交 — 稽核者</td> 
   <td>
    <ul> 
     <li>稽核提交</li> 
     <li>核准或拒絕提交</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>範本 — 作者 <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>建立及預覽最適化表單或互動式通訊範本</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>建立和修改表單資料模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>使用Agent UI存取通訊管理信件或互動式通訊</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editor</p> </td> 
   <td>
    <ul> 
     <li>建立收件匣應用程式</li> 
     <li>建立工作流程模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>使用AEM收件匣應用計畫<br /> <strong>注意： </strong>您必須有cm-agent-users和workflow-users群組指派，才能存取AEM收件匣中的互動式通訊代理程式UI。</li> 
     <li>管理工作流程例項</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>配置 PDF 產生器</li> 
     <li>設定Watched資料夾</li> 
     <li>管理工作流程應用程式</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. 具有表單 — 使用者群組許可權的使用者無法撰寫最適化表單的指令碼。
1. 具有範本作者群組許可權的使用者無法撰寫範本的指令碼。
