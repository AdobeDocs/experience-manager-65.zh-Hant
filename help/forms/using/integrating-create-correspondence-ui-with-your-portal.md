---
title: 將建立通訊UI與您的自訂入口網站整合
description: 瞭解如何將建立通訊UI與您的自訂入口網站整合
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# 將建立通訊UI與您的自訂入口網站整合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概觀 {#overview}

本文詳細說明如何將建立通訊解決方案與您的環境整合。

## URL型引動過程 {#url-based-invocation}

從自訂入口網站呼叫「建立通訊」應用程式的一種方法是使用下列請求引數準備URL：

* 信函範本的識別碼（使用cmLetterId引數）。

* 從所需資料來源擷取的XML資料的URL （使用cmDataUrl引數）。

例如，自訂入口網站會將URL準備為\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，可能是入口網站連結中的href。

>[!NOTE]
>
>以這種方式呼叫並不安全，因為必要的引數會作為GET請求傳遞，方法是在URL中公開相同的（明顯可見）。

>[!NOTE]
>
>在呼叫「建立通訊」應用程式之前，請儲存並上傳資料以在指定的dataURL呼叫「建立通訊」UI。 您可以從自訂入口網站本身或透過另一個後端程式執行此操作。

## 內嵌資料型引動過程 {#inline-data-based-invocation}

呼叫建立通訊應用程式的另一個（也是更安全的）方法可能是，直接點選https://&#39;[伺服器]：[連線埠]&#39;/[contextPath]/aem/forms/createcorrespondence.html的URL，同時傳送引數和資料以呼叫建立通訊應用程式作為POST要求（對一般使用者隱藏它們）。 這也表示您現在可以內嵌傳遞「建立對應」應用程式的XML資料（作為相同請求的一部分，使用cmData引數），這在先前的方法中是不可能的/理想的作法。

### 指定字母的引數 {#parameters-for-specifying-letter}

| **名稱** | **類型** | **說明** |
|---|---|---|
| cmLetterInstanceId | 字串 | 信件例項的識別碼。 |
| cmLetterId | 字串 | 信函範本的名稱。 |

表格中引數的順序會指定用來載入字母的引數偏好設定。

### 用於指定XML資料來源的引數 {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td> 
   <td><strong>類型</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>使用基本通訊協定（例如cq、ftp、http或檔案）的來源檔案中的XML資料。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字串</td> 
   <td>使用信件例項中可用的xml資料。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布林值</td> 
   <td>重複使用資料字典中附加的測試資料。</td> 
  </tr>
 </tbody>
</table>

表格中引數的順序會指定用來載入XML資料的引數偏好設定。

### 其他引數 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td> 
   <td><strong>類型</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布林值</td> 
   <td>True表示在預覽模式中開啟字母<br /> </td> 
  </tr>
  <tr>
   <td>隨機</td> 
   <td>時間戳記</td> 
   <td>解決瀏覽器快取問題。</td> 
  </tr>
 </tbody>
</table>

如果您使用cmDataURL的http或cq通訊協定，應可匿名存取http/cq的URL。
