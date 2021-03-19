---
title: 社群功能的Analytics設定
seo-title: 社群功能的Analytics設定
description: 設定社群分析
seo-description: 設定社群分析
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2757'
ht-degree: 3%

---


# 社群功能分析設定{#analytics-configuration-for-communities-features}

## 概覽 {#overview}

Adobe Analytics和Adobe Experience Manager(AEM)都是Adobe Marketing Cloud的解決方案。

Adobe Analytics可以為AEM Communities配置，以便成員與支援的社區功能交互時，事件將從中發送到Adobe Analytics，從中生成報告。

例如，當啟用社群網站的成員檢視指派給他們的視訊資源時，資源播放器會傳送事件至Analytics，包括視訊心率資料。 在社群網站上，管理員可以看到各種有關視訊播放的報表。

此外，必須分析以下事項：

* 在發佈環境中：

   * 報告社群[趨勢](/help/communities/trends.md)
   * 允許網站訪客依「檢視次數最多」、「最活躍」、「最喜歡」排序
   * 檢視UGC清單的計數

* 在作者環境中：

   * 在[成員管理控制台](/help/communities/members.md)（檢視、貼文、後續、按贊）中顯示參與率資料
   * 啟用資源[報告](/help/communities/reports.md)的趨勢摘要、視訊心率和視訊裝置

支援的社群功能包括：

* [啟用資源](/help/communities/resources.md)
* [論壇](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [部落格](/help/communities/blog-feature.md)
* [檔案庫](/help/communities/file-library.md)
* [日曆](/help/communities/calendar.md)

本節說明如何將Analytics報表套裝與社群功能連接。 基本步驟為：

1. [複製加密密](#replicate-the-crypto-key) 鑰以確保所有實例上的加密／解AEM密正確
1. 準備Adobe Analytics[報表套裝](#adobe-analytics-report-suite-for-video-reporting)
1. 建立AEMAnalytics [雲端服務](#aem-analytics-cloud-service-configuration)和[framework](#aem-analytics-framework-configuration)

1. [為社](#enable-analytics-for-a-community-site) 群網站啟用Analytics
1. [****](#verify-analytics-to-aem-variable-mapping) VerifyAnalytics與變AEM數對應
1. 識別[主要發行者](#primary-publisher)
1. [發](#publish-community-site-and-analytics-cloud-service) 布社群網站
1. 將[報表資料](#obtaining-reports-from-analytics)從Adobe Analytics匯入社群網站

## 必備條件 {#prerequisites}

若要設定Analytics for Communities功能，必須與您的帳戶代表合作，以設定Adobe Analytics帳戶和[報表套裝](#adobe-analytics-report-suite-for-video-reporting)。 建立後，應提供下列資訊：

* **公司名稱**

   與Adobe Analytics帳戶關聯的公司。

* **使用者名稱**

   獲授權管理Analytics帳戶之使用者的登入使用者名稱
（應包含Web服務存取權限）。

* **密碼**

   授權使用者的登入密碼。

* **Analytics資料中心**

   帳戶的Analytics資料中心URL。

* **報表套裝**

   要使用的Analytics報表套裝名稱。

## Adobe Analytics視訊報表套裝{#adobe-analytics-report-suite-for-video-reporting}

使用Adobe Marketing Cloud的[報表套裝管理員](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)，可以設定Analytics報表套裝，讓社群網站能夠提供社群功能的報表。

登入[Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html)並包含[公司名稱和使用者名稱](/help/communities/analytics.md#prerequisites)，即可設定新或現有的報表套裝：

* [11轉換變數](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** 透過啟 **`evar11`** 用

   * 可重複使用（重新命名）現有的eVar，或建立新eVar以用於社群功能

* [7成功事件](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html) （事件）

   * **`event1`** 透過啟 **`event7`** 用

   * 類型 **`Counter`**

      * 非 **`Counter (no subrelations)`**
   * 可重新使用（重新命名）現有事件或建立新事件以用於社群功能


* [視訊管理](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * 視訊報告主控台

      * 啟用 `Video Core`
      * 選擇保存
   * 視訊核心測量主控台

      * 選取 `Use Solution Variables`
      * 選擇保存


如果使用&#x200B;**新的報表套裝**，請注意，新的報表套裝可能只有4個evar和6個事件變數，而社群則需要11個evar和7個事件變數。

如果使用&#x200B;**現有報表套裝**，則可能需要[修改變數對應](#modifying-analytics-variable-mapping)，才能啟動社群網站的Analytics架構。

請連絡您的帳戶代表，以瞭解有關社群專用變數的任何疑慮。

>[!CAUTION]
>
>**若使用現有報表套裝，且報表套裝已在**
>
>* **`evar1`** through  **`evar11`**
   >
   >
* **`event1`** through  **`event7`**
>
>
**然後，在社群網站發佈之** 前，請務必移動在社群網站啟用AEMAnalytics時，自動對應至Analytics變數的變數，以還原預先存在的對應。
>
>若要還原預先存在的對應並將變AEM數移至其他Analytics變數，請參閱[修改Analytics變數對應](#modifying-analytics-variable-mapping)一節。
>
>如果不這樣做，可能會導致無法恢復的資料丟失。

### 視訊心率分析{#video-heartbeat-analytics}

授權「視訊心率分析」時，會指派`Marketing Cloud Org Id`。

若要在[設定視訊報表的Analytics報表套裝](#adobe-analytics-report-suite-for-video-reporting)後啟用視訊心率報表：

* 建立[Analytics雲端服務](#aem-analytics-cloud-service-configuration)
* 啟用[社群網站](#enable-analytics-for-a-community-site)的Analytics
* 將`Marketing Cloud Org Id`與社群網站建立關聯

`Marketing Cloud Org Id`可在[社區站點建立](/help/communities/sites-console.md#enablement)或更晚時通過[修改](/help/communities/sites-console.md#modifying-site-properties)社區站點屬性來輸入。[](#aem-analytics-cloud-service-configuration)

![marketing-org-id](assets/marketing-org-id.png)

啟用視訊心率分析時，視訊播放器的JavaScript(JS)程式碼會執行個體化視訊心率程式庫程式碼（也包含在JS中），此程式碼會處理每10秒傳送視訊狀態更新至Analytics視訊追蹤伺服器的所有邏輯（不可設定），並最終傳送視訊工作階段的累積報表至主要Analytics伺服器。

若未啟用，則不會執行個體化視訊心率程式碼，且只會將視訊進度和繼續位置追蹤持續保存至SRP以進行報告。

## AEMAnalytics Cloud服務配置{#aem-analytics-cloud-service-configuration}

若要建立新的Analytics整合，並使用作者例項上的AEM標準UI將Adobe Analytics與社群網站整合：

* 從全域導覽：**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**
* 向下捲動至&#x200B;**[!UICONTROL Adobe Analytics]**
* 選擇&#x200B;**[!UICONTROL 立即配置]**&#x200B;或&#x200B;**[!UICONTROL 顯示配置]**

![雲端組態](assets/cloud-config1.png)

### 建立配置對話框{#create-configuration-dialog}

* 選擇&#x200B;**[!UICONTROL 可用配置]**&#x200B;旁的`[+]`表徵圖以建立新配置

在「建立配置」對話框中，要輸入的值標識配置。

![create-cloud-config](assets/cloud-config2.png)

* **標題**

   （必要）設定的顯示標題。
例如，輸入*啟用社群分析*

* **名稱**

   （可選）如果未指定，名稱將預設為從標題派生的有效節點名稱。
例如，輸入*communities*

* **範本**

   選取 `Adobe Analytics Configuration`

* 選擇&#x200B;**建立**

   * 啟動配置頁並開啟`Analytics Settings`對話框

### Analytics設定對話方塊{#analytics-settings-dialog}

初次建立新Analytics設定時，會顯示設定，並顯示新對話方塊以輸入Analytics設定。 此對話框要求從帳戶代表處獲得[先決條件帳戶資訊](#prerequisites)。

![analytics-settings](assets/analytics-settings.png)

* **公司**

   與Adobe Analytics帳戶關聯的公司。

* **使用者名稱**

   獲授權管理Analytics帳戶之使用者的登入使用者名稱。

* **密碼**

   授權使用者的登入密碼。

* **資料中心**

   選取代管報表套裝的Analytics資料中心。

* **不要新增追蹤標記至頁面**

   保留為預設值（取消選取）。

* **使用 AppMeasurement**

   保留為預設值（取消選取）。

* **不要每晚匯入頁面印象 (作者)**

   保留為預設值（取消選取）。

* **不要每晚匯入頁面印象 (發佈)**

   保留為預設值（取消選取）。

要保存設定：

* 選擇&#x200B;**連線至Analytics**

   * 如果未成功，

      * 驗證條目是否不包含前導空格。
      * 嘗試不同的資料中心。

* 選擇&#x200B;**確定**。

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### 建立框架 {#create-framework}

成功配置到Adobe Analytics的基本連接後，必須為社區站點建立或編輯框架。 此架構的目的是將社群功能(AEM)變數對應至Analytics（報表套裝）變數。

* 選擇&#x200B;**[!UICONTROL 可用框架]**&#x200B;旁的`[+]`表徵圖以建立新框架

   ![analytics-framework](assets/analytics-framework.png)

* **標題**

   （必要）架構的顯示標題
例如，輸入*啟用社群架構*。

* **名稱**

   （可選）如果未指定，名稱將預設為從標題派生的有效節點名稱。
例如，輸入*communities*。

* *範本*

   選取 `Adobe Analytics Framework`.

* 選擇 **建立**。

建立Analytics架構會開啟要進行設定的架構。

## AEM Analytics Framework Configuration {#aem-analytics-framework-configuration}

此架構的目的是將變AEM數對應至Analytics變數（eVar和事件）。 可用於映射的Analytics變數為[，定義於報表套裝](#adobe-analytics-report-suite-for-video-reporting)中。

![analytics-enablement-framework](assets/analytics-framework1.png)

### 選擇報表套裝{#select-report-suite}

選取已針對視訊報表設定的報表套裝。

如果報表套裝尚未建立或未正確設定，請參閱上一節：
[Adobe Analytics視訊報表套裝](#adobe-analytics-report-suite-for-video-reporting)

不需要Sidekick且可將其最小化，以免妨礙存取「報表套裝」設定。

#### 選擇「新增項目」{#report-suites-dialog-before-and-after-selecting-add-item}前後的報表套裝對話方塊

![report-suite](assets/report-suite.png)

1. 選擇&#x200B;**添加項目+**。

   出現兩個下拉式方塊。

1. 選擇`Report suite.`

   與「公司」帳戶關聯的報表套裝可供選擇。

1. 在開啟的對話框中選擇&#x200B;**是**:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. 選擇`Run Mode`。

1. 選擇&#x200B;**Publish**。

![analytics-framework2](assets/analytics-framework2.png)

Analytic雲端服務與架構現已完成。 在啟用此Analytics服務後，社群網站建立後，即會定義映射。

## 啟用社群網站{#enable-analytics-for-a-community-site}的分析

### 啟用新社區站點{#enable-for-new-community-site}

若要在[建立新社群網站](/help/communities/sites-console.md)時新增Analytics雲端服務：

* 在步驟3中，在[ANALYTICS標籤](/help/communities/sites-console.md#analytics)下：
   * 選取「啟用Analytics **」核取方塊。**
   * 從下拉式方塊中選取架構。

* （可選）返回Analytics架構設定以調整變數映射。

### 啟用現有社區站點{#enable-for-existing-community-site}

若要將Analytics雲端服務新增至[現有社群網站](/help/communities/sites-console.md#modifying-site-properties):

* 導覽至&#x200B;**社群>網站**&#x200B;主控台。
* 選擇社群網站的「編輯網站」圖示。
* 選擇「設定」。
* 在「分析」區段中：
   * 選取「啟用Analytics **」核取方塊。**
   * 從下拉式方塊中選擇架構。

* （可選）返回Analytics架構設定以調整變數映射。

### 啟用自訂網站{#enable-for-customized-sites}

為了讓Analytics追蹤和匯入能正常運作於社群網站，必須有具有`scf-js-site-title`類別和href屬性的頁面元素。 頁面上只應存在一個此類元素，例如，在未修改的`sitepage.hbs`指令碼中，社群網站應該存在該元素。 提取`siteUrl`的值並作為&#x200B;*站點路徑*&#x200B;發送到Adobe Analytics。

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

對於覆蓋`sitepage.hbs`指令碼的&#x200B;**自訂社群站點**，請確保元素存在。 `siteUrl`變數會在伺服器上轉譯後，再提供給用戶端。

對於包含Communities元件的&#x200B;**AEM一般站點**，但不是使用[站點建立嚮導](/help/communities/sites-console.md)建立的，必須添加元素。 href的值應為網站的路徑。 例如，如果網站路徑為`/content/my/company/en`，則使用：

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## 社群分析功能{#analytics-for-communities-features}

Analytics會自動用於數個Communities功能。

作者環境的[OSGi configuration](/help/sites-deploying/configuring-osgi.md)、`AEM Communities Analytics Component Configuration`提供了已為Analytics所創作的元件的清單。 變數的自動對應由列出的元件決定。

如果建立了Analytics專用的新自訂元件，則應將其新增至此已設定元件清單。

### 元件配置{#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>日誌元件用於實施部落格功能。

### 將Analytics對AEM應至變數{#mapped-analytics-to-aem-variables}

在啟用Analytics並選取雲端設定架構的情況下儲存社群網站後，AEM變數將自動對應至Analytics eVars和events(分別以evar1和event1開始，並遞增1。

如果使用現有報表套裝來映射evar1到evar11和event1到event7中的任何變數，則必須[重新映射變AEM數](#modifying-analytics-variable-mapping)並還原原始映射。

以下是[快速入門教程](/help/communities/getting-started-enablement.md)之後的預設映射示例：

![map-analytics](assets/map-analytics1.png)

#### 與每個事件{#map-of-evars-sent-with-each-event}一起傳送的eVar映射

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>啟用<br />資源<br />類型</strong></td>
   <td><strong>網站<br />標題</strong></td>
   <td><strong>函式<br />類型</strong></td>
   <td><strong>群組<br />標題</strong></td>
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
* *[社群網站標題](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixx社區
* *[社群函式名稱](/help/communities/functions.md)*:論壇
* *[社群群組名稱](/help/communities/creating-groups.md#creating-a-new-group)*:遠足
* *社群群組內容的路徑*:  `/content/sites/<site name>/en/groups/hiking`
* *[UGC元件resourceType](/help/communities/essentials.md)*:  `social/forum/components/hbs/topic`
* *UGC元件標題*:遠足主題
* *login(authorizableId)*:  `aaron.mcdonald@mailinator.com`
* *SRP到UGC的路徑*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
或 
*要遵循的元件路徑*:  `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *社群網站內容的路徑*:  `/content/sites/<site name>/en`

### 修改Analytics變數對應{#modifying-analytics-variable-mapping}

在社群網站啟用Analytics後，從架構設AEM定可看到Analytics eVar和事件對應至變數。

啟用Analytics後，在社群網站發佈之前，從左側導軌拖曳所需的Analytics evar或事件並拖曳至對應表格的相關列，即可在架構中變更對應。

若要避免重複映射，請務必將滑鼠指標暫留在行上並選取Analytics變數元素右側的「X」，以移除已取代的Analytics evar或事件。

如果Communities eVar和事件覆寫報表套裝中預先存在的映射，則為避免資料遺失，請將Communities功能的變AEM數指派給其他Analytics eVar或事件，並還原原始映射。

>[!CAUTION]
>
>在啟用Analytics的社群網站[published](#publishing-the-community-site)之前重新對應，請務必留意，否則會有資料遺失的風險。

#### 範例步驟1:將Analytics evar14拖曳至對應表格{#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### 範例步驟2:選取&#39;x&#39;以移除已取代的evar11 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### 範例步驟3:AEMvar eventdata.siteId重新映射至Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## 發佈社群網站{#publishing-the-community-site}

### 驗證AnalyticsAEM與變數對應{#verify-analytics-to-aem-variable-mapping}

在發佈社群網站（也發佈Analytics雲端服務和架構）之前，最好先驗證變數對應。

請參閱章節：

* [將Analytics對應至變AEM數](#mapped-analytics-to-aem-variables)
* [修改Analytics變數對應](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**若使用現有報表套裝，且報表套裝已在**
>
>* **`evar1`** through  **`evar11`**
   >
   >
* **`event1`** through  **`event7`**
>
>
**然後，在社群網站發佈之前，** 請務必還原預先存在的對應，並將自動映射的社群AEM變數（在為社群網站啟用Analytics時）移至其他Analytics變數。此重新映射應在所有社區元件中保持一致。
>
>如果不這樣做，可能會導致無法恢復的資料丟失。

### 主要發行者{#primary-publisher}

當選擇的部署是[publish farm](/help/communities/topologies.md#tarmk-publish-farm)時，必須將一個發佈實例標識為輪詢Adobe Analytics的主發佈器，以便將報告資料寫入[SRP](/help/communities/working-with-srp.md)。

依預設，`AEM Communities Publisher Configuration` OSGi組態會將其發佈執行個體識別為主要發佈者，如此發佈群組中的所有發佈執行個體都會自行識別為主要發佈者。

因此，必須編輯所有次要發佈例項的設定，以取消選取「主要發佈者」核取方塊。****

有關具體說明，請參閱[部署社群](/help/communities/deploy-communities.md#primary-publisher)的主要發佈者部分。

>[!CAUTION]
>
>請務必設定主要發佈者，以防止從多個發佈例項進行輪詢。

### 複製加密密鑰{#replicate-the-crypto-key}

Adobe Analytics認證是加密的。 為方便作者和發佈者之間複製或傳輸加密的分析憑證，所有例項AEM都必須共用相同的主加密金鑰。

要執行此操作，請按照[複製加密密鑰](/help/communities/deploy-communities.md#replicate-the-crypto-key)中的說明操作。

### 發佈社群網站和Analytics Cloud服務{#publish-community-site-and-analytics-cloud-service}

在為社群網站啟用Analytics雲端服務後，並視需要調整[ Analytics與變數的對應AEM](#mapped-analytics-to-aem-variables)，就必須透過[(re)發佈社群網站](/help/communities/sites-console.md#publishing-the-site)，將組態複製至發佈環境。

## 從Analytics {#obtaining-reports-from-analytics}取得報表

### 報表管理{#report-management}

作者和主要發行者的[OSGi configuration](/help/sites-deploying/configuring-osgi.md)、`AEM Communities Analytics Report Management`可用來查詢Analytics。

在作者上，查詢是即時報告。

在主要發佈者上，查詢可用來提供資訊，以準備報表匯入工具的Analytic資料匯入。

查詢間隔預設為10秒。

### 報表匯入工具{#report-importer}

一旦發佈啟用Analytics的社群網站後，可將主要發行者的[OSGi configuration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`組態設定為針對未個別在CRXDE中設定的組態設定預設輪詢間隔。

輪詢間隔控制向Adobe Analytics請求要提取並保存到[SRP](/help/communities/working-with-srp.md)中的資料的頻率。

當資料可歸類為「大資料」時，更頻繁的投票可能會給社群網站帶來很大的負載。

預設輪詢&#x200B;**導入間隔**&#x200B;設定為12小時。

![report-importer](assets/report-importer.png)

### 元件報告自定義{#component-report-customization}

目前，若要自訂要追蹤的量度，系統會在儲存庫中建立節點，以定義要針對該量度產生報表的時段。

論壇主題是目前此項自訂的唯一範例：

* 在主要發行者上，以管理權限登入。
* 導覽至[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。 例如，[https://localhost:4503/crx/de](https://localhost:4503/crx/de)。

* 在語言根目錄的jcr:content節點下(例如`/content/sites/engage/en/jcr:content),`導覽至為Analytics報表設定的元件。
例如， **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 請注意所建立的時段：

   * `last30Days`
   * `last90Days`
   * `thisYear`

* 注意`total`節點。

   * 修改&#x200B;**`interval`**&#x200B;屬性會覆寫「報表匯入工具」間隔。
   * 值以秒為單位，並設為4小時（14400秒）。

![component-report](assets/component-report.png)

## 在Analytics {#manage-user-data-in-analytics}中管理使用者資料

Adobe Analytics提供API，可讓您存取、匯出和刪除使用者資料。 如需詳細資訊，請參閱[提交存取和刪除請求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)。

## 資源 {#resources}

* Adobe Experience Cloud:[Analytics說明與參考](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM:[與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)
* AEM:[具有外部提供者的Analytics](/help/sites-administering/external-providers.md)
