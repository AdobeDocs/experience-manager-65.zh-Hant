---
title: 啟用HTML5表單的記錄功能
seo-title: 啟用HTML5表單的記錄功能
description: The logger utility enables logging for a form and helps you debug form-related issues.
seo-description: The logger utility enables logging for a form and helps you debug form-related issues.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# 啟用HTML5表單的記錄功能{#enable-logging-for-html-forms}

您可以配置記錄器實用程式以開始建立HTML5表單的日誌。 The logger utility has various levels, you can set a level as your requirements. HTML5表格包含伺服器和用戶端元件。 您可以為這兩個元件配置日誌。

## 設定伺服器端記錄 {#configuring-server-side-logging}

執行下列步驟以設定伺服器端記錄檔：

1. 前往 `https://[server]:[port]/system/console/configMgr`. 找到並開啟 *Apace Sling logger configuration* option。 將出現一個對話框：

   ![ Apace Sling logger configuration option對話框](assets/logconfig.png)

   Apace Sling logging logger配置選項

1. 將「記錄 **層級** 」變 **更為Debug**。

1. 指定日誌檔案的名 **稱和路徑**。

   >[!NOTE]
   >
   >若要在HTML5表單記錄目錄中產生記錄檔，請在檔案名稱之前新增。./logs/。

1. 將 **Logger** 變 **更為HTMLFormsPerfLogger**。 按一下&#x200B;**「儲存」**。

## 配置客戶端日誌 {#configuring-client-logging}

您可以使用下列方法，在HTML5表單中啟用用戶端登入：

* 使用名為的請求參數 `log`
* 使用CQ Configuration Manager

### 使用請求參數啟用記錄 {#enabling-logging-using-request-parameter}

使用此方法，您可以產生特定要求的記錄檔。 請求參數的名稱為「log」。 日誌URL如下：

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

日誌配置由日誌級別和日誌程式類別組成。

#### 日誌目標 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>日誌目標</strong></th>
   <th><strong>說明</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>記錄檔會導向至瀏覽器控 <strong>制台</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>記錄檔會收集在用戶端的JavaScript物件中，並可張貼至伺 <strong>服器</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>上述兩種選項<br /> </td>
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
   <td>DEBUG<br type="_moz" /> </td>
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
   <td>xfaView（版面引擎相關記錄檔）<br type="_moz" /> </td>
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
   <td>目標：Server<br /> xfa級別：INFO<br /> xfaView級別：DEBUG<br /> xfaPerf級別：TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>每個日誌類別a(xfa)、b(xfaView)和c(xfaPerf)的預設日誌級別為2(ERROR)。 因此，對於日誌配置：2-b6，不同類別的記錄層級為：
>a(xfa):2（預設層級錯誤）
>b(xfaView):6（用戶指定的TRACE）
>a(xfaPerf):2（預設層級錯誤）

### 使用Configuration manager啟用記錄 {#enabling-logging-using-configuration-manager}

如果您使用Configuration manager來啟用記錄，則會為每個演算請求產生記錄，直到再次停用記錄。

1. 在登入CQ Configuration Manager，並使用 `https://[server]:[port]/system/console/configMgr` 管理員認證登入。
1. 搜尋並按一下「行 **動表單設定」**。
1. 在「除錯選項」文字方塊中，輸入上一節所述的記錄設定，例如 **2-a4-b5-c6**

   ![表單設定](assets/forms_configuration.png)

   表單設定

## 上傳記錄檔 {#uploading-logs}

如果目標設定為1，則所有客戶端指令碼日誌消息都會定向到控制台。 如果管理員需要這些日誌以及伺服器日誌，請將目標級別設定為2。 在此層級，所有記錄檔都會收集在用戶端的JS物件中，如果表單是以預設描述檔轉譯，則工具列的「反白顯示現有欄位 ******** 」按鈕左側會顯示「傳送記錄檔」按鈕。 當使用者按一下連結時，所有收集的記錄檔都會張貼至伺服器，並記錄在伺服器上已設定的錯誤記錄檔中。

預設情況下，所有資訊都添加到/crx-repository/logs/目錄下的error.log檔案中。

要更改日誌檔案的位置和名稱，請執行以下操作：

1. 以管理員身份登錄到Configuration Manager。 配置管理器的預設URL為 `https://[Server]:[Port]/system/console/configMgr`。
1. 按一 **下Apache Sling Logging Logger Configuration**。 將出現一個對話框。

   ![logconfig-1](assets/logconfig-1.png)

1. 將記錄 **層級變更** 為除錯。

1. 指定日誌檔案的路 **徑和名稱**。

   >[!NOTE]
   >
   >要在保存其他日誌檔案的同一目錄中建立日誌，請在「日誌檔案」屬性中指定。./logs/&lt;filename>。

1. 將 **Logger** 變更為 **HTMLFormsPerfLogger** ，然後按一下「 **儲存**」。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
