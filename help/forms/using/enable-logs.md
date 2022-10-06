---
title: 啟用HTML5表單的記錄
seo-title: Enable logging for HTML5 forms
description: 記錄器公用程式會啟用表單的記錄，並協助您偵錯表單相關問題。
seo-description: The logger utility enables logging for a form and helps you debug form-related issues.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 5%

---

# 啟用HTML5表單的記錄{#enable-logging-for-html-forms}

您可以設定記錄器公用程式，以開始建立HTML5表單的記錄。 記錄器公用程式有各種層級，您可以根據需求設定層級。 HTML5表單有伺服器和用戶端元件。 您可以為這兩個元件設定記錄檔。

## 設定伺服器端記錄 {#configuring-server-side-logging}

執行下列步驟來設定伺服器端記錄檔：

1. 前往 `https://'[server]:[port]'/system/console/configMgr`. 找出並開啟 *Apax Sling記錄器設定* 選項。 隨即出現對話方塊：

   ![ Apace Sling記錄器配置選項對話框](assets/logconfig.png)

   Apace Sling記錄器配置選項

1. 變更 **記錄層級** to **除錯**.

1. 指定 **記錄檔**.

   >[!NOTE]
   >
   >若要在HTML5表單記錄目錄中產生記錄，請在檔案名稱前新增……/logs/。

1. 變更 **記錄器** to **HTMLFormsPerfLogger**. 按一下「**儲存**」。

## 配置客戶端記錄 {#configuring-client-logging}

您可以使用下列方法來啟用HTML5表單中的用戶端記錄：

* 使用名為的請求參數 `log`
* 使用CQ Configuration Manager

### 使用請求參數啟用記錄 {#enabling-logging-using-request-parameter}

使用此方法，您可以產生特定請求的記錄。 請求參數的名稱為 `log`. 記錄URL如下：

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

日誌配置由日誌級別和記錄器類別組成。

#### 記錄目標 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>記錄目標</strong></th>
   <th><strong>說明</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>記錄檔會導向至瀏覽器 <strong>主控台</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>記錄會收集在用戶端的JavaScript物件中，並可張貼至 <strong>伺服器</strong> </td>
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
   <td>除錯<br type="_moz" /> </td>
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
   <td>xfa（指令碼引擎相關記錄檔）</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView（配置引擎相關日誌）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf（與效能相關的日誌）<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 記錄配置 {#log-configuration}

在記錄URL中，記錄設定查詢字串參數的定義如下：

`{destination}-{a level}-{b level}-{c level}`

例如：

<table>
 <tbody>
  <tr>
   <th>記錄配置</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>目的地：伺服器<br /> xfa層級：資訊<br /> xfaView級別：除錯<br /> xfaPerf級別：TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>每個日誌類別a(xfa)、b(xfaView)和c(xfaPerf)的預設日誌級別為2(ERROR)。 因此，對於日誌配置：2-b6，不同類別的記錄層級為：
>a(xfa):2（預設級別錯誤）
>b(xfaView):6(用戶指定的TRACE)
>a(xfaPerf):2（預設級別錯誤）

### 使用Configuration Manager啟用記錄 {#enabling-logging-using-configuration-manager}

如果您使用Configuration Manager來啟用記錄，則會為每個呈現請求產生記錄，直到再次停用記錄為止。

1. 登入CQ Configuration Manager，網址為 `https://'[server]:[port]'/system/console/configMgr` 並使用管理員憑證登入。
1. 搜尋並按一下 **行動Forms設定**.
1. 在「除錯選項」文字方塊中，輸入如上一節所述的記錄設定，例如 **2-a4-b5-c6**

   ![表單設定](assets/forms_configuration.png)

   表單設定

## 上傳記錄檔 {#uploading-logs}

如果目標設定為1，則所有客戶端指令碼日誌消息都將定向到控制台。 如果管理員需要這些日誌以及伺服器日誌，請將目標級別設定為2。 在此層級，所有記錄會收集在用戶端的JS物件中，如果表單是以預設設定檔呈現，則會 **傳送記錄檔** 按鈕顯示在的左側 **反白顯示現有欄位** 按鈕。 當使用者按一下連結時，所有收集的記錄都會張貼至伺服器，並記錄在伺服器上設定的錯誤記錄檔中。

預設情況下，所有資訊都將添加到/crx-repository/logs/目錄的error.log檔案中。

要更改日誌檔案的位置和名稱：

1. 以管理員身分登入Configuration Manager。 Configuration Manager的預設URL為 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下 **Apache Sling Logging Logger Configuration**. 對話方塊隨即顯示。

   ![logconfig-1](assets/logconfig-1.png)

1. 變更 **記錄層級** 除錯。

1. 指定 **記錄檔**.

   >[!NOTE]
   >
   >要在保存其他日誌檔案的同一目錄中建立日誌，請指定……/logs/&lt;filename> 在「日誌檔案」屬性中。

1. 變更 **記錄器** to **HTMLFormsPerfLogger** 按一下 **儲存**.
