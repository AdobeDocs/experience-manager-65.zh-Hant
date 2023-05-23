---
title: 檔案庫軟體包
seo-title: File Library Essentials
description: 使用檔案庫功能
seo-description: Working with the file library feature
uuid: 0630f13e-97b4-4f93-9dce-07f559287c29
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9019b967-fff8-4dda-bc5a-fd4a3e14a4ef
exl-id: 6d653331-c1ce-4ccb-bb45-656b6413ac3e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 檔案庫軟體包 {#file-library-essentials}

此頁提供了使用檔案庫功能的基本資訊。

## 客戶端基本知識 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td>社交/檔案庫/元件/hbs/檔案庫</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>客戶端</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs投票<br /> cq.social.hbs.filebrary</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="file-library.md">檔案庫功能</a></td>
  </tr>
 </tbody>
</table>

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [檔案庫API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [檔案庫端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 檔案庫功能 {#file-library-function}

包含該社區站點結構的 [檔案庫函式](functions.md#file-library-function)，包括已配置 `file library` 元件。

### 訪問已發佈的檔案庫注釋(UGC) {#accessing-comments-posted-for-file-libraries-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將不建議使用的實用程式方法映射到當前SRP實用程式方法。
