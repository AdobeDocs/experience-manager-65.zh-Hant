---
title: We.Gov參考站點FOIA逐步說明
seo-title: We.Gov reference site FOIA walkthrough
description: 請參閱We.Gov參考網站逐步說明，了解AEM Forms如何協助政府接收和傳遞個人根據《資訊自由法》要求提供的資訊。
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# We.Gov參考站點FOIA逐步說明 {#we-gov-reference-site-foia-walkthrough}

## 參考網站資訊自由法案情境 {#reference-site-freedom-of-information-act-scenario}

We.Gov是一個國營組織，允許養父母在收養孩子時報名接受子女撫養。 We.Gov還允許家長根據資訊自由法向下列政府部門索取資訊：

* 國防後勤局
* 國防部監察長辦公室
* 司法部 — 資訊政策廳
* 海軍部
* 環境保護署

有關《資訊自由法》的更多資訊，請參見 [www.foia.gov](https://www.foia.gov).

此情境包含下列角色：

* 莎拉·羅絲，那個
* 約翰·雅可布，負責處理請求的人將請求轉給相應部門
* 根據請求提供資訊的政府僱員格洛麗亞·里奧斯

## Sarah根據FOIA發起資訊請求 {#sarah-initiates-request-for-information-under-foia}

根據《資訊自由法》，Sarah要求提供2013-2016年年度兒童和家庭管理局案件記錄的副本。 Sarah向司法部 — 資訊政策辦公室提交了這一請求，並表示她願意支付最多100美元的印刷和郵資費。

### 運作方式 {#how-it-works}

### 你自己看 {#see-it-yourself}

在瀏覽器中，開啟 `https://<hostname>:<PublishPort>/wegov`. 在We.Gov網站中，點選「應用程式>所有應用程式」。 在「所有應用程式」頁面中，點選「Application for FOIA Request」（應用程式FOIA請求）下的「Apply（應用）」。

## Sarah開始申請FOIA的資訊 {#sarah-starts-her-application-for-information-under-foia}

Sarah點擊 **套用** 在《資訊自由法》申請表頁面中，Sarah輸入了以下資訊：

* **代理：** Sarah將請求處理的機構指定為司法部 — 資訊政策辦公室。

* **將支付**:莎拉說，她願意支付高達100美元的印刷和郵資費用。
* **詳細說明請求**:Sarah指明&quot;2013至2016財政年度請求兒童和家庭管理局案件日誌副本&quot;。

![要求提供2013至2016財政年度兒童和家庭管理局案件記錄副本](assets/sarahfiosform.png)

要求提供2013至2016財政年度兒童和家庭管理局案件記錄副本

Sarah隨時都可以點選「儲存」以儲存表單草稿，稍後再回來填寫表單並提交。 莎拉提交了表格。

>[!NOTE]
>
>從電子郵件繼續工作流程僅適用於登入的使用者。 在參考網站案例中，請確定已新增使用者Sarah Rose。 Sarah的登錄憑據為 `srose/password`.

## John Jacobs收到並核准申請 {#john-jacobs-receives-and-approves-the-application}

約翰·雅可布會收到請求，並將其路由給合適的人。 AEM收件匣可讓她在單一位置查看所有已提交的應用程式。

### 運作方式 {#how-it-works-1}

當Sarah填寫並提交FOIA應用程式時，會將應用程式的記錄發送到John Jacobs的收件箱。 John Jacobs可以查看提交的申請，並接受或拒絕。

### 你自己看 {#see-it-yourself-1}

您可以在https://&lt;訪問AEM收件箱&#x200B;***主機名***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html。 使用jjacobs/password作為John Jacobs的使用者名稱/密碼登入AEM收件匣，並查看FOIA應用程式。 如需有關將AEM收件匣用於表單導向工作流程工作的資訊，請參閱 [在AEM收件匣中管理Forms應用程式和任務](/help/forms/using/manage-applications-inbox.md).

![約翰雅各布](assets/johnjacobs.png)

John Jacobs可以從應用程式儀表板查看、批准或拒絕該應用程式。 John Jacobs會選取並開啟請求詳細資訊，並在檢閱請求後核准。

![johnjacobsetskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到確認電子郵件</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs批准該申請後，Sarah會收到We.Gov網站發來的確認電子郵件。 Sarah被告知了處理申請所需的費用和時間。 電子郵件中還包含電子郵件和電話詳細資訊，莎拉可以聯繫這些資訊，了解她的應用程式的更新。

![薩拉赫羅塞馬](assets/sarahroseemail.png)

## Gloria收到FOIA要求二級批准 {#gloria-receives-the-foia-request-for-second-level-approval}

約翰·雅各布斯填寫了要求的資訊，並批准了莎拉的請求，之後這些請求就會提交格洛麗亞·里奧斯，由他最終批准。 Gloria審閱所附記錄檔案並批准該請求。

![格洛里亞辛博克](assets/gloriariosinbox.png)

### 運作方式 {#how-it-works-2}

當John Jacobs批准FOIA請求時，將建立應用程式的PDF或記錄檔，併發送到Gloria Rios的收件箱。 Gloria可以查看提交的請求，並批准或拒絕它。

### 自己看 {#see-for-yourself}

您可以在https://&lt;訪問AEM收件箱&#x200B;***主機名***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html。 使用grios/password作為Gloria Rios的用戶名/密碼登錄AEM收件箱，並查看FOIS請求。

Gloria開啟請求並檢查FOIA請求的詳細資訊。 在審查了請求的詳情並檢查提供所需檔案的可行性之後，Gloria核准了該請求。

![格洛里亞利](assets/gloriariosapproves.png)

## Sarah會收到通知，通知她的請求已獲得批准 {#sarah-receives-notification-that-her-request-is-approved}

Gloria批准FOIA請求後，Sarah會收到一封電子郵件，通知她該請求已獲得批准。 該電子郵件還包括關於提供檔案的暫定時間表的資訊，以及就請求採取後續行動的聯繫詳情。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
