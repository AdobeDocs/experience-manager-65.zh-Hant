---
title: 為Adobe Analytics配置視頻跟蹤
seo-title: Configuring Video Tracking for Adobe Analytics
description: 瞭解配置視頻跟蹤以進行SiteCatalyst。
seo-description: Learn about configuring video tracking for SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 1%

---

# 為Adobe Analytics配置視頻跟蹤{#configuring-video-tracking-for-adobe-analytics}

有幾種方法可用於跟蹤視頻事件，其中2種是舊版Adobe Analytics的舊版選項。 這些舊選項包括：舊式里程碑和舊式秒數。

>[!NOTE]
>
>在繼續之前，請確保 **播放視頻** 上載於AEM。
>
>要確保視頻在頁面上播放，請咨詢 **[本教程](/help/sites-authoring/default-components-foundation.md#video)** 有關如何在中轉換視頻檔案的信AEM息。

使用以下步驟使用每種方法設定視頻跟蹤框架。

>[!NOTE]
>
>對於新實施，建議您 **不使用** 用於視頻跟蹤的傳統選項。 請使用 **里程碑** 的雙曲餘切值。

## 常見步驟 {#common-steps}

1. 通過拖動 **視頻元件** 從旁邊加一個可玩的 **視頻作為資產** 對於元件

1. [建立Adobe Analytics配置和框架](/help/sites-administering/adobeanalytics.md)。

   * 下面各節中的示例使用名稱 **my-sc-configuration** 的 **視頻** 框。

1. 在框架頁面上，選擇一個RSID並將用法設定為all。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 從Sidekick中的「常規」元件類別中，將視頻元件拖到框架上。
1. 選擇跟蹤方法：

   * [里程碑](/help/sites-administering/adobeanalytics.md)
   * [非舊式里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊式里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊秒](/help/sites-administering/adobeanalytics.md)

1. 選擇跟蹤方法時，CQ變數清單會相應更改。 有關如何進一步配置元件和將CQ變數與Adobe Analytics屬性映射的資訊，請使用下面的部分。

## 里程碑 {#milestones}

Milestones方法可跟蹤視頻的最多資訊，具有高度的可定製性，且易於配置。

要使用里程碑方法，請指定基於時間的軌道偏移以定義里程碑。 當視頻播放通過里程碑時，該頁會呼叫Adobe Analytics以跟蹤事件。 對於您定義的每個里程碑，元件會建立一個CQ變數，您可以將其映射到Adobe Analytics屬性。 這些CQ變數的名稱使用以下格式：

```shell
eventdata.events.milestoneXX
```

XX尾碼是定義里程碑的軌道偏移。 例如，指定4、8、16、20和28秒的磁軌偏移將生成以下CQ變數：

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

下表介紹了為Milestones方法提供的預設CQ變數：

<table>
 <tbody>
  <tr>
   <th>CQ變數</th>
   <th>Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>映射到此的變數將包含 <strong>用戶友好</strong> 名稱(<strong>標題</strong>)，如果在DAM中設定；如果未設定，則視頻 <strong>檔案名</strong> 將被發送。 在播放視頻的開始時只發送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此變數的變數將包含檔案名。 僅與eventdata.events.a.media.view一起發送 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此變數的變數將包含伺服器上的檔案路徑。 僅與eventdata.events.a.media.view一起發送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>每次傳遞段裡程碑時發送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>每次觸發里程碑時發送一次，用戶監視給定段所花費的秒數也會隨此事件一起發送。 例如，eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>在初始化視頻視圖時發送</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>視頻播放完後發送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>當給定里程碑通過時發送， X表示里程碑觸發的第二個時間<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>發送到每個里程碑；在Adobe Analytics通話中顯示為pev3，通常以「視頻」形式發送。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>完全匹配eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>包含有關已查看的段的資訊，例如2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可以設定視頻 **用戶友好** 通過在DAM中開啟視頻進行編輯並設定 **標題** 元資料欄位到所需名稱。

1. 選擇Milestones作為跟蹤方法後，在「跟蹤偏移」框中輸入以逗號分隔的跟蹤偏移清單（以秒為單位）。 例如，以下值在視頻開始後4、8、16、20和28秒定義里程碑：

   ```xml
   4,8,16,20,24
   ```

   偏移值必須是大於0的整數。 預設值為 `10,25,50,75`。

1. 要將CQ變數映射到Adobe Analytics屬性，請將Adobe Analytics屬性從元件上CQ變數旁的ContentFinder中拖動。

   有關優化映射的資訊，請參見 [Adobe Analytics視頻測量](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 的子菜單。

1. [添加框架](/help/sites-administering/adobeanalytics.md) 頁。
1. test中的設定 **預覽模式**，播放視頻以觸發Adobe Analytics呼叫。

以下Adobe Analytics跟蹤資料示例適用於里程碑跟蹤，使用4、8、16、20和24的跟蹤偏移以及CQ變數的以下映射：

<table>
 <tbody>
  <tr>
   <th>CQ 變數</th>
   <th>Adobe Analytics</th>
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
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

在此示例中，視頻元件如下所示出現在框架頁：

![video1](assets/video1.png)

>[!NOTE]
>
>要查看對Adobe Analytics的調用，請使用適當的工具，如DigitalPulse調試器或Fiddler。

使用提供的示例對Adobe Analytics的調用在使用DigitalPulse調試器查看時應如下所示：

![chlimage_1-128](assets/chlimage_1-128.png)

*這是&#x200B;**第一次呼叫**寫到Adobe Analytics，並包含以下值：*

* *prop1和eVar1（用於eventdata.a.media.name）,*
* *props2-4，以及包含contentType(video)和段(1)的eVar2和eVar3:O:1-4)*
* *映射到eventdata.events.a.media.view的事件3。*

![chlimage_1-129](assets/chlimage_1-129.png)

*這是&#x200B;**第三次呼叫**Adobe Analytics:*

* *prop1和eVar1包含a.media.name;*
* *事件1，因為已查看段*
* *事件2已發送，播放時間= 4*
* *event11已發送，因為已達到eventdata.events.milestone8*
* *prop2不發送到4（因為未觸發eventdata.events.a.media.view）*

## 非舊式里程碑 {#non-legacy-milestones}

「非舊式里程碑」方法與「里程碑」方法類似，但里程碑是使用跟蹤長度的百分比定義的。 共性如下：

* 當視頻播放通過里程碑時，該頁會呼叫Adobe Analytics以跟蹤事件。
* 的 [CQ變數的靜態集](#cqvars) 定義為與Adobe Analytics屬性映射。
* 對於您定義的每個里程碑，元件會建立一個CQ變數，您可以將其映射到Adobe Analytics屬性。

這些CQ變數的名稱使用以下格式：

XX尾碼是定義里程碑的軌道長度的百分比。 例如，指定10、25、50和75的百分比將生成以下CQ變數：

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 選擇「非舊式里程碑」作為跟蹤方法後，在「跟蹤偏移」框中，輸入以逗號分隔的跟蹤長度百分比清單。 例如，以下預設值將里程碑定義為軌道長度的10%、25%、50%和75%:

   ```xml
   10,25,50,75
   ```

   偏移值必須是大於0的整數。

1. 要將CQ變數映射到Adobe Analytics屬性，請將Adobe Analytics屬性從元件上CQ變數旁的ContentFinder中拖動。

   有關優化映射的資訊，請參見 [Adobe Analytics視頻測量](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 的子菜單。

1. [添加框架](/help/sites-administering/adobeanalytics.md) 頁。
1. test中的設定 **預覽模式**，播放視頻以觸發Adobe Analytics呼叫。

## 舊式里程碑 {#legacy-milestones}

此方法與Milestones方法類似，其區別在於 *跟蹤偏移* 欄位是百分比，而不是視頻中的設定點。

>[!NOTE]
>
>「跟蹤偏移」欄位只接受包含1到100之間整數的逗號分隔清單。

1. 設定「軌道偏移」(Track offset)。

   * e.g.10,50,75,100

   另外，發送給Adobe Analytics的資訊不太可定製；只有3個變數可用於映射：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>映射到此的變數將包含 <strong>用戶友好</strong> 名稱(<strong>標題</strong>)，如果在DAM中設定；如果未設定標題，則視頻 <strong>檔案名</strong> 將被發送。 在播放視頻的開始時只發送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此變數的變數將包含檔案名。 在播放視頻的開始時只發送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此變數的變數將包含伺服器上的檔案路徑。 在播放視頻的開始時只發送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可以設定視頻 **用戶友好** 通過在DAM中開啟視頻進行編輯並設定 **標題** 元資料欄位到所需名稱。 還需要保存完成時所做的更改。

1. 將這些變數映射到道具1到3

   的 **剩餘的相關資訊** 將連接到 **一個** 變數 **PEV**。

   **示例調用** 在使用DigitalPulse調試器查看時，使用所提供示例的Adobe Analytics應如下所示：

   ![lmilestones1](assets/lmilestones1.png)

   *的&#x200B;**PEV**在調用中發送的變數包含以下資訊：*

   * *名稱*  — 視頻檔案的名稱(*膠片*)

   * *長度*  — 視頻檔案的長度（秒）(*100*)

   * *播放器名稱*  — 用於播放視頻檔案的視頻播放器(*HTML5視頻*)

   * *播放的總秒數*  — 播放視頻的總秒數(*25*)

   * *開始時間戳*  — 標識視頻播放開始時間的時間戳(*133103567*)

   * *播放會話*  — 播放會話的詳細資訊。 此欄位指示用戶如何與視頻交互。 這可能包括資料，如他們開始播放視頻的位置、他們是否使用視頻滑塊來推進視頻，以及他們停止播放視頻的位置(*L10E24S58L58 — 視頻在秒內停止。 L10節的25個，然後跳到秒。 48*)

## 舊秒 {#legacy-seconds}

使用**傳統秒**方法時，Adobe Analytics呼叫每第N秒被觸發一次，其中N在「跟蹤偏移」欄位中指定。

1. 將「跟蹤偏移」設定為任意秒數，

   * 例如6
   >[!NOTE]
   >
   >「跟蹤偏移」欄位只接受大於0的整數

   發送給Adobe Analytics的資訊不太可定製。 只有3個變數可用於映射：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>映射到此的變數將包含 <strong>用戶友好</strong> 名稱(<strong>標題</strong>)，如果在DAM中設定；如果未設定標題，則視頻 <strong>檔案名</strong> 將被發送。 在播放視頻的開始時只發送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此變數的變數將包含檔案的名稱。 在播放視頻的開始時只發送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此變數的變數將包含伺服器上的檔案路徑。 在播放視頻的開始時只發送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可以設定視頻 **用戶友好** 通過在DAM中開啟視頻進行編輯並設定 **標題** 元資料欄位到所需名稱。 還需要保存完成時所做的更改。

1. 將這些變數映射到prop1、prop2和prop3

   的 **剩餘的相關資訊** 在呼叫中將被合併到 **一個** 變數 **PEV**。

   使用提供的示例對Adobe Analytics的調用在使用DigitalPulse調試器查看時應如下所示：

   ![秒](assets/lseconds.png)

   *該呼叫與上面的「舊式里程碑」呼叫類似。 請參閱PEV3上的資訊&#x200B;**[提供](/help/sites-administering/adobeanalytics.md)**。*

**本教程中使用的引用：**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
