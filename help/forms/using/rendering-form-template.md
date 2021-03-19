---
title: HTML5表單的轉換表單範本
seo-title: HTML5表單的轉換表單範本
description: HTML5表單描述檔會與描述檔轉譯相關聯。 描述檔轉譯是負責呼叫FormsOSGi服務來產生表單HTML表示的JSP頁面。
seo-description: HTML5表單描述檔會與描述檔轉譯相關聯。 描述檔轉譯是負責呼叫FormsOSGi服務來產生表單HTML表示的JSP頁面。
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: 行動表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---


# HTML5表單的轉換表單範本{#rendering-form-template-for-html-forms}

## 渲染端點{#render-endpoint}

HTML5表單的概念是&#x200B;**描述檔**，這些描述檔公開為REST端點，以啟用表單範本的行動轉譯。 這些配置檔案具有關聯的&#x200B;**配置檔案渲染器**。 它們是JSP頁面，負責呼叫FormsOSGi服務，以產生表單的HTML表示。 「描述檔」節點的JCR路徑會決定演算端點的URL。 指向「預設」描述檔的表單的預設演算端點看起來如下：

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*包含xdp*>的資料夾路徑&amp;template=*xdp*&#x200B;名稱

例如， `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

對於自訂描述檔，端點會隨之變更。 例如，名稱為hrforms的自訂描述檔的端點為：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果模板駐留在名為FormSubmission的AEM應用程式的儲存庫中，則URI為：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 渲染參數{#render-parameters}

將表單轉譯為HTML時支援的請求參數包括：

<table>
 <tbody>
  <tr>
   <th><strong>參數 </strong></th>
   <th><strong>說明</strong></th>
  </tr>
  <tr>
   <td>範本<br /> </td>
   <td>此參數指定模板檔案的名稱。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>此參數指定模板和相關資源所在的路徑。 此路徑可以是伺服器檔案系統路徑或儲存庫路徑或http或ftp路徑。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此參數指定張貼表單資料xml的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 合併資料與表單範本{#merge-data-with-form-template}

| 參數 | 說明 |
|---|---|
| dataRef | 此參數指定與模板合併的資料檔案的&#x200B;**絕對路徑**。 此參數可以是剩餘服務傳回xml格式資料的URL。 |
| 資料 | 此參數指定與範本合併的UTF-8編碼資料位元組。 如果指定此參數，HTML5表單會忽略dataRef參數。 |

### 傳遞演算參數{#passing-the-render-parameter}

HTML5表格支援三種傳遞演算參數的方法。 您可以透過URL、鍵值配對和描述檔節點傳遞參數。 在render參數中，鍵值對的優先順序最高，後跟配置檔案節點。 「URL請求」參數的優先順序最低。

* **URL請求參數**:您可以在URL中指定演算參數。在URL請求參數中，參數對一般使用者可見。 例如，下列提交URL在URL中包含範本參數：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute請求參數**:可以將渲染參數指定為鍵值對。在SetAttribute請求參數中，參數對最終用戶不可見。 您可以從任何其他JSP將請求轉發到HTML5表單描述檔轉譯器JSP，並在請求物件上使用&#x200B;*setAttribute*&#x200B;來傳遞所有演算參數。 此方法的優先順序最高。

* **配置檔案節點請求參** 數：可以將渲染參數指定為配置檔案節點的節點屬性。在描述檔節點請求參數中，一般使用者看不到這些參數。 描述檔節點是傳送請求的節點。 要將參數指定為節點屬性，請使用CRXDE lite。

### 提交參數{#submit-parameters}

HTML5表單提交資料；在伺服器上執行伺服器端指令碼和webAEM服務。 有關用於在伺服器上執行伺服器端指令碼和web-services的參數的詳細信AEM息，請參見[HTML5 forms Service Proxy](/help/forms/using/service-proxy.md)。
