---
title: 跳進Adobe Analytics和Adobe Target
seo-title: Opting Into Adobe Analytics and Adobe Target
description: 瞭解如何選擇Adobe Analytics和Adobe Target。
seo-description: Learn how to opt into Adobe Analytics and Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---

# 跳進Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

有AEM一個選擇程式，幫助您融入Adobe Analytics和Adobe Target。 這是現成的，作為分配給管理員用戶組的預載入任務。

以管理員身份登錄時，此任務(**配置分析和目標**) [收件箱](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)。 根據您提供的憑據，它幫助您配置和整合這些服務。

您有以下配置整合的選項：

* 通過任務配置整合。

   這可以立即執行，也可以稍後執行，任務將保留在收件箱中，直到執行某些操作。 在兩種情況下，配置都可直接在UI中完成，或使用預定義的 `.properties` 的子菜單。

* 選擇退出整合。

   如果您願意，請考慮此選項 [手動配置整合](/help/sites-administering/marketing-cloud.md)。 另請參閱 [使用AEMDTM與Adobe Target和Adobe Analytics整合](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

* 使用指令碼配置設定和設定。

## 配置整合 {#configuring-the-integration}

選擇與以下產品整合：

* 分析，以啟用其頁面跟蹤和分析功能。
* 目標：啟用其個性化功能。

對於任一選項，您都需要提供用戶帳戶資訊並指定要跟蹤的頁。

>[!NOTE]
>
>可以選擇使用伺服器啟動時讀取的屬性檔案來提供分析和目標帳戶資訊。 請參閱 [使用屬性檔案提供帳戶資訊](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)。

選擇整合時，執AEM行以下任務：

* 建立啟用與分析和目標連接的雲配置。
* 建立確定要跟蹤的資料的框架。
* 配置網頁以使用這些服務。

>[!NOTE]
>
>AT.js是預設客戶端庫。 這是在您的 [目標雲服務配置](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)。
>
>Adobe建議將AT.js用作客戶端庫。

要從預載入的現成任務中選擇加入：

1. 從 [收件箱，選擇並 **開啟** 配置分析和目標](/help/sites-authoring/inbox.md#taking-action-on-an-item) 的子菜單。

   ![奧普丁–01](assets/optin-01.png)

1. 對於分析：

   1. 輸入分析的用戶帳戶資訊，然後按一下相應的 **添加** 按鈕
   1. 對相應的憑據進行身份驗證。
   1. 驗證分析帳戶後，選擇要使用的分析報告套件。 檢AEM索那些分析報表套件。 狀態更新為 **已添加**。

1. 對於目標：

   1. 輸入目標的用戶帳戶資訊，然後按一下相應的 **添加** 按鈕
   1. 對相應的憑據進行身份驗證。 狀態更新為 **已添加**。

1. 選擇 **下一個**。
1. 選擇應使用分析和/或目標的站點。

1. 選擇 **完成** 完成。

   >[!CAUTION]
   >
   >在選擇加入配置後，您需要發佈受影響的網站/頁面，以將這些更改複製到發佈實例。

## 退出整合 {#opting-out-of-the-integration}

選擇退出與Analytics和Target的整合：

* 不想與這些產品整合。
* 首選手動配置整合。

   有關手動配置整合的資訊，請參見 [與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md) 和 [與Adobe Target整合](/help/sites-administering/target.md)。

要選擇退出，您需要完成預載入的任務：

* 從 [收件箱，選擇並 **完成** 配置分析和目標](/help/sites-authoring/inbox.md#taking-action-on-an-item) 的子菜單。

## 使用屬性檔案提供帳戶資訊 {#providing-account-information-using-a-properties-file}

安裝在伺服器啟AEM動時讀取的屬性檔案，以配置與Analytics和Target整合的帳戶屬性。 使用屬性檔案時，「選入」嚮導會自動使用檔案中的屬性，並相應地建立雲配置。

屬性檔案是名為marketingcloud.properties的文本檔案，您將其保存在進程所使用的工作目錄AEM中（通常與JAR檔案相同的目錄）。 該檔案包括以下屬性：

* analytics.server:您使用的分析資料中心的URL。
* analytics.company:與Analytics用戶帳戶關聯的公司。
* analytics.username:您的分析用戶名。
* analytics.secret:與Analytics用戶名關聯的機密。
* analytics.reportsuite:要使用的分析報告套件的名稱。
* target.client代碼：與目標帳戶關聯的客戶端代碼。
* target.email:用於驗證目標帳戶的電子郵件地址。
* target.password:與您的電子郵件地址關聯的密碼。

屬性和值以等號(=)分隔。 分析屬性的前置詞為 `analytics`，並且Target屬性的前置詞為 `target`。 要配置服務，請為該服務提供所有屬性的值。 如果不想配置服務，請不為該服務提供值。

以下示例 `.properties` 檔案包括用於為Analytics建立雲配置的屬性值：

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

以下過程介紹如何使用屬性檔案選擇整合。

1. 建立 `marketingcloud.properties` 進程正在使用的工作目AEM錄（作者實例）中的檔案。

   >[!NOTE]
   >
   >工作目錄通常是包含jar或 `license.properties` 的子菜單。
   >
   >但是，它也可以由system屬性定義為絕對路徑：
   >
   >`mac.provisioning.file.container`

1. 根據分析和/或目標帳戶添加屬性值。
1. 啟動或重新啟動伺服器，然後使用管理員帳戶登錄。
1. 開啟「配置分析和目標」任務（如所述） [配置整合](/help/sites-administering/opt-in.md#configuring-the-integration)。 嚮導不會請求帳戶資訊，而是使用 `.properties` 的子菜單。

   選擇 **添加** 對於相應的服務，請繼續嚮導。

   ![奧普丁–02](assets/optin-02.png)

## 關於雲配置 {#about-the-cloud-configurations}

配置與Analytics和Target的整合時，會自AEM動建立所需的雲配置和框架。 例如，Analytics雲配置稱為「預配的分析帳戶」。

您無需更改雲配置。 但是，您可以根據需要配置框架。 (請參閱 [使用Adobe Analytics屬性映射元件資料](/help/sites-administering/adobeanalytics-mapping.md) 和 [添加目標框架](/help/sites-administering/target.md)。)

>[!NOTE]
>
>預設情況下，當您選擇加入Adobe Target配置嚮導時，將啟用「準確定位」。
>
>準確定位意味著雲服務配置在載入內容之前等待上下文載入。 因此，從效能上看，準確的目標可能會在載入內容之前產生幾毫秒的延遲。
>
>始終在作者實例上啟用精確目標。 但是，在發佈實例上，您可以選擇在雲服務配置中清除「準確瞄準」旁邊的複選標籤，從而全局關閉準確瞄準(**http://localhost:4502/etc/cloudservices.html**)。 無論您在雲服務配置中的設定如何，您仍然可以針對各個元件開啟和關閉精確的目標。
>
>如果 ***已*** 建立了目標元件，並且您更改了此設定，您所做的更改不會影響這些元件。 必須直接對這些元件進行任何更改。

>[!CAUTION]
>
>選擇分析配置和特定 `reportsuite` 框架被限制為發佈運行模式。 這意味著跟蹤僅對發佈實例有效。
>
>如果在創作實例上需要跟蹤，則值應更改為 `all`。

## 通過指令碼配置安裝和設定 {#configuring-the-setup-and-provisioning-via-script}

作為管理員，您可能希望使用指令碼觸發設定和設定，而不是手動逐步執行嚮導。 您可以通過以下方式執行此操作：

* 將POST請求發送到 **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** 參數。

您發送的參數取決於以下參數：

* 如果要使用 **營銷雲。屬性** 已填入所有必需憑據的檔案，則必須發送以下參數：

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=連接已創AEM建的雲服務配置的頁面的路徑

   例如，建立分析和目標配置並將它們附加到we.retail頁的curl請求為：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* 如果您不想使用 **營銷雲。屬性** 然後，您必須發送憑據和參數；例如：

   * 自動設定= `true`
   * 服務名= `analytics|target`
   * path=連接建立AEM的雲服務配置的頁面的路徑；可以定義多個路徑
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   在這種情況下，建立分析和目標配置並將它們附加到我們零售頁面的curl請求將是：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
