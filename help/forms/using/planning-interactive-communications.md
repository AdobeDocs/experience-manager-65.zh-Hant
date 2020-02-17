---
title: 「教學課程：規劃互動式通訊」
seo-title: 規劃您的互動式通訊
description: 規劃互動式通訊的剖析
seo-description: 規劃互動式通訊的剖析
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# 教學課程：規劃互動式通訊 {#tutorial-plan-the-interactive-communication}

規劃互動式通訊的剖析

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是「建立您的第 [一個互動式通訊」系列的一個步驟](/help/forms/using/create-your-first-interactive-communication.md) 。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

規劃互動式通訊的第一步是完成互動式通訊的內容。 法律、財務、支援或行銷等部門的相關領域專家可協助您完成內容定稿。 完成內容後，您必須分析內容，以識別建立互動式通訊所需的各種資產類型。

## 規劃考量事項 {#planning-considerations}

互動式通訊包括下列元素：

* **靜態文本** (Static Text)主要包含了互動式通信的一些部分，這些部分在本質上是通用的，並且包含在與所有客戶的通信中。 例如頁首、頁尾、問候語或免責聲明。
* **來自後端系統（表單資料模型）的資料是客戶專屬的** ，並與互動式通訊動態合併。 例如，可使用表單資料模型來源於原則編號或位址。
* **互動式通訊** (Interactive Communication)的列印與網頁版面或範本。
* **Order** whith and the vorial text parfaces in the Interactive Communication.
* **由前線員工（代理UI）輸入的資料** ，此員工在傳送通訊前會自訂通訊。 例如，付款到期日。

* **根據預先定義** 的條件填入的條件資料。 例如，產生互動式通訊的日期。
* **儲存在儲存庫中的影像**，例如標誌和簽名影像。 大部分或所有互動式通訊中都會出現公司標誌等影像。
* **簡化互動式通訊** (Interactive Communication)中複雜資料表示所需的圖表和表格

## 互動式通訊剖析 {#anatomy-of-the-interactive-communication}

完成用於建立互動式通訊的內容和元素後，您就可以建立互動式通訊的剖析。 解剖結構必須包含「規劃考量事項」部分 [中列出的詳細](/help/forms/using/planning-interactive-communications.md#planning-considerations) 資訊。 根據我們的使用案例，以下是電信營運商傳送給其客戶之每月帳單的剖析範例。

解剖學影片的預留位置

解剖結構包括具有以下輸入模式的資料：

* 靜態文字
* 表單資料模型
* Agent UI
* 條件式資料
* 影像

在每個區段中，粗體文字代表靜態文字。 資料庫包括客戶、帳單和呼叫表。 表單資料模型可接收這些表格中的任何一個資料。 如需詳細資訊，請參 [閱建立表單資料模型](/help/forms/using/create-form-data-model0.md)。

下表說明互動式通訊結構中各欄位的資料來源：

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
   <td><p>「計畫」 <strong>欄位的 </strong>值</p> <p>表——客戶</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>發票編號</li>
     <li>帳單日期</li>
     <li>帳單期間</li>
    </ul> <p> </p> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>客戶詳細資訊</td>
   <td><p>供應地點</p> <p>州代碼</p> <p>行動號碼</p> <p>備用聯繫人號碼</p> <p>關係編號</p> <p>連接數</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>名稱</li>
     <li>地址</li>
     <li>行動號碼</li>
     <li>備用聯繫人號碼</li>
     <li>關係編號</li>
    </ul> <p>表——客戶</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>供應地點</li>
     <li>州代碼</li>
     <li>連接數</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>清單摘要</td>
   <td><p>上一餘額</p> <p>付款</p> <p>調整</p> <p>當前帳單期間費用</p> <p>到期金額</p> <p>到期日期</p> </td>
   <td><p>「費用當前 <strong>開單期間」欄位的 </strong> 值</p> <p>表——清單</p> </td>
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
   <td><p>通話費</p> <p>電話會議費用</p> <p>簡訊費 </p> <p>行動網際網路收費</p> <p>國家漫遊費用</p> <p>國際漫遊費用</p> <p>增值服務費用</p> <p>費用合計</p> <p>應付總額</p> <p>「增值服務費用」欄位的條件</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>通話費</li>
     <li>電話會議費用</li>
     <li>簡訊費 </li>
     <li>行動網際網路收費</li>
     <li>國家漫遊費用</li>
     <li>國際漫遊費用</li>
     <li>增值服務費用</li>
     <li>費用合計（計算欄位）</li>
     <li>應付總額（usagecharges計算欄位）</li>
    </ul> <p>表——清單</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>明細呼叫——去話</td>
   <td><p>欄名稱：</p>
    <ul>
     <li>日期</li>
     <li>時間</li>
     <li>數字</li>
     <li>持續時間</li>
     <li>費用</li>
    </ul> </td>
   <td><p>所有值</p> <p>表格——呼叫</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>立即付款</td>
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

