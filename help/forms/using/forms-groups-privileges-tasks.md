---
title: AEM Forms論OSGi組和特權
seo-title: AEM Forms on OSGi Groups and Privileges
description: 將用戶分配給組以在OSGi上管理AEM Forms
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
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# AEM Forms論OSGi組和特權{#aem-forms-on-osgi-groups-and-privileges}

你可以 [建立組](/help/sites-administering/user-group-ac-admin.md#group-administration) 並分配策略和 [用戶](/help/sites-administering/user-group-ac-admin.md#user-administration) 中的組AEM。 這些策略控制屬於組的用戶的權限。

安裝後 [AEM Forms附加包](../../forms/using/installing-configuring-aem-forms-osgi.md)，本文中提到的組（如forms-users和forms-power-user）可自動進行分配。 下表列出了用戶可根據組分配在OSGi上為AEM Forms執行的任務：

<table>
 <tbody>
  <tr>
   <td>群組</td> 
   <td>任務</td> 
  </tr>
  <tr>
   <td>表單用戶 <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈和提交自適應表單</li> 
     <li>建立、預覽和發佈互動式通信和文檔片段</li> 
     <li>將資產上載到實AEM例</li> 
     <li>建立主題</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表單超級用戶</td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈和提交自適應表單</li> 
     <li>建立、預覽和發佈互動式通信和文檔片段</li> 
     <li>使用代碼編輯器為自適應表單建立指令碼</li> 
     <li>上載資產（包括指令碼）</li> 
     <li>建立主題</li> 
     <li>導入包含XDP的包</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表單提交審核者</td> 
   <td>
    <ul> 
     <li>審查提交</li> 
     <li>批准或拒絕提交</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>模板作者 <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>建立和預覽自適應表單或互動式通信模板</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm作者</p> </td> 
   <td>
    <ul> 
     <li>建立和修改表單資料模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm代理用戶</td> 
   <td>
    <ul> 
     <li>使用代理UI訪問通信管理信函或交互通信</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>工作流編輯器</p> </td> 
   <td>
    <ul> 
     <li>建立收件箱應用程式</li> 
     <li>建立工作流模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>工作流用戶</td> 
   <td>
    <ul> 
     <li>使用收件箱AEM應用程式<br /> <strong>注： </strong>您必須具有cm-agent-users和workflow-users組分配才能訪問收件箱中的Interactive Communications Agent AEM UI。</li> 
     <li>管理工作流實例</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd管理員</td> 
   <td>
    <ul> 
     <li>配置 PDF 產生器</li> 
     <li>配置監視資料夾</li> 
     <li>管理工作流應用程式</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. 具有forms-users組權限的用戶無法為自適應表單編寫指令碼。
1. 具有模板作者組權限的用戶無法編寫模板指令碼。
