---
title: OSGi群組和權限上的AEM Forms
seo-title: OSGi群組和權限上的AEM Forms
description: 指派使用者至群組以管理OSGi上的AEM Forms
seo-description: 指派使用者至群組以管理OSGi上的AEM Forms
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# OSGi群組和權限上的AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

您可以 [在AEM中](/help/sites-administering/user-group-ac-admin.md#group-administration) ，建立群組 [，並指派原則](/help/sites-administering/user-group-ac-admin.md#user-administration) 和使用者至群組。 這些原則可控制屬於群組的使用者的權限。

在您安裝 [AEM Forms附加套件後](../../forms/using/installing-configuring-aem-forms-osgi.md)，本文提及的群組（例如forms-user和forms-power-user）會自動可供指派。 下表列出使用者可根據群組指派，對OSGi上的AEM Forms執行的工作：

<table>
 <tbody>
  <tr>
   <td>群組</td> 
   <td>任務</td> 
  </tr>
  <tr>
   <td>forms-user <sup><a href="#main-pars-text">[1]</a></sup></td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈及提交最適化表單</li> 
     <li>建立、預覽和發佈互動式通訊和檔案片段</li> 
     <li>上傳資產至AEM例項</li> 
     <li>建立主題</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-user</td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈及提交最適化表單</li> 
     <li>建立、預覽和發佈互動式通訊和檔案片段</li> 
     <li>使用程式碼編輯器建立最適化表單的指令碼</li> 
     <li>上傳包含指令碼的資產</li> 
     <li>建立主題</li> 
     <li>包含XDP的導入包</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>審查提交內容</li> 
     <li>批准或拒絕提交</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>範本作者 <sup><a href="#main-pars-text">[2]</a></sup></td> 
   <td>
    <ul> 
     <li>建立並預覽最適化表單或互動式通訊範本</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>模板——用戶</td> 
   <td>
    <ul> 
     <li>建立並預覽最適化表單或互動式通訊範本</li> 
     <li>使用程式碼編輯器，為最適化表單或互動式通訊範本建立指令碼</li> 
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
     <li>使用Agent UI訪問通信管理信函或交互通信</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>工作流程編輯器</p> </td> 
   <td>
    <ul> 
     <li>建立收件箱應用程式</li> 
     <li>建立工作流程模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>使用AEM收件匣應用程式<br /><strong>注意：您必 </strong>須有cm-agent-users和workflow-users群組指派，才能存取AEM收件匣中的Interactive Communications Agent UI。</li> 
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

1. 具有表單使用者群組權限的使用者無法編寫最適化表單的指令碼。
1. 具有模板作者組權限的用戶無法編寫模板指令碼。

