---
title: 「教學課程：規劃互動式通訊」
seo-title: Plan your Interactive Communication
description: 規劃互動式通訊的解剖結構
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

# 教學課程：規劃互動式通訊 {#tutorial-plan-the-interactive-communication}

規劃互動式通訊的解剖結構

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

規劃互動式通訊的第一步是完成互動式通訊的內容。 法律、財務、支援或行銷等部門的主題專家可協助您完成內容定稿。 內容完成後，您必須分析內容，以識別建立互動式通訊所需的各種資產類型。

## 規劃考量事項 {#planning-considerations}

互動式通訊包括下列元素：

* **靜態文字** 大多包括互動式通信的一般部分，並包括在與所有客戶的通信中。 例如頁首、頁尾、聲明或免責聲明。
* **來源於後端系統的資料（表單資料模型）** 是客戶專屬的，會動態與互動式通訊合併。 例如，策略編號或地址可使用表單資料模型來源。
* **版面或範本** （用於Interactive Communication的打印和Web版本）。
* **順序** 其中，各種文本段落出現在「互動式通信」中。
* **由前線員工輸入的資料（代理UI）** 在發送通信之前自定義通信的用戶。 例如，付款到期日。

* **條件式資料** 會根據預先定義的條件填入。 例如，互動式通訊的產生日期。
* **儲存在儲存庫中的影像**，例如標誌和簽名影像。 大部分或全部互動式通訊中都會出現企業標誌等影像。
* **圖表和表** 需要簡化交互通信中複雜資料的表示

## 互動式溝通的解剖 {#anatomy-of-the-interactive-communication}

完成建立互動式通訊的內容和元素後，您就可以建立互動式通訊的解剖結構。 解剖學中必須列出 [規劃考量事項](/help/forms/using/planning-interactive-communications.md#planning-considerations) 區段。 根據我們的使用案例，以下是電信營運商傳送給其客戶之每月帳單的剖析範例。

解剖結構包括具有以下輸入模式的資料：

* 靜態文字
* 表單資料模型
* Agent UI
* 條件式資料
* 影像

在每個區段中，粗體文字代表靜態文字。 資料庫包括客戶、帳單和呼叫表。 表單資料模型可接收來自任何這些表格的資料。 如需詳細資訊，請參閱 [建立表單資料模型](/help/forms/using/create-form-data-model0.md).

下表說明了Interactive Communication結構中每個欄位的資料源：

<table>
 <tbody>
  <tr>
   <td>章節</td>
   <td>靜態文字</td>
   <td>FDM </td>
   <td>Agent UI</td>
   <td>影像</td>
  </tr>
  <tr>
   <td>帳單詳細資訊</td>
   <td><p>發票編號</p> <p>帳單日期</p> <p>帳單期間</p> <p>您的計畫</p> </td>
   <td><p>的值 <strong>您的計畫 </strong>欄位</p> <p>表格 — 客戶</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>發票編號</li>
     <li>帳單日期</li>
     <li>帳單期間</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>客戶詳細資訊</td>
   <td><p>供應地</p> <p>狀態代碼</p> <p>行動號碼</p> <p>備用聯繫人號碼</p> <p>關係編號</p> <p>連接數</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>名稱</li>
     <li>地址</li>
     <li>行動號碼</li>
     <li>備用聯繫人號碼</li>
     <li>關係編號</li>
    </ul> <p>表格 — 客戶</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>供應地</li>
     <li>狀態代碼</li>
     <li>連接數</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>清單匯總</td>
   <td><p>上一餘額</p> <p>付款</p> <p>調整</p> <p>當前帳單期間費用</p> <p>到期金額</p> <p>到期日期</p> </td>
   <td><p>的值 <strong>當前帳單期間費用 </strong> 欄位</p> <p>表 — 清單</p> </td>
   <td><p>下列欄位的值：</p>
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
   <td><p>通話費</p> <p>電話會議費</p> <p>簡訊指控 </p> <p>行動網際網路收費</p> <p>國家漫遊費</p> <p>國際漫遊費</p> <p>增值服務費</p> <p>總費用</p> <p>應付總額</p> <p>「增值服務費」欄位中的條件</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>通話費</li>
     <li>電話會議費</li>
     <li>簡訊指控 </li>
     <li>行動網際網路收費</li>
     <li>國家漫遊費</li>
     <li>國際漫遊費</li>
     <li>增值服務費</li>
     <li>總費用（usagecharges計算欄位）</li>
     <li>應付總額（usagecharges計算欄位）</li>
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
   <td><p>所有值</p> <p>表格 — 呼叫</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>立即支付</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>增值服務</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
