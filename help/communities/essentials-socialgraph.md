---
title: Social Graph Essentials
seo-title: Social Graph Essentials
description: follow component and following component overview
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---


# 社交圖表基本功能{#social-graph-essentials}

社區成員遵循[活動](essentials-activities.md)以及遵循的能力通過以下兩個組成部分建立：

`following`元件必須與另一個資源關聯，而且此關聯已為[社區站點](overview.md#communitiessites)中現有社區成員和功能建立。

`following`元件列出當前成員後面或當前成員後面的成員。 此社交圖表包含在為社群網站建立的使用者設定檔中。

## 客戶端{#essentials-for-client-side}的基本功能

### 關注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationss</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱<a href="socialgraph.md">使用社交圖表</a></td>
  </tr>
  <tr>
   <td><strong> optional<br /> property</strong></td>
   <td>
    <ul>
     <li>名稱: <strong><code>outgoing</code></strong></li>
     <li>類型：布林值</li>
     <li>值:<br />
      <ul>
       <li><i>True  </i>-組 <code>following</code> 件將列出當前登錄成員的成員 <code>follows</code></li>
       <li><i>False  </i>-組 <code>following</code> 件將列出當前登 <code>follow </code>錄成員的成員</li>
      </ul> </li>
    </ul> <p>如果屬性遺失，則預設為<i>true</i>。 目前，無法使用作者模式中的編輯對話框來設定此屬性。 必須使用<a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>將屬性添加到<code>following </code>節點的實例。</p> </td>
  </tr>
 </tbody>
</table>

### 關注 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**included**](scf.md#add-or-include-a-communities-component) | 否 |
| **模板** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的基本工具

* [社交圖形API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交圖形端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [伺服器端自訂](server-customize.md)

