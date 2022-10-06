---
title: 社交圖表要點
seo-title: Social Graph Essentials
description: 後續元件和下列元件概觀
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# 社交圖表要點  {#social-graph-essentials}

社群成員遵循的能力 [活動](essentials-activities.md) 並透過兩個元件來建立：

此 `following` 元件必須與另一個資源關聯，並且此關聯已針對 [社群網站](overview.md#communitiessites).

此 `following` 元件列出當前成員後面或當前成員後面的成員。 此社交圖形中，成員之間關係包含在為社群網站建立的使用者設定檔中。

## 用戶端的要點 {#essentials-for-client-side}

### 關注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationships</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="socialgraph.md">使用社交圖表</a></td>
  </tr>
  <tr>
   <td><strong> 可選<br /> 屬性</strong></td>
   <td>
    <ul>
     <li>名稱: <strong><code>outgoing</code></strong></li>
     <li>類型：布林值</li>
     <li>值:<br />
      <ul>
       <li><i>True </i>- <code>following</code> 元件將列出當前登錄成員的成員 <code>follows</code></li>
       <li><i>False </i>- <code>following</code> 元件將列出 <code>follow </code>當前已登錄的成員</li>
      </ul> </li>
    </ul> <p>預設為 <i>true</i> 如果屬性遺失。 目前，無法在製作模式中使用編輯對話方塊來設定此屬性。 屬性必須新增至的例項 <code>following </code>節點使用 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 關注 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**包括**](scf.md#add-or-include-a-communities-component) | 否 |
| **範本** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **cs** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [用戶端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [社交圖表API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交圖表端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [伺服器端自訂](server-customize.md)
