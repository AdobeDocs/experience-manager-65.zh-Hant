---
title: We.Gov參考網站FOIA逐步說明
description: 請參閱We.Gov參考網站逐步說明，瞭解AEM Forms如何協助政府接收及傳閱個人依資訊自由法案要求之資訊。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# We.Gov參考網站FOIA逐步說明 {#we-gov-reference-site-foia-walkthrough}

## 參考網站資訊自由法案情境 {#reference-site-freedom-of-information-act-scenario}

We.Gov是國家營運的組織，如果養父母領養孩子，可讓他們註冊子女撫養費。 We.Gov也可讓家長根據資訊自由法，向下列政府部門要求資訊：

* 國防後勤局
* 國防部監察長辦公室
* 司法部 — 資訊政策辦公室
* 海軍部
* 環境保護局

如需資訊自由法案的詳細資訊，請參閱 [https://www.foia.gov/](https://www.foia.gov).

此案例涉及以下角色：

* Sarah Rose，此資訊索取人
* John Jacobs，處理要求的人員，會將要求轉送至適當部門
* Gloria Rios，根據要求提供資訊的政府職員

## Sarah在FOIA底下發起資訊請求 {#sarah-initiates-request-for-information-under-foia}

根據資訊自由法，Sarah要求2013年至2016年兒童與家庭管理(FY)案件記錄副本。 Sarah將此要求提交給司法部 — 資訊局政策，也表示她可支付高達100美元的列印和郵資費用。

### 運作方式 {#how-it-works}

### 親眼看看 {#see-it-yourself}

在您的瀏覽器中，開啟 `https://<hostname>:<PublishPort>/wegov`. 在We.Gov網站中，選取「應用程式」>「所有應用程式」。 在「所有應用程式」頁面中，選取「FOIA要求的應用程式」下的「套用」。

## Sarah開始申請FOIA下的資訊 {#sarah-starts-her-application-for-information-under-foia}

Sarah點按次數 **套用** 而在資訊自由法案申請表頁面中，Sarah會輸入以下資訊：

* **代理商：** Sarah指定要求所處理的機構為司法部 — 資訊政策辦公室。

* **將支付最高至**：Sarah指定她準備支付高達100美元的列印和郵資費用。
* **詳細說明請求**：Sarah指定「要求2013至2016會計年度的『兒童與家庭管理』個案記錄副本」。

![索取2013至2016會計年度「兒童與家庭管理」個案記錄的復本](assets/sarahfiosform.png)

索取2013至2016會計年度「兒童與家庭管理」個案記錄的復本

Sarah隨時可以選擇 **儲存** 以儲存表單草稿，稍後再回來填寫表單並提交它。 Sarah提交表單。

>[!NOTE]
>
>從電子郵件恢復工作流程僅適用於登入的使用者。 在參考網站案例中，確定已新增使用者Sarah Rose。 Sarah的登入憑證有 `srose/password`.

## John Jacobs收到並核准該申請 {#john-jacobs-receives-and-approves-the-application}

John Jacobs會收到要求，並導向給合適的人。 AEM收件匣可讓John在一個位置檢視所有已提交的申請。

### 運作方式 {#how-it-works-1}

當Sarah填寫並提交FOIA申請表時，申請表記錄會傳送到John Jacobs的收件匣。 John Jacobs可以檢視提交的應用程式，並接受或拒絕它。

### 親眼看看 {#see-it-yourself-1}

您可以在https://存取AEM收件匣&lt;***主機名稱***>：&lt;***Publishport***>/content/we-finance/global/en/login.html？resource=/aem/inbox.html. 使用jjacobs/password作為John Jacobs的使用者名稱/密碼登入AEM收件匣，並檢視FOIA應用程式。 如需有關使用AEM收件匣執行以表單為中心的工作流程任務的資訊，請參閱 [管理AEM收件匣中的Forms應用程式和工作](/help/forms/using/manage-applications-inbox.md).

![約翰雅各布](assets/johnjacobs.png)

John Jacobs可以從應用程式儀表板檢視、核准或拒絕應用程式。 John Jacobs會選取並開啟請求詳細資料，並在檢閱請求後核准請求。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到確認電子郵件</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs核准申請後，Sarah會收到We.Gov網站的認可電子郵件。 系統會通知Sarah處理申請所需的費用和時間。 電子郵件也包含Sarah可以聯絡以取得應用程式更新的電子郵件和電話詳細資訊。

![薩拉赫羅塞梅爾](assets/sarahroseemail.png)

## Gloria會收到FOIA的第二層核准請求 {#gloria-receives-the-foia-request-for-second-level-approval}

在John Jacobs填寫必填資訊並核准Sarah的請求後，該請求將轉至Gloria Rios進行最終核准。 Gloria會稽核附加的記錄檔案並核准請求。

![gloriariosinbox](assets/gloriariosinbox.png)

### 運作方式 {#how-it-works-2}

當John Jacobs核准FOIA請求時，應用程式的PDF或記錄檔案即會建立，並傳送至Gloria Rios的收件匣。 Gloria可以檢視已提交的請求，並核准或拒絕該請求。

### 親自檢視 {#see-for-yourself}

您可以在https://存取AEM收件匣&lt;***主機名稱***>：&lt;***Publishport***>/content/we-finance/global/en/login.html？resource=/aem/inbox.html. 使用grios/密碼作為Gloria Rios的使用者名稱/密碼登入AEM收件匣，並檢視FOIS要求。

Gloria會開啟要求，並檢查FOIA要求的詳細資料。 在檢閱請求的詳細資訊並檢查提供所需檔案的可行性後，Gloria核准了請求。

![gloriariosapens](assets/gloriariosapproves.png)

## Sarah收到請求獲得核准的通知 {#sarah-receives-notification-that-her-request-is-approved}

Gloria核准FOIA要求後，Sarah會收到電子郵件，通知她要求已核准。 此電子郵件也包含提供檔案的暫定時間表相關資訊，以及跟進請求的聯絡人詳細資訊。

![sarahrosemailapproval](assets/sarahroseemailapproval.png)
