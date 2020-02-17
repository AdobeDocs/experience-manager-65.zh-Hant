---
title: 疑難排解您的Adobe Campaign整合
seo-title: 疑難排解您的Adobe Campaign整合
description: 瞭解如何疑難排解Adobe Campaign整合的問題。
seo-description: 瞭解如何疑難排解Adobe Campaign整合的問題。
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 疑難排解您的Adobe Campaign整合{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>此頁面適用於Campaign Classic。

下列疑難排解提示可協助解決您將AEM與Adobe Campaign整合時最常遇到的問題：

## 一般疑難排解提示 {#general-troubleshooting-tips}

對於這兩種整合，您可以檢查是否傳送HTTP呼叫(AEM > Adobe Campaign、Adobe Campaign > AEM):

* 當整合失敗時，請確定這些呼叫會到達另一端（以避免防火牆/SSL問題）。
* 若為AEM功能，您會看到AEM作者介面中要求json呼叫；這不應導致HTTP-500錯誤。 如果您看到HTTP-500錯誤，請查看以取得 `error.log` 更多有關此的資訊。
* 提高AEM中促銷活動類別的除錯層級也有助於疑難排解問題。

## 如果連接失敗 {#if-the-connection-fails}

檢查您是否已在Adobe Campaign中 **設定** aemserver運算子。

## 如果影像未顯示在Adobe Campaign主控台中 {#if-images-do-not-appear-in-the-adobe-campaign-console}

檢查HTML來源並驗證您是否可從用戶端機器開啟URL。 如果URL中包含localhost:4503，則變更作者例項上的Day CQ Link Externalizer設定，以指向可從Adobe Campaign主控台機器存取的發佈例項。

請參 [閱設定Externalizer。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果您無法從AEM連線至Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign中尋找下列錯誤訊息：

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

若要修正此問題，請變更 **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml中的下列項目**:

`<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign對話方塊中未顯示任何資料 {#if-no-data-displays-in-the-adobe-campaign-dialog}

在Adobe Campaign中，請確定連結號後沒有尾隨斜線(/)。

![chlimage_1-149](assets/chlimage_1-149.png)

## 如果您收到有關設定的警告 {#if-you-get-a-warning-about-your-setlocale}

如果您要啟動Apache HTTPD服務，並看到錯誤 `"Warning: setlocale: LC_CTYPE cannot change locale"` ，請確定您的 **en_CA.ISO-8859-15地區設定已安裝在系統上** 。

您可以使用來檢查是否安裝了 `local -a`。 如果未安裝，您可以修補/usr/local/neolane/nl6/env.sh **指令碼** ，並將語言環境更改為已安裝的指令碼。

## 如果編譯指令碼&#39;get_nms_amcGetSeedMetaData_jssp&#39;時出錯 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM記錄檔中看到下列錯誤訊息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

使用下列解決方法：

1. 開啟檔 **案$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. 修改&quot;amcGetSeedMetaData&quot;方法的467行
1. Change `label : [inclView.@label](mailto:inclView.@label)` to `label : String([inclView.@label](mailto:inclView.@label))`

1. 儲存.
1. 重新啟動伺服器。

## 如果Adobe Campaign在按一下「同步化」按鈕時顯示錯誤 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

如果按一下Adobe Campaign **Classic中的** 「同步化」按鈕，您會看到下列錯誤：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

若要修正此問題，請確定可從機器存取「外部帳戶」中設定的AEM connection-url。

從 **localhost** 切換至IP位址可解決此問題。

## 如果您收到「無法剖析XTK日期+時間&#39;undefined&#39;」錯誤 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

按一下「同步化」後，您會看到頁面上發生指令碼的錯誤：無法剖析XTK Date+Time &#39;undefined&#39;:不是有效的XTK值。

如果AEM例項上仍有過時的Adobe Campaign資訊，就會發生此情況。 移除AEM上的所有促銷活動整合設定並重建這些設定，以解決此問題。 然後，建立新範本。

## 如果SSL連線在設定雲端服務時顯示錯誤 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

在AEM的error.log中，如果您看到下列項目：

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

請向Adobe Campaign支援團隊提出票證。

## 如果您在同步對話方塊中看到http，而非預期的https連結 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

使用下列設定：

* 使用https代管Adobe Campaign以便與AEM作者通訊
* 反向代理終止SSL
* 內部部署AEM Author實例

當嘗試同步Adobe Campaign傳送中的內容時，AEM會傳回電子報清單。 不過，清單中電子報的URL是http位址。 在選擇清單中的其中一個項目時，會出現錯誤。

要解決此問題：

* 必須將發送器或反向代理配置為將原始協定作為報頭傳遞。
* OSGi組態( *https://&lt;host>:&lt;port>/system/console/configMgr*[](http://localhost:4502/system/console/configMgr))中的Apache Felix Http Service SSL篩選器必須設定為個別的標題設定。 請參閱 [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 如果我建立的自訂範本無法在「頁面屬性」中選取 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

為Adobe Campaign建立郵件時，您必須在 **jcr:content** (jcr:content **)範本的節點中包含值** acMapping **，否則您將無法在AEM(field is disabled)的****** jcr:page Properties ContentMap中選取Adobe Campaign範本。

## 如果您在記錄檔中收到錯誤「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

使用自訂範本時，您的記錄檔中會出現「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」錯誤。 在此情況下，請務必從Package Share安裝Featurepack 6576 [](/help/sites-administering/package-manager.md#package-share)。 如果acMapping屬性設為recipient.firstName以外的值，Adobe Campaign manager會建立空白值，這就是問題。
