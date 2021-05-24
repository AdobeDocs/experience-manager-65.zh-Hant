---
title: 設定Adobe Analytics的視訊追蹤
seo-title: 設定Adobe Analytics的視訊追蹤
description: 了解如何設定視訊追蹤以供SiteCatalyst。
seo-description: 了解如何設定視訊追蹤以供SiteCatalyst。
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 1%

---

# 設定Adobe Analytics的視訊追蹤{#configuring-video-tracking-for-adobe-analytics}

有數種方法可用來追蹤視訊事件，其中2種是舊版Adobe Analytics的舊版選項。 以下是舊版選項：舊里程碑和舊秒。

>[!NOTE]
>
>繼續之前，請確定已在AEM中上傳&#x200B;**可播放視訊**。
>
>若要確保您的影片在頁面上播放，請參閱&#x200B;**[本教學課程](/help/sites-authoring/default-components-foundation.md#video)**，以了解如何在AEM中轉碼視訊檔案。

請依照下列步驟，使用每個方法來設定視訊追蹤的架構。

>[!NOTE]
>
>若為新實作，建議您&#x200B;**不要使用**&#x200B;舊版視訊追蹤選項。 請改用&#x200B;**Milestones**&#x200B;方法。

## 常見步驟{#common-steps}

1. 從sidekick拖曳&#x200B;**視訊元件**&#x200B;並新增可播放&#x200B;**視訊作為元件的資產**，以設定網頁

1. [建立Adobe Analytics設定和架構](/help/sites-administering/adobeanalytics.md)。

   * 後續各節中的範例針對設定使用名稱&#x200B;**my-sc-configuration**，框架使用&#x200B;**videow**。

1. 在架構頁面上，選取RSID並將使用情形設為全部。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 從Sidekick中的「一般」元件類別，將視訊元件拖曳至架構上。
1. 選取追蹤方法：

   * [里程碑](/help/sites-administering/adobeanalytics.md)
   * [非舊式里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊秒數](/help/sites-administering/adobeanalytics.md)

1. 選取追蹤方法時，CQ變數清單會隨之變更。 請使用下方的區段，了解如何進一步設定元件，以及將CQ變數與Adobe Analytics屬性對應。

## 里程碑 {#milestones}

Milestones方法可追蹤視訊的最多資訊、高度可自訂，且易於設定。

若要使用里程碑方法，請指定以時間為基礎的追蹤位移以定義里程碑。 當視訊播放超過里程碑時，頁面會呼叫Adobe Analytics以追蹤事件。 元件會針對您定義的每個里程碑建立CQ變數，您可將其對應至Adobe Analytics屬性。 這些CQ變數的名稱會使用下列格式：

```shell
eventdata.events.milestoneXX
```

XX尾碼是定義里程碑的追蹤位移。 例如，指定4、8、16、20和28秒的追蹤位移，會產生下列CQ變數：

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
   <td>若已在DAM中設定，則對應至此的變數將包含視訊的<strong>使用者易記</strong>名稱(<strong>Title</strong>);如果未設定，則會改為傳送視訊的<strong>檔案名稱</strong>。 播放視訊時，只傳送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此變數的變數將包含檔案的名稱。 僅隨eventdata.events.a.media.view一起傳送 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此的變數將包含伺服器上檔案的路徑。 僅隨eventdata.events.a.media.view一起傳送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>每次傳遞區段裡程碑時傳送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>每次觸發里程碑時傳送，使用者觀看指定區段所花費的秒數也會隨此事件一併傳送。 例如eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>在初始化視訊檢視時傳送</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>視訊完成播放時傳送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>當指定的里程碑傳遞時，X代表裡程碑在<br />觸發的秒數 </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>在每個里程碑上傳送；在Adobe Analytics呼叫中顯示為pev3，通常以"video"<br />傳送 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>完全符合eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>包含已檢視區段的資訊，例如2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以開啟視訊以在DAM中進行編輯，並將&#x200B;**Title**&#x200B;中繼資料欄位設為所需名稱，借此設定視訊的&#x200B;**使用者易記**&#x200B;名稱。

1. 選取里程碑作為追蹤方法後，在「追蹤位移」方塊中，輸入以逗號分隔的追蹤位移清單（以秒為單位）。 例如，下列值會在視訊開始後的4、8、16、20和28秒定義里程碑：

   ```xml
   4,8,16,20,24
   ```

   偏移值必須是大於0的整數。 預設值為 `10,25,50,75`.

1. 若要將CQ變數對應至Adobe Analytics屬性，請從元件上CQ變數旁的ContentFinder拖曳Adobe Analytics屬性。

   如需有關最佳化對應的資訊，請參閱[在Adobe Analytics中測量視訊](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)指南。

1. [將framework新](/help/sites-administering/adobeanalytics.md) 增至頁面。
1. 若要在&#x200B;**預覽模式**&#x200B;中測試設定，請播放視訊以觸發Adobe Analytics呼叫。

後面的Adobe Analytics追蹤資料範例適用於「里程碑」追蹤，使用4,8,16,20和24的追蹤位移，以及CQ變數的下列對應：

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

在此範例中，Video元件會在架構頁面上顯示如下：

![video1](assets/video1.png)

>[!NOTE]
>
>若要查看對Adobe Analytics進行的呼叫，請使用適當的工具，例如DigitalPulse除錯程式或Fiddler。

使用提供的範例呼叫Adobe Analytics，在使用DigitalPulse除錯程式檢視時應該看起來像這樣：

![chlimage_1-128](assets/chlimage_1-128.png)

*這是對Adobe Analytics **發出**的第一個呼叫，其中包含下列值：*

* *eventdata.a.media.name的prop1和eVar1,*
* *prop2-4，以及包含contentType（視訊）和segment(1:O:1-4)的eVar2和eVar3*
* *event3，已對應至eventdata.events.a.media.view。*

![chlimage_1-129](assets/chlimage_1-129.png)

*這是第三&#x200B;**次**呼叫Adobe Analytics:*

* *prop1和eVar1包含a.media.name;*
* *event1，因為已檢視區段*
* *播放時間時傳送的event2 = 4*
* *event11已傳送，因為已到達eventdata.events.milestone8*
* *prop2至4未傳送（因為eventdata.events.a.media.view未觸發）*

## 非舊式里程碑{#non-legacy-milestones}

非舊式里程碑方法與里程碑方法類似，但里程碑是使用追蹤長度的百分比定義。 共性如下：

* 當視訊播放超過里程碑時，頁面會呼叫Adobe Analytics以追蹤事件。
* 為與Adobe Analytics屬性對應而定義的CQ變數](#cqvars)靜態集。[
* 元件會針對您定義的每個里程碑建立CQ變數，您可將其對應至Adobe Analytics屬性。

這些CQ變數的名稱會使用下列格式：

XX尾碼是定義里程碑之追蹤長度的百分比。 例如，指定10、25、50和75的百分比會產生下列CQ變數：

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 選取「非舊式里程碑」作為追蹤方法後，在「追蹤位移」方塊中，輸入以逗號分隔的追蹤長度百分比清單。 例如，下列預設值會以10、25、50和75%的追蹤長度定義里程碑：

   ```xml
   10,25,50,75
   ```

   偏移值必須是大於0的整數。

1. 若要將CQ變數對應至Adobe Analytics屬性，請從元件上CQ變數旁的ContentFinder拖曳Adobe Analytics屬性。

   如需有關最佳化對應的資訊，請參閱[在Adobe Analytics中測量視訊](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)指南。

1. [將framework新](/help/sites-administering/adobeanalytics.md) 增至頁面。
1. 若要在&#x200B;**預覽模式**&#x200B;中測試設定，請播放視訊以觸發Adobe Analytics呼叫。

## 舊式里程碑{#legacy-milestones}

此方法與Milestones方法類似，其差異在於&#x200B;*Tracking offset*&#x200B;欄位中指定的里程碑是百分比，而非視訊中的設定點。

>[!NOTE]
>
>「追蹤位移」欄位只接受以逗號分隔的清單，清單中包含1到100之間的整數。

1. 設定「追蹤偏移」。

   * e.g.10,50,75,100

   此外，傳送至Adobe Analytics的資訊不易自訂；僅有3個變數可供對應：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>若已在DAM中設定，則對應至此的變數將包含視訊的<strong>使用者易記</strong>名稱(<strong>Title</strong>);如果未設定標題，則會改為傳送視訊的<strong>檔案名稱</strong>。 播放視訊時只傳送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此變數的變數將包含檔案的名稱。 播放視訊時，只傳送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此變數的變數將包含伺服器上的檔案路徑。 播放視訊時，只傳送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以開啟視訊以在DAM中進行編輯，並將&#x200B;**Title**&#x200B;中繼資料欄位設為所需名稱，借此設定視訊的&#x200B;**使用者易記**&#x200B;名稱。 您也需要儲存完成時所做的變更。

1. 將這些變數對應至prop 1至3

   呼叫中的&#x200B;**其餘相關資訊**&#x200B;將串連至&#x200B;**one**&#x200B;變數&#x200B;**pev3**。

   **使** 用提供的範例呼叫至Adobe Analytics的範例，在使用DigitalPulse除錯程式檢視時應如下所示：

   ![lmilestones1](assets/lmilestones1.png)

   *呼叫&#x200B;**中傳送的pev3**變數包含下列資訊：*

   * *名稱*  — 視訊檔案的名稱(*film.avi*)

   * *Length*  — 視訊檔案的長度（以秒為單位）(*100*)

   * *播放器名稱*  — 用來播放視訊檔案(*HTML5視訊*)的視訊播放器

   * *播放的總秒數*  — 視訊播放的總秒數(*25*)

   * *開始時間戳記*  — 識別視訊播放開始時間的時間戳記(*133103567*)

   * *播放工作階段*  — 播放工作階段的詳細資料。此欄位指出使用者與視訊互動的方式。 這可能包括資料，例如開始播放視訊的位置、他們是否使用視訊滑桿來前進視訊，以及停止播放視訊的位置(*L10E24S58L58 — 視訊停止於秒。 第L10節的第25節，然後跳到秒。 48*)

## 舊秒{#legacy-seconds}

使用**舊秒**方法時，Adobe Analytics呼叫會每隔N秒觸發一次，其中N會在追蹤位移欄位中指定。

1. 將「追蹤位移」設為任何秒數，

   * 例如6
   >[!NOTE]
   >
   >「追蹤位移」欄位僅接受大於0的整數

   傳送至Adobe Analytics的資訊不易自訂。 只有3個變數可用於對應：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>若已在DAM中設定，則對應至此的變數將包含視訊的<strong>使用者易記</strong>名稱(<strong>Title</strong>);如果未設定標題，則會改為傳送視訊的<strong>檔案名稱</strong>。 播放視訊時只傳送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案的名稱。 播放視訊時，只傳送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此變數的變數將包含伺服器上的檔案路徑。 播放視訊時，只傳送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以開啟視訊以在DAM中進行編輯，並將&#x200B;**Title**&#x200B;中繼資料欄位設為所需名稱，借此設定視訊的&#x200B;**使用者易記**&#x200B;名稱。 您也需要儲存完成時所做的變更。

1. 將這些變數對應至prop1、prop2和prop3

   呼叫中的&#x200B;**其餘相關資訊**&#x200B;將會連結至&#x200B;**一個**&#x200B;變數&#x200B;**pev3**。

   使用提供的範例呼叫Adobe Analytics，在使用DigitalPulse除錯程式檢視時應該看起來像這樣：

   ![lseconds](assets/lseconds.png)

   *呼叫類似於上述的舊版里程碑呼叫。請參閱此處提供的pev3 **[的相關資訊。](/help/sites-administering/adobeanalytics.md)**.*

**本教學課程中使用的參考：**

[0] [https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)
