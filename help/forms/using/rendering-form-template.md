---
title: 用於HTML5個表單的呈現表單模板
seo-title: Rendering form template for HTML5 forms
description: HTML5表單配置檔案與配置檔案呈現關聯。 配置檔案呈現是JSP頁，通過調用FormsOSGi服務來生成表單的HTML表示。
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

# 用於HTML5個表單的呈現表單模板 {#rendering-form-template-for-html-forms}

## 呈現終結點 {#render-endpoint}

HTML5的形式 **配置檔案** 以REST端點形式公開，以啟用表單模板的移動呈現。 這些配置檔案已關聯 **配置檔案呈現器**。 它們是JSP頁，通過調用FormsOSGi服務來生成表單的HTML表示。 「配置檔案」節點的JCR路徑確定呈現端點的URL。 指向「default」配置檔案的表單的預設渲染端點如下所示：

https://&lt;*主機*>:&lt;*埠*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*包含xdp的資料夾的路徑*>&amp;template=&lt;*xdp的名稱*>

例如 `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

對於自定義配置檔案，端點會相應更改。 例如，具有名稱hrforms的自定義配置檔案的終點是：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果模板駐留在名AEM為FormSubmission的應用程式的儲存庫中，則URI為：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 渲染參數 {#render-parameters}

將表單呈現為HTML時支援的請求參數包括：

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
   <td>內容根<br /> </td>
   <td>此參數指定模板和關聯資源所在的路徑。 此路徑可以是伺服器檔案系統路徑或儲存庫路徑、http或ftp路徑。<br /> </td>
  </tr>
  <tr>
   <td>提交URL<br /> </td>
   <td>此參數指定表單資料xml發佈到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 將資料與表單模板合併 {#merge-data-with-form-template}

| 參數 | 說明 |
|---|---|
| 資料引用 | 此參數指定 **絕對路徑** 與模板合併的資料檔案。 此參數可以是以xml格式返回資料的余料服務的URL。 |
| 資料 | 此參數指定與模板合併的UTF-8編碼資料位元組。 如果指定此參數，則HTML5表單將忽略dataRef參數。 |

### 傳遞呈現參數 {#passing-the-render-parameter}

HTML5表單支援三種傳遞渲染參數的方法。 可以通過URL、鍵值對和配置檔案節點傳遞參數。 在render參數中，鍵值對具有最高優先順序，後跟配置檔案節點。 URL請求參數的優先順序最低。

* **URL請求參數**:可以在URL中指定呈現參數。 在URL請求參數中，參數對最終用戶可見。 例如，以下提交URL在URL中包含模板參數： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute請求參數**:可以將渲染參數指定為鍵值對。 在SetAttribute請求參數中，參數對最終用戶不可見。 您可以將請求從任何其它JSP轉發到HTML5表單配置檔案呈現器JSP並使用 *setAttribute* on request對象傳遞所有呈現參數。 此方法具有最高優先順序。

* **配置檔案節點請求參數：** 可以將渲染參數指定為配置檔案節點的節點屬性。 在配置檔案節點請求參數中，參數對最終用戶不可見。 配置檔案節點是發送請求的節點。 要將參數指定為節點屬性，請使用CRXDE lite。

### 提交參數 {#submit-parameters}

HTML5個表格提交資料；在伺服器上執行伺服器端指令碼和WebAEM服務。 有關用於在伺服器上執行伺服器端指令碼和Web服務的參數的詳細信AEM息，請參見 [HTML5表單服務代理](/help/forms/using/service-proxy.md)。
