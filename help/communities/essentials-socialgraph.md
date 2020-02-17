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
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Social Graph Essentials {#social-graph-essentials}

社區成員可以通過兩個 [構成](essentials-activities.md) ，來開展和開展活動：

組 `follow`件必須與其他資源關聯，並且此關聯已為社區站點中現有的社區成員和功能 [建立](overview.md#communitiessites)。

組 `following`件列出當前成員後面或當前成員後面的成員。 此社交圖表包含在為社群網站建立的使用者設定檔中。

## 用戶端基本功能 {#essentials-for-client-side}

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
   <td>請參 <a href="socialgraph.md">閱使用社交圖表</a></td>
  </tr>
  <tr>
   <td><strong> optional<br /> property</strong></td>
   <td>
    <ul>
     <li>名稱: <strong><code>outgoing</code></strong></li>
     <li>類型：布林值</li>
     <li>值:<br />
      <ul>
       <li><i>true </i>-組 <code>following</code> 件將列出當前已登錄成員的成員 <code>follows</code></li>
       <li><i>false </i>-組 <code>following</code> 件將列出當前登 <code>follow </code>錄成員的成員</li>
      </ul> </li>
    </ul> <p>如果 <i>屬性遺失</i> ，則預設為true。 目前，無法使用作者模式中的編輯對話框來設定此屬性。 必須使用 <code>following </code>CRXDE|Lite將屬性添加到節 <a href="../../help/sites-developing/developing-with-crxde-lite.md">點的實</a>例中。</p> </td>
  </tr>
 </tbody>
</table>

### 關注 {#follow}

| **resourceType** | social/socialgraph/components/hbs/following |
|---|---|
| [**included **](scf.md#add-or-include-a-communities-component) | 否 |
| **模板** | /libs/social/socialgraph/components/hbs/following/following.hbs |
| **css** | /libs/social/socialgraph/components/hbs/following/clientlibs/following.css |

* [用戶端自訂](client-customize.md)

## 伺服器端的基本功能 {#essentials-for-server-side}

* [社交圖形API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交圖形端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [伺服器端自訂](server-customize.md)

