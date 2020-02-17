---
title: 選擇使用Adobe Analytics和Adobe Target
seo-title: 選擇使用Adobe Analytics和Adobe Target
description: 瞭解如何選擇加入Adobe Analytics和Adobe Target。
seo-description: 瞭解如何選擇加入Adobe Analytics和Adobe Target。
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 選擇使用Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM有選擇加入程式，可協助您整合Adobe Analytics和Adobe Target。 這是現成可用的，作為分配給管理員用戶組的預載入任務。

當您以管理員身分登入時，此工作(**設定分析與定位**)可從收件 [匣中使用](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)。 根據您提供的認證，它可協助您設定和整合這些服務。

您有下列設定整合的選項：

* 透過工作設定整合。

   您可以立即或稍後執行此操作，任務將保留在收件箱中，直到執行某些操作。 無論是哪種情況，您都可以直接在UI中完成設定，或使用預先定義的檔 `.properties` 案。

* 選擇退出整合。

   如果您偏好手動設定 [整合，請考慮此選項](/help/sites-administering/marketing-cloud.md)。 另請參 [閱「使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)」。

* 使用指令碼配置設定和布建。

## 設定整合 {#configuring-the-integration}

選擇加入與以下項目的整合：

* Analytics，以啟用其頁面追蹤和分析功能。
* Target可讓您使用其個人化功能。

對於任一選項，您都必須提供使用者帳戶資訊並指定要追蹤的頁面。

>[!NOTE]
>
>您可選擇使用伺服器啟動時讀取的屬性檔案來提供Analytics和Target帳戶資訊。 請參 [閱使用屬性檔案提供帳戶資訊](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)。

當您選擇加入整合時，AEM會執行下列工作：

* 建立雲端設定，以啟用與Analytics和Target的連線。
* 建立可決定所追蹤資料的架構。
* 配置網頁以使用這些服務。

>[!NOTE]
>
>AT.js是預設用戶端程式庫。 這是在您的目標雲端 [服務設定下設定](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)。
>
>Adobe建議您使用AT.js作為用戶端程式庫。

若要選擇加入預先載入、立即可用的工作：

1. 從您的收 [件匣中，選取並 **開啟** 「設定分析與定位」工作](/help/sites-authoring/inbox.md#taking-action-on-an-item) 。

   ![optin-01](assets/optin-01.png)

1. 針對Analytics:

   1. 輸入Analytics的使用者帳戶資訊，然後按一下對應的「新 **增** 」按鈕。
   1. 驗證適當的認證。
   1. 驗證Analytics帳戶後，請選取要使用的Analytics報表套裝。 AEM會擷取這些Analytics報表套裝。 狀態會更新為「已 **新增」**。

1. 針對Target:

   1. 輸入Target的使用者帳戶資訊，然後按一下對應的「新 **增** 」按鈕。
   1. 驗證適當的認證。 狀態會更新為「已 **新增」**。

1. 選擇 **下一步**。
1. 選取應使用Analytics和／或Target的網站。

1. 選擇「 **完成** 」以完成。

   >[!CAUTION]
   >
   >選擇加入設定後，您需要發佈受影響的網站／頁面，以將這些變更複製至您的發佈例項。

## 退出整合 {#opting-out-of-the-integration}

選擇退出與Analytics和Target的整合，條件是：

* 不想與這些產品整合。
* 偏好手動設定整合。

   如需手動設定整合的詳細資訊，請 [參閱「與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)[與與Adobe Target整合」](/help/sites-administering/target.md)。

若要選擇退出，您必須完成預先載入的工作：

* 從您的收 [件匣中，選取並 **完成**](/help/sites-authoring/inbox.md#taking-action-on-an-item) 「設定分析與定位」任務。

## 使用屬性檔案提供帳戶資訊 {#providing-account-information-using-a-properties-file}

安裝AEM在伺服器啟動時讀取的屬性檔案，以設定與Analytics和Target整合的帳戶屬性。 當您使用屬性檔案時，選擇加入精靈會自動使用檔案中的屬性，而雲端組態也會隨之建立。

屬性檔案是名為marketingcloud.properties的文字檔案，您會儲存在AEM程式所使用的工作目錄中（通常與JAR檔案相同的目錄）。 該檔案包含以下屬性：

* analytics.server:您使用之Analytics資料中心的URL。
* analytics.company:與您的Analytics使用者帳戶關聯的公司。
* analytics.username:您的Analytics使用者名稱。
* analytics.secret:與您的Analytics使用者名稱關聯的機密。
* analytics.reportsuite:要使用的Analytics報表套裝名稱。
* target.clientcode:與您的Target帳戶關聯的用戶端代碼。
* target.email:您用來驗證Target帳戶的電子郵件地址。
* target.password:與您的電子郵件地址關聯的密碼。

屬性和值以等號(=)分隔。 Analytics屬性會加上前置詞 `analytics`，而Target屬性會加上前置詞 `target`。 要配置服務，請為該服務的所有屬性提供值。 如果您不想設定服務，請不提供該服務的值。

下列範例檔 `.properties` 案包含用於建立Analytics雲端設定的屬性值：

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

下列程式說明如何使用屬性檔案選擇加入整合。

1. 在AEM `marketingcloud.properties` 程式正在使用的工作目錄中建立檔案（作者例項）。

   >[!NOTE]
   >
   >工作目錄通常是包含jar或檔案的 `license.properties` 目錄。
   >
   >但是，它也可以由系統屬性定義為絕對路徑：
   >
   >`mac.provisioning.file.container`

1. 根據您的Analytics和／或Target帳戶新增屬性值。
1. 啟動或重新啟動伺服器，然後使用管理員帳戶登錄。
1. 開啟「設定分析與定位」工作，如「設定整 [合」所述](/help/sites-administering/opt-in.md#configuring-the-integration)。 精靈不會要求您的帳戶資訊，而是使用檔案中的 `.properties` 值。

   選擇 **添加** (Add for the appropriate service)，然後繼續嚮導。

   ![optin-02](assets/optin-02.png)

## 關於雲端設定 {#about-the-cloud-configurations}

當您設定與Analytics和Target的整合時，AEM會自動建立必要的雲端設定和架構。 例如，Analytics雲端設定稱為「布建的Analytics帳戶」。

您不需要變更雲端組態。 不過，您可以視需要設定架構。 (請參 [閱使用Adobe Analytics屬性對應元件資料](/help/sites-administering/adobeanalytics-mapping.md)[和新增Target Framework](/help/sites-administering/target.md))。

>[!NOTE]
>
>在您選擇加入Adobe target設定精靈時，預設會啟用「精確定位」。
>
>精確定位意味著雲端服務設定會在載入內容之前等待載入內容。 因此，在效能方面，精確定位可能會在載入內容前造成毫秒數的延遲。
>
>作者例項一律會啟用正確定位。 不過，在發佈例項中，您可以透過清除雲端服務設定中「精確定位」旁的核取標籤(**http://localhost:4502/etc/cloudservices.html**)，選擇全域關閉精確定位。 您也可以針對個別元件開啟或關閉精確定位，不論您在雲端服務組態中的設定為何。
>
>如果您已建 ***立目標元件*** ，而且您變更了此設定，則您所做的變更不會影響這些元件。 您必須直接對這些元件進行任何變更。

>[!CAUTION]
>
>當您選擇加入Analytics設定並選取特定 `reportsuite` 時，架構會限制為發佈執行模式。 這表示追蹤只適用於發佈例項。
>
>如果編寫例項需要追蹤，且值也應變更為 `all`。

## 通過指令碼配置設定和布建 {#configuring-the-setup-and-provisioning-via-script}

身為管理員，您可能希望使用指令碼觸發設定和置備，而不是手動逐步執行嚮導。 您可以透過下列方式完成：

* 使用所需參數將POST **請求** 傳送至/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json。

您傳送的參數取決於下列項目：

* 如果您想使用填 **入所有必要憑證的marketingcloud.properties** 檔案，則必須傳送下列參數：

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=AEM頁面的路徑，以附加已建立的雲端服務設定
   例如，建立Analytics和Target組態並將它們附加至we.retail頁面的捲動請求為：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* 如果您不想使用 **marketingcloud.properties** 檔案，則必須傳送憑證和參數；例如：

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path to an AEM page to attach the created cloud services configs;可定義多個路徑
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`
   在此例中，建立Analytics和Target組態並附加至we-retail頁面的捲動請求為：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

