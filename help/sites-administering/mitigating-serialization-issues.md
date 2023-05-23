---
title: 緩解中的序列化問AEM題
seo-title: Mitigating serialization issues in AEM
description: 瞭解如何緩解中的序列化問AEM題。
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 614c4c88f3f09feb5a400ade9f45f634ac4fbcd5
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 緩解中的序列化問AEM題{#mitigating-serialization-issues-in-aem}

## 概觀 {#overview}

AdobeAEM團隊與開源項目密切合作 [非SoSerial](https://github.com/kantega/notsoserial) 幫助減輕中描述的漏洞 **CVE-2015-7501**。 NotSoSerial在 [Apache 2許可證](https://www.apache.org/licenses/LICENSE-2.0) 並包括根據其自身許可的ASM代碼 [類BSD許可證](https://asm.ow2.io/)。

此包中包含的代理jar是Adobe修改的NotSoSerial分發。

NotSoSerial是Java™級別問題的Java™級別解決方案，不AEM特定。 它會向嘗試反序列化對象添加印前檢查。 此檢查將類名與防火牆樣式的允許清單或阻止清單或兩者test。 由於預設塊清單中的類數有限，因此此test不太可能對您的系統或代碼產生影響。

預設情況下，代理會針對當前已知的易受攻擊類執行阻止清單檢查。 此阻止清單旨在保護您免受使用此類漏洞的當前漏洞清單的攻擊。

可以按照 [配置代理](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 文章。

代理旨在幫助緩解最新的已知易受攻擊類。 如果您的項目正在反序列化不受信任的資料，則它仍可能易受拒絕服務攻擊、記憶體不足攻擊和未知的未來反序列化漏洞攻擊。

Adobe正式支援Java™ 6、7和8。 但是，Adobe的理解是NotSoSerial也支援Java™ 5。

## 安裝代理 {#installing-the-agent}

>[!NOTE]
>
>如果您以前安裝了6.1的序列化AEM修補程式，請從Java™運行行中刪除代理啟動命令。

1. 安裝 **com.adobe.cq.cq序列化測試器** 捆綁。

1. 轉至「捆綁Web控制台」，位於 `https://server:port/system/console/bundles`
1. 查找序列化包並啟動它。 這樣做會動態自動載入NotSoSerial代理。

## 在應用程式伺服器上安裝代理 {#installing-the-agent-on-application-servers}

NotSoSerial代理未包含在應用程式伺服器的標準AEM分發中。 但是，您可以從jar分發中提取它AEM，並將其與應用程式伺服器安裝程式一起使用：

1. 首先，下載快AEM速啟動檔案並解壓它：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 轉到新解壓快AEM速啟動的位置， `crx-quickstart/opt/notsoserial/` 資料夾 `crx-quickstart` 應用程式伺服器安AEM裝的資料夾。

1. 更改的所有權 `/opt` 運行伺服器的用戶：

   ```shell
   chown -R opt <user running the server>
   ```

1. 配置並檢查代理是否已正確激活，如本文以下各節所示。

## 配置代理 {#configuring-the-agent}

預設配置適用於大多數安裝。 此配置包括已知遠程運行易受攻擊類的阻止清單和信任資料反序列化安全的程式包允許清單。

防火牆配置是動態的，可以隨時通過以下方式進行更改：

1. 轉到Web控制台 `https://server:port/system/console/configMgr`
1. 搜索並按一下 **反序列化防火牆配置。**

   >[!NOTE]
   也可以通過訪問以下URL直接訪問配置頁：
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含允許清單、阻止清單和反序列化日誌記錄。

**允許清單**

在「允許清單」部分，這些清單是允許反序列化的類或包前置詞。 如果正在反序列化自己的類，請將類或包添加到此允許清單。

**塊清單**

在塊清單部分中是不允許反序列化的類。 這些類的初始集僅限於發現易受遠程執行攻擊的類。 在任何允許列出的條目之前應用阻止清單。

**診斷日誌記錄**

在診斷日誌記錄部分中，可以選擇幾個選項以在反序列化進行時進行日誌。 這些選項僅在首次使用時登錄，在後續使用時不再登錄。

預設值 **僅類名** 通知您正在反序列化的類。

也可以設定 **全堆棧** 選項，該選項記錄第一次反序列化嘗試的Java™堆棧，以通知您反序列化的發生地。 此選項對於查找和從使用中刪除反序列化非常有用。

## 驗證代理的激活 {#verifying-the-agent-s-activation}

通過瀏覽到以下URL，可以驗證反序列化代理的配置：

* `https://server:port/system/console/healthcheck?tags=deserialization`

訪問URL後，將顯示與代理相關的運行狀況檢查清單。 通過驗證運行狀況檢查是否正在通過，可以確定代理是否正確激活。 如果失敗，必須手動載入代理。

有關解決代理程式問題的詳細資訊，請參閱 [處理動態代理載入時的錯誤](#handling-errors-with-dynamic-agent-loading) 下。

>[!NOTE]
如果添加 `org.apache.commons.collections.functors` 在allowlist中，運行狀況檢查始終失敗。

## 處理動態代理載入的錯誤 {#handling-errors-with-dynamic-agent-loading}

如果日誌中顯示了錯誤，或驗證步驟檢測到載入代理時出現問題，請手動載入代理。 如果使用JRE（Java™運行時環境）而不是JDK（Java™開發工具包），則還建議使用此工作流，因為用於動態載入的工具不可用。

要手動載入代理，請執行以下操作：

1. 編輯CQ jar的JVM啟動參數，添加以下選項：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   要求您也使用 — nofork CQ/AEM選項以及相應的JVM記憶體設定，因為未在分類的JVM上啟用代理。

   >[!NOTE]
   NotSoSerial代理jar的Adobe分佈可在 `crx-quickstart/opt/notsoserial/` 資料夾AEM。

1. 停止並重新啟動JVM;

1. 按照中介紹的上述步驟再次驗證代理的激活 [驗證代理的激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)。

## 其他注意事項 {#other-considerations}

如果您在IBM® JVM上運行，請查看有關Java™ Attach API支援的文檔，地址為 [此位置](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api)。
