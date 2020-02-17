---
title: 設定Adobe Target cloud服務
seo-title: 設定Adobe Target cloud服務
description: 請依照本頁瞭解如何取得使用者和群組的適當權限集、建立雲端服務、設定活動的應用程式，以及最後產生內容。
seo-description: 請依照本頁瞭解如何取得使用者和群組的適當權限集、建立雲端服務、設定活動的應用程式，以及最後產生內容。
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定Adobe Target cloud服務 {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案是「AEM Mobile快速入門手冊」( [](/help/mobile/getting-started-aem-mobile.md) AEM Mobile參考的建議起點)的一部分。

在內容作者開始為行動應用程式產生目標內容之前，需要先整合許多步驟：您可以為使用者和群組取得適當的權限集、建立雲端服務、設定活動的應用程式，最後產生內容。

未來的假設是 [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) has been successfully deployed and accessible via the AEM Mobile Dashboard.

## 權限 {#permissions}

需要存取個人化主控台的使用者必須屬於群組的一 `target-activity-authors` 部分。 建議在使用者和群組設定中，將target-activity-group新增至應用程式管理員群組。 新增target-activity-authors群組，可讓使用者查看個人化導覽功能表項目。

忘記將您想要擁有個人化管理控制台存取權的使用者或群組新增至target-activity-authors群組，將會防止使用者看到個人化主控台。

## 雲端服務 {#cloud-services}

若要讓針對行動應用程式的目標內容運作，需要設定兩項服務：Adobe Target服務和Adobe Mobile services服務。 Adobe Target服務提供處理用戶端要求及傳回個人化內容的引擎。 Adobe Mobile services服務透過ADBMobileConfig.json檔案（由AMS Cordova增效模組使用）提供Adobe服務與行動應用程式之間的連線。 從AEM Mobile Dashboard，您可以新增兩個服務來設定您的應用程式。

## Adobe Target cloud服務 {#adobe-target-cloud-service}

從AEM Mobile Dashboard找到「管理雲端服務」，然後按一下+按鈕。

![chlimage_1-8](assets/chlimage_1-8.png)

從「新增雲端服務」精靈中，選取「Adobe Target」雲端服務卡，然後按「下一步」。

![chlimage_1-9](assets/chlimage_1-9.png)

從「選擇配置」下拉式清單中，您可以建立新的配置或從現有的配置中選擇。 要建立新配置，請從下拉清單中選擇「建立配置」。 輸入Target設定的標題。 輸入您的客戶代碼、電子郵件和密碼，這些程式碼與您的Target帳戶相關聯。 如果您不知道這些欄位的值，請連絡Adobe Target支援。 按一下「驗證」按鈕以驗證憑據。 在驗證後，按一下「提交」按鈕以建立雲端服務。

建立的雲端服務會透過精靈自動與行動應用程式關聯。 cq:cloudserviceconfiges屬性值會設定在應用程式群組節點的jcr:content節點上。 對於混合應用程式範例，它會設定在/content/mobileapps/hybrid-reference-app/jcr:content上，其值指向位於/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework的自動產生的架構節點。 框架節點預設設定兩個屬性，性別和年齡。 此架構僅供AEM預覽使用，對裝置沒有任何影響。

精靈完成後，「管理雲端服務」方塊將包含Target雲端服務，但包含有關遺失Adobe Mobile服務帳戶的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

AMS服務也必須將Adobe Mobile Services(AMS)帳戶連結至應用程式，提供必要的ADBMobileConfig.json檔案，其中包含Target用戶端程式碼資訊。 在建立與AMS帳戶的關聯之前，AMS帳戶需要由具有AMS權限的使用者修改。

### 用戶端代碼 {#client-code}

若要登入AMS服務，請造 [訪https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，選取行動應用程式，然後按一下設定。 找到「SDK目標選項」欄位，並將用戶端程式碼放入欄位中，然後按一下「儲存」。

![chlimage_1-11](assets/chlimage_1-11.png)

現在用戶端程式碼已與行動應用程式關聯，當透過Adobe Mobile Dashboard設定AMS雲端服務時，服務設定的設定將會透過ADBMobileConfig.json檔案傳送。

### Adobe Mobile Service Could Service {#adobe-mobile-service-could-service}

現在已設定AMS，是時候在Adobe Mobile Dashboard中建立行動應用程式的關聯了。 從AEM Mobile Dashboard找到「管理雲端服務」，然後按一下+按鈕。

![chlimage_1-12](assets/chlimage_1-12.png)

選取Adobe Mobile services卡，然後按一下「下一步」。

![chlimage_1-13](assets/chlimage_1-13.png)

從「建立」或「選取」精靈步驟中，選取「Mobile Service」下拉式清單，並選取「建立設定」項目。 提供標題、公司、使用者名稱、密碼，並選取適當的資料中心。 如果您不知道這些值，請連絡您的Adobe Mobile服務管理員以取得這些值。 填寫完所有欄位後，按一下「驗證」按鈕。 驗證程式會移至AMS並驗證帳戶的憑證，一旦成功驗證，就會填入行動應用程式清單，您可從下拉式清單中選取關聯的行動應用程式。 按一下「提交」按鈕以完成嚮導。 此程式可能需要一些時間才能取得設定資料以及與應用程式相關的任何分析。 完成程式後，按一下模型中的「完成」按鈕，返回Adobe Mobile Dashboard。

「管理雲端服務」圖格會返回Mobile Dashboard，其中包含AMS雲端服務。 您也會注意到，「分析量度」方塊將會填入生命週期報表。

![chlimage_1-14](assets/chlimage_1-14.png)

## 目標內容同步處理常式 {#target-content-sync-handlers}

若要將內容傳送至使用者的裝置內容，請轉譯由AEM內容作者建立的選件。 若要處理目標選件的轉譯，有新的內容同步處理常式會處理選件。 以Hybrid Reference Application為範例，en（英文）內容套件包含ContentSyncConfig和 [mobileapporfers處理常式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 。 下一步是向裝置轉譯選件的關鍵。 Mobileapporfers處理常式具有path屬性，可識別要用於應用程式的個人化活動路徑。

例如，如果有位於 */content/campaigns/hybridref的活動複製此路徑，並將其貼為值至mobileapporfers處理常式的*** path屬性。

對於混合參考應用程式，有兩個mobileapporfer處理常式，一個用於開發，另一個用於製作。

在mobileapporfers處理常式的path屬性中設定活動路徑後，會儲存處理常式。 處理常式現在已準備好開始轉換我們行動裝置的選件。

### 演算模式 {#render-mode}

Mobileapporfers處理常式的設定與發佈和開發設定不同。 對於發佈設定，有一個名 *為renderMode* 的屬性，其值 ** 在cq:ContentSyncConfig節點上設定。 Mobileapporfers處理常式會參考renderMode，如果設為publish，則會修改建立的mbox ID。 依預設，由AEM建立的mbox會在mbox ID中附加一個—author值。 這可識別活動尚未發佈，且應使用未發佈的促銷活動來解決選件。

當內容透過Adobe Mobile Dashboard進行轉移時，轉移內容會被視為生產就緒內容，並會透過非開發內容同步設定轉譯。 以此方式呈現會導致-author從所有mbox ID中移除，並預期Target伺服器上會有已發佈的活動。 測試分段內容之前，請確定活動已發佈。

## 建立內容 {#creating-content}

現在，已建立雲端服務並設定mobileapporfers處理常式，內容作者現在可以開始產生目標體驗。
