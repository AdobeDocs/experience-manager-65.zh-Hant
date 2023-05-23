---
title: HTML5表單服務代理
seo-title: HTML5 forms service proxy
description: HTML5表單服務代理是註冊提交服務的代理的配置。 要配置服務代理，請通過request參數submissionServiceProxy指定提交服務的URL。
seo-description: HTML5 forms Service Proxy is a configuration to register a proxy for the submission service. To configure Service Proxy, specify the URL of submission service through request parameter submissionServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# HTML5表單服務代理{#html-forms-service-proxy}

HTML5表單服務代理是註冊提交服務的代理的配置。 要配置服務代理，請通過request參數指定提交服務的URL *submissionServiceProxy*。

## 服務代理的優勢 {#benefits-of-service-proxy-br}

服務代理消除了以下內容：

* HTML5表單工作流要求為HTML5表單用戶開啟提交服務「/content/xfaforms/submission/default」。 它使伺服器AEM面向更廣泛的意外受眾。
* 服務URL被嵌入到表單的運行時模型中。 無法更改服務URL路徑。
* 提交過程分為兩步。 要提交表單資料，提交至少需要兩次到伺服器。 因此，增加了伺服器上的負載。
* HTML5表單在POST請求中發送資料，而不是PDF請求。 對於涉及PDF和HTML5表單的工作流，需要兩種不同的處理提交的方法。

### 拓撲 {#topologies-br}

HTML5表單可以使用以下拓撲連接到服AEM務器。

* 一種拓撲，AEM伺服器或HTML5表單通過POST將資料發送到伺服器。
* 代理伺服器將POST資料發送到伺服器的拓撲。

![HTML5形式服務代理拓撲](assets/topology.png)

HTML5形式服務代理拓撲

HTML5表單連AEM接到伺服器以運行伺服器端指令碼、 Web服務和提交。 HTML5表單的XFA運行時使用「/bin/xfaforms/submitaction」端點上的Ajax調用以及各種參數連接到服AEM務器。 HTML5表AEM單連接伺服器以執行以下操作：

#### 執行伺服器端指令碼和Web服務 {#execute-server-sided-scripts-and-web-services}

標籤為在伺服器上運行的指令碼稱為伺服器端指令碼。 下表列出了在伺服器端指令碼和Web服務中使用的所有參數。

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>活動</p> </td>
   <td><p>活動包含觸發請求的事件。 如按一下、退出或更改</p> </td>
  </tr>
  <tr>
   <td><p>上下文索姆</p> </td>
   <td><p>contextSom包含執行事件的對象的SOM表達式。</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>模板包含用於呈現表單的模板。</p> </td>
  </tr>
  <tr>
   <td><p>內容根</p> </td>
   <td><p>contentRoot包含用於呈現表單的模板根目錄。</p> </td>
  </tr>
  <tr>
   <td><p>資料</p> </td>
   <td><p>資料包含用於呈現表單的bata位元組。</p> </td>
  </tr>
  <tr>
   <td><p>窗體域</p> </td>
   <td><p>formDom包含JSON格式的HTML5窗體的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>分組</p> </td>
   <td><p>資料包被指定為窗體。</p> </td>
  </tr>
  <tr>
   <td><p>調試目錄</p> </td>
   <td><p>debugDir包含用於呈現表單的調試目錄。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交資料 {#submit-data}

按一下「提交」按鈕後，HTML5個表單將資料發送到伺服器。 下表列出了HTML5個表單發送到伺服器的所有參數。

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>用於呈現表單的模板。</p> </td>
  </tr>
  <tr>
   <td><p>內容根</p> </td>
   <td><p>用於呈現表單的模板根目錄。</p> </td>
  </tr>
  <tr>
   <td><p>資料</p> </td>
   <td><p>用於呈現窗體的bata位元組。</p> </td>
  </tr>
  <tr>
   <td><p>窗體域</p> </td>
   <td><p>JSON格式的HTML5窗體的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>提交者</p> </td>
   <td><p>發佈資料XML的URL。</p> </td>
  </tr>
  <tr>
   <td><p>調試目錄</p> </td>
   <td><p>用於呈現窗體的調試目錄。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交代理的工作方式？ {#how-nbsp-the-nbsp-submit-proxy-works}

如果request參數中不存在提交url，則提交服務代理將充當傳遞。 它起到傳遞的作用。 它將請求發送到/bin/xfaforms/submitaction結束點，並將響應發送到XFA運行時。

如果請求參數中存在提交url，則提交服務代理會選擇拓撲。

* 如AEM果伺服器發佈資料，則代理服務將充當傳遞。 它將請求發送到/bin/xfaforms/submitaction結束點，並將響應發送到XFA運行時。
* 如果代理發佈資料，則代理服務會將除submitUrl之外的所有參數傳遞給 */bin/xfaforms/submits(/bin/xfaforms/submit)* 在響應流中接收xml位元組。 然後，代理服務將資料xml位元組發佈到submitUrl以進行處理。

* 在向伺服器發送資料(POST請求)之前，HTML5個表單會驗證伺服器的連通性和可用性。 為驗證連接性和可用性，HTML表單向伺服器發送空頭請求。 如果伺服器可用，HTML5表單會向伺服器發送資料(POST請求)。 如果伺服器不可用，則顯示錯誤消息， *無法連接到伺服器，* 的上界。 該提前檢測防止了用戶重新填寫表格的麻煩。 代理Servlet處理頭請求且不引發異常。
