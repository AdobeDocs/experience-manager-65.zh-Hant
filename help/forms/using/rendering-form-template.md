---
title: 轉譯HTML5表單範本
seo-title: Rendering form template for HTML5 forms
description: HTML5表單設定檔與設定檔轉譯相關聯。 配置檔案呈現是JSP頁，通過調用Forms OSGi服務生成表單的HTML表示。
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# 轉譯HTML5表單範本 {#rendering-form-template-for-html-forms}

## 呈現端點 {#render-endpoint}

HTML5表單的概念是 **設定檔** 以REST端點形式公開，以啟用表單範本的行動轉譯。 這些設定檔已建立關聯 **描述檔轉譯器**. 它們是JSP頁面，負責借由呼叫Forms OSGi服務來產生表單的HTML表示。 「配置檔案」節點的JCR路徑決定渲染終點的URL。 指向「預設」配置檔案的表單的預設渲染端點看起來類似：

https://&lt;*主機*>:&lt;*埠*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*包含xdp的資料夾路徑*>&amp;template=&lt;*xdp的名稱*>

例如， `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

對於自訂設定檔，端點會據此變更。 例如，具有名稱hrforms的自訂設定檔的端點為：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的模板位於名為FormSubmission的應用程式的AEM儲存庫中，則URI為：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 呈現參數 {#render-parameters}

以HTML形式呈現表單時支援的請求參數為：

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
   <td>此參數指定模板和關聯資源所在的路徑。 此路徑可以是伺服器檔案系統路徑、存放庫路徑、http或ftp路徑。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此參數指定張貼表單資料xml的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 將資料與表單範本合併 {#merge-data-with-form-template}

| 參數 | 說明 |
|---|---|
| dataRef | 此參數會指定 **絕對路徑** 與範本合併的資料檔案。 此參數可以是rest服務傳回xml格式資料的URL。 |
| 資料 | 此參數指定與範本合併的UTF-8編碼資料位元組。 如果指定了此參數，HTML5表單將忽略dataRef參數。 |

### 傳遞轉譯參數 {#passing-the-render-parameter}

HTML5表單支援三種傳遞轉譯參數的方法。 您可以透過URL、索引鍵值配對和設定檔節點傳遞參數。 在轉譯參數中，索引鍵值配對的優先順序最高，其次是設定檔節點。 URL要求參數的優先順序最低。

* **URL要求參數**:您可以在URL中指定轉譯參數。 在URL要求參數中，一般使用者可看到參數。 例如，下列提交URL在URL中包含範本參數： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute請求參數**:可以將渲染參數指定為鍵值對。 在SetAttribute請求參數中，最終用戶看不到這些參數。 您可以將任何其他JSP的請求轉發到HTML5表單配置檔案轉譯器JSP，並使用 *setAttribute* 請求物件，以傳遞所有轉譯參數。 此方法的優先順序最高。

* **設定檔節點請求參數：** 您可以將呈現參數指定為配置檔案節點的節點屬性。 在設定檔節點要求參數中，一般使用者看不到這些參數。 設定檔節點是傳送請求的節點。 要將參數指定為節點屬性，請使用CRXDE lite。

### 提交參數 {#submit-parameters}

HTML5表單提交資料；在AEM伺服器上執行伺服器端指令碼和web服務。 有關在AEM伺服器上執行伺服器端指令碼和Web服務所使用的參數的詳細資訊，請參見 [HTML5表單服務代理](/help/forms/using/service-proxy.md).
