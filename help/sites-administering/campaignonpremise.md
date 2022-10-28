---
title: 與Adobe Campaign Classic整合
seo-title: Integrating with Adobe Campaign Classic
description: 了解如何整合AEM與Adobe Campaign Classic
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: 7fed5ce55f6ee7638d2578ee7ef2d84deb24277f
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# 與Adobe Campaign Classic整合 {#integrating-campaign-classic}

將AEM與Adobe Campaign整合後，您就可以直接在AEM中管理電子郵件傳遞、內容和表單。 需要Adobe Campaign Classic和AEM中的設定步驟，才能啟用解決方案之間的雙向通訊。

此整合可讓AEM和Adobe Campaign Classic獨立使用。 行銷人員可在Adobe Campaign中建立行銷活動及使用鎖定目標，而內容建立者可同時在AEM中進行內容設計。 整合可讓Adobe Campaign鎖定AEM中促銷活動的內容與設計，並加以傳送。

## 整合步驟 {#integration-steps}

AEM和Campaign之間的整合需要兩個解決方案中的許多步驟。

1. [在Campaign中安裝AEM整合套件。](#install-package)
1. [在Campaign中建立AEM的運算子](#create-operator)
1. [在AEM中設定Campaign整合](#campaign-integration)
1. [設定AEM Externalizer](#externalizer)
1. [在AEM中設定campaign-remote使用者](#configure-user)
1. [在Campaign中設定AEM外部帳戶](#acc-setup)

本檔案會詳細引導您完成這些步驟。

## 必備條件 {#prerequisites}

* 管理員存取Adobe Campaign Classic
   * 若要執行整合，您需要有可運作的Adobe Campaign Classic例項，包括已設定的資料庫。
   * 若您需要有關如何設定和設定Adobe Campaign Classic的其他詳細資訊，請參閱 [Adobe Campaign Classic檔案，](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html) 特別是《安裝及設定指南》。
* 管理員AEM存取權

## 在Campaign安裝AEM整合套件 {#install-package}

此 **AEM整合** Adobe Campaign中的套件包含連線至AEM所需的許多標準設定。

1. 以管理員身分，使用用戶端主控台登入Adobe Campaign執行個體。

1. 選擇 **工具** > **進階** > **導入包……**.

   ![匯入套件](assets/import-package.png)

1. 按一下 **安裝標準套件** 然後按一下 **下一個**.

1. 檢查 **AEM整合** 包。

   ![安裝標準套件](assets/select-package.png)

1. 按一下 **下一個**，然後 **開始** 以開始安裝。

   ![安裝進度](assets/installation.png)

1. 按一下 **關閉** 安裝完成後。

整合套件現已安裝。

## 在Campaign中建立AEM的運算子 {#create-operator}

整合套件會自動建立 `aemserver` 運算子(AEM用來連線至Adobe Campaign)。 必須為此運算子定義安全區域並設定其密碼。

1. 使用用戶端主控台以管理員身分登入Adobe Campaign。

1. 選擇 **工具** -> **瀏覽器** 的上界。

1. 在瀏覽器中，導覽至 **管理** > **存取管理** > **運算子** 節點。

1. 選取 `aemserver` 運算元。

1. 在 **編輯** 索引標籤，選取 **存取權限** 按一下子標籤，然後按一下 **編輯訪問參數……** 連結。

   ![設定安全區域](assets/access-rights.png)

1. 選擇適當的安全區域，並根據需要定義受信任的IP掩碼。

1. 按一下「**儲存**」。

1. 登出Adobe Campaign用戶端。

1. 在Adobe Campaign伺服器的檔案系統上，導覽至Campaign安裝位置並編輯 `serverConf.xml` 檔案。 此檔案通常位於：
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` 在Windows中。
   * `/usr/local/neolane/nl6/conf/eng` 在Linux中。

1. 搜尋 `securityZone` 和請確定已為AEM運算子的安全區域設定下列參數。

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`。

1. 儲存檔案。

1. 確保安全區域不會被 `config-<server name>.xml` 檔案。

   * 如果配置檔案包含單獨的安全區域設定，請更改 `allowUserPassword` 屬性至 `true`.

1. 如果要變更Adobe Campaign Classic伺服器埠，請取代 `8080` 和所需埠。

   >[!CAUTION]
   >
   >預設情況下，沒有為運算子配置安全區域。 若要讓AEM連線至Adobe Campaign，您必須選取區域，如先前步驟所述。
   >
   >Adobe強烈建議建立專用於AEM的安全區域，以避免任何安全性問題。 有關此主題的詳細資訊，請參閱 [Adobe Campaign Classic檔案。](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. 在Campaign用戶端中，返回 `aemserver` 運算子，然後選取 **一般** 標籤。

1. 按一下 **重置密碼……** 連結。

1. 指定密碼並將其儲存在安全位置，以供日後使用。

1. 按一下 **確定** 為 `aemserver` 運算元。

## 在AEM中設定Campaign整合 {#campaign-integration}

AEM使用 [您已在Campaign中設定的運算子](#create-operator) 以便與Campaign通訊

1. 以管理員身分登入AEM製作執行個體。

1. 在全域導覽側邊欄中，選取 **工具** > **Cloud Services** > **舊版Cloud Services** > **Adobe Campaign**，然後按一下 **立即配置**.

   ![設定Adobe Campaign](assets/configure-campaign-service.png)

1. 在對話方塊中，輸入 **標題** 按一下 **建立**.

   ![設定Campaign對話方塊](assets/configure-campaign-dialog.png)

1. 將開啟新窗口和對話框以編輯配置。 提供必要的資訊。

   * **使用者名稱**  — 這是 [在上一步驟中建立的Adobe Campaign AEM整合套件運算子。](#create-operator) 預設為 `aemserver`.
   * **密碼**  — 這是 [在上一步驟中建立的Adobe Campaign AEM整合套件運算子。](#create-operator)
   * **API端點**  — 這是Adobe Campaign執行個體URL。

   ![在AEM中設定Adobe Campaign](assets/configure-campaign.png)

1. 選擇 **連線至Adobe Campaign** 驗證連接，然後按一下 **確定**.

AEM現在可與Adobe Campaign通訊。

>[!NOTE]
>
>請確定您的Adobe Campaign伺服器可透過網際網路存取。 AEM無法存取專用網路。

## 設定復寫至AEM Publish執行個體 {#replication}

促銷活動內容是由內容作者在AEM製作例項上建立。 此例項通常僅供貴組織內部使用。 若要讓行銷活動的收件者存取影像和資產等內容，您需要發佈該內容。

復寫代理負責將您的內容從AEM製作例項發佈至發佈例項，且必須進行設定，整合才能正常運作。 若要將某些製作執行個體設定複製到發佈執行個體，也必須執行此步驟。

若要設定從AEM製作執行個體到發佈執行個體的復寫：

1. 以管理員身分登入AEM製作執行個體。

1. 在全域導覽側邊欄中，選取 **工具** > **部署** > **復寫** > **作者代理**，然後點選或按一下 **預設代理（發佈）**.

   ![配置複製代理](assets/acc-replication-config.png)

1. 點選或按一下 **編輯** 然後選取 **運輸** 標籤。

1. 設定 **URI** 欄位，取代預設值 `localhost` 值與AEM發佈執行個體的IP位址。

   ![傳輸標籤](assets/acc-transport-tab.png)

1. 點選或按一下 **確定** 以保存對代理設定的更改。

您已設定到AEM發佈執行個體的復寫，讓您的行銷活動收件者可以存取您的內容。

>[!NOTE]
>
>如果您不想使用復寫URL，而是使用公開的URL，您可以透過OSGi在下列組態設定中設定公用URL
>
>在全域導覽側邊欄中，選取 **工具** > **操作** > **Web主控台** > **OSGi配置** 和搜索 **AEM Campaign整合 — 設定**. 編輯設定並變更欄位 **公用URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 設定AEM Externalizer {#externalizer}

[Externalizer](/help/sites-developing/externalizer.md) 是AEM中的OSGi服務，可將資源路徑轉換為外部和絕對URL，這是AEM提供Campaign可使用的內容所必要的。 您必須進行設定，Campaign整合才能運作。

1. 以管理員身分登入AEM製作執行個體。
1. 在全域導覽側邊欄中，選取 **工具** > **操作** > **Web主控台** > **OSGi配置** 和搜索 **Day CQ link Externalizer**.
1. 依預設， **網域** 欄位適用於發佈例項。 將URL從預設值變更為 `http://localhost:4503` 至您公開可用的發佈例項。

   ![配置外部化程式](assets/acc-externalizer-config.png)

1. 點選或按一下 **儲存**.

您已設定Externalizer且Adobe Campaign無法存取您的內容。

>[!NOTE]
必須可從Adobe Campaign伺服器存取發佈執行個體。 如果指向 `localhost:4503` 或Adobe Campaign無法存取的其他伺服器，來自AEM的影像將不會顯示在Adobe Campaign主控台中。

## 在AEM中設定campaign-remote使用者 {#configure-user}

為了讓Campaign與AEM通訊，您必須為 `campaign-remote` 使用者。

1. 以管理員身分登入AEM。
1. 在主導覽主控台上，按一下 **工具** 在左側邊欄。
1. 然後按一下 **安全性** -> **使用者** 以開啟使用者管理控制台。
1. 找出 `campaign-remote` 使用者。
1. 選取 `campaign-remote` 使用者，按一下 **屬性** 來編輯用戶。
1. 在 **編輯使用者設定** 按一下 **更改密碼**.
1. 為用戶提供新密碼，並在安全位置記下密碼，以備將來使用。
1. 按一下 **儲存** 保存密碼更改。
1. 按一下 **儲存並關閉** 儲存 `campaign-remote` 使用者。

## 在Campaign中設定AEM外部帳戶 {#acc-setup}

當 [安裝 **AEM整合** Campaign中的套件，](#install-package) 為AEM建立外部帳戶。 透過設定此外部帳戶，Adobe Campaign可以連線至AEM，以啟用解決方案之間的雙向通訊。

1. 使用用戶端主控台以管理員身分登入Adobe Campaign。

1. 選擇 **工具** -> **瀏覽器** 的上界。

1. 在瀏覽器中，導覽至 **管理** > **平台** > **外部帳戶** 節點。

   ![外部帳戶](assets/external-accounts.png)

1. 找出外部AEM帳戶。 依預設，其值為：

   * **類型** - `AEM`
   * **標籤** - `AEM Instance`
   * **內部名稱** - `aemInstance`

1. 在 **一般** 索引標籤，輸入您在 [設定Campaign-remote用戶密碼](#set-campaign-remote-password) 步驟。

   * **伺服器** - AEM作者伺服器位址
      * 必須可從Adobe Campaign Classic伺服器例項存取AEM作者伺服器。
      * 確保伺服器地址確定 **not** 結尾為斜線。
   * **帳戶**  — 依預設，這是 `campaign-remote` 您在AEM中設定的使用者 [設定Campaign-remote用戶密碼](#set-campaign-remote-password) 步驟。
   * **密碼**  — 此密碼與 `campaign-remote` 您在AEM中設定的使用者 [設定Campaign-remote用戶密碼](#set-campaign-remote-password) 步驟。

1. 選取 **已啟用** 核取方塊。

1. 按一下「**儲存**」。

Adobe Campaign現在可與AEM通訊。

## 後續步驟 {#next-steps}

同時設定Adobe Campaign Classic和AEM後，整合現在已完成。

您現在可以繼續使用，了解如何在Adobe Experience Manager中建立電子報 [此文檔。](/help/sites-authoring/campaign.md)
