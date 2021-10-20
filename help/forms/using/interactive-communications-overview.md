---
title: 互動式通訊概述
seo-title: Interactive Communications Overview
description: 本文包括概述、使用案例範例、建立工作流程，以及互動式通訊與信函之間的差異。
seo-description: Interactive Communication key capabilities, sample use cases, creation workflow, and differences between Interactive Communication and Correspondence Management
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
source-git-commit: 415744ca5c46a1495fe90369c162158c7fc2f1d4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 7%

---


# 互動式通訊概述 {#interactive-communications-overview}

本文包括概述、使用案例範例、建立工作流程，以及互動式通訊與信函之間的差異。

![](do-not-localize/correspondence-management.png)

「互動式通訊」可集中處理和管理安全、個人化與互動式通信的建立、集合與傳送，例如商業信函、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。

## 關鍵功能 {#key-capabilities}

以下是互動式通訊的主要功能：

- 與表單資料模型的現成整合，可輕鬆簡化存取後端資料庫和其他CRM系統(例如MS® Dynamics)
- 用於打印和Web通道的整合創作介面，能夠自動從打印通道生成Web通道
- 在打印和網路中以易於理解的視覺格式呈現資訊的圖表
- 檔案片段支援規則編輯器和表單資料模型
- 代理用戶介面顯示互動式通信的打印和Web預覽
- 拖放元件，以快速建構列印和Web頻道

## 互動式通訊建立 {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### 工作流程 {#workflow}

若要建立互動式通訊，請使用 [構建基礎](#buildingblocks) 針對互動式通訊，然後完成下列步驟：

1. 選擇 [建立互動式通訊](/help/forms/using/create-interactive-communication.md).

1. 指定 [表單資料模型](/help/forms/using/data-integration.md)、預填服務和 [列印與網頁頻道範本](/help/forms/using/web-channel-print-channel.md). 您可以選擇從列印管道產生網頁管道。

1. 使用 [拖放介面](/help/forms/using/introduction-interactive-communication-authoring.md)，根據需要添加要打印的文檔片段、影像、元件和Interactive Communication的Web通道。
1. 為插入的元件配置屬性，如：

   1. [影像](/help/forms/using/create-interactive-communication.md#step2)
   1. [表格](/help/forms/using/create-interactive-communication.md#tables) （包括版面片段）
   1. [圖表](/help/forms/using/chart-component-interactive-communications.md)
   1. [檔案片段](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 預覽打印和Web通道，並根據需要編輯互動式通信。
1. 代理使用代理UI [準備互動式通訊](/help/forms/using/prepare-send-interactive-communication.md) 將其傳送至收件者/貼文程式。

### 建置區塊 {#buildingblocks}

以下是建立互動式通訊所需的基礎要素：

- [表單資料模型](/help/forms/using/data-integration.md)
- [列印和網頁頻道範本](/help/forms/using/web-channel-print-channel.md)
- [檔案片段](/help/forms/using/document-fragments.md)
- 影像
- [主題](/help/forms/using/themes.md) 針對網頁頻道

## 互動式通訊與通信管理 {#interactive-communications-vs-correspondence-management}

互動式通訊是建立客戶通訊的預設且建議方法。 若要繼續使用AEM 6.3 Forms和AEM 6.2 Forms中建立的字母，您必須 [安裝相容性套件](/help/forms/using/compatibility-package.md). 以下是互動式通訊和信函功能的比較。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>互動式通訊</strong></td>
   <td><strong>字母</strong></td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>打印和Web</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>結構描述</td>
   <td>表單資料模型 </td>
   <td>資料字典 </td>
  </tr>
  <tr>
   <td>本土化</td>
   <td>表單資料模型中不支援</td>
   <td>資料字典支援</td>
  </tr>
  <tr>
   <td>規則編輯器</td>
   <td>
    <ul>
     <li>用於建立內嵌條件的文字和條件支援規則編輯器</li>
     <li>互動式通信編輯器支援在Web通道的元件上應用規則</li>
    </ul> </td>
   <td>沒有用於建立條件表達式的UI</td>
  </tr>
  <tr>
   <td>製作</td>
   <td>用於構造打印和Web通道的拖放介面</td>
   <td>無拖放機構 </td>
  </tr>
  <tr>
   <td>圖表</td>
   <td>打印和Web通道中支援的圖表</td>
   <td>不支援</td>
  </tr>
  <tr>
   <td>主題</td>
   <td>使用主題來設定網路管道的樣式</td>
   <td>不支援主題</td>
  </tr>
   <tr>
   <td>草稿</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>提交</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
  <tr>
   <td>稽核</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
   <tr>
   <td>版本設定</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
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
   <td>遠程函式</td>
   <td>不支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>
