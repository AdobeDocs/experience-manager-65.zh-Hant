---
title: 檔案程式庫基本需知
description: 瞭解在Adobe Experience Manager社群中使用檔案庫功能的基礎知識。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6d653331-c1ce-4ccb-bb45-656b6413ac3e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# 檔案程式庫基本需知 {#file-library-essentials}

本頁提供使用檔案庫功能的基本資訊。

## 使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/filelibrary/components/hbs/filelibrary</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱<a href="file-library.md">檔案庫功能</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [檔案庫API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [檔案庫端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 檔案庫功能 {#file-library-function}

包含[檔案庫函式](functions.md#file-library-function)的社群網站結構包含已設定的`file library`元件。

### 存取針對檔案庫(UGC)張貼的評論 {#accessing-comments-posted-for-file-libraries-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
請參閱[仲裁使用者產生的內容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用UGC的[公用存放區](working-with-srp.md)時，無論選擇的存放區選項（例如ASRP、MSRP或JSRP）為何，都可程式化存取UGC。

**存放庫中UGC的位置和格式可能會變更，而不會出現警告**。

請參閱：

* [儲存資源提供者概觀](srp.md) — 簡介和存放庫使用概觀。
* [SRP與UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
