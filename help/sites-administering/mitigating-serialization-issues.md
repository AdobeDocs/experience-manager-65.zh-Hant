---
title: 緩解AEM中的序列化問題
seo-title: 緩解AEM中的序列化問題
description: 了解如何緩解AEM中的序列化問題。
seo-description: 了解如何緩解AEM中的序列化問題。
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# 緩解AEM{#mitigating-serialization-issues-in-aem}中的序列化問題

## 概覽 {#overview}

Adobe的AEM團隊已與開放原始碼專案[NotSoSerial](https://github.com/kantega/notsoserial)密切合作，協助減輕&#x200B;**CVE-2015-7501**&#x200B;中所述的弱點。 NotSoSerial是在[Apache 2許可證](https://www.apache.org/licenses/LICENSE-2.0)下授予許可的，並包括在其自己的[BSD類許可證](https://asm.ow2.org/license.html)下授予許可的ASM代碼。

此包中包含的代理jar是Adobe修改的NotSoSerial分發。

NotSoSerial是Java級問題的Java級解決方案，不特定於AEM。 它會將預檢檢查新增至嘗試反序列化物件。 此檢查將根據防火牆樣式的允許清單和/或阻止清單測試類名。 由於預設區塊清單中的類別數目有限，這不太可能對您的系統或程式碼造成影響。

預設情況下，代理將對當前已知的易受攻擊類執行塊清單檢查。 此阻止清單旨在保護您免受使用此類型漏洞的當前木馬程式清單的攻擊。

可以按照本文[配置代理](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)部分中的說明配置塊清單和允許清單。

代理旨在幫助緩解最新已知的易受攻擊類。 如果您的項目正在反序列化不受信任的資料，則它仍可能容易受到拒絕服務攻擊、記憶體不足攻擊和未知的未來反序列化木馬攻擊。

Adobe正式支援Java 6、7和8，但我們了解NotSoSerial也支援Java 5。

## 安裝代理{#installing-the-agent}

>[!NOTE]
>
>如果您先前已安裝AEM 6.1的序列化Hotfix，請從java執行行中移除代理啟動命令。

1. 安裝&#x200B;**com.adobe.cq.cq-serialization-tester**&#x200B;套件組合。

1. 前往`https://server:port/system/console/bundles`的捆綁式Web控制台
1. 尋找序列化套件並啟動。 這應會動態自動載入NotSoSerial代理。

## 在應用程式伺服器{#installing-the-agent-on-application-servers}上安裝代理

應用程式伺服器的AEM標準分發中不包含NotSoSerial代理。 不過，您可從AEM jar分發中擷取，並搭配應用程式伺服器設定使用：

1. 首先，下載AEM快速入門檔案並加以擷取：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 轉到新解壓縮的AEM快速入門的位置，然後將`crx-quickstart/opt/notsoserial/`資料夾複製到AEM應用程式伺服器安裝的`crx-quickstart`資料夾。

1. 將`/opt`的所有權更改為運行伺服器的用戶：

   ```shell
   chown -R opt <user running the server>
   ```

1. 配置並檢查代理是否已正確激活，如本文的以下各節所示。

## 配置代理{#configuring-the-agent}

預設配置適用於大多數安裝。 這包括已知遠程執行漏洞類的塊清單和允許包清單，其中可信資料的反序列化應相對安全。

防火牆配置是動態的，可隨時通過以下方式進行更改：

1. 前往`https://server:port/system/console/configMgr`的Web主控台
1. 搜索並按一下&#x200B;**反序列化防火牆配置。**

   >[!NOTE]
   >
   >您也可以存取以下網址的URL，直接存取設定頁面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此設定包含允許清單、封鎖清單和反序列化記錄。

**允許清單**

在允許清單區段中，這些是允許進行反序列化的類或包前置詞。 請務必注意，如果您正在反序列化自己的類，則需要將類或包添加到此允許清單中。

**塊清單**

在塊清單部分中，是不允許用於反序列化的類。 這些類的初始集僅限於那些發現易受遠程執行攻擊的類。 在任何允許的列出條目之前應用阻止清單。

**診斷日誌記錄**

在診斷記錄的區段中，您可以選取進行反序列化時要記錄的數個選項。 這些僅會先登入，而後續使用不會再登入。

預設值&#x200B;**class-name-only**&#x200B;將通知您正在反序列化的類。

您也可以設定&#x200B;**full-stack**&#x200B;選項，該選項將記錄第一個反序列化嘗試的Java堆棧，以通知您反序列化的發生位置。 這對於尋找和移除使用中的反序列化非常有用。

## 驗證代理的激活{#verifying-the-agent-s-activation}

您可以瀏覽至以下網址，以驗證反序列化代理的設定：

* `https://server:port/system/console/healthcheck?tags=deserialization`

存取URL後，會顯示與代理相關的健康狀態檢查清單。 通過驗證運行狀況檢查是否通過，可以確定代理是否正確激活。 如果失敗，則可能需要手動載入代理。

有關疑難排解代理問題的詳細資訊，請參閱下方的[處理動態代理載入的錯誤](#handling-errors-with-dynamic-agent-loading)。

>[!NOTE]
>
>如果將`org.apache.commons.collections.functors`新增至允許清單，則健康狀況檢查一律會失敗。

## 處理動態代理載入{#handling-errors-with-dynamic-agent-loading}時的錯誤

如果日誌中顯示了錯誤，或驗證步驟檢測到載入代理時出現問題，則可能需要手動載入代理。 如果您使用的是JRE（Java運行時環境），而不是JDK（Java開發工具包），則也建議使用此方法，因為動態載入工具不可用。

要手動載入代理，請按照以下說明操作：

1. 修改CQ jar的JVM啟動參數，並添加以下選項：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >這需要使用 — nofork CQ/AEM選項，以及適當的JVM記憶體設定，因為不會在已取用的JVM上啟用代理。

   >[!NOTE]
   >
   >可在AEM安裝的`crx-quickstart/opt/notsoserial/`資料夾中找到NotSoSerial代理jar的Adobe分佈。

1. 停止並重新啟動JVM;

1. 按照[驗證代理的激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)中所述的步驟再次驗證代理的激活。

## 其他注意事項{#other-considerations}

如果您正在IBM JVM上運行，請在[此位置](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)查看有關Java Attach API支援的文檔。
