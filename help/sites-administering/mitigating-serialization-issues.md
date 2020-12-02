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
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# 減輕AEM{#mitigating-serialization-issues-in-aem}中的序列化問題

## 概覽 {#overview}

Adobe的AEM團隊與開放原始碼專案[NotSoSerial](https://github.com/kantega/notsoserial)密切合作，協助您降低&#x200B;**CVE-2015-7501**&#x200B;中所述的弱點。 NotSoSerial是依[Apache 2授權](https://www.apache.org/licenses/LICENSE-2.0)授權授權，並包含依其自有[類似BSD的授權](https://asm.ow2.org/license.html)授權的ASM程式碼。

此套件中包含的代理jar是Adobe修改的NotSoSerial散發。

NotSoSerial是Java層級問題的Java層級解決方案，並非AEM專屬。 它會將預檢檢查加入嘗試反序列化物件的動作。 此檢查將根據防火牆樣式的允許清單和／或阻止清單來測試類名。 由於預設區塊清單中的類別數目有限，因此這不太可能對您的系統或程式碼造成影響。

預設情況下，代理將對當前已知的易受攻擊類執行塊清單檢查。 此塊清單旨在保護您免受使用此類漏洞的當前利用漏洞的攻擊清單的攻擊。

按照本文[「配置代理」部分中的說明，可以配置塊清單和允許清單。](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)

代理旨在幫助緩解最新已知的易受攻擊類。 如果您的專案正在反序列化不受信任的資料，它仍可能容易受到拒絕服務攻擊、記憶體不足攻擊，以及未知的未來還原序列化利用攻擊。

Adobe正式支援Java 6、7和8，但我們瞭解NotSoSerial也支援Java 5。

## 安裝代理{#installing-the-agent}

>[!NOTE]
>
>如果您先前已安裝AEM 6.1的序列化修補程式，請從java執行行移除代理程式啟動指令。

1. 安裝&#x200B;**com.adobe.cq.cq-serialization-tester**&#x200B;套件。

1. 前往`https://server:port/system/console/bundles`的Bundle Web Console
1. 尋找序列化套裝並開始它。 這應會動態自動載入NotSoSerial代理。

## 在應用程式伺服器上安裝代理{#installing-the-agent-on-application-servers}

NotSoSerial代理未包含在應用程式伺服器的AEM標準散發中。 不過，您可以從AEM jar散發中擷取它，並搭配您的應用程式伺服器設定使用：

1. 首先，下載AEM快速入門檔案並解壓縮：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 前往新解壓縮的AEM快速入門的位置，並將`crx-quickstart/opt/notsoserial/`檔案夾複製至AEM應用程式伺服器安裝的`crx-quickstart`檔案夾。

1. 將`/opt`的所有權更改為運行伺服器的用戶：

   ```shell
   chown -R opt <user running the server>
   ```

1. 設定並檢查代理是否已正確啟動，如本文的下列章節所示。

## 配置代理{#configuring-the-agent}

預設配置適用於大多數安裝。 這包括已知遠程執行易受攻擊類的塊清單和允許包清單，其中對受信任資料的還原序列化應該相對安全。

防火牆配置是動態的，可隨時通過以下方式進行更改：

1. 前往`https://server:port/system/console/configMgr`的Web控制台
1. 搜索並按一下&#x200B;**還原序列化防火牆配置。**

   >[!NOTE]
   >
   >您也可以存取URL，直接存取設定頁面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含允許清單、塊清單和還原序列化記錄。

**允許列出**

在允許清單部分中，這些是允許用於還原序列化的類或包前置詞。 請務必注意，如果要反序列化自己的類，則需要將類或包添加到此允許清單中。

**塊清單**

在塊清單部分中是不允許反序列化的類。 這些類的初始集僅限於發現易受遠程執行攻擊的類。 在允許列出任何條目之前，將應用塊清單。

**診斷記錄**

在診斷記錄的章節中，您可以選擇數個選項來在進行還原序列化時進行記錄。 這些僅記錄在首次使用中，而後續使用不會再記錄。

**class-name-only**&#x200B;的預設值將通知您正在取消序列化的類。

您也可以設定&#x200B;**full-stack**&#x200B;選項，此選項會記錄第一次還原序列化嘗試的Java堆疊，以通知您還原序列化的發生地。 這對於尋找和使用移除還原序列化非常有用。

## 驗證代理程式的激活{#verifying-the-agent-s-activation}

您可瀏覽至URL，確認還原序列化代理的設定：

* `https://server:port/system/console/healthcheck?tags=deserialization`

一旦您存取URL，就會顯示與代理相關的健康狀態檢查清單。 通過驗證運行狀況檢查是否正在傳遞，可以確定代理是否已正確激活。 如果代理失敗，您可能需要手動載入代理。

有關疑難排解代理問題的詳細資訊，請參閱下面的[使用動態代理載入處理錯誤](#handling-errors-with-dynamic-agent-loading)。

>[!NOTE]
>
>如果您將`org.apache.commons.collections.functors`新增至allow清單，則健康狀況檢查永遠會失敗。

## 處理動態代理載入{#handling-errors-with-dynamic-agent-loading}時的錯誤

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
   >NotSoSerial代理jar的Adobe散發位於AEM安裝的`crx-quickstart/opt/notsoserial/`資料夾中。

1. 停止並重新啟動JVM;

1. 按照[驗證代理激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)中所述的步驟再次驗證代理激活。

## 其他考量事項{#other-considerations}

如果您正在IBM JVM上運行，請在[此位置](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)查看有關Java Attach API支援的文檔。
