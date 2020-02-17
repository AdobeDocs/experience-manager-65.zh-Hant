---
title: 減輕AEM中的序列化問題
seo-title: 減輕AEM中的序列化問題
description: 瞭解如何減輕AEM中的序列化問題。
seo-description: 瞭解如何減輕AEM中的序列化問題。
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 減輕AEM中的序列化問題{#mitigating-serialization-issues-in-aem}

## 概覽 {#overview}

Adobe的AEM團隊與開放原始碼專案 [NotSoSerial](https://github.com/kantega/notsoserial) 密切合作，協助減輕 **CVE-2015-7501中描述的弱點**。 NotSoSerial是依據 [Apache 2授權授權](https://www.apache.org/licenses/LICENSE-2.0) ，並包含依其自有的 [BSD類似授權授權的ASM程式碼](https://asm.ow2.org/license.html)。

此套件中包含的代理jar是Adobe修改的NotSoSerial散發。

NotSoSerial是Java層級問題的Java層級解決方案，並非AEM專屬。 它會將預檢檢查加入嘗試反序列化物件的動作。 此檢查將針對防火牆類型的白名單和／或黑名單測試類名。 由於預設黑名單中的類數有限，這不太可能對您的系統或代碼產生影響。

預設情況下，代理將對當前已知的易受攻擊類執行黑名單檢查。 此黑名單旨在保護您免受使用此類漏洞的當前利用漏洞的攻擊清單的侵害。

按照本文「配置代理」部分中的說明，可以配 [置黑名單和白名單](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 。

代理旨在幫助緩解最新已知的易受攻擊類。 如果您的專案正在反序列化不受信任的資料，它仍可能容易受到拒絕服務攻擊、記憶體不足攻擊，以及未知的未來還原序列化利用攻擊。

Adobe正式支援Java 6、7和8，但我們瞭解NotSoSerial也支援Java 5。

## 安裝代理 {#installing-the-agent}

>[!NOTE]
>
>如果您先前已安裝AEM 6.1的序列化修補程式，請從java執行行移除代理程式啟動指令。

1. 安裝com.adobe.cq.cq **-serialization-tester套件** 。

1. 前往Bundle Web Console(位於 `https://server:port/system/console/bundles`
1. 尋找序列化套裝並開始它。 這應會動態自動載入NotSoSerial代理。

## 在應用程式伺服器上安裝代理 {#installing-the-agent-on-application-servers}

應用程式伺服器的AEM標準散發中未包含NotSoSerial代理。 不過，您可以從AEM jar散發中擷取它，並搭配您的應用程式伺服器設定使用：

1. 首先，下載AEM快速入門檔案並解壓縮：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 前往新解壓縮的AEM快速入門的位置，並將檔 `crx-quickstart/opt/notsoserial/` 案夾複製 `crx-quickstart` 至AEM應用程式伺服器安裝的檔案夾。

1. 將對運行服 `/opt` 務器的用戶的所有權更改為：

   ```shell
   chown -R opt <user running the server>
   ```

1. 設定並檢查代理是否已正確啟動，如本文的下列章節所示。

## 配置代理 {#configuring-the-agent}

預設配置適用於大多數安裝。 這包括已知遠程執行易受攻擊類的黑名單和包的白名單，其中對受信任資料的還原序列化應該相對安全。

防火牆配置是動態的，可隨時通過以下方式進行更改：

1. 前往Web主控台，網址為 `https://server:port/system/console/configMgr`
1. 搜索並按一下還原序列化 **防火牆配置。**

   >[!NOTE]
   >
   >您也可以存取URL，直接存取設定頁面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含白名單、黑名單和還原序列化記錄。

**白名單**

在白名單區段中，這些類別或封裝前置詞將允許用於還原序列化。 請務必注意，如果要反序列化自己的類，則需要將類或包添加到此白名單中。

**黑名單**

在黑名單部分中是不允許反序列化的類。 這些類的初始集僅限於發現易受遠程執行攻擊的類。 在列入白名單的條目之前應用黑名單。

**診斷記錄**

在診斷記錄的章節中，您可以選擇數個選項來在進行還原序列化時進行記錄。 這些僅記錄在首次使用中，而後續使用不會再記錄。

僅限 **class-name的預設值** ，將通知您正在取消序列化的類。

您也可以設定 **完整堆疊選項** ，此選項會記錄第一次還原序列化嘗試的Java堆疊，以通知您還原序列化的發生地。 這對於尋找和使用移除還原序列化非常有用。

## 驗證代理程式的激活 {#verifying-the-agent-s-activation}

您可瀏覽至URL，確認還原序列化代理的設定：

* `https://server:port/system/console/healthcheck?tags=deserialization`

一旦您存取URL，就會顯示與代理相關的健康狀態檢查清單。 通過驗證運行狀況檢查是否正在傳遞，可以確定代理是否已正確激活。 如果代理失敗，您可能需要手動載入代理。

有關疑難排解代理問題的詳細資訊，請參 [閱下方的動態代理載入處理錯誤](#handling-errors-with-dynamic-agent-loading) 。

>[!NOTE]
>
>如果您新增 `org.apache.commons.collections.functors` 至白名單，則健康狀況檢查永遠會失敗。

## 處理動態代理載入時的錯誤 {#handling-errors-with-dynamic-agent-loading}

如果日誌中顯示錯誤，或驗證步驟檢測到載入代理時出現問題，則可能需要手動載入代理。 如果您使用JRE（Java Runtime環境）而不是JDK（Java開發工具套件），也建議您使用此工具，因為無法使用動態載入工具。

要手動載入代理，請遵循以下說明：

1. 修改CQ jar的JVM啟動參數，添加以下選項：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >這需要使用-nofork CQ/AEM選項以及適當的JVM記憶體設定，因為Agent不會在已封鎖的JVM上啟用。

   >[!NOTE]
   >
   >您可在AEM安裝的資料夾中找到NotSoSerial代理程 `crx-quickstart/opt/notsoserial/` 式Jar的Adobe散發。

1. 停止並重新啟動JVM;

1. 請依照上述驗證代理程式啟動中的步驟， [再次驗證代理程式的啟動](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)。

## 其他考量事項 {#other-considerations}

如果您正在IBM JVM上執行，請在此位置檢閱有關Java Attach API支援的 [檔案](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)。

