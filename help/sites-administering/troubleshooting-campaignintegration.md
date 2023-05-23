---
title: 排除您的Adobe Campaign整合故障
seo-title: Troubleshooting your Adobe Campaign Integration
description: 瞭解如何解決Adobe Campaign整合問題。
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# 排除您的Adobe Campaign整合故障{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>此頁適用於Campaign Classic。

以下故障排除提示有助於解決您與Adobe Campaign整合時可能遇到的最AEM常見問題：

## 一般故障排除提示 {#general-troubleshooting-tips}

對於兩個整合，您可以檢查是否發送HTTP調用(AEM>Adobe Campaign、Adobe CampaignAEM>):

* 當整合失敗時，確保這些呼叫到達另一端（以避免防火牆/SSL問題）。
* 在功AEM能方面，您將看到json調用是從作者介面AEM請求的；這不應導致HTTP-500錯誤。 如果您看到HTTP-500錯誤，請檢查 `error.log` 的雙曲余弦值。
* 提高中市場活動類的調試級別AEM也有助於解決問題。

## 如果連接失敗 {#if-the-connection-fails}

檢查是否已配置 **AemServer** 在Adobe Campaign。

## 如果影像未出現在Adobe Campaign控制台中 {#if-images-do-not-appear-in-the-adobe-campaign-console}

檢查HTML源，並驗證是否可以從客戶端電腦開啟URL。 如果URL中包含localhost:4503，則更改作者實例上的Day CQ連結外部化程式的配置，以指向可從Adobe Campaign控制台電腦訪問的發佈實例。

請參閱 [正在配置外部化程式。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果無法從連AEM接到Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign查找以下錯誤消息：

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

要解決此問題，請在 **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign對話框中沒有顯示資料 {#if-no-data-displays-in-the-adobe-campaign-dialog}

在Adobe Campaign，確保埠號後沒有尾斜線(/)。

![chlimage_1-149](assets/chlimage_1-149.png)

## 如果您收到有關設定區域設定的警告 {#if-you-get-a-warning-about-your-setlocale}

如果正在啟動Apache HTTPD服務，並查看錯誤 `"Warning: setlocale: LC_CTYPE cannot change locale"` 確保你 **en_CA.ISO-8859-15區域設定** 安裝在系統上。

您可以使用 `local -a`。 如果未安裝，您可以修補 **/usr/local/neolane/nl6/env.sh** 編寫指令碼並將區域設定更改為已安裝的區域設定。

## 如果編譯指令碼「get_nms_amcGetSeedMetaData_jssp」時出錯 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果在日誌檔案中看到以下AEM錯誤消息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

使用以下解決方法：

1. 開啟檔案 **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. 修改方法&quot;amcGetSeedMetaData&quot;的第467行
1. 更改 `label : [inclView.@label](mailto:inclView.@label)` 至 `label : String([inclView.@label](mailto:inclView.@label))`

1. 儲存.
1. 重新啟動伺服器。

## 如果Adobe Campaign在按一下「同步」按鈕時顯示錯誤 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

如果按一下 **同步** 按鈕，將看到以下錯誤：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

要解決此問題，請確AEM保在「外部帳戶」中配置的connection-url可以從電腦訪問。

交換機 **本地主機** 到IP地址就解決了這個問題。

## 如果遇到「無法分析XTK日期+時間「undefined」錯誤 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

按一下「同步」後，您會發現頁面上出現指令碼的錯誤：無法分析XTK Date+Time &#39;undefined&#39;:不是有效的XTK值。

如果實例上仍有過時的Adobe Campaign資訊，則會AEM發生。 通過刪除所有正在進行的市場活動整合配置並重AEM建它們來解決此問題。 然後，建立新模板。

## 如果在設定雲服務時與SSL的連接顯示錯誤 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

在的error.log中AEM，如果您看到以下內容：

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

請向Adobe Campaign支援隊提票。

## 如果在同步對話框中看到http而不是預期的https連結 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

使用以下設定：

* 使用https托管Adobe Campaign與AEM作者通信
* 反向代理終止SSL
* Onpremise AEM Author實例

嘗試在Adobe Campaign交付中同步內容時，AEM返回新聞稿清單。 但是，清單中新聞稿的url是http地址。 選擇清單中的一個項時，會出錯。

要解決此問題：

* 需要將調度程式或反向代理配置為將原始協定作為報頭傳遞。
* 的 *Apache Felix Http服務SSL篩選器* 在OSGi配置中([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))需要配置為相應的標頭設定。 請參閱 [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 如果無法在「頁面屬性」中選擇我建立的自定義模板 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

為Adobe Campaign建立郵件模板時，必須包括該屬性 **acMapping** 值 **mapRecipient** 的 **jcr：內容** 節點，或者您無法在 **頁面屬性** { 0AEM}。

## 如果日誌中出現錯誤「com.day.cq.mcm.campaign.servlet.util.ParameterMapper」 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

使用自定義模板時，日誌中會出現錯誤「com.day.cq.mcm.campaign.servlet.util.ParameterMapper」。 在此情況下，請確保從 [包共用](/help/sites-administering/package-manager.md#package-share)。 如果acMapping屬性設定為recipient.firstName以外的值，則在Adobe Campaign管理器端建立空值時，將會出現此問題。
