---
title: Communities功能的Analytics設定
seo-title: Communities功能的Analytics設定
description: 為社群設定分析
seo-description: 為社群設定分析
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Administrator
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2756'
ht-degree: 3%

---

# Communities功能的Analytics設定{#analytics-configuration-for-communities-features}

## 概覽 {#overview}

Adobe Analytics和Adobe Experience Manager(AEM)都是Adobe Marketing Cloud的解決方案。

Adobe Analytics可針對AEM Communities進行設定，以便成員與支援的社群功能互動時，事件會傳送至Adobe Analytics，並從中產生報表。

例如，當啟用社群網站的成員檢視指派給他們的視訊資源時，資源播放器會將事件傳送至Analytics，包括視訊心率資料。 從社群網站，管理員可以查看有關播放視訊的各種報表。

此外，對於以下情況，也需要分析：

* 在發佈環境中：

   * 關於社群[趨勢](/help/communities/trends.md)的報告
   * 允許網站訪客依「檢視次數最多」、「最活躍」、「最喜歡」排序
   * 查看UGC清單上的計數

* 在製作環境中：

   * 在[成員管理控制台](/help/communities/members.md)中顯示參與率資料（檢視、貼文、後續、按贊）
   * 啟用資源[報表](/help/communities/reports.md)的趨勢摘要、視訊心率和視訊裝置

支援的社群功能包括：

* [啟用資源](/help/communities/resources.md)
* [論壇](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [部落格](/help/communities/blog-feature.md)
* [檔案庫](/help/communities/file-library.md)
* [日曆](/help/communities/calendar.md)

本檔案的本節說明如何將Analytics報表套裝與Communities功能連結。 基本步驟為：

1. [複製加密密](#replicate-the-crypto-key) 鑰以確保在所有AEM實例上正確進行加密/解密
1. 準備Adobe Analytics [報表套裝](#adobe-analytics-report-suite-for-video-reporting)
1. 建立AEM Analytics [雲端服務](#aem-analytics-cloud-service-configuration)和[framework](#aem-analytics-framework-configuration)

1. [為社](#enable-analytics-for-a-community-site) 群網站啟用分析
1. [****](#verify-analytics-to-aem-variable-mapping) 驗證AEM與Analytics變數的對應
1. 識別[主要發佈者](#primary-publisher)
1. [](#publish-community-site-and-analytics-cloud-service) 發佈社群網站
1. 設定從Adobe Analytics匯入[報表資料](#obtaining-reports-from-analytics)至社群網站

## 必備條件 {#prerequisites}

若要設定Analytics for Communities功能，必須與您的帳戶代表合作，設定Adobe Analytics帳戶和[報表套裝](#adobe-analytics-report-suite-for-video-reporting)。 建立後，應提供下列資訊：

* **公司名稱**

   與Adobe Analytics帳戶相關聯的公司。

* **使用者名稱**

   獲授權管理Analytics帳戶之使用者的登入使用者名稱
（應包含網站服務存取權限）。

* **密碼**

   授權用戶的登錄密碼。

* **Analytics資料中心**

   帳戶的Analytics資料中心URL。

* **報表套裝**

   要使用的Analytics報表套裝名稱。

## Adobe Analytics視訊報表報表套裝{#adobe-analytics-report-suite-for-video-reporting}

使用Adobe Marketing Cloud的[報表套裝管理器](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)，即可設定Analytics報表套裝，讓社群網站能夠提供社群功能的報表。

透過[公司名稱和使用者名稱](/help/communities/analytics.md#prerequisites)登入[Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html)，即可設定新或現有的報表套裝，使其具備：

* [11轉換變數](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** 啟用 **`evar11`** 

   * 可以重新使用（重新命名）現有的eVar，或建立新eVar以用於Communities功能

* [7成功事件](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html) （事件）

   * **`event1`** 啟用 **`event7`** 

   * 類型 **`Counter`**

      * 非 **`Counter (no subrelations)`**
   * 可以重新使用（重新命名）現有事件，或建立新事件以用於Communities功能


* [視訊管理](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * 視訊報表主控台

      * 啟用 `Video Core`
      * 選擇保存
   * 視訊核心測量主控台

      * 選取 `Use Solution Variables`
      * 選擇保存


若使用&#x200B;**新的報表套裝**，請注意，新的報表套裝可能只有4個eVar和6個事件變數，而Communities則需有11個eVar和7個事件變數。

若使用&#x200B;**現有報表套裝**，則在啟用社群網站的Analytics架構之前，可能需要[修改變數對應](#modifying-analytics-variable-mapping)。

如對社群專用變數有任何疑慮，請連絡您的客戶代表。

>[!CAUTION]
>
>**若使用的現有報表套裝已在**
>
>* **`evar1`** through  **`evar11`**
   >
   >
* **`event1`** through  **`event7`**
>
>
**然後，在社群網站發佈前，** 請務必移動在社群網站啟用Analytics時，自動對應至Analytics變數的AEM變數，以還原原先的對應。
>
>若要還原預先存在的對應並將AEM變數移至其他Analytics變數，請參閱[修改Analytics變數對應](#modifying-analytics-variable-mapping)上的一節。
>
>若無法這麼做，可能會導致無法復原的資料遺失。

### 視訊心率分析{#video-heartbeat-analytics}

授權Video Heartbeat Analytics時，會指派`Marketing Cloud Org Id`。

若要在[設定視訊報表的Analytics報表套裝](#adobe-analytics-report-suite-for-video-reporting)後啟用視訊心率報表：

* 建立[Analytics雲端服務](#aem-analytics-cloud-service-configuration)
* 為社群網站啟用[Analytics](#enable-analytics-for-a-community-site)
* 將`Marketing Cloud Org Id`與社區站點關聯

`Marketing Cloud Org Id`可在[社區站點建立](/help/communities/sites-console.md#enablement)時或更後通過[修改](/help/communities/sites-console.md#modifying-site-properties)社區站點屬性來輸入。[](#aem-analytics-cloud-service-configuration)

![marketing-org-id](assets/marketing-org-id.png)

啟用視訊心率分析時，視訊播放器的JavaScript(JS)程式碼會實例化視訊心率程式庫程式碼（亦在JS中），此程式碼會處理每10秒傳送視訊狀態更新至Analytics視訊追蹤伺服器（不可設定）的所有邏輯，並最終傳送視訊工作階段的累積報表至主要Analytics伺服器。

若未啟用，視訊心率程式碼將不會具現化，且只會將視訊進度和繼續位置追蹤保存至SRP以供報告。

## AEM Analytics Cloud服務設定{#aem-analytics-cloud-service-configuration}

若要使用製作執行個體上的標準UI，建立整合Adobe Analytics與AEM社群網站的新Analytics整合：

* 從全局導航：**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**
* 向下捲動至&#x200B;**[!UICONTROL Adobe Analytics]**
* 選擇「**[!UICONTROL 立即配置]**」或「**[!UICONTROL 顯示配置]**」

![雲端設定](assets/cloud-config1.png)

### 建立配置對話框{#create-configuration-dialog}

* 選擇&#x200B;**[!UICONTROL 可用配置]**&#x200B;旁的`[+]`表徵圖以建立新配置

在「建立配置」對話框中，要輸入的值標識配置。

![create-cloud-config](assets/cloud-config2.png)

* **標題**

   （必要）設定的顯示標題。
例如，輸入*啟用社群分析*

* **名稱**

   （可選）如果未指定，則名稱將預設為從標題派生的有效節點名稱。
例如，輸入*communities*

* **範本**

   選取 `Adobe Analytics Configuration`

* 選擇&#x200B;**建立**

   * 啟動配置頁並開啟`Analytics Settings`對話框

### 分析設定對話方塊{#analytics-settings-dialog}

初始建立新Analytics設定時，會顯示設定，並顯示新對話方塊，供您輸入Analytics設定。 此對話框要求從帳戶代表處獲取[必備帳戶資訊](#prerequisites)。

![analytics-settings](assets/analytics-settings.png)

* **公司**

   與Adobe Analytics帳戶相關聯的公司。

* **使用者名稱**

   獲授權管理Analytics帳戶之使用者的登入使用者名稱。

* **密碼**

   授權用戶的登錄密碼。

* **資料中心**

   選取托管報表套裝的Analytics資料中心。

* **不要新增追蹤標記至頁面**

   保留為預設值（取消選取）。

* **使用 AppMeasurement**

   保留為預設值（取消選取）。

* **不要每晚匯入頁面印象 (作者)**

   保留為預設值（取消選取）。

* **不要每晚匯入頁面印象 (發佈)**

   保留為預設值（取消選取）。

若要儲存設定：

* 選取&#x200B;**連線至Analytics**

   * 若未成功，

      * 驗證條目不包含前導空格。
      * 嘗試其他資料中心。

* 選擇&#x200B;**OK**。

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### 建立框架 {#create-framework}

成功設定與Adobe Analytics的基本連線後，必須建立或編輯社群網站的架構。 此架構的目的是將Communities功能(AEM)變數對應至Analytics（報表套裝）變數。

* 選取&#x200B;**[!UICONTROL 可用架構]**&#x200B;旁的`[+]`圖示以建立新架構

   ![analytics-framework](assets/analytics-framework.png)

* **標題**

   （必要）架構的顯示標題
例如，輸入*啟用社群架構*。

* **名稱**

   （可選）如果未指定，則名稱將預設為從標題派生的有效節點名稱。
例如，輸入*communities*。

* *範本*

   選取 `Adobe Analytics Framework`.

* 選擇 **建立**。

建立Analytics架構會開啟設定的架構。

## AEM Analytics架構設定{#aem-analytics-framework-configuration}

此架構的用途是將AEM變數對應至Analytics變數（eVar和事件）。 可用於對應的Analytics變數為[，定義於報表套裝](#adobe-analytics-report-suite-for-video-reporting)中。

![analytics-enablement-framework](assets/analytics-framework1.png)

### 選擇報表套裝{#select-report-suite}

選取已針對視訊報表設定的報表套裝。

如果報表套裝尚未建立或未正確設定，請參閱上一節：
[Adobe Analytics視訊報表報表套裝](#adobe-analytics-report-suite-for-video-reporting)

不需要Sidekick，且可盡可能最小化，以免妨礙存取報表套裝設定。

#### 選取「新增項目」{#report-suites-dialog-before-and-after-selecting-add-item}之前和之後的報表套裝對話方塊

![報表套裝](assets/report-suite.png)

1. 選擇&#x200B;**添加項+**。

   隨即顯示兩個下拉式方塊。

1. 選擇`Report suite.`

   可選擇與公司帳戶相關聯的報表套裝。

1. 在開啟的對話框中選擇&#x200B;**是**:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. 選擇`Run Mode`。

1. 選擇&#x200B;**Publish**。

![analytics-framework2](assets/analytics-framework2.png)

Analytic雲服務和架構現已完成。 一旦建立社群網站並啟用此Analytics服務，就會定義對應。

## 為社群網站{#enable-analytics-for-a-community-site}啟用Analytics

### 為新社區站點{#enable-for-new-community-site}啟用

若要在[建立新社群網站](/help/communities/sites-console.md)時新增Analytics雲端服務：

* 在步驟3中，在[ANALYTICS標籤](/help/communities/sites-console.md#analytics)下：
   * 選取&#x200B;**啟用Analytics**&#x200B;核取方塊。
   * 從下拉式方塊中選取架構。

* （可選）返回Analytics架構設定以調整變數對應。

### 啟用現有社區站點{#enable-for-existing-community-site}

若要將Analytics雲端服務新增至[現有社群網站](/help/communities/sites-console.md#modifying-site-properties):

* 導覽至&#x200B;**Communities > Sites**&#x200B;主控台。
* 選擇社區站點的「編輯站點」表徵圖。
* 選取「設定」。
* 在Analytics區段中：
   * 選取&#x200B;**啟用Analytics**&#x200B;核取方塊。
   * 從下拉式方塊中選擇架構。

* （可選）返回Analytics架構設定以調整變數對應。

### 啟用自定義站點{#enable-for-customized-sites}

為了讓Analytics追蹤和匯入正常運作社群網站，必須存在具有`scf-js-site-title`類別和href屬性的頁面元素。 頁面上只應存在一個此類元素，例如社群網站的未修改`sitepage.hbs`指令碼中。 會擷取`siteUrl`的值，並以&#x200B;*網站路徑*&#x200B;的形式傳送至Adobe Analytics。

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

對於覆蓋`sitepage.hbs`指令碼的&#x200B;**自訂社群網站**，請確保元素存在。 `siteUrl`變數將在伺服器上呈現後再提供給客戶端時設定。

對於&#x200B;**一般AEM網站**（包含Communities元件），但未使用[網站建立精靈](/help/communities/sites-console.md)建立)，必須新增元素。 href的值應為網站路徑。 例如，如果網站路徑為`/content/my/company/en`，則使用：

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Analytics for Communities功能{#analytics-for-communities-features}

Analytics會自動用於數個Communities功能。

製作環境的[OSGi設定](/help/sites-deploying/configuring-osgi.md)、`AEM Communities Analytics Component Configuration`提供已為Analytics檢測的元件清單。 變數的自動對應由列出的元件決定。

如果已建立為Analytics創作的新自訂元件，則應將其新增至已設定元件的清單。

### 元件配置{#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>日誌元件用於實施部落格功能。

### 將Analytics對應至AEM變數{#mapped-analytics-to-aem-variables}

在啟用Analytics並選取雲端設定架構後，儲存社群網站時，AEM變數會自動對應至分別以evar1和event1開頭的Analytics eVar和事件，並增加1。

如果使用將evar1至evar11內任何變數以及event1至event7內的任何變數對應的現有報表套裝，則必須[重新映射AEM變數](#modifying-analytics-variable-mapping)並還原原始對應。

以下是遵循[快速入門教程](/help/communities/getting-started-enablement.md)之後的預設映射的示例：

![map-analytics](assets/map-analytics1.png)

#### 隨每個事件{#map-of-evars-sent-with-each-event}傳送的eVar地圖

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>啟用<br />資源<br />類型</strong></td>
   <td><strong>網站<br />標題</strong></td>
   <td><strong>函式<br />類型</strong></td>
   <td><strong>組<br />標題</strong></td>
   <td><strong>組<br />路徑</strong></td>
   <td><strong>UGC<br />類型</strong></td>
   <td><strong>UGC<br />標題</strong></td>
   <td><strong>用戶<br />（成員）</strong></td>
   <td><strong>UGC<br />路徑</strong></td>
   <td><strong>站點<br />路徑</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br />資源播放</strong></td>
   <td><em>(a)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>(i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(a)</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate(Post)</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
 </tbody>
</table>

**eVar值的範例：**

* *[MIME類型](https://www.iana.org/assignments/media-types)*:video/mp4
* *[社群網站標題](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixx社群
* *[社群函式名稱](/help/communities/functions.md)*:論壇
* *[社群群組名稱](/help/communities/creating-groups.md#creating-a-new-group)*:徒步旅行
* *社群群組內容路徑*:  `/content/sites/<site name>/en/groups/hiking`
* *[UGC元件resourceType](/help/communities/essentials.md)*:  `social/forum/components/hbs/topic`
* *UGC元件標題*:健行主題
* *login（可授權ID）*:  `aaron.mcdonald@mailinator.com`
* *SRP到UGC的路徑*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
或 
*要遵循的元件路徑*:  `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *社群網站內容路徑*:  `/content/sites/<site name>/en`

### 修改Analytics變數對應{#modifying-analytics-variable-mapping}

為社群網站啟用Analytics後，可從架構設定看到Analytics eVar和事件對應至AEM變數。

啟用Analytics後，在社群網站發佈前，您可將所需的Analyticsevar或事件從左側邊欄拖曳至對應表格中的相關列，以在架構中變更對應。

若要避免重複對應，請務必將游標移至該列並選取Analytics變數元素右側顯示的「X」，以移除該列中已取代的Analytics evar或事件。

如果Communities eVar和事件覆寫報表套裝中預先存在的對應，則為避免資料遺失，請將Communities功能的AEM變數指派至其他Analytics eVar或事件，並還原原始對應。

>[!CAUTION]
>
>在啟用Analytics後，請務必在社群網站[已發佈](#publishing-the-community-site)前重新映射，否則就有資料遺失的風險。

#### 範例步驟1:將Analytics evar14拖曳至對應表{#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### 範例步驟2:選取「x」以移除已取代的evar11 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### 範例步驟3:AEM var eventdata.siteId重新對應至Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## 發佈社群網站{#publishing-the-community-site}

### 驗證Analytics與AEM變數的對應{#verify-analytics-to-aem-variable-mapping}

發佈社群網站（亦會發佈Analytics雲端服務和架構）前，最好先驗證變數對應。

請參閱以下章節：

* [將Analytics對應至AEM變數](#mapped-analytics-to-aem-variables)
* [修改Analytics變數對應](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**若使用的現有報表套裝已在**
>
>* **`evar1`** through  **`evar11`**
   >
   >
* **`event1`** through  **`event7`**
>
>
**然後，在社群網站發佈前，** 請務必還原原先的對應，並將自動對應的Communities AEM變數（當社群網站已啟用Analytics時）移至其他Analytics變數。此重新對應應在所有Communities元件之間保持一致。
>
>若無法這麼做，可能會導致無法復原的資料遺失。

### 主發佈者{#primary-publisher}

當選擇的部署是[publish farm](/help/communities/topologies.md#tarmk-publish-farm)時，必須將一個AEM發佈執行個體識別為輪詢Adobe Analytics以寫入[SRP](/help/communities/working-with-srp.md)的報表資料的主要發佈者。

依預設，`AEM Communities Publisher Configuration` OSGi設定會將其發佈執行個體識別為主要發佈者，這樣發佈伺服器陣列中的所有發佈執行個體都會自行識別為主要發佈者。

因此，必須編輯所有次要發佈執行個體的設定，以取消選取「**主要發佈者**」核取方塊。

有關具體說明，請參閱[Deploying Communities](/help/communities/deploy-communities.md#primary-publisher)的主要發佈者部分。

>[!CAUTION]
>
>請務必將主要發佈者設定為防止從多個發佈執行個體進行輪詢。

### 複製加密密鑰{#replicate-the-crypto-key}

Adobe Analytics憑證會經過加密。 為方便製作者與發佈者之間復寫或傳輸加密的AEM憑證，所有Analytics執行個體必須共用相同的主要加密金鑰。

要執行此操作，請按照[複製加密密鑰](/help/communities/deploy-communities.md#replicate-the-crypto-key)中的說明操作。

### 發佈社群網站和Analytics Cloud服務{#publish-community-site-and-analytics-cloud-service}

為社群網站啟用Analytics雲端服務後，若有需要，[對應AEM變數](#mapped-analytics-to-aem-variables)便需要透過[(re)發佈社群網站](/help/communities/sites-console.md#publishing-the-site)，將設定複製到發佈環境。

## 從Analytics取得報表{#obtaining-reports-from-analytics}

### 報表管理{#report-management}

作者和主要發佈者的[OSGi設定](/help/sites-deploying/configuring-osgi.md) `AEM Communities Analytics Report Management`可用來查詢Analytics。

在作者上，查詢適用於即時報表。

在主要發佈者上，查詢可用來提供資訊，以準備報表匯入工具的Analytic資料匯入。

查詢間隔預設為10秒。

### 報表匯入工具{#report-importer}

發佈已啟用Analytics的社群網站後，主要發行者的[OSGi設定](/help/sites-deploying/configuring-osgi.md)`AEM Communities Analytics Report Importer`可設定這些設定的預設輪詢間隔，這些設定並非個別在CRXDE中設定。

輪詢間隔控制要提取並儲存至[SRP](/help/communities/working-with-srp.md)的資料向Adobe Analytics提出的請求的頻率。

當資料可歸類為「大資料」時，更頻繁的輪詢可能會給社群網站帶來大量負載。

預設輪詢&#x200B;**Import interval**&#x200B;設定為12小時。

![report-importer](assets/report-importer.png)

### 元件報表自定義{#component-report-customization}

目前，若要自訂要追蹤的量度，系統會在儲存庫中建立節點，定義要針對該量度產生報表的時段。

論壇主題目前是此自訂的唯一範例：

* 在主要發佈商上，使用管理權限登入。
* 導覽至[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。 例如， [https://localhost:4503/crx/de](https://localhost:4503/crx/de)。

* 在語言根的jcr:content節點下(例如`/content/sites/engage/en/jcr:content),`導覽至為Analytics報表設定的元件。
例如， **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 請注意建立的時段：

   * `last30Days`
   * `last90Days`
   * `thisYear`

* 注意`total`節點。

   * 修改&#x200B;**`interval`**&#x200B;屬性會覆寫「報表匯入工具」間隔。
   * 值以秒為單位，設為4小時(14400秒)。

![元件報表](assets/component-report.png)

## 在Analytics {#manage-user-data-in-analytics}中管理使用者資料

Adobe Analytics提供可讓您存取、匯出和刪除使用者資料的API。 如需詳細資訊，請參閱[提交存取和刪除請求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)。

## 資源 {#resources}

* Adobe Experience Cloud:[Analytics說明和參考](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM:[與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)
* AEM:[具有外部提供者的Analytics](/help/sites-administering/external-providers.md)
