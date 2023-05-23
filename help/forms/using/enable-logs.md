---
title: 啟用HTML5窗體的日誌記錄
seo-title: Enable logging for HTML5 forms
description: 記錄器實用程式啟用表單的日誌記錄並幫助您調試表單相關問題。
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

# 啟用HTML5窗體的日誌記錄{#enable-logging-for-html-forms}

可以配置記錄器實用程式以開始為HTML5表單建立日誌。 記錄器實用程式具有各種級別，您可以根據要求設定一個級別。 HTML5表單包含伺服器和客戶端元件。 可以為這兩個元件配置日誌。

## 配置伺服器端日誌 {#configuring-server-side-logging}

執行以下步驟來配置伺服器端日誌：

1. 前往 `https://'[server]:[port]'/system/console/configMgr`. 查找並開啟 *Paxe Sling日誌記錄記錄器配置* 的雙曲餘切值。 出現一個對話框：

   ![ 「快速Sling日誌記錄器配置選項」對話框](assets/logconfig.png)

   Paxe Sling日誌記錄記錄器配置選項

1. 更改 **日誌級別** 至 **調試**。

1. 指定的名稱和路徑 **日誌檔案**。

   >[!NOTE]
   >
   >要在HTML5表單日誌目錄中生成日誌，請在檔案名前添加……/logs/。

1. 更改 **記錄器** 至 **HTMLFormsPerfLogger**。 按一下「**儲存**」。

## 配置客戶端日誌 {#configuring-client-logging}

可以使用以下方法在HTML5窗體中啟用客戶端登錄：

* 使用名為的請求參數 `log`
* 使用CQ Configuration Manager

### 使用請求參數啟用日誌記錄 {#enabling-logging-using-request-parameter}

使用此方法，可以為特定請求生成日誌。 請求參數的名稱為 `log`。 日誌URL如下所示：

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

日誌配置由日誌級別和記錄器類別組成。

#### 日誌目標 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>日誌目標</strong></th>
   <th><strong>說明</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>日誌被定向到瀏覽器 <strong>控制台</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>日誌在客戶端上的JavaScript對象中收集，可以發佈到 <strong>伺服器</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>上述兩項購股權<br /> </td>
  </tr>
 </tbody>
</table>

#### 日誌級別 {#log-levels}

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
   <td>調試<br type="_moz" /> </td>
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
   <th>日誌類別</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>a</td>
   <td>xfa（編寫與引擎相關的日誌指令碼）</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView（佈局引擎相關日誌）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf（與效能相關的日誌）<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 日誌配置 {#log-configuration}

在日誌URL中，日誌配置查詢字串參數的定義如下：

`{destination}-{a level}-{b level}-{c level}`

例如：

<table>
 <tbody>
  <tr>
   <th>日誌配置</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>目標：伺服器<br /> xfa級別：資訊<br /> xfaView級別：調試<br /> xfaPerf級別：TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>每個日誌類別a(xfa)、b(xfaView)和c(xfaPerf)的預設日誌級別為2(ERROR)。 因此，對於日誌配置：2-b6，不同類別的日誌級別為：
>a(xfa):2（預設級別錯誤）
>b(xfaView):6(用戶指定的TRACE)
>a(xfaPerf):2（預設級別錯誤）

### 使用Configuration Manager啟用日誌記錄 {#enabling-logging-using-configuration-manager}

如果使用Configuration Manager啟用日誌記錄，則會為每個呈現請求生成日誌，直到再次禁用日誌記錄。

1. 登錄到CQ Configuration Manager(位於 `https://'[server]:[port]'/system/console/configMgr` 並使用管理員憑據登錄。
1. 搜索並按一下 **移動Forms配置**。
1. 在「調試選項」文本框中，按上一節中所述輸入日誌配置，例如， **2-a4-b5-c6**

   ![表單設定](assets/forms_configuration.png)

   表單設定

## 正在上載日誌 {#uploading-logs}

如果目標設定為1，則所有客戶端指令碼日誌消息都會定向到控制台。 如果管理員需要這些日誌以及伺服器日誌，請將目標級別設定為2。 在此級別，所有日誌都收集在客戶端的JS對象中，如果表單呈現時使用預設配置檔案，則 **發送日誌** 按鈕 **突出顯示現有欄位** 按鈕 當用戶按一下該連結時，所有收集的日誌都會發佈到伺服器上，並記錄到伺服器上配置的錯誤日誌檔案中。

預設情況下，所有資訊都會添加到/crx-repository/logs/目錄的error.log檔案中。

要更改日誌檔案的位置和名稱：

1. 以管理員身份登錄到Configuration Manager。 Configuration Manager的預設URL為 `https://'[server]:[port]'/system/console/configMgr`。
1. 按一下 **Apache Sling日誌記錄器配置**。 對話方塊隨即顯示。

   ![logconfig-1](assets/logconfig-1.png)

1. 更改 **日誌級別** 調試。

1. 指定路徑和名稱 **日誌檔案**。

   >[!NOTE]
   >
   >要在保存其他日誌檔案的同一目錄中建立日誌，請指定……/logs/&lt;filename> 中。

1. 更改 **記錄器** 至 **HTMLFormsPerfLogger** 按一下 **保存**。
