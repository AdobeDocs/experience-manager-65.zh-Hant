---
title: 設定Adobe TargetCloud Service
description: 請依照本頁面的說明操作，瞭解如何為使用者和群組取得正確的一組許可權、建立雲端服務、為活動設定應用程式，以及最終產生內容。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 1%

---

# 設定Adobe TargetCloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>本檔案屬於 [Adobe Experience Manager (AEM) Mobile快速入門](/help/mobile/getting-started-aem-mobile.md) 指南，AEM Mobile參考的建議起點。

必須先執行數個步驟，內容作者才能開始為行動應用程式產生鎖定內容：為使用者和群組取得正確的一組許可權、建立雲端服務、為活動設定應用程式，以及最終產生內容。

未來的假設是 [AEM Mobile混合式參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 已成功透過AEM Mobile儀表板部署及存取。

## 權限 {#permissions}

需要存取個人化主控台的使用者必須屬於 `target-activity-authors` 群組。 建議將target-activity-group新增至apps-admins群組，作為使用者和群組設定的一部分。 透過新增target-activity-authors群組，這可讓使用者看到「個人化」導覽功能表專案。

若忘記將您想要存取個人化Admin Console的使用者或群組新增至target-activity-authors群組，會導致使用者無法看到個人化主控台。

## 雲端服務 {#cloud-services}

若要讓目標內容適用於行動應用程式，有兩個服務必須設定： Adobe Target服務和Adobe行動服務服務。 Adobe Target服務提供處理使用者端請求和傳回個人化內容的引擎。 Adobe行動服務會透過AMS Cordova外掛程式使用的ADBMobileConfig.json檔案，提供Adobe服務和行動應用程式之間的連線。 在AEM Mobile Dashboard中，您可以新增兩項服務來設定應用程式。

## Adobe TargetCloud Service {#adobe-target-cloud-service}

在AEM Mobile控制面板中，找出管理Cloud Service並按一下+按鈕。

![chlimage_1-8](assets/chlimage_1-8.png)

在新增Cloud Service精靈中，選取「Adobe Target」雲端服務卡並按下一步。

![chlimage_1-9](assets/chlimage_1-9.png)

從「選取組態」下拉式清單中，您可以建立組態或從現有組態中選取。 若要建立設定，請從下拉式清單中選取「建立設定」。 輸入Target設定的標題。 輸入與您的Target帳戶相關聯的使用者端代碼、電子郵件和密碼。 如果您不知道這些欄位的值，請聯絡Adobe Target支援。 按一下「驗證」按鈕以驗證認證。 確認後，按一下提交按鈕以建立雲端服務。

所建立的雲端服務會透過精靈自動關聯至行動應用程式。 在應用程式群組節點的jcr：content節點上設定cq：cloudserviceconfigs屬性值。 對於混合式應用程式範例，它會在/content/mobileapps/hybrid-reference-app/jcr：content上設定，且值指向自動產生的framework節點，它位在/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework。 框架節點預設會設定兩個屬性：性別和年齡。 此架構僅供AEM預覽使用，對裝置沒有任何影響。

完成精靈後， 「管理Cloud Service」表徵圖會包含Target雲端服務，但是它會包含有關遺失Adobe行動服務帳戶的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe行動服務 {#adobe-mobile-service}

也必須將AdobeMobile Services (AMS)帳戶連結至應用程式，AMS服務提供必要的ADBMobileConfig.json檔案（其中包含Target使用者端程式碼資訊）。 在與AMS帳戶建立關聯之前，必須由擁有AMS許可權的使用者修改AMS帳戶。

### 用戶端代碼 {#client-code}

若要登入AMS服務，請造訪 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，選取行動應用程式，然後按一下設定。 找出「SDK目標選項」欄位，並將使用者端代碼置於欄位中，然後按一下「儲存」。

![chlimage_1-11](assets/chlimage_1-11.png)

現在，使用者端代碼已與行動應用程式相關聯，當透過Adobe行動儀表板設定AMS雲端服務時，服務設定的設定將透過ADBMobileConfig.json檔案傳送。

### Adobe行動服務可提供服務 {#adobe-mobile-service-could-service}

現在已設定AMS，是時候在Adobe行動控制面板中建立行動應用程式的關聯了。 在AEM Mobile控制面板中，找出管理Cloud Service並按一下+按鈕。

![chlimage_1-12](assets/chlimage_1-12.png)

選取AdobeMobile Services卡片，然後按下一步。

![chlimage_1-13](assets/chlimage_1-13.png)

從建立或選取精靈步驟中，選取行動服務下拉式清單，然後選取建立設定專案。 提供標題、公司、使用者名稱、密碼，並選取適當的資料中心。 如果您不知道這些值，請聯絡您的Adobe Mobile Service管理員以取得這些值。 填寫完所有欄位後，按一下 **驗證**. 驗證程式會移至AMS並驗證帳戶的憑證，在成功驗證後，行動應用程式清單將會填入，您可在此處從下拉式清單中選取關聯的行動應用程式。 按一下送出按鈕以完成精靈。 此程式可能需要一點時間才能取得設定資料，以及與應用程式關聯的任何分析。 程式完成後，按一下 **完成** 從強制回應視窗返回Adobe行動控制面板。

回到行動控制面板時，「管理Cloud Service」表徵圖會包含AMS雲端服務。 此外，「分析量度」圖磚會填入生命週期報表。

![chlimage_1-14](assets/chlimage_1-14.png)

## Target內容同步處理常式 {#target-content-sync-handlers}

為了將內容傳送至使用者的裝置，內容會透過轉譯AEM內容作者建立的選件來產生。 為了處理目標選件的轉譯，有一個新的內容同步處理常式可處理選件。 使用混合參考應用程式作為範例，en （英文）內容套件包含的ContentSyncConfig具有 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 處理常式。 下一步是將選件轉譯至裝置時十分重要。 mobileappoffers處理常式具有path屬性，可識別用於應用程式的個人化活動的路徑。

例如，如果活動在 */content/campaigns/hybridref*，複製此路徑，並將其作為值貼到 *路徑* mobileappoffers處理常式的屬性。

對於混合參考應用程式，有兩個mobileappoffers處理常式，一個用於開發，另一個用於生產。

在mobileappoffers處理常式的path屬性中設定活動路徑後，請儲存處理常式。 處理常式現在已準備好開始呈現行動裝置的選件。

### 演算模式 {#render-mode}

Mobileappoffers處理常式的設定方式與發佈和開發設定不同。 對於發佈設定，有一個稱為的屬性 *轉譯模式* ，值為 *發佈* 在cq：ContentSyncConfig節點上設定。 mobileappoffers處理常式會參照renderMode，並在設為publish時編輯所建立的mbox id。 依預設，AEM建立的mbox會將 — author值附加至mbox ID。 這會識別活動尚未發佈，且應使用未發佈的行銷活動來解析優惠方案。

透過Adobe行動儀表板將內容分段時，分段內容會被視為生產就緒內容，並透過非開發內容同步設定進行轉譯。 以此方式轉譯會導致 — author從所有mbox id中移除，並預期Target伺服器上可以使用已發佈的活動。 在測試分階段內容之前，請確定活動已發佈。

## 建立內容 {#creating-content}

現在已建立雲端服務並設定mobileappoffers處理常式，內容作者就可以開始產生鎖定目標的體驗。
