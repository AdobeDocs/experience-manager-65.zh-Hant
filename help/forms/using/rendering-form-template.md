---
title: 轉譯 HTML5 表單的表單範本
description: HTML5表單設定檔與設定檔轉譯器相關聯。 設定檔轉譯器是JSP頁面，負責呼叫HTML OSGi服務來產生表單的Forms表示法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms,Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%
---
# 轉譯 HTML5 表單的表單範本 {#rendering-form-template-for-html-forms}

## 轉譯端點 {#render-endpoint}

HTML5表單具有&#x200B;**設定檔**&#x200B;的概念，此設定檔會公開為REST端點，以啟用表單範本的行動轉譯。 這些設定檔已關聯&#x200B;**設定檔轉譯器**。 這些是JSP頁面，負責呼叫HTML OSGi服務來產生Forms表單表示法。 「設定檔」節點的JCR路徑會決定轉譯器端點的URL。 指向「預設」設定檔之表單的預設轉譯端點看起來如下所示：

https://<*主機*>：<*連線埠*>/content/xfaforms/profiles/default.html?contentRoot=<*包含表單xdp*>&template=<*xdp*&#x200B;名稱的資料夾路徑

例如 `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

對於自訂設定檔，端點會據此變更。 例如，名稱為表單的自訂設定檔的端點是：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的範本位在名為FormSubmission的應用程式中的AEM存放庫，則URI會是：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 演算引數 {#render-parameters}

將表單轉譯為HTML時支援的請求引數包括：

<table>
 <tbody>
  <tr>
   <th><strong>參數 </strong></th>
   <th><strong>說明</strong></th>
  </tr>
  <tr>
   <td>範本<br /> </td>
   <td>此引數指定範本檔案的名稱。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>此引數會指定範本和相關資源所在的路徑。 此路徑可以是伺服器檔案系統路徑或存放庫路徑、http或ftp路徑。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此引數指定表單資料xml張貼到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 將資料與表單範本合併 {#merge-data-with-form-template}

| 參數 | 說明 |
|---|---|
| dataRef | 此引數指定與範本合併之資料檔案的&#x200B;**絕對路徑**。 此引數可以是Rest服務的URL，會以xml格式傳回資料。 |
| 資料 | 此引數會指定與範本合併的UTF-8編碼資料位元組。 如果指定此引數，HTML5表單會忽略dataRef引數。 |

### 傳遞轉譯器引數 {#passing-the-render-parameter}

HTML5 Forms支援三種傳遞轉譯器引數的方法。 您可以透過URL、索引鍵值配對和設定檔節點傳遞引數。 在轉譯器引數中，機碼值組擁有最高的優先順序，其後是設定檔節點。 URL要求引數的優先順序最低。

* **URL要求引數**：您可以在URL中指定轉譯器引數。 一般使用者可以在URL要求引數中看到引數。 例如，下列提交URL在URL中包含範本引數： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute要求引數**：您可以將轉譯器引數指定為機碼值組。 在SetAttribute要求引數中，一般使用者看不到這些引數。 您可以從任何其他JSP轉送要求至HTML5表單設定檔轉譯器JSP，並在要求物件上使用&#x200B;*setAttribute*&#x200B;以傳遞所有轉譯器引數。 此方法的優先順序最高。

* **設定檔節點要求引數：**&#x200B;您可以將轉譯器引數指定為設定檔節點的節點屬性。 一般使用者在設定檔節點請求引數中看不到引數。 設定檔節點是傳送請求的節點。 若要將引數指定為節點屬性，請使用CRXDE lite。

### 提交引數 {#submit-parameters}

HTML5 forms會提交資料；在AEM伺服器上執行伺服器端指令碼和網頁服務。 如需在AEM伺服器上執行伺服器端指令碼和Web服務所使用的引數的詳細資訊，請參閱[HTML5 Forms Service Proxy](/help/forms/using/service-proxy.md)。
