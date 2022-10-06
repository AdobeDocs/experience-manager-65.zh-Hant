---
title: 設定Adobe TargetCloud Service
seo-title: Configuring Adobe Target Cloud Service
description: 請依照本頁面了解如何為使用者和群組取得正確的權限集、建立雲端服務、設定活動的應用程式，以及最後產生內容。
seo-description: Follow this page to understand how to get right set of permissions for users and groups, creating cloud services, configuring the application for the activity, and finally generating the content.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# 設定Adobe TargetCloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案是 [開始使用AEM Mobile](/help/mobile/getting-started-aem-mobile.md) 指南，此為AEM Mobile參考的建議起點。

內容作者必須先完成許多步驟，才能開始為行動應用程式產生目標式內容：為使用者和群組取得正確的權限集、建立雲端服務、設定活動的應用程式，最後產生內容。

未來的假設是 [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 已成功部署，並可透過AEM Mobile控制面板存取。

## 權限 {#permissions}

需要存取個人化控制台的使用者必須屬於 `target-activity-authors` 群組。 建議在使用者和群組設定中，將target-activity-group新增至apps-admins群組。 借由新增target-activity-authors群組，使用者將能查看個人化導覽功能表項目。

忘記將您想要擁有個人化管理控制台存取權的使用者或群組新增至target-activity-authors群組，將會讓使用者看不到個人化主控台。

## 雲端服務 {#cloud-services}

若要讓目標內容適用於行動應用程式，需要設定兩項服務：Adobe Target服務與AdobeMobile Services服務。 Adobe Target服務提供處理用戶端請求及傳回個人化內容的引擎。 AdobeMobile Services服務透過ADBMobileConfig.json檔案（由AMS Cordova外掛程式使用）提供Adobe服務與行動應用程式之間的連線。 從AEM Mobile控制面板，您可以新增兩個服務來設定應用程式。

## Adobe TargetCloud Service {#adobe-target-cloud-service}

在AEM Mobile控制面板中找出管理Cloud Services，然後按一下+按鈕。

![chlimage_1-8](assets/chlimage_1-8.png)

從「新增Cloud Service」精靈中選取「Adobe Target」雲端服務卡，然後按一下「下一步」。

![chlimage_1-9](assets/chlimage_1-9.png)

從「選取設定」下拉式清單中，您可以建立新設定或從現有設定中選取。 要建立新配置，請從下拉式清單中選擇「建立配置」。 輸入Target設定的標題。 輸入與您的Target帳戶相關聯的用戶端代碼、電子郵件和密碼。 如果您不知道這些欄位的值，請聯絡Adobe Target支援。 按一下「驗證」按鈕以驗證憑證。 驗證後，按一下提交按鈕以建立雲端服務。

建立的雲端服務會透過精靈自動與行動應用程式相關聯。 在應用程式群組節點的jcr:content節點上設定cq:cloudserviceconfigs屬性值。 對於混合式應用程式範例，會在/content/mobileapps/hybrid-reference-app/jcr:content上設定，值指向位於/etc/cloudservices/testandtarget/adobe-target的自動產生的架構節點 — aem-apps/framework。 框架節點預設設定了兩個屬性，即性別和年齡。 框架僅用於AEM預覽，對裝置沒有任何影響。

精靈完成後，「管理Cloud Service」方塊將包含Target雲端服務，但包含有關遺失AdobeMobile Service帳戶的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe行動服務 {#adobe-mobile-service}

您也必須將AdobeMobile Services(AMS)帳戶連結至應用程式，AMS服務會提供必要的ADBMobileConfig.json檔案，其中包含Target用戶端代碼資訊。 在建立與AMS帳戶的關聯之前，AMS帳戶必須由具有AMS權限的使用者修改。

### 用戶端代碼 {#client-code}

若要登入AMS服務，請造訪 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，請選取行動應用程式並按一下設定。 找出「SDK目標選項」欄位，並將用戶端代碼放入欄位中，然後按一下「儲存」。

![chlimage_1-11](assets/chlimage_1-11.png)

現在用戶端代碼已與行動應用程式相關聯，透過Adobe行動控制面板設定AMS雲端服務時，服務設定的設定將透過ADBMobileConfig.json檔案傳送。

### Adobe行動服務可能提供服務 {#adobe-mobile-service-could-service}

現在AMS已設定完畢，您可以在Adobe行動控制面板中建立行動應用程式的關聯。 在AEM Mobile控制面板中找出管理Cloud Services，然後按一下+按鈕。

![chlimage_1-12](assets/chlimage_1-12.png)

選取「AdobeMobile Services」卡片，然後按一下「下一步」。

![chlimage_1-13](assets/chlimage_1-13.png)

在建立或選取精靈步驟中，選取Mobile Service下拉式清單，然後選取建立設定項目。 提供標題、公司、使用者名稱、密碼，並選取適當的資料中心。 如果您不知道這些值，請連絡您的AdobeMobile Service管理員以取得。 填寫完所有欄位後，按一下「驗證」按鈕。 驗證程式會前往AMS並驗證帳戶的憑證，一旦成功驗證，便會填入行動應用程式清單，您可在此從下拉式清單中選取相關聯的行動應用程式。 按一下「提交」按鈕以完成精靈。 該過程可能需要一些時間來獲取配置資料以及與應用程式的任何關聯分析。 程式完成後，按一下強制回應視窗中的「完成」按鈕，返回「Adobe行動控制面板」。

返回Mobile Dashboard時，「管理Cloud Services」方塊將會包含AMS雲端服務。 您也會注意，「分析量度」方塊將會填入生命週期報表。

![chlimage_1-14](assets/chlimage_1-14.png)

## 目標內容同步處理常式 {#target-content-sync-handlers}

若要傳送內容至使用者的裝置內容，需透過轉譯由AEM內容作者建立的選件來產生。 若要處理target選件的轉譯，有一個新的內容同步處理常式將處理選件。 以混合參考應用程式為範例，en（英文）內容套件包含ContentSyncConfig，並搭配 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 處理常式。 下一個步驟對於向裝置轉譯選件至關重要。 Mobileappoffers處理常式具有path屬性，可識別要用於應用程式的個人化活動的路徑。

例如，如果有位於 */content/campaigns/hybridref* 複製此路徑並貼上為 *路徑* mobileappoffers處理常式的屬性。

對於混合引用應用程式，有兩個mobileappoffer處理程式，一個用於開發，一個用於生產。

在Mobileappoffers處理常式的path屬性中設定活動路徑後，會儲存處理常式。 處理常式現在已準備好開始為行動裝置呈現選件。

### 呈現模式 {#render-mode}

針對發佈和開發設定，Mobileappoffers處理常式的設定不同。 若為發佈設定，有一個屬性稱為 *renderMode* 值為 *發佈* 在cq:ContentSyncConfig節點上設定。 mobileappoffers處理常式會參考renderMode，如果設為publish，則會修改所建立的mbox id。 依預設，由AEM建立的mbox會在mbox id上附加一個 — 作者值。 這可識別活動尚未發佈，應將取消發佈的促銷活動用於優惠方案解決方案。

透過「Adobe行動控制面板」存放內容時，存放內容會視為生產就緒內容，並透過非開發內容同步設定呈現。 以此方式呈現會導致：作者從所有mbox ID中移除，且預期已發佈的活動可在Target伺服器上使用。 測試分段內容之前，請確定活動已發佈。

## 建立內容 {#creating-content}

現在，雲端服務已建立，且mobileappoffers處理常式已設定完畢，內容作者就可以開始產生鎖定的體驗。
