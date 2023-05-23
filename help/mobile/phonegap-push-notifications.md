---
title: 推播通知
description: 請按照此頁瞭解如何在Adobe Experience Manager Mobile應用中使用推送通知。
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '3293'
ht-degree: 1%

---

# 推播通知{#push-notifications}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

能夠用重要通知即時提醒你的AEM Mobile應用用戶，對於移動應用的價值及其營銷活動至關重要。 在此，我們將介紹允許您的應用程式接收推送通知所需執行的步驟，以及如何配置並將來自AEM Mobile的推送發送到手機上安裝的應用程式。 此外，本節介紹如何配置 [深度連結](#deeplinking) 功能。

>[!NOTE]
>
>*推送通知不能保證交付；更像是公告。 盡最大努力確保每個人都能收到這些檔案，但它們不是保證的遞送機制。 此外，推車的時間可能從不到一秒到長達半小時不等。*

使用推送通知AEM需要一些不同的技術。 首先，必須使用推送通知服務提供商來管理認證和設AEM備（目前尚未這樣做）。 兩個提供程式是開箱配置的，具AEM有： [Amazon簡單通知服務](https://aws.amazon.com/sns/) （或SNS）, [普什沃什](https://www.pushwoosh.com/)。 其次，給定移動作業系統的推送技術必須通過適當的服務 — Apple為iOS設備提供的推送通知服務(APNS);和GoogleAndroid設備雲消息(GCM)。 雖然AEM不直接與這些平台特定的服務通信，但是必須通過通AEM知提供一些相關配置資訊，以便這些服務執行推送。

安裝和配置後（如下所述），其工作方式如下：

1. 推送通知在中創AEM建，併發送給服務提供商(AmazonSNS或Pushwosh)。
1. 服務提供商將接收該服務，並將其發送到核心提供商（APNS或GCM）。
1. 核心提供方將通知推送到為該推送註冊的所有設備。 對於每台設備，它使用蜂窩資料網路或WiFi（以設備上當前可用的方式）。
1. 如果註冊的應用未運行，則通知將顯示在設備上。 點擊通知的用戶將啟動應用並在應用內顯示通知。 如果應用程式已在運行，則只顯示應用程式內通知。

此版本支AEM持iOS和Android移動設備。

## 概述和過程 {#overview-and-procedure}

要在AEM Mobile應用中使用推送通知，必須執行以下高級步驟。

通常，Experience Manager開發人員執行以下操作：

1. 註冊Apple和Google消息服務
1. 向推送消息服務註冊並配置
1. 向應用添加推送支援
1. 準備電話以進行測試

Experience Manager管理員執行以下操作：

1. 配置推送應AEM用
1. 生成和部署應用
1. 發送推送通知
1. 配置深度連結 *（可選）*

### 步驟1:註冊Apple和Google消息服務 {#step-register-with-apple-and-google-messaging-services}

#### 使用Apple推送通知服務(APNS) {#using-the-apple-push-notification-service-apns}

轉到Apple頁 [這裡](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) 熟悉Apple推送通知服務。

要使用APN，您需要 **證書** 檔案（.cer檔案），推送 **私鑰** （a .p12檔案）和 **私鑰密碼** Apple。 有關如何執行此操作的說明，可以找到 [這裡](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/)。

#### 使用Google雲消息(GCM)服務 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google正在用一項名為Firebase Cloud Messaging(FCM)的類似服務取代GCM。 有關FCM的詳細資訊，請按一下 [這裡](https://developers.google.com/cloud-messaging/faq)。

轉到Google頁 [這裡](https://developer.android.com/google/gcm/index.html) 熟悉GoogleAndroid雲消息。

您需要執行步驟 [這裡](https://developer.android.com/google/gcm/gs.html) 至 **建立GoogleAPI項目**。 **啟用GCM服務**, **獲取API密鑰**。 你需要 **API密鑰** 向Android設備發送推送通知。 另外，錄制 **項目編號**，有時也稱為 **GCM發件人ID**。

以下步驟顯示了建立GCM API密鑰的不同方法：

1. 登錄Google並轉到 [Google開發商頁面](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm)。
1. 從清單中選擇您的應用（或建立新應用）。
1. 在Android包名稱下，輸入您的應用ID，即 `com.adobe.cq.mobile.weretail.outdoorsapp`。 (如果這不起作用，請使用「test.test」重試。)
1. 按一下 **繼續選擇和配置服務**
1. 選擇雲消息，然後按一下 **啟用Google雲消息**。
1. 然後將顯示新的伺服器API密鑰和（新的或現有的）發件人ID。

>[!NOTE]
>
>記錄伺服器API密鑰。 此值是在推送提供程式的站點上輸入的。

### 步驟2:註冊和配置推送消息服務 {#step-register-and-configure-a-push-messaging-service}

已AEM配置為使用以下三種服務之一進行推送通知：

* Amazon SNS
* Pushwoosh
* Adobe移動服務

*AmazonSNS* 和 *普什沃什* 配置將允許您從內部螢幕發送AEM消息。

*Adobe移動服務* 配置允許您使用Adobe Analytics帳戶從Adobe移動服務中配置和發送推送通知（但需要使用此配置集構建應用以啟用AMS推送通知）。

#### 使用AmazonSNS消息服務 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*有關AmazonSNS的資訊，以及建立新AWS帳戶的連結 [這裡](https://aws.amazon.com/sns/)。 你可以得到一年的免費帳戶。*

如果不想使用AmazonSNS，可以跳過這些步驟。

按照以下步驟設定AmazonSNS以進行推送通知：

1. **註冊到AmazonSNS**

   1. 記錄帳戶ID。 格式應為12位，不帶空格或短划線，即「123456789012」。
   1. 確保您位於「us-east」或「eu」區域，因為後續步驟（身份池建立）需要其中一個。
   1. 註冊後，登錄管理控制台並選擇 [SNS](https://console.aws.amazon.com/sns/) （推送通知服務）。 如果出現「Get Started（開始）」，請按一下。

1. **建立訪問密鑰和ID**

   1. 按一下螢幕右上角的登錄名，然後從菜單中選擇「安全身份證明」。
   1. 按一下「Access Keys（訪問密鑰）」 ，然後在下面的空格中按一下 **建立新訪問密鑰**。
   1. 按一下 **顯示訪問密鑰**，並複製和保存顯示的訪問密鑰ID和密鑰訪問密鑰。 如果選擇下載密鑰的選項，則將獲得包含相同值的csv檔案。
   1. 可以在此頁上管理其他安全相關證書以及其他證書。

   >[!NOTE]
   >
   >訪問密鑰可用於多個應用。

   對於使用「AWS沙盒」帳戶的組織，步驟非常相似，並在此處概述：

   1. 按一下螢幕右上角的登錄名，然後從菜單中選擇「我的安全憑據」。
   1. 按一下左側操作清單中的「用戶」 ，然後選擇您的用戶名。
   1. 按一下「安全憑據」頁籤。
   1. 從這裡您可以看到您的密鑰並建立新密鑰。 保存密鑰以供以後使用。


1. **建立主題**

   1. 按一下 **建立主題** 選擇主題名稱。 記錄所有欄位，如「主題ARN」、「主題所有者」、「區域」和「顯示名稱」。
   1. 按一下 **其他主題操作** > **編輯主題策略**。 下 **允許這些用戶訂閱此主題**&#x200B;選中 **各位。**
   1. 按一下 **更新策略**。

   >[!NOTE]
   >
   >您可以為不同的方案建立多個主題，如開發、test、演示等。 SNS配置的其餘部分可以保持不變。 用不同的主題構建應用；發送到該主題的推送通知將僅由與該主題一起構建的應用程式接收。

1. **建立平台應用程式**

   1. 按一下應用程式，然後按一下建立平台應用程式。 選擇一個名稱並選擇一個平台(APNS foriOS,GCM for Android)。 根據平台的不同，需要填寫以下欄位：

      1. 對於APNS，必須輸入P12檔案、密碼、證書和私鑰。 這些應該在步驟中獲得 *使用Apple推送通知服務(APNS)* 上。
      1. 對於GCM，必須輸入API密鑰。 本應在步驟中獲得 *使用Google雲消息(GCM)服務* 上。
   1. 對要支援的每個平台重複上述步驟一次。 為了能夠向iOS和Android推廣，必須建立兩個平台應用程式。


1. **建立標識池**

   1. 使用 [Cognito](https://console.aws.amazon.com/cognito) 建立標識池，該池將儲存未經身份驗證的用戶的基本資料。 請注意，目前只有「us-east」和「eu」區域受到AmazonCognito的支援。
   1. 給它一個名稱，並選中「啟用對未經身份驗證的身份的訪問」框。
   1. 在下一頁(&quot;*您的Cognito身份需要訪問您的資源*&quot;)按一下允許。
   1. 在頁面右上角，按一下連結「」*編輯標識池&quot;*。 將顯示標識池ID。 保存此文本以備以後使用。
   1. 在同一頁上，選擇「未驗證角色」旁邊的下拉框，並確保它具有Cognito_角色&lt;pool name=&quot;&quot;>已選擇UnauthRole。 保存更改。

1. **設定存取權限**

   1. 登錄到 [身份和訪問管理](https://console.aws.amazon.com/iam/home) (IAM)
   1. 選擇角色
   1. 按一下上一步建立的名為Cognito_的角色&lt;youridentitypoolname>取消驗證角色。 記錄顯示的「角色ARN」。
   1. 如果尚未開啟「內聯策略」，請開啟它。 您應該看到一個名稱類似oneClick_Cognito_的策略&lt;youridentitypoolname>Unauth_Role_1234567890123。
   1. 按一下「編輯策略」。 將策略文檔的內容替換為此JSON片段：

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{ 0}</p> <p> "版本":《2012-10-17》</p> <p> "陳述式": [</p> <p> {</p> <p> "動作": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito同步：*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS：訂閱"</p> <p> ],</p> <p> "效果":"允許",</p> <p> "資源": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. 按一下 **應用策略**


#### 使用Pushwoosh消息傳遞服務 {#using-the-pushwoosh-messaging-service}

如果不想使用Pushwoosh，可跳過此步驟。

要使用Pushwoosh:

1. **註冊到Pushwoosh**

   1. 轉到pushwoosh.com並建立新帳戶。

1. **建立API訪問令牌**

   1. 在Pushwoosh站點上，轉到「API訪問」菜單項以生成API訪問令牌。 您需要安全地記錄此內容。

1. **建立新的應用程式**

   1. 要獲得Android支援，您需要提供GCM API密鑰。
   1. 配置應用時，選擇Cordova作為框架。
   1. 要獲得iOS支援，您需要提供證書檔案(.cer)、推送證書(.p12)和私鑰密碼；這些資料應該是從Apple的APNS網站獲得的。 對於「框架」，選擇Cordova。
   1. Pushwoosh將為該應用生成一個App Id，格式為「XXXXX-XXXXX」，其中每個X都是十六進位值（0到F）。

>[!NOTE]
>
>*如果第二個應用配置了AEM相同的應用ID(和其他相關值：API訪問令牌（和GCM Id），通過第二個應用發送的任何推送通知AEM都將轉到具有該應用ID的任何其他應用。*

### 第3步：向應用添加推送支援 {#step-add-push-support-to-the-app}

#### 添加ContentSync配置 {#add-contentsync-configuration}

建立兩個名為notificationsConfig的內容節點（一個在app-config中，一個在app-config-dev中）:

* /內容/`<your app>`/shell/jcr:content/pge-app/app-config-dev/notificationsConfig
* /內容/`<your app>`/shell/jcr:content/pge-app/app-config/notificationsConfig

使用這些屬性（.content.xml檔案）:
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; xmlns:nt=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; jcr:primaryType=&quot;nt:antrobusted&quot; excludeProperties=&quot;[appAPIAccessToken]&quot;路徑=&quot;。./../../..&quot;
[targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>內容同步處理程式會查找這些節點，如果這些節點不在，則不會寫出pge-notifications-config.json檔案。

#### 添加客戶端庫 {#add-client-libraries}

必須通過以下步驟將推送通知客戶端庫添加到應用：

在CRXDE Lite:

1. 導航到 */etc/designs/phonegap//&lt;app name=&quot;&quot;>/clientlibsall。*
1. 按兩下「屬性」窗格中的嵌入節。
1. 在顯示的對話框中，按一下+按鈕添加新的客戶端庫。
1. 在新文本欄位中，添加&quot;cq.mobile.push&quot;，然後按一下「確定」。
1. 再添加一個名為cq.mobile.push.amazon，然後按一下「確定」。
1. 儲存變更。

>[!NOTE]
>
>如果出於應用程式上的空間考慮，刪除或未使用推式通知，並避免出現控制台錯誤消息，請從應用程式中刪除這些客戶端。

### 第4步：準備電話以進行測試 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*對於推送通知，您需要在實際設備上test，因為模擬器無法接收推送通知。*

#### iOS {#ios}

對於iOS，您需要使用Mac作業系統電腦，並且您需要加入 [iOS開發商計畫](https://developer.apple.com/programs/ios/)。 有些公司擁有可供所有開發商使用的公司許可證。

使用XCode 8.1，在使用「推送通知」之前，必須轉到項目中的「權能」頁籤，並切換「推送通知」開啟。

#### Android {#android}

要使用CLI在Android手機上安裝應用(請參見以下內容： **步驟6 — 構建和部署應用**)，首先必須將手機置於「開發者模式」。 請參閱 [啟用設備上開發人員選項](https://developer.android.com/tools/device.html#developer-device-options) 詳細瞭解。

### 第5步：配置推送應AEM用 {#step-configure-push-on-aem-apps}

在構建並部署到已配置的移動設備之前，必須為您決定使用的消息服務配置通知設定。

1. 為推送通知建立相應的授權組。
1. 以適AEM當用戶身份登錄，按一下「應用」頁籤。
1. 按一下應用。
1. 查找「管理Cloud Services」磁貼並按一下鉛筆，以修改雲配置。
1. 選擇「AmazonSNS連接」、「Pushwoosh連接」或「Adobe移動服務」作為通知配置。
1. 輸入提供程式屬性，然後按一下提交以保存它們，然後按一下完成。 除AMS外，在此階段未遠程驗證它們。
1. 現在，您應看到您剛在「管理Cloud Services」磁貼上輸入的配置。

### 步驟6:生成和部署應用 {#step-build-and-deploy-the-app}

**注：** 另請參閱我們的說明 [這裡](/help/mobile/building-app-mobile-phonegap.md) 構建PhoneGap應用程式。

使用PhoneGap構建和部署應用有兩種方法。

**注：** 對於推送通知測試，模擬器不能滿足要求，因為推送通知在推送提供程式(Apple或Google)和設備之間使用不同的協定。 當前的Mac/PC硬體和模擬器不支援此功能。

1. *PhoneGap Build* 是PhoneGap提供的服務，它將在您的伺服器上為您構建應用程式，並允許您直接將其下載到您的設備。 請參閱 [PhoneGap Build文檔](https://build.phonegap.com/) 學習如何設定和使用PhoneGap Build。

1. *PhoneGap命令行介面* (CLI)允許您使用命令行上的一組豐富的PhoneGap命令來構建、調試和部署應用。 請參閱 [PhoneGap開發人員文檔](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) 瞭解如何設定和使用PhoneGap CLI。

### 第7步：發送推送通知 {#step-send-a-push-notification}

要建立新通知併發送它，請執行以下步驟。

1. 建立新通知

   * 在您的AEM Mobile應用的儀表板中，查找「推送通知」磁貼。
   * 在右上角的菜單中，選擇「建立」。 請注意，在首次設定雲配置之前，此按鈕將不可用。
   * 在建立通知嚮導中，輸入標題和消息，然後按一下「建立」按鈕。 您的通知現已準備好立即或稍後發送。 可以編輯該消息和/或標題，並且可以更改和保存該消息和/或標題。

1. 發送通知

   * 在「應用」儀表板中，查找「推送通知」磁貼。
   * 選擇通知，或按一下右下角的詳細資訊按鈕(。。。)，顯示通知清單。 此清單還指示通知是否已準備好發送、是否已發送，或是否在發送過程中出錯。
   * 選中一個通知（僅）的複選框，然後按一下清單上方的「發送通知」按鈕。 您將有一次機會在顯示的對話框中「取消」或「發送」通知。

1. 處理結果

   * 如果推送通知服務(AmazonSNS或Pushwoosh)收到發送請求，確認其有效，並成功將其發送到本機提供程式（APNS和GCM），則「發送」對話框將關閉，但不顯示任何消息。 在通知清單中，該通知的狀態將列為「已發送」。
   * 如果推送發送失敗，對話框將顯示一條消息，指明問題。 在通知清單中，該通知的狀態將列為「錯誤」，但如果問題得到糾正，則可以再次發送通知。 發生錯誤時，伺服器錯誤日誌中應顯示其他錯誤資訊。
   * 請注意，iOS和Android推送通知之間存在一些平台差異。 其中：

      * 使用CLI構建應用程式將在部署到Android上後啟動。 在iOS，你必須手動啟動。 由於推送註冊步驟在啟動時進行，因此Android應用可以立即接收推送通知（因為它將已啟動並註冊），而iOS應用則不會。
      * 在Android系統上，「確定」按鈕文本位於所有大寫（以及應用程式內通知上添加的任何其他按鈕），而在iOS則不在。

對於AMS推送通知，必須從AMS伺服器合成併發送通知。 AMS提供了除AWS和Pushwoosh通知提供的通AEM知之外的其他推送通知功能。

>[!NOTE]
>
>*推送通知不能保證交付；更像是公告。 盡了最大努力確保每個人都聽到，但它們不是保證的交付機制。 此外，推車的時間可能從不到一秒到長達半小時不等。*

### 配置使用推送通知的深度連結 {#configuring-deep-linking-with-push-notifications}

什麼是深度連結？ 在推送通知的上下文中，它是一種允許應用開啟或定向（如果開啟）到應用內指定位置的方法。

它是如何工作的？ 按鍵通知的作者可選地添加按鈕標籤(即「給我看看！」) 通過可視路徑瀏覽器，選擇希望在通知中連結的頁面。 發送時，按鍵將正常，但在應用內消息中，「確定」按鈕被「取消」按鈕替換，並指定新按鈕（「顯示我！」） 的上界。 按一下新按鈕將使應用轉到應用中指定的頁面。 按一下「消除」將只消消除消息。

如果應用未開啟，陰影將顯示為正常。 對陰影中的通知執行操作將開啟應用，然後根據推送通知中配置的內容向用戶顯示深度連結按鈕。

建立通知，為可選深度連結添加按鈕文本和連結路徑：

>[!CAUTION]
>
>.要訪問儀表板中的「推送通知」磁貼，請執行以下步驟。

1. 按一下右上角的編輯 **管理Cloud Services** 平鋪。

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 選擇 **普什沃什連接**。 按一下&#x200B;**下一步**。

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. 輸入屬性的詳細資訊，然後按一下 **提交**。

   ![chlimage_1-110](assets/chlimage_1-110.png)

   提交配置後， **推送通知** 磁貼顯示在儀表板中。

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 建立通知精靈 {#create-notification-wizard}

一旦 **推送通知** 磁貼顯示在儀表板中，使用「建立通知」嚮導添加內容：

1. 按一下右上角的添加符號 **推送通知** 平鋪以開啟 **建立通知嚮導**。

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. 按一下連結路徑中的瀏覽表徵圖，向用戶顯示應用的內容結構。

   選擇路徑後，按一下「檢查」表徵圖。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >連結按鈕文本限制為20個字元。
   >
   >如果最終用戶沒有應用程式的最新版本且連結的路徑不可用，則確認深度連結的操作將使用戶進入應用程式的首頁。

1. 輸入 **文本詳細資訊** 的 **建立通知嚮導** 按一下 **建立**。

   ![chlimage_1-114](assets/chlimage_1-114.png)

   通過按一下從 **推送通知** 平鋪。

   您可以編輯屬性、發送通知或刪除通知。

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**其他資訊**:
>
>在6.4版發佈後將不支援Pushwoosh和AmazonSNS，並將作為軟體包共用的附加項提供。

### 後續步驟 {#the-next-steps}

一旦瞭解有關應用推送通知的詳細資訊，請參閱 [AEM Mobile內容個性化](/help/mobile/phonegap-aem-mobile-content-personalization.md)。
