---
title: 設定Adobe Analytics的視訊追蹤
description: 瞭解如何設定SiteCatalyst的視訊追蹤。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# 設定Adobe Analytics的視訊追蹤{#configuring-video-tracking-for-adobe-analytics}

有數種方法可用來追蹤視訊事件，其中2種是舊版Adobe Analytics的舊版選項。 這些舊版選項為：舊版里程碑和舊版秒數。

>[!NOTE]
>
>繼續之前，請確定您已在AEM中上傳&#x200B;**可播放的視訊**。
>
>若要確保您的視訊在頁面上播放，請參閱&#x200B;**[本教學課程](/help/sites-authoring/default-components-foundation.md#video)**，以瞭解如何在AEM中轉碼視訊檔案。

使用下列程式，以使用每種方法設定視訊追蹤的架構。

>[!NOTE]
>
>若是新的實作，建議您&#x200B;**不要使用**&#x200B;舊版選項進行視訊追蹤。 請改用&#x200B;**里程碑**&#x200B;方法。

## 常見步驟 {#common-steps}

1. 從Sidekick拖曳&#x200B;**視訊元件**&#x200B;並將可播放的&#x200B;**視訊新增為該元件的資產**，以設定網頁

1. [建立Adobe Analytics組態和架構](/help/sites-administering/adobeanalytics.md)。

   * 後續章節中的範例使用名稱&#x200B;**my-sc-configuration**&#x200B;作為組態，使用&#x200B;**videofw**&#x200B;作為架構。

1. 在Framework頁面上，選取RSID並將使用設定為all。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 從Sidekick的「一般」元件類別中，將「視訊」元件拖曳至架構。
1. 選取追蹤方法：

   * [里程碑](/help/sites-administering/adobeanalytics.md)
   * [非舊版里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊版里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊版秒數](/help/sites-administering/adobeanalytics.md)

1. 當您選取追蹤方法時，CQ變數的清單會隨之變更。 使用下列章節，瞭解如何進一步設定元件，並透過Adobe Analytics屬性對應CQ變數。

## 里程碑 {#milestones}

Milestones方法可追蹤視訊的最多資訊，是高度可自訂的，且易於設定。

若要使用「里程碑」方法，請指定以時間為基礎的追蹤位移，以定義里程碑。 當視訊播放超過里程碑時，頁面會呼叫Adobe Analytics以追蹤事件。 元件會為您定義的每個里程碑建立CQ變數，供您對應至Adobe Analytics屬性。 這些CQ變數的名稱會使用以下格式：

```shell
eventdata.events.milestoneXX
```

XX尾碼是定義里程碑的軌跡位移。 例如，指定4、8、16、20和28秒的追蹤位移會產生下列CQ變數：

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

下表說明為Milestones方法提供的預設CQ變數：

<table>
 <tbody>
  <tr>
   <th>CQ變數</th>
   <th>Adobe Analytics屬性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>對應至此的變數將包含視訊的<strong>使用者易記的</strong>名稱（<strong>標題</strong>），若在DAM中設定；若未設定，將改為傳送視訊的<strong>檔案名稱</strong>。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案名稱。 僅與eventdata.events.a.media.view一起傳送 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>對應至此的變數將包含檔案在伺服器上的路徑。 僅與eventdata.events.a.media.view一起傳送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>每次超過區段里程碑時傳送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>每次觸發里程碑時都會傳送，使用者觀看指定區段所花費的秒數也會與此事件一併傳送。 例如，eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>在初始化視訊檢視時傳送</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>視訊播放完畢時傳送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>當指定的里程碑通過時傳送，X代表里程碑在<br />觸發的秒數 </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>在每個里程碑上傳送；在Adobe Analytics呼叫中顯示為pev3，通常傳送為「視訊」<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>完全符合eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>包含已檢視區段的資訊，例如，<code>2:O:4-8</code> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以開啟視訊以在DAM中編輯，並將&#x200B;**Title**&#x200B;中繼資料欄位設定為所要的名稱，藉此設定視訊的&#x200B;**好記的**&#x200B;名稱。

1. 選取「里程碑」作為追蹤方法後，在「追蹤位移」方塊中，輸入以逗號分隔的追蹤位移清單（以秒為單位）。 例如，下列值會定義里程碑在視訊開始後的4、8、16、20和28秒：

   ```xml
   4,8,16,20,24
   ```

   位移值必須是大於0的整數。 預設值為 `10,25,50,75`。

1. 若要將CQ變數對應至Adobe Analytics屬性，請將Adobe Analytics屬性從ContentFinder拖曳至元件上CQ變數旁邊。

   如需最佳化對應的詳細資訊，請參閱[在Adobe Analytics中測量視訊](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)指南。

1. [將架構](/help/sites-administering/adobeanalytics.md)新增至頁面。
1. 若要在&#x200B;**預覽模式**&#x200B;中測試設定，請播放視訊以讓Adobe Analytics呼叫觸發。

以下的Adobe Analytics追蹤資料範例適用於使用4、8、16、20和24的追蹤位移，以及CQ變數的下列對應的里程碑追蹤：

<table>
 <tbody>
  <tr>
   <th>CQ 變數</th>
   <th>Adobe Analytics屬性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>EVAR3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1， prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>EVAR2</td>
  </tr>
 </tbody>
</table>

在此範例中，視訊元件在架構頁面上如下所示：

![視訊1](assets/video1.png)

>[!NOTE]
>
>若要檢視對Adobe Analytics發出的呼叫，請使用適當的工具，例如DigitalPulse Debugger或Fiddler。

使用DigitalPulse Debugger檢視時，使用所提供範例呼叫Adobe Analytics時看起來會像這樣：

![chlimage_1-128](assets/chlimage_1-128.png)

*這是對Adobe Analytics發出的&#x200B;**第一個呼叫**，包含下列值：*

* eventdata.a.media.name的&#x200B;*prop1和eVar1，*
* *props2-4，以及包含contentType （視訊）和區段(1:O:1-4)*&#x200B;的eVar2和eVar3
* 已對應至eventdata.events.a.media.view.*的* event3

![chlimage_1-129](assets/chlimage_1-129.png)

*這是對Adobe Analytics發出的&#x200B;**第三次呼叫**：*

* *prop1和eVar1包含a.media.name；*
* *event1，因為已檢視區段*
* *event2已傳送並播放時間= 4*
* *event11已傳送，因為已達到eventdata.events.milestone8*
* *prop2至4未傳送（因為未觸發eventdata.events.a.media.view）*

## 非舊版里程碑 {#non-legacy-milestones}

「非舊版里程碑」方法類似於「里程碑」方法，但里程碑是使用追蹤長度的百分比定義。 共同之處如下：

* 當視訊播放超過里程碑時，頁面會呼叫Adobe Analytics以追蹤事件。
* 定義為與Adobe Analytics屬性對應之CQ變數的[靜態集合](#cqvars)。
* 元件會為您定義的每個里程碑建立CQ變數，供您對應至Adobe Analytics屬性。

這些CQ變數的名稱會使用以下格式：

XX尾碼是定義里程碑的軌跡長度的百分比。 例如，指定10、25、50和75的百分比會產生下列CQ變數：

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 選取「非舊版里程碑」作為追蹤方法後，在「追蹤位移」方塊中，輸入以逗號分隔的追蹤長度百分比清單。 例如，下列預設值會定義里程碑為軌跡長度的10%、25%、50%和75%：

   ```xml
   10,25,50,75
   ```

   位移值必須是大於0的整數。

1. 若要將CQ變數對應至Adobe Analytics屬性，請將Adobe Analytics屬性從ContentFinder拖曳至元件上CQ變數旁邊。

   如需最佳化對應的詳細資訊，請參閱[在Adobe Analytics中測量視訊](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)指南。

1. [將架構](/help/sites-administering/adobeanalytics.md)新增至頁面。
1. 若要在&#x200B;**預覽模式**&#x200B;中測試設定，請播放視訊以讓Adobe Analytics呼叫觸發。

## 舊版里程碑 {#legacy-milestones}

此方法類似於Milestones方法，不同之處在於&#x200B;*追蹤位移*&#x200B;欄位中指定的里程碑是百分比，而不是視訊中的設定點。

>[!NOTE]
>
>「追蹤位移」欄位僅接受逗號分隔的清單，其中包含1到100之間的整數。

1. 設定軌跡位移。

   * 例如，10,50,75,100

   此外，傳送至Adobe Analytics的資訊不易自訂；只有3個變數可用於對應：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>對應至此的變數將包含視訊的<strong>使用者易記的</strong>名稱（<strong>標題</strong>），如果在DAM中設定；如果未設定標題，將改為傳送視訊的<strong>檔案名稱</strong>。 只傳送一次，在播放視訊開始時傳送。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案名稱。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>對應至此的變數將包含檔案在伺服器上的路徑。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以開啟視訊以在DAM中編輯，並將&#x200B;**Title**&#x200B;中繼資料欄位設定為所要的名稱，藉此設定視訊的&#x200B;**好記的**&#x200B;名稱。 完成時，您還需要儲存所做的變更。

1. 將這些變數對應至prop 1至3

   呼叫中的&#x200B;**其餘相關資訊**&#x200B;將串連傳送至名為&#x200B;**pev3**&#x200B;的&#x200B;**one**&#x200B;變數。

   使用提供的範例對Adobe Analytics進行&#x200B;**範例呼叫**&#x200B;在透過DigitalPulse Debugger檢視時，看起來應該像這樣：

   ![里程碑1](assets/lmilestones1.png)

   *呼叫中傳送的&#x200B;**pev3**變數包含下列資訊：*

   * *名稱* — 視訊檔的名稱(*film.avi*)

   * *Length* — 視訊檔案的長度（以秒為單位） (*100*)

   * *播放器名稱* — 用來播放視訊檔案的視訊播放器(*HTML5視訊*)

   * *播放的總秒數* — 播放視訊的總秒數(*25*)

   * *開始時間戳記* — 識別視訊播放開始的時間戳記(*1331035567*)

   * *播放工作階段* — 播放工作階段的詳細資料。 此欄位指出使用者與視訊的互動方式。 這可能包括開始播放視訊的位置、是否使用視訊滑桿來推進視訊，以及停止播放視訊的位置(*L10E24S58L58 — 視訊在秒後停止。 L10區段的25個，然後略過到秒。 48*)

## 舊版秒數 {#legacy-seconds}

使用**舊版秒**方法時，Adobe Analytics呼叫會每隔N秒觸發一次，其中N會在「追蹤位移」欄位中指定。

1. 將追蹤位移設為任何秒數，

   * 例如， 6

   >[!NOTE]
   >
   >「追蹤位移」欄位僅接受大於0的整數

   傳送至Adobe Analytics的資訊較不易自訂。 只有3個變數可用於對應：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>對應至此的變數將包含視訊的<strong>使用者易記的</strong>名稱（<strong>標題</strong>），如果在DAM中設定；如果未設定標題，將改為傳送視訊的<strong>檔案名稱</strong>。 只傳送一次，在播放視訊開始時傳送。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案名稱。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>對應至此的變數將包含檔案在伺服器上的路徑。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以開啟視訊以在DAM中編輯，並將&#x200B;**Title**&#x200B;中繼資料欄位設定為所要的名稱，藉此設定視訊的&#x200B;**好記的**&#x200B;名稱。 完成時，您還需要儲存所做的變更。

1. 將這些變數對應至prop1、prop2和prop3

   呼叫中的&#x200B;**其餘相關資訊**&#x200B;將會連線傳送至名為&#x200B;**pev3**&#x200B;的&#x200B;**one**&#x200B;變數中。

   使用DigitalPulse Debugger檢視時，使用所提供範例呼叫Adobe Analytics時看起來會像這樣：

   ![lseconds](assets/lseconds.png)

   *此呼叫類似於上述舊版里程碑呼叫。 檢視[與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)下提供的pev3相關資訊。*

此教學課程中使用的&#x200B;**參考：**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
