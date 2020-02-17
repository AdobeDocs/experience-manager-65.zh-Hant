---
title: Assignments Essentials
seo-title: Assignments Essentials
description: 啟用社群的工作功能總覽
seo-description: 啟用社群的工作功能總覽
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Assignments Essentials{#assignments-essentials}

閱讀以瞭解使用啟用社群網站的指派功能的 [必要資訊](/help/communities/overview.md#enablement-community) 。

指派功能是將啟用資源和學習路徑指派給啟用社群成員的能力。

## 用戶端基本功能 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參 <a href="/help/communities/assignments.md">閱指派功能</a></td>
  </tr>
 </tbody>
</table>

### 完成與成功狀態 {#completion-and-success-status}

「工作總攬」的報表和狀態橫幅會使用「完成」和「成功」狀態。

完成狀態:

* 未指派
* 未開始（新）
* 進行中
* 完成

成功狀態:

* 未知
* 通過
* 失敗

「完成」和「成功狀態」的唯一可能組合為：

| **完成** | **成功** |
|---|---|
| 尚未開始 | 未知 |
| 進行中 | 未知 |
| 完成 | 通過 |
| 完成 | 失敗 |

## 伺服器端的基本功能 {#essentials-for-server-side}

### 指定任務功能 {#assignments-function}

包含「工作總攬」功能的社 [群網站結構](/help/communities/functions.md#assignments-function)，包含已設定的 ` [assignments](/help/communities/assignments.md)` 元件。

### 參考API {#reference-apis}

* [啟用API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [報告API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [報告分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

