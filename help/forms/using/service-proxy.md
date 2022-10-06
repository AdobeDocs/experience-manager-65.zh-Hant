---
title: HTML5表單服務代理
seo-title: HTML5 forms service proxy
description: HTML5表單服務代理是註冊提交服務代理的配置。 要配置服務代理，請通過請求參數submissionServiceProxy指定提交服務的URL。
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

HTML5表單服務代理是註冊提交服務代理的配置。 要配置服務代理，請通過請求參數指定提交服務的URL *submissionServiceProxy*.

## 服務代理的優勢 {#benefits-of-service-proxy-br}

服務代理消除了以下內容：

* HTML5表單工作流程需要為HTML5表單使用者開啟提交服務「/content/xfaforms/submission/default」。 這會讓AEM伺服器受到更廣泛的非預期受眾。
* 服務URL內嵌在表單的執行階段模型中。 無法更改服務URL路徑。
* 提交是兩步驟程式。 若要提交表單資料，提交至少需要兩個伺服器歷程。 因此，會增加伺服器上的負載。
* HTML5表單會在POST請求中傳送資料，而非PDF請求。 對於同時涉及PDF和HTML5表單的工作流程，需要兩種不同的處理提交的方法。

### 拓撲 {#topologies-br}

HTML5表單可使用下列拓撲來連接AEM伺服器。

* 一種拓撲，AEM Server或HTML5表單通過POST將資料發送到伺服器。
* 代理伺服器將POST資料發送到伺服器的拓撲。

![HTML5表單服務代理拓撲](assets/topology.png)

HTML5表單服務代理拓撲

HTML5表單會連線至AEM伺服器，執行伺服器端指令碼、網站服務和提交。 HTML5表單的XFA執行階段使用「/bin/xfaforms/submitaction」端點上的Ajax呼叫，搭配各種參數連線至AEM伺服器。 HTML5 forms連接AEM伺服器以執行下列操作：

#### 執行伺服器端指令碼和Web服務 {#execute-server-sided-scripts-and-web-services}

標籤為在伺服器上運行的指令碼稱為伺服器端指令碼。 下表列出了伺服器端指令碼和Web服務中使用的所有參數。

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>活動</p> </td>
   <td><p>活動包含觸發請求的事件。 例如點按、退出或變更</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom包含執行事件之物件的SOM運算式。</p> </td>
  </tr>
  <tr>
   <td><p>範本</p> </td>
   <td><p>模板包含用於呈現表單的模板。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot包含用於呈現表單的模板根目錄。</p> </td>
  </tr>
  <tr>
   <td><p>資料</p> </td>
   <td><p>資料包含用於呈現表單的bata位元組。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom包含JSON格式的HTML5表單DOM。</p> </td>
  </tr>
  <tr>
   <td><p>封包</p> </td>
   <td><p>資料包指定為表單。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir包含用於呈現表單的調試目錄。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交資料 {#submit-data}

按一下提交按鈕後，HTML5個表單會將資料傳送至伺服器。 下表列出HTML5個表單傳送至伺服器的所有參數。

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
   <td><p>contentRoot</p> </td>
   <td><p>用於呈現表單的模板根目錄。</p> </td>
  </tr>
  <tr>
   <td><p>資料</p> </td>
   <td><p>用於呈現表單的bata位元組。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON格式的HTML5表單DOM。</p> </td>
  </tr>
  <tr>
   <td><p>提交url</p> </td>
   <td><p>發佈資料XML的URL。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>用於呈現表單的調試目錄。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交代理如何運作？ {#how-nbsp-the-nbsp-submit-proxy-works}

如果要求參數中未出現提交url，則提交服務代理會作為傳遞。 它是傳遞。 它會將請求發送到/bin/xfaforms/submitaction端點並將響應發送到XFA運行時。

如果請求參數中存在提交url，則提交服務代理將選擇拓撲。

* 如果AEM伺服器發佈資料，Proxy服務會作為傳遞。 它會將請求發送到/bin/xfaforms/submitaction端點並將響應發送到XFA運行時。
* 如果代理發佈資料，則代理服務會將submitUrl以外的所有參數傳遞至 */bin/xfaforms/submitaction* 結束點和接收響應流中的xml位元組。 接著，代理服務會將資料xml位元組發佈至submitUrl以進行處理。

* 在將資料(POST請求)傳送至伺服器之前，HTML5個表單會驗證伺服器的連線性和可用性。 為了驗證連通性和可用性，HTML表單向伺服器發送空頭請求。 如果伺服器可用，HTML5表單會將資料(POST請求)傳送至伺服器。 如果伺服器不可用，將顯示一條錯誤消息， *無法連接到伺服器，* 的下界。 進階偵測可避免使用者重新填寫表單的麻煩。 代理Servlet處理頭請求，且不會引發異常。
