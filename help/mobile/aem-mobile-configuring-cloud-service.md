---
title: 配置Adobe TargetCloud Service
seo-title: Configuring Adobe Target Cloud Service
description: 按照本頁瞭解如何為用戶和組獲取正確的權限集、建立雲服務、配置活動應用程式，以及最終生成內容。
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
ht-degree: 1%

---

# 配置Adobe TargetCloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>此文檔是 [AEM Mobile入門](/help/mobile/getting-started-aem-mobile.md) 指南，推薦的AEM Mobile參考起點。

在內容作者開始為移動應用生成目標內容之前，需要先採取許多步驟：獲取用戶和組的正確權限集、建立雲服務、配置活動應用程式，最後生成內容。

未來的假設是 [AEM Mobile混合參考應用](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 已成功部署並可通過AEM Mobile儀表板訪問。

## 權限 {#permissions}

需要訪問個性化控制台的用戶必須是 `target-activity-authors` 組。 建議在用戶和組設定中將target-activity-group添加到apps-admins組。 通過添加target-activity-authors組，用戶將能夠查看個性化導航菜單條目。

忘記將想要訪問個性化管理控制台的用戶或組添加到target-activity-authors組將阻止用戶看到個性化控制台。

## 雲端服務 {#cloud-services}

要使針對移動應用程式的目標內容工作，需要配置兩種服務：Adobe Target服務和Adobe移動服務。 Adobe Target服務提供處理客戶請求和返回個性化內容的引擎。 Adobe移動服務服務通過AMS Cordova插件使用的ADBMobileConfig.json檔案提供Adobe服務與移動應用程式之間的連接。 在AEM Mobile儀表板中，您可以通過添加兩個服務來配置應用程式。

## Adobe TargetCloud Service {#adobe-target-cloud-service}

在AEM Mobile儀表板中找到管理Cloud Services，然後按一下+按鈕。

![chlimage_1-8](assets/chlimage_1-8.png)

在「添加Cloud Service」嚮導中，選擇「Adobe Target」雲服務卡，然後按一下「下一步」。

![chlimage_1-9](assets/chlimage_1-9.png)

從「選擇配置」下拉清單中，您可以建立新配置或從現有配置中進行選擇。 要建立新配置，請從下拉清單中選擇「建立配置」。 輸入目標配置的標題。 輸入與目標帳戶關聯的客戶端代碼、電子郵件和密碼。 如果您不知道這些欄位的值，請與Adobe Target支援部門聯繫。 按一下「驗證」按鈕驗證憑據。 驗證後，按一下「提交」按鈕建立雲服務。

建立的雲服務通過嚮導自動與移動應用程式關聯。 在應用程式組節點的jcr:content節點上設定cq:cloudserviceconfigs屬性值。 對於混合應用示例，將在/content/mobileapps/hybrid-reference-app/jcr:content上設定，其值指向位於/etc/cloudservices/testandarget/adobe-target的自動生成的框架節點 — aem-apps/framework。 框架節點具有預設設定的兩個屬性：性別和年齡。 該框架僅通過預AEM覽使用，對設備沒有任何影響。

完成嚮導後，「管理Cloud Service」磁貼將包含目標雲服務，但它包含有關缺少Adobe移動服務帳戶的警告。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe移動服務 {#adobe-mobile-service}

還必須將Adobe移動服務(AMS)帳戶連結到應用程式，AMS服務提供所需的ADBMobileConfig.json檔案，其中包含目標客戶端代碼資訊。 在建立與AMS帳戶的關聯之前，AMS帳戶需要由具有AMS權限的用戶修改。

### 用戶端代碼 {#client-code}

要登錄AMS服務，請訪問 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，選擇移動應用程式，然後按一下設定。 找到「SDK目標選項」欄位，將客戶端代碼放入該欄位，然後按一下「保存」。

![chlimage_1-11](assets/chlimage_1-11.png)

既然客戶端代碼已與移動應用程式關聯，則當通過Adobe移動儀表板配置AMS雲服務時，服務設定的設定將通過ADBMobileConfig.json檔案傳遞。

### Adobe移動服務可以服務 {#adobe-mobile-service-could-service}

既然已配置AMS，現在就應該將移動應用程式關聯到Adobe移動儀表板。 在AEM Mobile儀表板中找到管理Cloud Services，然後按一下+按鈕。

![chlimage_1-12](assets/chlimage_1-12.png)

選擇Adobe移動服務卡，然後按一下「下一步」。

![chlimage_1-13](assets/chlimage_1-13.png)

在「建立」或「選擇」嚮導步驟中，選擇「移動服務」下拉清單，然後選擇「建立配置」條目。 提供標題、公司、用戶名、密碼，並選擇相應的資料中心。 如果您不知道這些值，請與Adobe移動服務管理員聯繫以獲取這些值。 填寫完所有欄位後，按一下「驗證」按鈕。 驗證過程將轉到AMS並驗證帳戶的憑據，在成功驗證後，將填充移動應用程式清單，從下拉清單中選擇關聯的移動應用程式。 按一下「提交」按鈕以完成嚮導。 該過程可能需要一段時間來獲取配置資料以及與應用程式相關的任何分析。 完成該過程後，按一下模式中的「完成」(Done)按鈕，返回Adobe移動儀表板。

返回到Mobile Dashboard時，「管理Cloud Services」磁貼將包含AMS雲服務。 您還將注意到，「分析度量」磁貼將填充生命週期報告。

![chlimage_1-14](assets/chlimage_1-14.png)

## 目標內容同步處理程式 {#target-content-sync-handlers}

通過呈現由內容作者建立的優惠來生成向用戶的設備內容傳送AEM內容。 要處理目標提供的呈現，有一個新的內容同步處理程式將處理提供。 使用混合引用應用程式作為示例，en（英語）內容包包含帶有 [移動助理](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 處理程式。 下一步對於向設備呈現優惠資訊至關重要。 mobileapporfers處理程式具有路徑屬性，該路徑屬性標識要用於應用程式的個性化活動的路徑。

例如，如果有活動位於 */內容/市場活動/混合* 複製此路徑並將其貼上為 *路徑* mobileapporfers處理程式的屬性。

對於混合引用應用程式，有兩個移動apporfers處理程式，一個用於開發，一個用於生產。

在mobileapporfers處理程式的路徑屬性中設定活動路徑後，保存處理程式。 處理程式現在將準備好開始為我們的移動設備呈現優惠。

### 呈現模式 {#render-mode}

為發佈和開發設定，移動程式處理程式的配置方式不同。 對於發佈設定，有一個名為 *renderMode* 值為 *發佈* 在cq:ContentSyncConfig節點上設定。 mobileapporffers處理程式引用renderMode，如果設定為發佈，將修改建立的mbox id。 預設情況下，由建立的框AEM的mbox id附加了 — author值。 這表明活動尚未發佈，應使用未發佈的促銷活動解決方案。

當內容通過Adobe移動控制板轉移時，轉移內容被視為生產就緒內容，並通過非開發內容同步配置來呈現。 以這種方式呈現將導致 — 作者從所有mbox id中刪除，並期望在目標伺服器上提供已發佈的活動。 在測試分段內容之前，請確保已發佈該活動。

## 建立內容 {#creating-content}

既然已建立了雲服務並配置了移動審批程式處理程式，內容作者現在就可以開始生成目標體驗。
