---
title: 「教程：規劃互動交流」
seo-title: Plan your Interactive Communication
description: 規劃互動式通信的解剖結構
seo-description: Plan the anatomy for your Interactive Communication
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
exl-id: ea0c8971-56f4-4094-87e4-1b222b73951f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 2%

---

# 教程：規劃互動式通信 {#tutorial-plan-the-interactive-communication}

規劃互動式通信的解剖結構

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教程是 [建立您的第一個互動式通信](/help/forms/using/create-your-first-interactive-communication.md) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

規劃互動式通信的第一步是最終確定互動式通信的內容。 來自法律、財務、支援或市場營銷等部門的主題專家可以幫助您最終確定內容。 定稿後，您必須分析內容以確定建立互動式通信所需的各種資產類型。

## 規劃注意事項 {#planning-considerations}

一種互動式通信包括下列元素：

* **靜態文本** 主要包括互動式通信的一般部分，並包括在與所有客戶的通信中。 例如，頁眉、頁腳、稱謂或免責聲明。
* **從後端系統（表單資料模型）來源的資料** 是特定於客戶的，並與互動式通信動態合併。 例如，可以使用表單資料模型來源補充策略編號或地址。
* **佈局或模板** 打印和Web版本。
* **訂單** 其中，各種文本段落出現在互動式通信中。
* **由前線員工輸入的資料（代理UI）** 在發送通信之前，誰正在自定義通信。 例如，付款到期日。

* **條件資料** 根據預定義條件填充的。 例如，生成互動式通信的日期。
* **儲存在儲存庫中的影像**&#x200B;例如徽標和簽名影像。 大多數或所有互動式通信中都會出現公司徽標等影像。
* **圖表和表** 簡化交互通信中複雜資料的表示

## 互動交流的解剖 {#anatomy-of-the-interactive-communication}

完成用於建立互動式通信的內容和元素後，您就可以建立互動式通信的解剖。 解剖結構中必須列出 [規劃注意事項](/help/forms/using/planning-interactive-communications.md#planning-considerations) 的子菜單。 根據我們的使用案例，以下是電信運營商向客戶發送的每月賬單分析示例。

解剖結構包括具有以下輸入模式的資料：

* 靜態文本
* 窗體資料模型
* Agent UI
* 條件資料
* 影像

在每節中，粗體文本表示靜態文本。 資料庫包括customer、bills和calls表。 表單資料模型可以從這些表中的任何一個接收資料。 有關詳細資訊，請參見 [建立表單資料模型](/help/forms/using/create-form-data-model0.md)。

下表說明了互動式通信結構中每個欄位的資料源：

<table>
 <tbody>
  <tr>
   <td>章節</td>
   <td>靜態文本</td>
   <td>FDM </td>
   <td>Agent UI</td>
   <td>影像</td>
  </tr>
  <tr>
   <td>清單詳細資訊</td>
   <td><p>發票編號</p> <p>帳單日期</p> <p>清單期間</p> <p>您的計畫</p> </td>
   <td><p>值 <strong>您的計畫 </strong>場</p> <p>表 — 客戶</p> </td>
   <td><p>以下欄位的值：</p>
    <ul>
     <li>發票編號</li>
     <li>帳單日期</li>
     <li>清單期間</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>客戶詳細資訊</td>
   <td><p>供應地點</p> <p>狀態代碼</p> <p>移動號碼</p> <p>備用聯繫人號碼</p> <p>關係編號</p> <p>連接數</p> </td>
   <td><p>以下欄位的值：</p>
    <ul>
     <li>名稱</li>
     <li>地址</li>
     <li>移動號碼</li>
     <li>備用聯繫人號碼</li>
     <li>關係編號</li>
    </ul> <p>表 — 客戶</p> </td>
   <td><p>以下欄位的值：</p>
    <ul>
     <li>供應地點</li>
     <li>狀態代碼</li>
     <li>連接數</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>清單摘要</td>
   <td><p>上一餘額</p> <p>付款</p> <p>調整</p> <p>費用當前開單期間</p> <p>到期金額</p> <p>到期日期</p> </td>
   <td><p>值 <strong>費用當前開單期間 </strong> 場</p> <p>表 — 清單</p> </td>
   <td><p>以下欄位的值：</p>
    <ul>
     <li>上一餘額</li>
     <li>付款</li>
     <li>調整</li>
     <li>到期金額</li>
     <li>到期日期</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>費用匯總</td>
   <td><p>呼叫費用</p> <p>電話會議費用</p> <p>簡訊費 </p> <p>移動網際網路收費</p> <p>國家漫遊費用</p> <p>國際漫遊費用</p> <p>增值服務費</p> <p>費用合計</p> <p>應付總額</p> <p>「增值服務費用」欄位的條件</p> </td>
   <td><p>以下欄位的值：</p>
    <ul>
     <li>呼叫費用</li>
     <li>電話會議費用</li>
     <li>簡訊費 </li>
     <li>移動網際網路收費</li>
     <li>國家漫遊費用</li>
     <li>國際漫遊費用</li>
     <li>增值服務費</li>
     <li>總費用（usagecharges計算欄位）</li>
     <li>應付總額（計算欄位）</li>
    </ul> <p>表 — 清單</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>分項呼叫 — 傳出</td>
   <td><p>列名：</p>
    <ul>
     <li>日期</li>
     <li>時間</li>
     <li>數字</li>
     <li>持續時間</li>
     <li>費用</li>
    </ul> </td>
   <td><p>所有值</p> <p>表 — 呼叫</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>立即支付</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>立即付款</td>
  </tr>
  <tr>
   <td>增值服務</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>增值服務</td>
  </tr>
 </tbody>
</table>
