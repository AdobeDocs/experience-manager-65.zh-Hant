---
title: 推播通知
seo-title: Push Notifications
description: 請詳閱本頁面，了解如何在AEM Mobile應用程式中使用推播通知。
seo-description: Follow this page to learn about how to use push notifications in an AEM Mobile app.
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3273'
ht-degree: 1%

---

# 推播通知{#push-notifications}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

若能立即以重要通知提醒您的AEM Mobile應用程式使用者，對行動應用程式及其行銷活動的價值至關重要。 在此，我們將說明需要採取哪些步驟來讓您的應用程式接收推播通知，以及如何設定並將來自AEM Mobile的推播傳送至手機上安裝的應用程式。 此外，本節說明如何設定 [深層連結](#deeplinking) 功能。

>[!NOTE]
>
>*推播通知無法保證傳送；它們更像公告。 我們會盡力確保每個人都能收到，但並非保證的傳送機制。 此外，傳送推播的時間可能會從少於一秒到最多半小時不等。*

搭配AEM使用推播通知需要幾項不同技術。 首先，必須使用推播通知服務提供者來管理通知和裝置(AEM尚未這麼做)。 兩個提供者皆已透過AEM立即設定： [Amazon簡單通知服務](https://aws.amazon.com/sns/) （或SNS），以及 [普什沃什](https://www.pushwoosh.com/). 其次，特定行動作業系統的推播技術必須經過適當的服務，即適用於iOS裝置的Apple推播通知服務（或APNS）;和適用於Android裝置的Google雲端通訊（或GCM）。 雖然AEM不會直接與這些平台特定服務通訊，但AEM必須提供一些相關設定資訊及通知，這些服務才能執行推播。

安裝並設定後（如下所述），其運作方式如下：

1. 推播通知會在AEM中建立，並傳送至服務提供者(Amazon SNS或Pushwoosh)。
1. 服務提供者會收到資料，並傳送至核心提供者（APNS或GCM）。
1. 核心提供者會將通知推送至為該推送註冊的所有裝置。 對於每個設備，它使用蜂窩資料網路或WiFi（以當前設備上可用的為準）。
1. 如果其註冊的應用程式未執行，通知會顯示在裝置上。 點選通知的使用者將啟動應用程式，並在應用程式內顯示通知。 如果應用程式已執行，則只會顯示應用程式內通知。

此版AEM支援iOS和Android行動裝置。

## 概述與程式 {#overview-and-procedure}

若要在AEM Mobile應用程式中使用推播通知，必須執行下列高階步驟。

通常，AEM開發人員會：

1. 向Apple和Google傳訊服務註冊
1. 向推送訊息服務註冊並進行配置
1. 新增推送支援至應用程式
1. 準備電話進行測試

而AEM管理員會：

1. 在AEM應用程式上設定推送
1. 建置和部署應用程式
1. 傳送推播通知
1. 設定深層連結 *（可選）*

### 步驟1:向Apple和Google傳訊服務註冊 {#step-register-with-apple-and-google-messaging-services}

#### 使用Apple推播通知服務(APNS) {#using-the-apple-push-notification-service-apns}

前往Apple頁面 [此處](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) 以熟悉Apple推播通知服務。

若要使用APNS，您需要 **憑證** 檔案（.cer檔案）、推送 **私密金鑰** （a.p12檔案）和 **私密金鑰密碼** 從Apple。 如何進行此操作的說明 [此處](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html).

#### 使用Google雲端通訊(GCM)服務 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google正以名為Firebase雲端通訊(FCM)的類似服務取代GCM。 如需FCM的詳細資訊，請按一下 [此處](https://developers.google.com/cloud-messaging/faq).

前往Google頁面 [此處](https://developer.android.com/google/gcm/index.html) 以熟悉適用於Android的Google雲端訊息。

您需要依照 [此處](https://developer.android.com/google/gcm/gs.html) to **建立Google API專案**, **啟用GCM服務**，和 **取得API金鑰**. 您需要 **API金鑰** 傳送推播通知至Android裝置。 另外，請錄制 **項目編號**，有時也稱為 **GCM寄件者Id**.

下列步驟顯示建立GCM API金鑰的不同方法：

1. 登入google並前往 [Google的開發人員頁面](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. 從清單中選擇您的應用程式（或建立新的應用程式）。
1. 在Android封裝名稱下，輸入您的應用程式id，即 `com.adobe.cq.mobile.weretail.outdoorsapp`. （如果無法運作，請使用「test.test」再試一次。）
1. 按一下 **繼續選擇和配置服務**
1. 選取雲端訊息，然後按一下 **啟用Google雲端訊息**.
1. 接著會顯示新的伺服器API金鑰和（新的或現有的）傳送者ID。

>[!NOTE]
>
>記錄伺服器API金鑰。 此值是在您的推送提供者網站上輸入。

### 步驟2:註冊及設定推送訊息服務 {#step-register-and-configure-a-push-messaging-service}

AEM設定為使用下列三種服務其中之一來傳送推播通知：

* Amazon SNS
* Pushwoosh
* AdobeMobile Services

*Amazon SNS* 和 *普什沃什* 設定可讓您從AEM畫面內推送。

*AdobeMobile Services* 設定可讓您使用Adobe Analytics帳戶，從AdobeMobile Services中設定及傳送推播通知（但必須使用此設定來建置應用程式，才能啟用AMS推播通知）。

#### 使用Amazon SNS報文傳送服務 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*有關Amazon SNS和建立新AWS帳戶的連結的資訊 [此處](https://aws.amazon.com/sns/). 你可以免費開一年的賬戶。*

如果您不想使用Amazon SNS，可以跳過這些步驟。

請按照以下步驟設定Amazon SNS以獲取推播通知：

1. **向Amazon SNS註冊**

   1. 記錄您的帳戶ID。 格式應為12位數，不含空格或破折號，即&quot;123456789012&quot;。
   1. 請確定您位於「美國東部」或「歐盟」地區，因為稍後的步驟（身份池建立）需要其中一個步驟。
   1. 註冊後，登錄管理控制台並選擇 [SNS](https://console.aws.amazon.com/sns/) （推播通知服務）。 如果出現「Get Started（開始）」，請按一下。

1. **建立存取金鑰和ID**

   1. 按一下螢幕右上方的登錄名，然後從菜單中選擇「安全憑據」。
   1. 按一下「Access Keys（訪問密鑰）」 ，然後在下面的空格中按一下 **建立新訪問密鑰**.
   1. 按一下 **顯示訪問密鑰**，並複製並儲存顯示的存取金鑰ID和秘密存取金鑰。 如果您選擇下載索引鍵的選項，您會收到包含這些相同值的csv檔案。
   1. 可在此頁面上管理其他安全相關憑證及其他憑證。

   >[!NOTE]
   >
   >存取金鑰可用於多個應用程式。

   對於使用「AWS沙箱」帳戶的組織，步驟非常類似，並概述如下：

   1. 按一下螢幕右上方的登錄名，然後從菜單中選擇「我的安全憑據」。
   1. 按一下動作左側清單中的使用者，然後選擇您的使用者名稱。
   1. 按一下「安全憑據」頁簽。
   1. 從這裡，您會看到您的金鑰並建立新金鑰。 儲存金鑰以供稍後使用。


1. **建立主題**

   1. 按一下 **建立主題** 並選擇主題名稱。 記錄所有欄位，如「主題ARN」、「主題所有者」、「地區」、「顯示名稱」。
   1. 按一下 **其他主題動作** > **編輯主題策略**. 在 **允許這些用戶訂閱此主題**，選取 **大家。**
   1. 按一下 **更新策略**.

   >[!NOTE]
   >
   >您可以針對不同案例建立多個主題，例如開發、測試、示範等。 其餘的SNS配置可以保持不變。 使用不同主題建立應用程式；傳送至該主題的推播通知只會由使用該主題建立的應用程式接收。

1. **建立平台應用程式**

   1. 按一下「應用程式」，然後按一下「建立平台應用程式」。 選擇名稱並選取平台(iOS適用的APNS、Android適用的GCM)。 根據平台，其他欄位需要填入：

      1. 若為APNS，必須輸入P12檔案、密碼、憑證和私密金鑰。 應在步驟中取得 *使用Apple推播通知服務(APNS)* 上。
      1. 若為GCM，必須輸入API金鑰。 本應在步驟中取得 *使用Google雲端通訊(GCM)服務* 上。
   1. 對您要支援的每個平台重複上述步驟一次。 若要同時推送至iOS和Android，必須建立兩個平台應用程式。


1. **建立身份池**

   1. 使用 [Cognito](https://console.aws.amazon.com/cognito) 建立身份池，該池將儲存未驗證用戶的基本資料。 請注意，目前只有「美國東部」和「歐盟」地區受Amazon Cognito支援。
   1. 請為其命名，並勾選「啟用未驗證身分的存取」方塊。
   1. 在下一頁(「*您的Cognito身份需要訪問您的資源*&quot;)按一下「允許」。
   1. 在頁面右上方，按一下連結「*編輯標識池&quot;*. 將顯示標識池Id。 保存此文本以備以後使用。
   1. 在同一頁上，選擇「未驗證角色」旁邊的下拉清單，並確保它具有Cognito_角色&lt;pool name=&quot;&quot;>已選取UnauthRole。 儲存您的變更。

1. **設定存取權限**

   1. 登入 [身分與存取管理](https://console.aws.amazon.com/iam/home) (IAM)
   1. 選擇角色
   1. 按一下在上一步中建立的角色，稱為Cognito_&lt;youridentitypoolname>取消驗證角色。 記錄顯示的「角色ARN」。
   1. 如果尚未開啟「內嵌原則」，請開啟它。 您應該會在那裡看到一個名稱類似oneClick_Cognito_的策略&lt;youridentitypoolname>Unauth_Role_1234567890123。
   1. 按一下「編輯策略」。 用此JSON片段替換策略文檔的內容：

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "版本":"2012-10-17",</p> <p> "陳述式": [</p> <p> {</p> <p> "動作": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS：訂閱"</p> <p> ],</p> <p> 「效果」："允許",</p> <p> "資源": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. 按一下 **應用策略**


#### 使用Pushwoosh報文傳送服務 {#using-the-pushwoosh-messaging-service}

如果您不想使用Pushwoosh，可跳過此步驟。

使用Pushwoosh:

1. **用Pushwoosh註冊**

   1. 前往pushwoosh.com並建立新帳戶。

1. **建立API存取權杖**

   1. 在Pushwoosh網站上，前往API存取功能表項目以產生API存取權杖。 您需要安全地記錄此內容。

1. **建立新的應用程式**

   1. 若要取得Android支援，您需要提供GCM API金鑰。
   1. 設定應用程式時，請選擇Cordova作為架構。
   1. 若要取得iOS支援，您必須提供憑證檔案(.cer)、推送憑證(.p12)和私密金鑰密碼；這些內容應可從Apple的APNS網站取得。 對於「框架」，請選擇「Cordova」。
   1. Pushwoosh會以「XXXXX-XXXXX」的形式產生該應用程式的應用程式ID，其中每個X都是十六進位值（0到F）。

>[!NOTE]
>
>*如果在AEM中設定第二個應用程式時使用相同的應用程式ID（和其他相關值）:API存取Token和GCM Id)，透過AEM上第二個應用程式傳送的任何推播通知，都會隨該應用程式ID前往任何其他應用程式。*

### 步驟3:新增推送支援至應用程式 {#step-add-push-support-to-the-app}

#### 添加ContentSync配置 {#add-contentsync-configuration}

建立兩個名為notificationsConfig的內容節點（一個在app-config中，一個在app-config-dev中）:

* /content/`<your app>`/shell/jcr:content/pge-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/pge-app/app-config/notificationsConfig

使用下列屬性（.content.xml檔案）:
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot; jcr:primaryType=&quot;nt:unstructured&quot; excludeProperties=&quot;[appAPIAccessToken]&quot; path=&quot;。./../../../....
[targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>內容同步處理常式會尋找這些節點，如果節點不在，則不會寫出pge-notifications-config.json檔案。

#### 添加客戶端庫 {#add-client-libraries}

必須依照下列步驟，將推播通知用戶端程式庫新增至應用程式：

CRXDE Lite:

1. 導覽至 */etc/designs/phonegap/&lt;app name=&quot;&quot;>/clientlibsall。*
1. 連按兩下屬性窗格中的內嵌區段。
1. 在顯示的對話方塊中，按一下+按鈕以新增用戶端資料庫。
1. 在新文字欄位中新增「cq.mobile.push」，然後按一下「確定」。
1. 新增另一個名為cq.mobile.push.amazon的，然後按一下「確定」。
1. 儲存變更。

>[!NOTE]
>
>如果推播通知遭移除或未使用，基於應用程式上的空間考量，以及為了避免主控台錯誤訊息，請從應用程式中移除這些clientlib。

### 步驟4:準備電話以進行測試 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*若是推播通知，您必須在實際裝置上進行測試，因為模擬器無法接收推播通知。*

#### iOS {#ios}

若是iOS，您需要使用Mac OS電腦，而且您必須加入 [iOS開發人員計畫](https://developer.apple.com/programs/ios/). 有些公司擁有公司許可證，可供所有開發商使用。

若使用XCode 8.1，在使用推播通知之前，您必須前往專案中的功能標籤，並將推播通知切換為開啟。

#### Android {#android}

若要使用CLI在Android手機上安裝應用程式(請參閱下列內容： **步驟6 — 建置和部署應用程式**)，您必須先將手機置於「開發人員模式」。 請參閱 [啟用裝置上開發人員選項](https://developer.android.com/tools/device.html#developer-device-options) 以了解執行此操作的詳細資訊。

### 步驟5:在AEM應用程式上設定推送 {#step-configure-push-on-aem-apps}

在建立並部署至您已設定的行動裝置之前，您必須針對您決定使用的訊息服務配置通知設定。

1. 為推播通知建立適當的授權群組。
1. 以適當使用者身分登入AEM，按一下「應用程式」標籤。
1. 按一下應用程式。
1. 找到「管理Cloud Services」圖磚，然後按一下鉛筆，以修改您的雲端設定。
1. 選擇「Amazon SNS連接」、「Pushwoosh連接」或「AdobeMobile Services」作為通知配置。
1. 輸入提供程式屬性，然後按一下提交以保存它們，然後按一下完成。 在此階段，除了AMS外，這些證書未進行遠程驗證。
1. 您現在應該會看到您剛在「管理Cloud Services」方塊上輸入的設定。

### 步驟6:建置和部署應用程式 {#step-build-and-deploy-the-app}

**注意：** 另請參閱我們的指示 [此處](/help/mobile/building-app-mobile-phonegap.md) 建置PhoneGap應用程式。

使用PhoneGap建立和部署您的應用程式有兩種方式。

**注意：** 針對推播通知測試，模擬器不足，因為推播通知會在推播提供者(Apple或Google)和裝置之間使用不同的通訊協定。 當前的Mac/PC硬體和模擬器不支援此功能。

1. *PhoneGap Build* 是PhoneGap提供的服務，可在其伺服器上為您建立應用程式，並可讓您直接下載至裝置。 請參閱 [PhoneGap Build檔案](https://build.phonegap.com/) 了解如何設定和使用PhoneGap Build。

1. *PhoneGap命令行介面* (CLI)可讓您在命令列上使用一組豐富的PhoneGap命令，來建置、除錯和部署您的應用程式。 請參閱 [PhoneGap開發人員檔案](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) 了解如何設定和使用PhoneGap CLI。

### 步驟7:傳送推播通知 {#step-send-a-push-notification}

若要建立新通知並加以傳送，請依照下列步驟進行。

1. 建立新通知

   * 在AEM Mobile應用程式的控制面板中，尋找「推播通知」方塊。
   * 在右上角的功能表中，選擇「建立」。 請注意，此按鈕要等到雲端設定首次設定後才可用。
   * 在建立通知精靈中，輸入標題和訊息，然後按一下「建立」按鈕。 您的通知現在已準備好立即或稍後傳送。 可編輯訊息和/或標題，且可變更及儲存。

1. 傳送通知

   * 在「應用程式」控制面板中，找到「推播通知」方塊。
   * 選取通知，或按一下右下角的詳細資訊按鈕(...)，以顯示通知清單。 此清單也會指出通知是否已準備好傳送、已傳送，或傳送期間是否發生錯誤。
   * 選取一個通知的核取方塊（僅限），然後按一下清單上方的「傳送通知」按鈕。 您將有一次機會在顯示的對話方塊上「取消」或「傳送」通知。

1. 處理結果

   * 如果推播通知服務(Amazon SNS或Pushwoosh)收到傳送要求，確認其有效，並成功將其傳送至原生提供者（APNS和GCM），則「傳送」對話方塊將會關閉，且不會顯示訊息。 在通知清單中，該通知的狀態將列為已傳送。
   * 如果推送傳送失敗，對話方塊將顯示指出問題的訊息。 在通知清單中，該通知的狀態將列為「錯誤」，但如果問題得到糾正，則可以再次發送通知。 發生錯誤時，伺服器錯誤記錄中應會顯示其他錯誤資訊。
   * 請注意，iOS和Android推播通知之間有一些平台差異。 其中：

      * 使用CLI建立應用程式會在部署於Android後啟動。 在iOS上，您必須手動啟動。 由於推播註冊步驟會在啟動時進行，因此Android應用程式可以立即收到推播通知（因為它會啟動並註冊），而iOS應用程式則不會。
      * 在Android上，「確定」按鈕文字為全大寫（以及應用程式內通知上新增的任何其他按鈕），而在iOS中則非全大寫。

若為AMS推播通知，必須從AMS伺服器撰寫及傳送通知。 AMS提供的推播通知功能，超過了AEM通知AWS和Pushwoosh提供的功能。

>[!NOTE]
>
>*推播通知無法保證傳送；它們更像公告。 請盡最大努力確保每個人都聽到，但並非保證的傳送機制。 此外，傳送推播的時間可能會從少於一秒到最多半小時不等。*

### 使用推播通知設定深層連結 {#configuring-deep-linking-with-push-notifications}

什麼是深層連結？ 在推播通知的內容中，這是可讓應用程式開啟或導向（如果開啟）至應用程式內指定位置的方法。

如何運作？ 推播通知的作者可選擇新增按鈕標籤(即「給我看看！」) 至通知，並透過視覺路徑瀏覽器選擇要在通知中連結的頁面。 傳送後，推播會正常發生，除了應用程式內訊息中的「確定」按鈕會取代為「關閉」按鈕，並指定新按鈕（「顯示我！」） 的上界。 按一下新按鈕後，應用程式會前往應用程式內的指定頁面。 按一下「關閉」會關閉訊息。

如果應用程式未開啟，陰影會正常顯示。 在陰影中對通知採取動作，會開啟應用程式，然後根據推播通知中已設定的項目，向使用者呈現深層連結按鈕。

建立通知、新增按鈕文字和連結路徑供選用的深層連結使用：

>[!CAUTION]
>
>.若要存取控制面板中的「推播通知」方塊，請遵循下列步驟。

1. 按一下 **管理Cloud Services** 方塊。

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 選取 **Pushwoosh連接**. 按一下&#x200B;**下一步**。

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. 輸入屬性的詳細資訊，然後按一下 **提交**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   提交設定後， **推播通知** 圖磚會顯示在控制面板中。

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 建立通知精靈 {#create-notification-wizard}

一旦 **推播通知** 圖磚會顯示在控制面板中，使用建立通知精靈來新增內容：

1. 按一下右上角的添加符號 **推播通知** 圖磚以開啟 **建立通知精靈**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. 按一下連結路徑中的瀏覽圖示，會向使用者呈現應用程式的內容結構。

   選取路徑後，按一下核取圖示。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >「連結按鈕文字」限制為20個字元。
   >
   >如果使用者沒有最新版本的應用程式，且連結的路徑無法使用，則確認深層連結的動作會將使用者帶往應用程式的主要頁面。

1. 輸入 **文字詳細資料** 在 **建立通知精靈** 按一下 **建立**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   按一下您從 **推播通知** 方塊。

   您可以編輯屬性、傳送通知或刪除通知。

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**其他資訊**:
>
>6.4版後將不支援Pushwoosh和Amazon SNS，並且將作為包共用的附加元件提供。

### 後續步驟 {#the-next-steps}

了解應用程式推播通知的詳細資訊後，請參閱 [AEM Mobile內容個人化](/help/mobile/phonegap-aem-mobile-content-personalization.md).
