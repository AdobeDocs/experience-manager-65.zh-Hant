---
title: 工作總攬
seo-title: Assignments Essentials
description: 啟用社群的工作總攬功能概觀
seo-description: Assignments feature overview for enablement communities
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 12%

---

# 工作總攬 {#assignments-essentials}

閱讀以了解使用的工作任務功能的基本資訊 [啟用社群](/help/communities/overview.md#enablement-community) 網站。

指派功能是將啟用資源和學習路徑指派給啟用社群的成員。

## 用戶端的要點 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.beadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="/help/communities/assignments.md">工作總攬功能</a></td>
  </tr>
 </tbody>
</table>

### 完成和成功狀態 {#completion-and-success-status}

「完成」和「成功」狀態用於「工作總攬」上的報表和狀態橫幅。

完成狀態:

* 未指派
* 未開始（新）
* 進行中
* 完成

成功狀態:

* 未知
* 通過
* 失敗

完成和成功狀態的唯一可能組合是：

| **完成** | **成功** |
|---|---|
| 尚未開始 | 未知 |
| 進行中 | 未知 |
| 完成 | 通過 |
| 完成 | 失敗 |

## 伺服器端的Essentials {#essentials-for-server-side}

### 指定任務功能 {#assignments-function}

包含 [分配函式](/help/communities/functions.md#assignments-function)，包含已設定的 ` [assignments](/help/communities/assignments.md)` 元件。

### 參考API {#reference-apis}

* [啟用API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [報表API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [報表分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
