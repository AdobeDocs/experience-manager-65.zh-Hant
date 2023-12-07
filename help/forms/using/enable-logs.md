---
title: 啟用HTML5表單的記錄
description: 記錄器公用程式可啟用表單的記錄，並幫助您偵錯表單相關問題。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---

# 啟用HTML5表單的記錄{#enable-logging-for-html-forms}

您可以設定記錄器公用程式，以開始建立HTML5表單的記錄。 記錄器公用程式有各種等級，您可以根據自己的需求設定等級。 HTML5 forms包含伺服器和使用者端元件。 您可以為這兩個元件設定記錄檔。

## 設定伺服器端記錄 {#configuring-server-side-logging}

執行以下步驟來設定伺服器端記錄檔：

1. 前往 `https://'[server]:[port]'/system/console/configMgr`. 找到並開啟 *Apace Sling記錄記錄器設定* 選項。 對話方塊隨即顯示：

   ![ Apace Sling記錄記錄器組態選項對話方塊](assets/logconfig.png)

   Apace Sling記錄記錄器設定選項

1. 變更 **記錄層級** 至 **偵錯**.

1. 指定下列專案的名稱和路徑： **記錄檔**.

   >[!NOTE]
   >
   >若要在HTML5表單記錄目錄中產生記錄，請在檔案名稱前新增……/logs/ 。

1. 變更 **Logger** 至 **HTMLFormsPerfLogger**. 按一下「**儲存**」。

## 設定使用者端記錄 {#configuring-client-logging}

您可以使用下列方法在HTML5表單中啟用使用者端記錄：

* 使用名為的請求引數 `log`
* 使用CQ設定管理員

### 使用請求引數啟用記錄 {#enabling-logging-using-request-parameter}

使用此方法，您可以產生特定請求的記錄。 請求引數的名稱為 `log`. 記錄URL如下：

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

記錄設定由記錄層級和記錄器類別組成。

#### 記錄檔目的地 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>記錄檔目的地</strong></th>
   <th><strong>說明</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>記錄檔會導向至瀏覽器 <strong>主控台</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>記錄檔收集於使用者端的JavaScript物件中，並可張貼至 <strong>伺服器</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>上述兩個選項<br /> </td>
  </tr>
 </tbody>
</table>

#### 記錄層級 {#log-levels}

<table>
 <tbody>
  <tr>
   <th>記錄層級</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>0</td>
   <td>關閉<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>1</td>
   <td>致命<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>錯誤<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>警告<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>資訊<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>偵錯<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>全部<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 記錄器類別 {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>記錄類別</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>a</td>
   <td>xfa （指令碼引擎相關的記錄）</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView （版面引擎相關記錄）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf （效能相關記錄）<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 記錄設定 {#log-configuration}

在記錄URL中，記錄設定查詢字串引數的定義如下：

`{destination}-{a level}-{b level}-{c level}`

例如：

<table>
 <tbody>
  <tr>
   <th>記錄設定</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>目的地：伺服器<br /> xfa層級： INFO<br /> xfaView層級： DEBUG<br /> xfaPerf層級：TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>每個日誌類別a (xfa)、b (xfaView)和c (xfaPerf)的預設日誌層級為2 （錯誤）。 因此，對於記錄設定：2-b6，不同類別的記錄層級為：
>a (xfa)：2 （預設層次錯誤）
>b (xfaView)： 6 (使用者指定的TRACE)
>a (xfaPerf)：2 （預設層級ERROR）

### 使用Configuration Manager啟用記錄 {#enabling-logging-using-configuration-manager}

如果您使用Configuration Manager來啟用記錄，則會為每個轉譯器請求產生記錄，直到再次停用記錄為止。

1. 請在登入CQ Configuration Manager `https://'[server]:[port]'/system/console/configMgr` 並使用管理員憑證登入。
1. 搜尋並按一下 **行動Forms設定**.
1. 在「除錯選項」文字方塊中，依照上一節所述輸入記錄組態，例如： **2-a4-b5-c6**

   ![Forms設定](assets/forms_configuration.png)

   表單設定

## 正在上傳記錄檔 {#uploading-logs}

如果目的地設為1，所有使用者端指令碼記錄訊息都會導向至主控台。 如果管理員需要這些記錄以及伺服器記錄，請將目的地層級設定為2。 在此層級，所有記錄都會收集到使用者端的JS物件中，如果表單是以預設設定檔呈現，則 **傳送記錄檔** 按鈕出現在的左側 **反白顯示現有欄位** 工具列中的按鈕。 當使用者按一下連結時，所有收集的記錄都會發佈到伺服器，並記錄到伺服器上設定的錯誤記錄檔中。

依預設，所有資訊都會新增至/crx-repository/logs/目錄的error.log檔案中。

變更記錄檔的位置和名稱：

1. 以管理員身分登入Configuration Manager。 Configuration Manager的預設URL為 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下 **Apache Sling記錄記錄器設定**. 對話方塊隨即顯示。

   ![logconfig-1](assets/logconfig-1.png)

1. 變更 **記錄層級** 進行偵錯。

1. 指定路徑和名稱 **記錄檔**.

   >[!NOTE]
   >
   >若要在保留其他記錄檔的同一目錄中建立記錄，請指定……/logs/&lt;filename> 在「記錄檔」屬性中。

1. 變更 **Logger** 至 **HTMLFormsPerfLogger** 並按一下 **儲存**.
