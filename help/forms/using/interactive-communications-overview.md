---
title: 互動式通訊概觀
seo-title: 互動式通訊概觀
description: 本文包括概述、範例使用案例、建立工作流程，以及互動式通訊與信函之間的差異。
seo-description: 互動式通訊主要功能、範例使用案例、建立工作流程，以及互動式通訊與通訊管理之間的差異
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
translation-type: tm+mt
source-git-commit: dc7804c9985bf9a14bfad40f546e393b39615dab

---


# 互動式通訊概觀 {#interactive-communications-overview}

本文包括概述、範例使用案例、建立工作流程，以及互動式通訊與信函之間的差異。

![](do-not-localize/correspondence-management.png)

互動式通訊可集中管理安全、個人化及互動式通訊的建立、組裝與傳遞，例如商業通訊、檔案、陳述、利益通知、行銷郵件、帳單和歡迎套件。

## 主要功能 {#key-capabilities}

以下是互動式通訊的主要功能：

* 與表單資料模型立即可用的整合，讓您輕鬆簡化對後端資料庫和其他CRM系統（例如MS® Dynamics）的存取
* 整合的製作介面，適用於列印和網頁通道，並可自動從列印通道產生網頁通道
* 以易於理解的視覺格式呈現列印和網頁中的資訊圖表
* 檔案片段支援規則編輯器和表單資料模型
* 代理用戶介面顯示互動式通信的打印和Web預覽
* 拖放元件，以快速建構列印和網頁頻道

## 範例使用案例 {#sample-use-case}

信用 [卡客戶範例使用案例的歡迎套件](/help/forms/using/finance-reference-site-walkthrough.md#credit-card-application-walkthrough) ，展示互動式通訊的功能。

## Interactive Communication creation  {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### 工作流程 {#workflow}

若要建立互動式通訊，請準備好 [互動式通訊的](#buildingblocks) 「建立區塊」，然後完成下列步驟：

1. 選擇建立 [互動式通訊](/help/forms/using/create-interactive-communication.md)。

1. 指定表 [單資料模型](/help/forms/using/data-integration.md)、預填服務，以 [及列印和網路頻道範本](/help/forms/using/web-channel-print-channel.md)。 您可以選擇從列印頻道產生網頁頻道。

1. 使用 [拖放介面](/help/forms/using/introduction-interactive-communication-authoring.md)，視需要新增檔案片段、影像、元件以列印和網路通路。
1. 為插入的元件配置屬性，例如：

   1. [影像](/help/forms/using/create-interactive-communication.md#step2)
   1. [表格](/help/forms/using/create-interactive-communication.md#tables) （包括版面片段）
   1. [圖表](/help/forms/using/chart-component-interactive-communications.md)
   1. [檔案片段](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 預覽列印和網路頻道，並視需要編輯互動式通訊。
1. 代理使用代理UI來準 [備Interactive Communication](/help/forms/using/prepare-send-interactive-communication.md) ，以便將它發送給收件人／後置進程。

### 建置區塊 {#buildingblocks}

以下是建立互動式通信所需的構造塊：

* [表單資料模型](/help/forms/using/data-integration.md)
* [列印和網頁頻道範本](/help/forms/using/web-channel-print-channel.md)
* [檔案片段](/help/forms/using/document-fragments.md)
* 影像
* [Web頻道](/help/forms/using/themes.md) 的主題

## 互動式通訊與通訊管理 {#interactive-communications-vs-correspondence-management}

互動式通訊是建立客戶通訊的預設和建議方式。 若要繼續使用AEM 6.3 Forms和AEM 6.2 Forms中建立的字母，您必須安 [裝相容套件](/help/forms/using/compatibility-package.md)。 以下是互動式通訊和信函功能的比較。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>互動式通訊</strong></td>
   <td><strong>字母</strong></td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>印刷與網頁</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>結構描述</td>
   <td>表單資料模型 </td>
   <td>資料字典 </td>
  </tr>
  <tr>
   <td>本土化</td>
   <td>表單資料模型不支援</td>
   <td>資料字典支援</td>
  </tr>
  <tr>
   <td>規則編輯器</td>
   <td>
    <ul>
     <li>文字和條件支援規則編輯器，以建立內嵌條件</li>
     <li>互動式通訊編輯器支援規則在網路頻道元件上的應用</li>
    </ul> </td>
   <td>沒有用於建立條件式運算式的UI</td>
  </tr>
  <tr>
   <td>製作</td>
   <td>用於構建打印和Web通道的拖放介面</td>
   <td>無拖放機制 </td>
  </tr>
  <tr>
   <td>圖表</td>
   <td>支援列印和網頁頻道的圖表</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>主題</td>
   <td>使用主題來設定網頁頻道的樣式</td>
   <td>不支援主題</td>
  </tr>
  <tr>
   <td>審核和版本修訂</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>草稿和管理例項</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>批次處理</td>
   <td>支援 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td>代理簽名</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>遠程功能</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

