---
title: 整合建立對應UI與您的自訂入口網站
seo-title: 整合建立對應UI與您的自訂入口網站
description: 瞭解如何將建立通訊UI與您的自訂入口網站整合
seo-description: 瞭解如何將建立通訊UI與您的自訂入口網站整合
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# 整合建立對應UI與您的自訂入口網站{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概覽 {#overview}

本文詳細說明如何將「建立通信解決方案」與您的環境整合。

## 以URL為基礎的呼叫 {#url-based-invocation}

從自訂入口網站呼叫「建立對應」應用程式的一種方式，是使用下列請求參數來準備URL:

* 字母範本的識別碼（使用cmLetterId參數）。

* 從所需資料來源擷取的XML資料的URL（使用cmDataUrl參數）。

例如，自訂入口網站會將URL準備為\
`https://[server]:[port]/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，這可以是入口網站上連結的href。

>[!NOTE]
>
>以此方式呼叫並不安全，因為必要的參數會隨GET要求傳遞，方法是在URL中顯示相同（清楚可見）。

>[!NOTE]
>
>在呼叫「建立對應」應用程式之前，儲存並上傳資料，以在指定dataURL呼叫「建立對應」UI。 這可從自訂入口網站本身或透過另一個後端程式完成。

## 內嵌資料式呼叫 {#inline-data-based-invocation}

另一個（也是更安全的）呼叫「建立對應」應用程式的方式是，只要點擊https://[server]:port[/]contextPath[]/aem/forms/createcorrespondence.html的URL，同時傳送參數和資料以POST要求呼叫「建立對應」應用程式（隱藏於使用者）。 這也表示您現在可以將XML資料傳遞至內嵌的「建立對應」應用程式（使用cmData參數做為相同要求的一部分），這在先前的方法中是不可能的／理想的。

### 用於指定字母的參數 {#parameters-for-specifying-letter}

| **名稱** | **類型** | **說明** |
|---|---|---|
| cmLetterInstanceId | 字串 | 字母實例的標識符。 |
| cmLetterId | 字串 | 字母模板的名稱。 |

表中參數的順序指定用於載入字母的參數的首選項。

### 指定XML資料來源的參數 {#parameters-for-specifying-the-xml-data-source}

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
   <td>使用基本通訊協定（例如cq、ftp、http或檔案）從來源檔案取得XML資料。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字串</td> 
   <td>使用字母實例中可用的xml資料。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布林值 (Boolean)</td> 
   <td>重複使用資料字典中附加的測試資料。</td> 
  </tr>
 </tbody>
</table>

表中參數的順序指定用於載入XML資料的參數的首選項。

### 其他參數 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td> 
   <td><strong>類型</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布林值 (Boolean)</td> 
   <td>True可在預覽模式中開啟字母<br /> </td> 
  </tr>
  <tr>
   <td>隨機</td> 
   <td>時間戳記</td> 
   <td>若要解決瀏覽器快取問題。</td> 
  </tr>
 </tbody>
</table>

如果您對cmDataURL使用http或cq通訊協定，http/cq的URL應匿名存取。
