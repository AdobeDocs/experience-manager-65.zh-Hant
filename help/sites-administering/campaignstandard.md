---
title: 與Adobe Campaign Standard整合
seo-title: Integrating with Adobe Campaign Standard
description: 學習如何與AEMAdobe Campaign Standard融合。
seo-description: Learn how to integrate AEM with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: a0062ffbdd6477eca494fea4142d271f3015599a
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 0%

---


# 與Adobe Campaign Standard整合 {#integrating-with-adobe-campaign-standard}

通過與AEMAdobe Campaign整合，您可以直接在中管理電子郵件傳遞、內容和表AEM單。 在Adobe Campaign Standard和都需AEM要配置步驟，以便實現解決方案之間的雙向通信。

這一整合AEM使Adobe Campaign Standard能夠獨立使用。 營銷人員可以在Adobe Campaign建立活動和使用目標，而內容建立者可以在中進行內容設AEM計。 通過整合，Adobe Campaign可以定向和提供在中創AEM建的活動的內容和設計。

## 整合步驟 {#integration-steps}

配置與Adobe Campaign Standard之間AEM的整合需要在兩個解決方案中執行若干步驟。

1. [配置 ](#aemserver-user)
1. [驗證 ](#resource-type-filter)
1. [在市場活AEM動中建立特定電子郵件傳遞模板](#aem-email-delivery-template)
1. [在中配置市場活動集AEM成](#campaign-integration)
1. [配置到AEM發佈實例的複製](#replication)
1. [配置外部AEM化器](#externalizer)
1. [配置 ](#campaign-remote-user)
1. [在市場活AEM動中配置外部帳戶](#acc-external-user)

本文檔將詳細引導您完成這些步驟中的每一個。

## 必備條件 {#prerequisites}

* 管理員對Adobe Campaign Standard的訪問
   * 如果您需要有關如何設定和配置Adobe Campaign Standard的其他詳細資訊，請參閱 [Adobe Campaign Standard檔案。](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* 管理員訪問權AEM限

## 在市場活動中配置Aemserver用戶 {#aemserver-user}

Adobe Campaign Standard預設 `aemserver` 用於連AEM接到Adobe Campaign的用戶。 您必須為此用戶分配適當的安全組並設定其密碼。

1. 以管理員身份登錄Adobe Campaign。

1. 點擊或按一下菜單欄左上角的Adobe Campaign徽標以開啟全局導航，然後選擇 **管理** > **用戶和安全** > **用戶** 的子菜單。

1. 點擊或按一下 `aemserver` 用戶。

1. 確保 `aemserver` 用戶至少被分配給具有角色的安全組 `deliveryPrepare` 分配給它。 預設情況下，組 `Standard Users` 有這個角色。

   ![Adobe Campaignaemserver用戶](assets/acs-aemserver-user.png)

1. 點擊或按一下 **保存** 的子菜單。

您 `aemserver` 用戶現在具有必要的權限，AEM以便使用它與Adobe Campaign通信。

但是，在AEM使用 `aemserver` 用戶，必須設定其密碼。 這不能通過Adobe Campaign。 必須由Adobe支援工程師執行。 [請向Adobe客戶服務部提交票證](https://experienceleague.adobe.com/?support-tab=home#support) 請求重置 `aemserver` 密碼。 一旦您獲得了Adobe客戶服務部的密碼，請將其保留在安全位置。

## 驗證市場活動中的AEMResourceTypeFilter {#resource-type-filter}

的 `AEMResourceTypeFilter` 是Adobe Campaign的一個選項，用於過濾AEM可在Adobe Campaign使用的資源。 由AEM於包含大量內容，此選項充當過濾器，使Adobe Campaign只能檢索專AEM門設計用於Adobe Campaign的類型的內容。

此選項已預配置。 但是，如果您已自定義了的市場活動元件，則可能需要更新AEM它。 驗證 `AEMResourceTypeFilter` 選項已配置，請執行以下步驟。

1. 以管理員身份登錄Adobe Campaign。

1. 點擊或按一下菜單欄左上角的Adobe Campaign徽標以開啟全局導航，然後選擇 **管理** > **應用程式設定** > **選項** 的子菜單。

1. 點擊或按一下 `AEMResourceTypeFilter` 的子菜單。

1. 確認 `AEMResourceTypeFilter`。 路徑用逗號分隔，預設情況下包含：

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 點擊或按一下 **保存** 的子菜單。

您 `AEMResourceTypeFilter` 現在已配置為從中檢索正確的內AEM容。

## 在市場活AEM動中建立特定電子郵件傳遞模板 {#aem-email-delivery-template}

預設情況下，AEM在Adobe Campaign的電子郵件模板中未啟用。 必須配置新的電子郵件傳遞模板，該模板可用於使用內容創AEM建電子郵件。 要建立特AEM定的電子郵件傳遞模板，請執行以下步驟。

1. 以管理員身份登錄Adobe Campaign。

1. 點擊或按一下菜單欄左上角的Adobe Campaign徽標以開啟全局導航，然後選擇 **資源** > **模板** > **交貨模板** 的子菜單。

1. 在傳遞模板控制台中，找到預設的電子郵件模板 **通過電子郵件（郵件）發送** 將滑鼠懸停在代表它的卡（或行）上，以顯示選項。 按一下 **重複元素**。

   ![重複元素](assets/acs-copy-template.png)

1. 在 **確認** 對話框，按一下 **確認** 複製模板。

   ![確認對話框](assets/acs-confirmation.png)

1. 將開啟模板編輯器，其副本 **通過電子郵件（郵件）發送** 的下界。 按一下 **編輯屬性** 的上界。

   ![範本編輯器](assets/acs-template-editor.png)

1. 在「屬性」窗口中，更改 **標籤** 欄位，以描述新模AEM板。

1. 按一下 **內容** 標題展開並選擇 **Adobe Experience Manager** 的 **內容源** 下拉。

1. 這揭示了 **Adobe Experience Manager帳戶** 的子菜單。 使用下拉框選擇 **Adobe Experience Manager實例(aemInstance)** 。 這是整合的預設外部AEM用戶。

![配置模板屬性](assets/acs-template-properties.png)

1. 按一下 **確認** 的子菜單。

1. 在模板編輯器中，按一下 **保存** 保存修改後的電子郵件模板副本，以便與一AEM起使用。

您現在擁有一個可使用內容的電子郵件AEM模板。

## 在中配置市場活動集AEM成 {#campaign-integration}

與AEMAdobe Campaign通信時， `aemserver` 您在Adobe Campaign配置的用戶。 按照以下步驟配置此整合。

1. 以管理員身AEM份登錄到創作實例。

1. 從全局導航側欄中，選擇 **工具** > **Cloud Services** > **舊Cloud Services** > **Adobe Campaign**，然後按一下 **立即配置**。

   ![配置Adobe Campaign](assets/configure-campaign-service.png)

1. 在對話框中，通過輸入 **標題** 按一下 **建立**。

   ![「配置市場活動」對話框](assets/configure-campaign-dialog.png)

1. 將開啟一個新窗口和對話框以編輯配置。 提供必要的資訊。

   * **用戶名**  — 這是 [這樣 `aemserver` 在上一步中配置的Adobe Campaign用戶。](#aemserver-user) 預設情況下， `aemserver`。
   * **密碼**  — 這是 [這樣 `aemserver` 用戶，您在上一步中向「Adobe客戶服務」請求。](#aemserver-user)
   * **API端點**  — 這是Adobe Campaign實例URL。

   ![配置Adobe CampaignAEM](assets/configure-campaign.png)

1. 選擇 **連接到Adobe Campaign** 驗證連接，然後按一下 **確定**。

現AEM在可以和Adobe Campaign通信。

>[!NOTE]
>
>確保通過Internet訪問您的Adobe Campaign伺服器。 無法AEM訪問專用網路。

## 配置到AEM發佈實例的複製 {#replication}

市場活動內容由創作實例上的內容作者AEM建立。 此實例通常僅在組織內部可用。 對於要讓活動的收件人能夠訪問的內容（如影像和資產），您需要發佈該內容。

複製代理負責將您的內容從作者實AEM例發佈到發佈實例，必須設定該代理才能使整合正常工作。 此步驟對於將某些創作實例配置複製到發佈實例中也是必要的。

要配置從作者實AEM例到發佈實例的複製：

1. 以管理員身AEM份登錄到創作實例。

1. 從全局導航側欄中，選擇 **工具** > **部署** > **複製** > **作者代理**，然後按一下 **預設代理（發佈）**。

   ![配置複製代理](assets/acc-replication-config.png)

1. 點擊或按一下 **編輯** 選擇 **運輸** 頁籤。

1. 配置 **URI** 欄位 `localhost` 具有發佈實例的IP地AEM址的值。

   ![「傳輸」頁籤](assets/acc-transport-tab.png)

1. 點擊或按一下 **確定** 以保存對代理設定所做的更改。

您已配置到發佈實例AEM的複製，以便您的市場活動收件人可以訪問您的內容。

>[!NOTE]
>
>如果不想使用複製URL，而是使用面向公共的URL，則可以通過OSGi在以下配置設定中設定公共URL
>
>從全局導航側欄中，選擇 **工具** > **操作** > **Web控制台** > **OSGi配置** 並搜索 **市場活AEM動整合 — 配置**。 編輯配置並更改欄位 **公共URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 配置外部AEM化器 {#externalizer}

[外部化器](/help/sites-developing/externalizer.md) 是一種OSGi服務，AEM它將資源路徑轉換為外部和絕對URL，這是為市場活動可以使AEM用的內容提供服務所必需的。 您必須將其配置為「市場活動」整合才能正常工作。

1. 以管理員身AEM份登錄到創作實例。
1. 從全局導航側欄中，選擇 **工具** > **操作** > **Web控制台** > **OSGi配置** 並搜索 **第CQ天連結外部化程式**。
1. 預設情況下， **域** 欄位用於發佈實例。 更改預設URL `http://localhost:4503` 發佈實例。

   ![配置外部化程式](assets/acc-externalizer-config.png)

1. 點選或按一下&#x200B;**儲存**。

您已配置外部化程式，Adobe Campaign現在可以訪問您的內容。

>[!NOTE]
必須可以從Adobe Campaign伺服器訪問發佈實例。 如果它指向 `localhost:4503` 或者Adobe Campaign無法訪問的另一台伺服器，AEM來自Adobe Campaign的映像將不會顯示。

## 在中配置市場活動遠程用AEM戶 {#campaign-remote-user}

正如您需要Adobe Campaign的用戶AEM可以與Adobe Campaign通信一樣，Adobe Campaign也需要用AEM戶與通AEM信。 預設情況下，市場活動整合將建立 `campaign-remote` 中AEM。 按照以下步驟配置此用戶。

1. 以管理AEM員身份登錄。
1. 在主導航控制台上，按一下 **工具** 左欄。
1. 然後按一下 **安全** > **用戶** 開啟用戶管理控制台。
1. 查找 `campaign-remote` 。
1. 選擇 `campaign-remote` 按一下 **屬性** 編輯
1. 在 **編輯用戶設定** 窗口，按一下 **更改密碼**。
1. 為用戶提供新密碼，並在安全位置記錄該密碼以供將來使用。
1. 按一下 **保存** 的子菜單。
1. 按一下 **保存並關閉** 以保存對 `campaign-remote` 。

## 在市場活AEM動中配置外部帳戶 {#acc-external-user}

當你 [建立了AEM特定的電子郵件傳遞模板，](#aem-email-delivery-template) 指定模板應使用 `aemInstance` 與外部帳戶通AEM信。 為了在兩個解決方案之間實現雙向通信，您需要在Adobe Campaign配置此帳戶。

1. 以管理員身份登錄Adobe Campaign。

1. 點擊或按一下菜單欄左上角的Adobe Campaign徽標以開啟全局導航，然後選擇 **管理** > **應用程式設定** > **外部帳戶** 的子菜單。

1. 點擊或按一下 **Adobe Experience Manager實例(aemInstance)** 用戶。

1. 確保用戶 **Adobe Experience Manager** 的 **類型**。

1. 在 **連接** 中定義以下欄位：

   1. 伺服器：這是您的創作服AEM務器的URL。 這不應該以斜槓結尾。
   1. 帳戶：這是 `campaign-remote` 用戶 [以前在中配AEM置。](#campaign-remote-user)
   1. 密碼：這是 `campaign-remote`用戶 [以前在中配AEM置。](#campaign-remote-user)

   ![編輯aemInstance用戶](assets/acs-external-acount-editor.png)

1. 確保 **已啟用** 複選框，然後按一下 **保存** 的子菜單。

恭喜！您已完成與Adobe Campaign StandardAEM的整合！

## 後續步驟 {#next-steps}

通過Adobe Campaign Classic和配AEM置，整合現已完成。

您現在可以繼續學習如何在Adobe Experience Manager建立新聞簡報 [。](/help/sites-authoring/campaign.md)
