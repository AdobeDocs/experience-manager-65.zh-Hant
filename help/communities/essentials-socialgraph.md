---
title: 社會圖表要點
seo-title: Social Graph Essentials
description: 後續元件和後續元件概述
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

# 社會圖表要點  {#social-graph-essentials}

社區成員遵循的能力 [活動](essentials-activities.md) 並通過兩個部分建立：

的 `following` 元件必須與另一個資源關聯，並且此關聯已針對中的現有社區成員和功能建立 [社區站點](overview.md#communitiessites)。

的 `following` 元件列出當前成員後面或當前成員後面的成員。 在為社區站點建立的用戶配置檔案中包括成員之間關係的社會圖形。

## 客戶端基本知識 {#essentials-for-client-side}

### 關注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社交/社交圖/元件/hbs/關係</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="socialgraph.md">使用社交圖</a></td>
  </tr>
  <tr>
   <td><strong> 可選<br /> 屬性</strong></td>
   <td>
    <ul>
     <li>名稱: <strong><code>outgoing</code></strong></li>
     <li>類型：布爾型</li>
     <li>值:<br />
      <ul>
       <li><i>真 </i>- <code>following</code> 元件將列出當前登錄成員的成員 <code>follows</code></li>
       <li><i>假 </i>- <code>following</code> 元件將列出 <code>follow </code>當前已登錄的成員</li>
      </ul> </li>
    </ul> <p>預設為 <i>真</i> 的子菜單。 當前，無法在作者模式下使用編輯對話框設定此屬性。 必須將屬性添加到的實例 <code>following </code>節點使用 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>。</p> </td>
  </tr>
 </tbody>
</table>

### 關注 {#follow}

| **資源類型** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**包含**](scf.md#add-or-include-a-communities-component) | 否 |
| **模板** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **cs** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [社交圖API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交圖終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [伺服器端自定義](server-customize.md)
