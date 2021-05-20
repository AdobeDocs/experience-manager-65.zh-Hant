---
title: 轉譯HTML5表單的表單範本
seo-title: 轉譯HTML5表單的表單範本
description: HTML5表單描述檔與描述檔轉譯相關聯。 「描述檔轉譯」是JSP頁面，負責呼叫Forms OSGi服務來產生表單的HTML表示。
seo-description: HTML5表單描述檔與描述檔轉譯相關聯。 「描述檔轉譯」是JSP頁面，負責呼叫Forms OSGi服務來產生表單的HTML表示。
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: 行動表單
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 呈現HTML5表單的表單模板{#rendering-form-template-for-html-forms}

## 呈現終結點{#render-endpoint}

HTML5表單的概念為&#x200B;**Profiles**，這些表單以REST端點形式公開，以啟用表單範本的行動轉譯。 這些配置式具有關聯的&#x200B;**配置式呈現器**。 它們是JSP頁面，負責呼叫Forms OSGi服務，以產生表單的HTML表示。 「配置檔案」節點的JCR路徑決定渲染終點的URL。 指向「預設」配置檔案的表單的預設渲染端點看起來類似：

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*包含xdp*>&amp;template=&lt;*xdp*&#x200B;名稱的資料夾路徑

例如， `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

對於自訂設定檔，端點會據此變更。 例如，具有名稱hrforms的自訂設定檔的端點為：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的模板位於名為FormSubmission的應用程式的AEM儲存庫中，則URI為：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 呈現參數{#render-parameters}

以HTML呈現表單時支援的請求參數為：

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
   <td>此參數指定模板和關聯資源所在的路徑。 此路徑可以是伺服器檔案系統路徑或儲存庫路徑、http或ftp路徑。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此參數指定將表單資料xml發佈到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 將資料與表單模板合併{#merge-data-with-form-template}

| 參數 | 說明 |
|---|---|
| dataRef | 此參數指定與模板合併的資料檔案的&#x200B;**絕對路徑**。 此參數可以是rest服務傳回xml格式資料的URL。 |
| 資料 | 此參數指定與範本合併的UTF-8編碼資料位元組。 如果指定了此參數，HTML5表單將忽略dataRef參數。 |

### 傳遞呈現參數{#passing-the-render-parameter}

HTML5表單支援三種傳遞轉譯參數的方法。 您可以透過URL、索引鍵值配對和設定檔節點傳遞參數。 在轉譯參數中，索引鍵值配對的優先順序最高，其次是設定檔節點。 URL要求參數的優先順序最低。

* **URL要求參數**:您可以在URL中指定轉譯參數。在URL要求參數中，一般使用者可看到參數。 例如，下列提交URL在URL中包含範本參數：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute請求參數**:可以將渲染參數指定為鍵值對。在SetAttribute請求參數中，最終用戶看不到這些參數。 您可以將任何其他JSP的請求轉發到HTML5表單配置檔案轉譯器JSP，並對請求對象使用&#x200B;*setAttribute*&#x200B;以傳遞所有渲染參數。 此方法的優先順序最高。

* **設定檔節點請求參數：** 您可以將演算參數指定為設定檔節點的節點屬性。在設定檔節點要求參數中，一般使用者看不到這些參數。 設定檔節點是傳送請求的節點。 要將參數指定為節點屬性，請使用CRXDE lite。

### 提交參數{#submit-parameters}

HTML5表單提交資料；在AEM伺服器上執行伺服器端指令碼和web服務。 有關用於在AEM伺服器上執行伺服器端指令碼和Web服務的參數的詳細資訊，請參閱[HTML5表單服務代理](/help/forms/using/service-proxy.md)。
