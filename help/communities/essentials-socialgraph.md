---
title: 社交圖基本資訊
description: 瞭解以下元件和以下元件。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 2%

---

# 社交圖基本資訊  {#social-graph-essentials}

社群成員可關注的功能 [活動](essentials-activities.md) 並遵循透過兩個元件建立：

此 `following` 元件必須與另一個資源相關聯，而且此關聯已針對中的現有Communities成員和功能建立 [社群網站](overview.md#communitiessites).

此 `following` 元件會列出目前成員之後的成員，或目前成員之後的成員。 此成員間關係的社交圖表包含在為社群網站建立的使用者個人資料中。

## 使用者端的Essentials {#essentials-for-client-side}

### 關注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationships</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
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
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>另請參閱 <a href="socialgraph.md">使用社交圖</a></td>
  </tr>
  <tr>
   <td><strong> 可選<br /> 屬性</strong></td>
   <td>
    <ul>
     <li>名稱: <strong><code>outgoing</code></strong></li>
     <li>型別：布林值</li>
     <li>值:<br />
      <ul>
       <li><i>真 </i>- <code>following</code> 元件會列出登入的成員 <code>follows</code></li>
       <li><i>假 </i>- <code>following</code> 元件會列出符合以下條件的成員 <code>follow </code>登入會員</li>
      </ul> </li>
    </ul> <p>預設為 <i>true</i> 如果屬性遺失。 無法在作者模式中使用編輯對話方塊設定此屬性。 必須將屬性新增至 <code>following</code> 節點使用 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 關注 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**包含**](scf.md#add-or-include-a-communities-component) | 否 |
| **範本** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [社交圖API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交圖端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [伺服器端自訂](server-customize.md)
