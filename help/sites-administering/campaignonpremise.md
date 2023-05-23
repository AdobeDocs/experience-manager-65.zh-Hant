---
title: 與Adobe Campaign Classic整合
seo-title: Integrating with Adobe Campaign Classic
description: 瞭解如何與AEMAdobe Campaign Classic整合
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: 4712f57808ae769646b00d1098648686815121b6
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---


# 與Adobe Campaign Classic整合 {#integrating-campaign-classic}

通過與AEMAdobe Campaign整合，您可以直接在中管理電子郵件傳遞、內容和表AEM單。 在Adobe Campaign Classic和都需AEM要配置步驟，以便實現解決方案之間的雙向通信。

這一整合AEM使Adobe Campaign Classic能夠獨立使用。 營銷人員可以在Adobe Campaign建立活動和使用目標，而內容建立者可以在中進行內容設AEM計。 通過整合，Adobe Campaign可以定向和提供在中創AEM建的活動的內容和設計。

## 整合步驟 {#integration-steps}

整合AEM和市場活動需要在兩個解決方案中執行若干步驟。

1. [在市場活AEM動中安裝整合包。](#install-package)
1. [在市場活動中創AEM建運算子](#create-operator)
1. [在中配置市場活動集AEM成](#campaign-integration)
1. [配置外部AEM化器](#externalizer)
1. [在中配置市場活動遠程用AEM戶](#configure-user)
1. [在市場活AEM動中配置外部帳戶](#acc-setup)

本文檔將詳細引導您完成這些步驟中的每一個。

## 必備條件 {#prerequisites}

* 管理員對Adobe Campaign Classic的訪問
   * 要執行整合，您需要一個工作的Adobe Campaign Classic實例，包括一個已配置的資料庫。
   * 如果您需要有關如何設定和配置Adobe Campaign Classic的其他詳細資訊，請參閱 [Adobe Campaign Classic檔案，](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html) 尤其是《安裝及設定指南》。
* 管理員訪問權AEM限

## 在市場活AEM動中安裝整合包 {#install-package}

的 **集AEM成** Adobe Campaign的軟體包包括連接到的許多標準配AEM置。

1. 作為管理員，使用客戶端控制台登錄Adobe Campaign實例。

1. 選擇 **工具** > **高級** > **導入包……**。

   ![導入包](assets/import-package.png)

1. 按一下 **安裝標準軟體包** 然後按一下 **下一個**。

1. 檢查 **集AEM成** 檔案。

   ![安裝標準軟體包](assets/select-package.png)

1. 按一下 **下一個**，然後 **開始** 開始安裝。

   ![安裝進度](assets/installation.png)

1. 按一下 **關閉** 安裝完成時。

現在已安裝整合包。

## 在市場活動中創AEM建運算子 {#create-operator}

整合包將自動建立 `aemserver` 用於連AEM接Adobe Campaign的運算子。 必須為此運算子定義安全區域並設定其密碼。

1. 使用客戶端控制台以管理員身份登錄Adobe Campaign。

1. 選擇 **工具** -> **瀏覽器** 的上界。

1. 在瀏覽器中，導航到 **管理** > **訪問管理** > **運算子** 的下界。

1. 選擇 `aemserver` 運算子。

1. 在 **編輯** 的子菜單。 **訪問權限** 頁籤，然後按一下 **編輯訪問參數……** 的子菜單。

   ![設定安全區域](assets/access-rights.png)

1. 選擇適當的安全區域，並根據需要定義受信任的IP掩碼。

1. 按一下「**儲存**」。

1. 從Adobe Campaign客戶端註銷。

1. 在Adobe Campaign伺服器的檔案系統上，導航到市場活動安裝位置並編輯 `serverConf.xml` 檔案。 此檔案通常位於：
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` 的子菜單。
   * `/usr/local/neolane/nl6/conf/eng` 在Linux中。

1. 搜索 `securityZone` 並確保為操作員的安全區域設定以下AEM參數。

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`。

1. 儲存檔案。

1. 確保安全區域不會被 `config-<server name>.xml` 的子菜單。

   * 如果配置檔案包含單獨的安全區域設定，則更改 `allowUserPassword` 屬性 `true`。

1. 如果要更改Adobe Campaign Classic伺服器埠，請替換 `8080` 和所需埠。

   >[!CAUTION]
   >
   >預設情況下，沒有為操作員配置安全區域。 要連AEM接到Adobe Campaign，必須選擇前面步驟中詳細說明的區域。
   >
   >Adobe強烈建議建立專用於避AEM免任何安全問題的安全區。 有關此主題的詳細資訊，請參閱 [Adobe Campaign Classic檔案。](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. 在市場活動客戶端中，返回 `aemserver` 運算子，然後選擇 **常規** 頁籤。

1. 按一下 **重置密碼……** 的子菜單。

1. 指定密碼並將其儲存在安全位置以備將來使用。

1. 按一下 **確定** 為 `aemserver` 運算子。

## 在中配置市場活動集AEM成 {#campaign-integration}

AEM使用 [已在市場活動中設定的操作員](#create-operator) 以便與市場活動溝通

1. 以管理員身AEM份登錄到創作實例。

1. 從全局導航側欄中，選擇 **工具** > **Cloud Services** > **舊Cloud Services** > **Adobe Campaign**，然後按一下 **立即配置**。

   ![配置Adobe Campaign](assets/configure-campaign-service.png)

1. 在對話框中，通過輸入 **標題** 按一下 **建立**。

   ![「配置市場活動」對話框](assets/configure-campaign-dialog.png)

1. 將開啟一個新窗口和對話框以編輯配置。 提供必要的資訊。

   * **用戶名**  — 這是 [在上AEM一步中建立的Adobe Campaign整合包運算子。](#create-operator) 預設情況下， `aemserver`。
   * **密碼**  — 這是 [在上AEM一步中建立的Adobe Campaign整合包運算子。](#create-operator)
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

[外部化器](/help/sites-developing/externalizer.md) 是一種OSGi服務，AEM它將資源路徑轉換為外部和絕對URL，這是為市場活動可以使AEM用的內容提供服務所必需的。 您必須配置它，使市場活動整合工作。

1. 以管理員身AEM份登錄到創作實例。
1. 從全局導航側欄中，選擇 **工具** > **操作** > **Web控制台** > **OSGi配置** 並搜索 **第CQ天連結外部化程式**。
1. 預設情況下， **域** 欄位用於發佈實例。 更改預設URL `http://localhost:4503` 發佈實例。

   ![配置外部化程式](assets/acc-externalizer-config.png)

1. 點選或按一下&#x200B;**儲存**。

您已配置外部化程式，Adobe Campaign現在可以訪問您的內容。

>[!NOTE]
必須可以從Adobe Campaign伺服器訪問發佈實例。 如果它指向 `localhost:4503` 或者Adobe Campaign無法訪問的另一台伺服器，AEM來自Adobe Campaign的映像將不會顯示。

## 在中配置市場活動遠程用AEM戶 {#configure-user}

為了與市場活動AEM通信，您需要為 `campaign-remote` 中AEM。

1. 以管理AEM員身份登錄。
1. 在主導航控制台上，按一下 **工具** 左欄。
1. 然後按一下 **安全** -> **用戶** 開啟用戶管理控制台。
1. 查找 `campaign-remote` 。
1. 選擇 `campaign-remote` 按一下 **屬性** 編輯
1. 在 **編輯用戶設定** 窗口，按一下 **更改密碼**。
1. 為用戶提供新密碼，並在安全位置記錄該密碼以供將來使用。
1. 按一下 **保存** 的子菜單。
1. 按一下 **保存並關閉** 以保存對 `campaign-remote` 。

## 在市場活AEM動中配置外部帳戶 {#acc-setup}

當 [安裝 **集AEM成** 在市場活動中，](#install-package) 為建立外部帳戶AEM。 通過配置此外部帳戶，Adobe Campaign可AEM以連接到，從而實現解決方案之間的雙向通信。

1. 使用客戶端控制台以管理員身份登錄Adobe Campaign。

1. 選擇 **工具** -> **瀏覽器** 的上界。

1. 在瀏覽器中，導航到 **管理** > **平台** > **外部帳戶** 的下界。

   ![外部帳戶](assets/external-accounts.png)

1. 找到外部AEM帳戶。 預設情況下，它具有以下值：

   * **類型** - `AEM`
   * **標籤** - `AEM Instance`
   * **內部名稱** - `aemInstance`

1. 在 **常規** 的子菜單，輸入在 [設定市場活動遠程用戶密碼](#set-campaign-remote-password) 的子菜單。

   * **伺服器**  — 作者服AEM務器地址
      * 必須AEM從Adobe Campaign Classic伺服器實例訪問作者伺服器。
      * 確保伺服器地址確實 **不** 以尾斜線結尾。
   * **帳戶**  — 預設情況下， `campaign-remote` 在中設定AEM的用戶 [設定市場活動遠程用戶密碼](#set-campaign-remote-password) 的子菜單。
   * **密碼**  — 此密碼與 `campaign-remote` 在中設定AEM的用戶 [設定市場活動遠程用戶密碼](#set-campaign-remote-password) 的子菜單。

1. 選擇 **已啟用** 複選框。

1. 按一下「**儲存**」。

Adobe Campaign現在可以和AEM他溝通

## 後續步驟 {#next-steps}

通過Adobe Campaign Classic和配AEM置，整合現已完成。

您現在可以繼續學習如何在Adobe Experience Manager建立新聞簡報 [。](/help/sites-authoring/campaign.md)
