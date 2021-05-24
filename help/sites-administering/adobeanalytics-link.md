---
title: 設定Adobe Analytics的連結追蹤
seo-title: 設定Adobe Analytics的連結追蹤
description: 了解如何設定SiteCatalyst的連結追蹤。
seo-description: 了解如何設定SiteCatalyst的連結追蹤。
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# 設定Adobe Analytics的連結追蹤{#configuring-link-tracking-for-adobe-analytics}

當使用者按一下您網站頁面上的連結時，即可在Adobe Analytics中擷取相關資訊。 例如，使用連結追蹤來了解使用者如何與您的網站互動、追蹤檔案下載及追蹤退出連結。

## 為Adobe Analytics架構{#configuring-link-tracking-for-an-adobe-analytics-framework}設定連結追蹤

1. 使用&#x200B;**導覽**，透過&#x200B;**部署**、**Cloud Services**&#x200B;前往&#x200B;**Adobe Analytics**&#x200B;區段。

1. 使用&#x200B;**顯示配置**&#x200B;開啟所需的Adobe Analytics框架。
1. 展開&#x200B;**連結追蹤設定**&#x200B;區段，並視需要進行設定（本頁面提供詳細資訊）:

   ![aa-08](assets/aa-08.png)

## 追蹤檔案下載{#tracking-file-downloads}

設定Adobe Analytics架構，以便從關聯頁面下載的檔案在Adobe Analytics中以下載形式自動受到追蹤。 當您啟用下載追蹤時，只會追蹤您指定的檔案類型。

預設會追蹤下列檔案類型的下載：

* exe
* ZIP
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* PDF
* xls

因此，例如，在為PDF檔案啟用下載追蹤時，每當使用者按一下PDF檔案的連結時，就會追蹤PDF的下載。

框架的下載跟蹤屬性在為頁面生成的`analytics.sitecatalyst.js`檔案中以代碼的形式實現。 下列程式碼範例代表預設的下載追蹤設定：

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

若要啟用Adobe Analytics架構的下載追蹤：

1. [開啟Adobe Analytics架構，然後展開「連結追蹤設定」區段](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 啟用&#x200B;**追蹤下載**。
1. 在&#x200B;**下載檔案類型**&#x200B;框中，鍵入要跟蹤的檔案類型的副檔名。

## 追蹤外部連結{#tracking-external-links}

您可以追蹤頁面上外部連結（退出連結）的點按。

若要追蹤Adobe Analytics架構的外部連結：

1. [開啟Adobe Analytics架構，然後展開「連 **結追蹤** 設定」區段](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根據您的需求設定下列屬性。

點按外部連結時的追蹤屬性：

* **追蹤外**
部啟用外部連結追蹤。

* **外部篩選器**
（選用）定義用以比對連結目標的外部URL的篩選器。當連結目標符合篩選時，就會追蹤連結。 外部篩選器對於只追蹤您頁面上的部分外部連結很實用。

   若要指定要追蹤的外部連結，請輸入連結目標的全部或部分URL。 請使用逗號分隔多個篩選器。 將字串文字括在單引號中。 沒有值（預設值`''`，兩個單引號）會導致所有外部連結受到追蹤。

* **內部**
篩選器定義用於匹配內部連結URL的篩選器。當連結鎖定符合此篩選的URL時，不會追蹤連結。 預設值是javascript命令，可傳回目前視窗位址的URL主機名稱。

   若要指定未追蹤的內部連結，請輸入連結目標的全部或部分內部URL。 請使用逗號分隔多個篩選器。 將字串文字括在單引號中。

   預設值為 `'javascript:,'+window.location.hostname`

* **在評估與內**
部和外部篩選器的相符項目時，請保留查詢字串包含URL參數。

   根據外部和內部篩選器評估連結目標URL時，啟用以包含URL參數。

外部連結追蹤屬性在為頁面產生的`analytics.sitecatalyst.js`檔案中以程式碼的形式實作。 系統會為與已啟用外部連結追蹤的架構相關聯的頁面，透過下列設定產生下列范常式式碼：

* 外部篩選器為`'google.com'`
* 內部篩選器是`'javascript:,'+window.location.hostname`的預設值
* 根據篩選條件評估連結目標時不會包含查詢字串。

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## 傳送含有連結點按次數的變數資料{#sending-variable-data-with-link-clicks}

您可以設定使用者按一下連結時，將事件和變數資料傳送至Adobe Analytics。 **連結追蹤設定**&#x200B;屬性可讓您指定要在發生連結點按時追蹤的Adobe Analytics事件和變數。

架構對應會決定事件和變數值。 您可以將Adobe Analytics變數對應至內容元件的變數，這些變數會在您點按連結時儲存您要追蹤的資料。

若要隨連結點按傳送變數資料：

1. [開啟Adobe Analytics架構，然後展開「連結追蹤設定」區段](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根據您的需求設定下列屬性。

透過連結點按傳送變數資料的屬性：

* **連結追**
蹤事件輸入您要用來計算連結點擊次數的Adobe Analytics事件變數。

   請使用逗號分隔多個變數名稱。

   預設值`None`不會導致事件追蹤。

* **連結追**
蹤變數輸入在按一下連結時，您要傳送至Adobe Analytics的Adobe Analytics變數。請使用逗號分隔多個變數名稱。

   預設值`None`不會傳送任何變數資料。

當您指定要傳送的事件和變數時，會在為頁面產生的`analytics.sitecatalyst.js`檔案中以程式碼方式實作設定。 當架構追蹤`event10`事件和`prop4`屬性時，會為頁面產生下列范常式式碼：

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## 連結追蹤設定範例{#example-link-tracking-configuration}

執行下列程式，探索Adobe Analytics整合的連結追蹤行為。 程式會顯示[Adobe Marketing Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)的結果。

### 一般配置{#general-configuration}

此範例說明對應如何在追蹤和偵錯工具的內容中運作：

1. 開啟已與網頁關聯的架構。
1. 將&#x200B;**Page**&#x200B;元件拖曳至架構的對應區域。 **Page**&#x200B;元件屬於Sidekick中的&#x200B;**General**&#x200B;元件組。

   >[!NOTE]
   >
   >您在實際案例中應使用的元件取決於繼承的元件（如果有）。
   >
   >若非如此，您應將自己的元件公開於該處（透過在其頁面元件中定義分析子節點）。

   從左側面板拖曳Analytics(SiteCatalyst)變數，以根據下表設定對應：

<table>
 <tbody>
  <tr>
   <th>CQ變數<br /> </th>
   <th>變數瀏覽器中的項<br /> </th>
   <th>Adobe Analytics變數</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>自訂eVar1(eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>自訂1(event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. 將「搜索」元件拖動到框架的映射區。 Search元件屬於Sidekick中的General元件組。 從左側面板拖曳Analytics(SiteCatalyst)變數，以根據下表設定對應：

<table>
 <tbody>
  <tr>
   <th>CQ變數<br /> </th>
   <th>變數瀏覽器中的輸入</th>
   <th>Adobe Analytics變數</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>自訂eVar2(eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>自訂eVar3(eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>自訂2(event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### 設定外部連結追蹤{#configure-external-link-tracking}

1. 在您的架構中，展開&#x200B;**連結追蹤設定**&#x200B;區域。
1. 取消選擇&#x200B;**追蹤下載**。

1. 選擇&#x200B;**Track External**。
1. 取消選擇&#x200B;**保留查詢字串**。
1. 對&#x200B;**外部篩選器**&#x200B;清單使用下列值，將其識別為外部URL:

   `‘yahoo.com’`

1. 將下列值新增至&#x200B;**連結追蹤事件**&#x200B;欄位：

   ```
       event1,event2
   ```

1. 將下列值新增至&#x200B;**連結追蹤變數**&#x200B;欄位：

   ```
       eVar1,eVar2
   ```

1. 在與框架關聯的頁面上，添加&#x200B;**Text**&#x200B;元件。 在&#x200B;**Text**&#x200B;元件內，添加指向以下地址的超連結：

   `https://search.yahoo.com/?p=this`

1. 切換至&#x200B;**預覽模式**，然後按一下連結。

使用Adobe Marketing Cloud Debugger檢視時，發出的呼叫將如下所示：

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>URL不包含查詢字串：`?p=this`

### 納入URL參數{#include-the-url-parameter}

1. 在框架中，展開&#x200B;**連結追蹤設定**&#x200B;區域。
1. 啟用&#x200B;**保留查詢字串**。
1. 重新載入頁面預覽，然後按一下連結。

Adobe Marketing Cloud Debugger中顯示的呼叫詳細資料類似下列範例：

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>此時，URL不會包含查詢字串：`?p=this`

## 臨機連結追蹤{#ad-hoc-link-tracking}

臨機連結追蹤可讓內容作者設定元件的連結追蹤。 元件的配置將覆蓋框架的&#x200B;**連結跟蹤配置**，因此，在與框架關聯的頁面上，可以配置&#x200B;**文本**&#x200B;元件以用於URL的連結跟蹤。

臨機連結追蹤可讓您追蹤下載連結、外部連結，以及事件和變數資料。

若要啟用臨機連結追蹤，您必須：

* [將包含Text元件的頁 **** 面與框架相關聯](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。
* [設定Adobe Analytics架構以啟用臨機連結追蹤](#enabling-ad-hoc-link-tracking)。
* [設定文字元件的連結追蹤](#configuring-link-tracking-for-a-text-component)。

### 啟用臨機連結追蹤{#enabling-ad-hoc-link-tracking}

設定您的Adobe Analytics架構以啟用臨機連結追蹤。

1. 開啟Adobe Analytics架構，並展開&#x200B;**連結追蹤設定**&#x200B;區段。

1. 啟用&#x200B;**臨機連結追蹤**。

   >[!NOTE]
   >
   >並非所有使用者類型都能存取此核取方塊。 如果您需要存取權限，請連絡您的網站管理員。

>[!NOTE]
>
>XSS Antisamy設定現在位於路徑&#x200B;**/libs/sling/xss.config.xml**&#x200B;下的SLING中，且需要新增下列規則，才能讓臨機連結運作：

#### 錨點標籤規則副檔名{#anchor-tag-rule-extension}

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

### 配置文本元件{#configuring-link-tracking-for-a-text-component}的連結跟蹤

若要設定&#x200B;**Text**&#x200B;元件本身的臨機連結追蹤，必須已實作下列設定：

* [Adobe Analytics架構已設定為啟用臨機連結追蹤](#enabling-ad-hoc-link-tracking)。
* 包含&#x200B;**Text**&#x200B;元件的[頁面與框架](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)相關聯。

請依照下列程式來設定&#x200B;**Text**&#x200B;元件的連結追蹤：

1. 以編輯模式開啟頁面，並編輯&#x200B;**Text**&#x200B;元件。

1. 選擇要用作超文本的文本，然後按一下「超連結」按鈕。

   ![](do-not-localize/chlimage_1.png)

1. 在「連結至」方塊中新增目標URL，然後展開「連結追蹤」區域。

   >[!NOTE]
   >
   >自訂連結追蹤會以個別動作的形式顯示，位於「連結/取消連結」動作（Analytics圖示）旁。
   >
   >只有在您已在RTE中選取有效的連結時，才會啟用此功能。

   ![aa-17](assets/aa-17.png)

1. 啟用&#x200B;**自訂連結追蹤**&#x200B;以覆寫Adobe Analytics架構的連結追蹤設定，並啟用目前連結的連結追蹤。

1. （選用）若要追蹤含有連結點擊的事件，請在&#x200B;**「包含Adobe Analytics變數」欄位中新增Adobe Analytics事件名稱。**&#x200B;以逗號分隔多個事件名稱，例如

   `event1, event22`。

1. （選用）若要透過連結點擊追蹤變數資料，請在&#x200B;**「包含Adobe Analytics變數」欄位中新增Adobe Analytics變數**。 使用下列任一格式：

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*:  *`‘CONSTANT'`*

   下列範例說明各種格式：

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   請使用逗號分隔多個值。

1. 選擇&#x200B;**OK**。
