---
title: 將建立通信UI與自定義門戶整合
seo-title: Integrating Create Correspondence UI with your custom portal
description: 瞭解如何將建立通信UI與自定義門戶整合
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# 將建立通信UI與自定義門戶整合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概觀 {#overview}

本文詳細介紹了如何將建立通信解決方案與您的環境整合。

## 基於URL的調用 {#url-based-invocation}

從自定義門戶調用「建立對應」應用程式的一種方法是使用以下請求參數準備URL:

* 字母模板的標識符（使用cmLetterId參數）。

* 從所需資料源（使用cmDataUrl參數）獲取的XML資料的URL。

例如，自定義門戶將準備URL為\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，可能是入口連結的href。

>[!NOTE]
>
>通過在URL中顯示相同（明顯可見），以這種方式調用是不安全的，因為必需的參數作為GET請求傳遞。

>[!NOTE]
>
>在調用「建立對應」應用程式之前，保存並上載資料，以在給定dataURL上調用「建立對應」UI。 這可以通過自定義門戶本身或通過另一個後端過程來完成。

## 基於內聯資料的調用 {#inline-data-based-invocation}

調用「建立通信」應用程式的另一種（而且更安全）方法是，只需點擊https://&#39;上的URL即可[伺服器]:[埠]&#39;/[上下文路徑]/aem/forms/createcorrespondence.html ，同時發送參數和資料以作為POST請求調用「建立對應」應用程式（將其隱藏在最終用戶面前）。 這還意味著您現在可以以內聯方式（作為同一請求的一部分，使用cmData參數）傳遞Create Tergement應用程式的XML資料，這在以前的方法中是不可能的/不理想的。

### 用於指定字母的參數 {#parameters-for-specifying-letter}

| **名稱** | **類型** | **說明** |
|---|---|---|
| cmLetterInstanceId | 字串 | 字母實例的標識符。 |
| cmLetterId | 字串 | 字母模板的名稱。 |

表中參數的順序指定了用於載入字母的參數的首選項。

### 用於指定XML資料源的參數 {#parameters-for-specifying-the-xml-data-source}

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
   <td>使用基本協定（如cq、ftp、http或檔案）從源檔案獲取的XML資料。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字串</td> 
   <td>使用字母實例中可用的xml資料。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布林值</td> 
   <td>重用資料字典中附加的test資料。</td> 
  </tr>
 </tbody>
</table>

表中參數的順序指定了用於載入XML資料的參數的首選項。

### 其他參數 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td> 
   <td><strong>類型</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>cm預覽<br /> </td> 
   <td>布林值</td> 
   <td>為True以預覽模式開啟字母<br /> </td> 
  </tr>
  <tr>
   <td>隨機</td> 
   <td>時間戳</td> 
   <td>解決瀏覽器快取問題。</td> 
  </tr>
 </tbody>
</table>

如果對cmDataURL使用http或cq協定，則應匿名訪問http/cq的URL。
