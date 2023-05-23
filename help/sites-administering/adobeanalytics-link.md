---
title: 為Adobe Analytics配置鏈路跟蹤
seo-title: Configuring Link Tracking for Adobe Analytics
description: 瞭解如何配置連結跟蹤以進行SiteCatalyst。
seo-description: Learn about configuring link tracking for SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 0%

---

# 為Adobe Analytics配置鏈路跟蹤{#configuring-link-tracking-for-adobe-analytics}

當用戶按一下您網站頁面上的連結時，您可以在Adobe Analytics捕獲相關資訊。 例如，使用連結跟蹤瞭解用戶如何與您的站點交互、跟蹤檔案下載和跟蹤退出連結。

## 為Adobe Analytics框架配置鏈路跟蹤 {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. 使用 **導航**，通過 **部署**。 **Cloud Services** 到 **Adobe Analytics** 的子菜單。

1. 使用 **顯示配置**，開啟所需的Adobe Analytics框架。
1. 展開 **連結跟蹤配置** 按需配置(本頁提供更多詳細資訊：

   ![aa-08](assets/aa-08.png)

## 跟蹤檔案下載 {#tracking-file-downloads}

配置Adobe Analytics框架，以便自動跟蹤從關聯頁面下載的檔案作為Adobe Analytics的下載。 啟用下載跟蹤時，僅跟蹤您指定的檔案類型。

預設情況下會跟蹤以下檔案類型的下載：

* exe
* ZIP
* 瓦
* mp3
* 莫夫
* mpg
* 艾維
* WMV
* doc
* PDF
* xls

例如，啟用了PDF檔案的下載跟蹤後，每當用戶按一下指向PDF檔案的連結時，就會跟蹤PDF的下載。

該框架的下載跟蹤屬性在 `analytics.sitecatalyst.js` 為頁面生成的檔案。 以下代碼示例表示預設下載跟蹤配置：

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

要啟用Adobe Analytics框架的下載跟蹤：

1. [開啟Adobe Analytics框架並展開「連結跟蹤配置」部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 啟用 **跟蹤下載**。
1. 在 **下載檔案類型** 框中，鍵入要跟蹤的檔案類型的檔案副檔名。

## 跟蹤外部連結 {#tracking-external-links}

您可以跟蹤頁面上外部連結（退出連結）的按一下。

要跟蹤Adobe Analytics框架的外部連結：

1. [開啟Adobe Analytics框架， **連結跟蹤配置** 節](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根據您的要求配置以下屬性。

按一下外部連結時用於跟蹤的屬性：

* **跟蹤外部**
啟用外部連結跟蹤。

* **外部篩選器**
（可選）定義用於匹配連結目標的外部URL的篩選器。 當連結目標與篩選器匹配時，將跟蹤連結。 外部篩選器僅用於跟蹤頁面上的某些外部連結。

   要指定要跟蹤的外部連結，請鍵入連結目標的URL的全部或部分。 用逗號分隔多個篩選器。 將字串文字用單引號括起來。 無值(預設值為 `''`，兩個單引號)將跟蹤所有外部連結。

* **內部篩選器**
定義用於匹配內部連結的URL的篩選器。 當連結指向與此篩選器匹配的URL時，不跟蹤該連結。 預設值是javascript命令，返回當前窗口地址的URL主機名。

   要指定未跟蹤的內部連結，請鍵入連結目標的內部URL的全部或部分。 用逗號分隔多個篩選器。 將字串文字用單引號括起來。

   預設值為 `'javascript:,'+window.location.hostname`

* **保留查詢字串**
在計算與內部和外部篩選器的匹配時包括URL參數。

   啟用以在根據外部和內部篩選器評估連結目標URL時包括URL參數。

外部鏈路跟蹤屬性在 `analytics.sitecatalyst.js` 為頁面生成的檔案。 為與啟用了外部連結跟蹤的框架關聯的頁面生成以下示例代碼：

* 外部篩選器為 `'google.com'`
* 內部篩選器是 `'javascript:,'+window.location.hostname`
* 根據篩選器評估連結目標時不包括查詢字串。

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## 通過按一下連結發送變數資料 {#sending-variable-data-with-link-clicks}

您可以配置AEM在用戶按一下連結時將事件和變數資料發送到Adobe Analytics。 的 **連結跟蹤配置** 屬性允許您指定在連結按一下時跟蹤的Adobe Analytics事件和變數。

框架映射確定事件和變數值。 您可以將Adobe Analytics變數映射到內容元件的變數，這些變數儲存在按一下連結時要跟蹤的資料。

要通過連結按一下來發送變數資料：

1. [開啟Adobe Analytics框架並展開「連結跟蹤配置」部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根據您的要求配置以下屬性。

通過連結按一下發送變數資料的屬性：

* **連結跟蹤事件**
輸入要用於計數連結按一下次數的Adobe Analytics事件變數。

   用逗號分隔多個變數名稱。

   預設值 `None` 導致事件跟蹤。

* **連結跟蹤變數**
輸入按一下連結時要發送到Adobe Analytics的Adobe Analytics變數。 用逗號分隔多個變數名稱。

   預設值 `None` 導致無變數資料被發送。

指定要發送的事件和變數時，配置將在 `analytics.sitecatalyst.js` 為頁面生成的檔案。 框架跟蹤頁面時，將為頁面生成以下示例代碼 `event10` 事件和 `prop4` 屬性：

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## 連結跟蹤配置示例 {#example-link-tracking-configuration}

執行以下步驟以探討Adobe Analytics整合的連結跟蹤行為。 過程顯示結果來自 [Adobe Marketing Cloud調試器](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html)。

### 常規配置 {#general-configuration}

此示例說明映射在跟蹤和調試器的上下文中如何工作：

1. 開啟已與網頁關聯的框架。
1. 拖動 **頁面** 元件到框架的映射區域。 的 **頁面** 元件屬於 **常規** Sidekick中的元件組。

   >[!NOTE]
   >
   >在實際場景中應使用的元件取決於繼承自的元件（如果是）。
   >
   >如果不是，您應將自己的元件暴露在其中（通過在其頁面元件中定義分析子節點）。

   通過從左側面板拖動分析(SiteCatalyst)變數，根據下表配置映射：

<table>
 <tbody>
  <tr>
   <th>CQ變數<br /> </th>
   <th>變數瀏覽器中的條目<br /> </th>
   <th>Adobe Analytics變數</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>自定義eVar1(eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>自定義1（事件1）</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. 將「搜索」元件拖到框架的映射區域。 搜索元件屬於Sidekick中的「常規」元件組。 通過從左側面板拖動分析(SiteCatalyst)變數，根據下表配置映射：

<table>
 <tbody>
  <tr>
   <th>CQ變數<br /> </th>
   <th>變數瀏覽器中的條目</th>
   <th>Adobe Analytics變數</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>自定義eVar2(eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>自定義eVar3(eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>自定義2（事件2）</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### 配置外部鏈路跟蹤 {#configure-external-link-tracking}

1. 在框架中，展開 **連結跟蹤配置** 的子菜單。
1. 取消選擇 **跟蹤下載**。

1. 選擇 **跟蹤外部**。
1. 取消選擇 **保留查詢字串**。
1. 使用以下值 **外部篩選器** 清單，將其標識為外部URL:

   `‘yahoo.com’`

1. 將以下值添加到 **連結跟蹤事件** 欄位：

   ```
       event1,event2
   ```

1. 將以下值添加到 **連結軌道變數** 欄位：

   ```
       eVar1,eVar2
   ```

1. 在與框架關聯的頁面上，添加 **文本** 元件。 在 **文本** 添加指向以下地址的超連結：

   `https://search.yahoo.com/?p=this`

1. 切換到 **預覽模式** 按一下連結。

在使用Adobe Marketing Cloud調試器查看時，所發出的調用將如下所示：

![a-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>該URL不包含查詢字串： `?p=this`

### 包括URL參數 {#include-the-url-parameter}

1. 在框架中，展開 **連結跟蹤配置** 的子菜單。
1. 啟用 **保留查詢字串**。
1. 重新載入頁面預覽，然後按一下連結。

在Adobe Marketing Cloud調試器中顯示的調用詳細資訊與以下示例類似：

![a-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>此時，URL確實包含查詢字串： `?p=this`

## 點對點鏈路跟蹤 {#ad-hoc-link-tracking}

點對點連結跟蹤允許內容作者為元件配置連結跟蹤。 元件的配置將覆蓋 **連結跟蹤配置** 框架，所以在與框架關聯的頁面上， **文本** 可以配置元件以跟蹤URL的連結。

點對點連結跟蹤使您能夠跟蹤下載連結、外部連結以及事件和變數資料。

要啟用點對點連結跟蹤，您需要：

* [關聯包含 **文本** 具有框架的元件](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。
* [配置Adobe Analytics框架以啟用點對點鏈路跟蹤](#enabling-ad-hoc-link-tracking)。
* [配置文本元件的連結跟蹤](#configuring-link-tracking-for-a-text-component)。

### 啟用即席鏈路跟蹤 {#enabling-ad-hoc-link-tracking}

配置Adobe Analytics框架以啟用點對點鏈路跟蹤。

1. 開啟Adobe Analytics框架， **連結跟蹤配置** 的子菜單。

1. 啟用 **即席鏈路跟蹤**。

   >[!NOTE]
   >
   >並非所有用戶類型都有權訪問此複選框。 如果需要訪問權限，請與網站管理員聯繫。

>[!NOTE]
>
>XSS反滑結構現在在SLING下 **/libs/sling/xss.config.xml** 需要添加以下規則，以便臨時連結到工作：

#### 錨記規則擴展 {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### 配置文本元件的連結跟蹤 {#configuring-link-tracking-for-a-text-component}

在配置點對點連結跟蹤之前 **文本** 元件本身，必須已實施以下配置：

* 的 [Adobe Analytics框架配置為啟用ad hoc鏈路跟蹤](#enabling-ad-hoc-link-tracking)。
* 的 [包含 **文本** 元件與框架關聯](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。

請按下列步驟為 **文本** 元件：

1. 以編輯模式開啟頁面並編輯 **文本** 元件。

1. 選擇要用作超文本的文本，然後按一下「超連結」按鈕。

   ![](do-not-localize/chlimage_1.png)

1. 在「連結到」框中添加目標URL，然後展開「連結跟蹤」區域。

   >[!NOTE]
   >
   >自定義連結跟蹤可以作為單獨的操作顯示，位於「連結/解除連結」操作（分析表徵圖）旁。
   >
   >只有在選擇了RTE中的有效連結時，才會啟用它。

   ![aa-17](assets/aa-17.png)

1. 啟用 **自定義連結跟蹤** 覆蓋Adobe Analytics框架的鏈路跟蹤配置並啟用當前連結的連結跟蹤。

1. （可選）要通過按一下連結跟蹤事件，請在 **包括Adobe Analytics變數** 的子菜單。 用逗號分隔多個事件名稱，例如

   `event1, event22`。

1. （可選）要通過按一下連結跟蹤變數資料，請在 **包括Adobe Analytics變數** 的子菜單。 使用下列格式之一：

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`‘CONSTANT'`*

   以下示例說明了每種格式：

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   用逗號分隔多個值。

1. 選擇 **確定**。
