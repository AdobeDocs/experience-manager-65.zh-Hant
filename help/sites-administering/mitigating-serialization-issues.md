---
title: 緩解AEM中的序列化問題
description: 瞭解如何減少AEM中的序列化問題。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 緩解AEM中的序列化問題{#mitigating-serialization-issues-in-aem}

## 概觀 {#overview}

Adobe的AEM團隊與開放原始碼專案[NotSoSerial](https://github.com/kantega/notsoserial)緊密合作，協助緩解&#x200B;**CVE-2015-7501**&#x200B;中描述的弱點。 NotSoSerial是以[Apache 2授權](https://www.apache.org/licenses/LICENSE-2.0)授權，並包含以自己的[類似BSD的授權](https://asm.ow2.io/)授權的ASM代碼。

此封裝包含的代理程式jar是Adobe修改過的NotSoSerial散發。

NotSoSerial是Java™層級問題的Java™層級解決方案，不是AEM專屬的解決方案。 它會新增預檢檢查以嘗試還原序列化物件。 此檢查會針對防火牆樣式的允許清單或/和封鎖清單來測試類別名稱。 由於預設封鎖清單中的類別數量有限，此測試不太可能對您的系統或程式碼造成影響。

依預設，代理程式會針對目前已知的易受攻擊類別執行封鎖清單檢查。 此封鎖清單旨在保護您免受目前使用這類漏洞的利用漏洞清單。

封鎖清單和允許清單可以依照本文的[設定代理程式](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)一節中的指示進行設定。

此代理程式的用途是協助緩解最新已知的脆弱類別。 如果您的專案正在還原序列化不受信任的資料，它仍可能容易受到拒絕服務攻擊、記憶體不足攻擊和未知的未來還原序列化利用的攻擊。

Adobe正式支援Java™ 6、7和8。 不過，Adobe的理解是NotSoSerial也支援Java™ 5。

## 安裝代理程式 {#installing-the-agent}

>[!NOTE]
>
>如果您先前已安裝AEM 6.1的序列化Hotfix，請從Java™執行列移除代理程式啟動命令。

1. 安裝&#x200B;**com.adobe.cq.cq-serialization-tester**&#x200B;套件。

1. 前往位於`https://server:port/system/console/bundles`的套件組合網頁主控台
1. 尋找序列化套件組合併加以啟動。 如此會動態自動載入NotSoSerial代理程式。

## 在應用程式伺服器上安裝代理程式 {#installing-the-agent-on-application-servers}

NotSoSerial代理程式不包含在應用程式伺服器的AEM標準散發中。 不過，您可以從AEM jar散發擷取它，並將其用於應用程式伺服器設定：

1. 首先，下載AEM快速入門檔案並解壓縮：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 移至新解壓縮的AEM快速入門的位置，並將`crx-quickstart/opt/notsoserial/`資料夾複製到AEM應用程式伺服器安裝的`crx-quickstart`資料夾。

1. 將`/opt`的擁有權變更為執行伺服器的使用者：

   ```shell
   chown -R opt <user running the server>
   ```

1. 設定代理程式並檢查代理程式是否已正確啟動，如本文後續章節所示。

## 設定代理程式 {#configuring-the-agent}

預設設定足以進行大部分的安裝。 此設定包含已知遠端執行易受攻擊的類別的封鎖清單，以及可安全還原序列化受信任資料的套件允許清單。

防火牆設定是動態的，可透過以下方式隨時變更：

1. 前往位於`https://server:port/system/console/configMgr`的Web主控台
1. 正在搜尋並按一下&#x200B;**還原序列化防火牆設定。**

   >[!NOTE]
   >
   >您也可以透過存取URL直接存取設定頁面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

此設定包含允許清單、封鎖清單和反序列化記錄。

**允許清單**

在允許清單區段中，這些清單是允許還原序列化的類別或套件首碼。 如果您要還原序列化自己的類別，請將類別或套件加入此允許清單。

**封鎖清單**

在區塊清單區段中，是永遠不允許還原序列化的類別。 這些類別的初始集僅限於已發現容易遭受遠端執行攻擊的類別。 封鎖清單會在任何允許清單專案之前套用。

**診斷記錄**

在診斷記錄區段中，您可以選擇數個選項，以便在還原序列化進行時記錄。 這些選項僅會在首次使用時記錄，而不會在後續使用時再次記錄。

**class-name-only**&#x200B;的預設值會通知您正在還原序列化的類別。

您也可以設定&#x200B;**完整棧疊**&#x200B;選項，此選項會記錄第一次還原序列化嘗試的Java™棧疊，以通知您正在還原序列化的位置。 此選項對於在使用中尋找和移除還原序列化相當實用。

## 驗證代理程式的啟用 {#verifying-the-agent-s-activation}

您可以瀏覽至下列URL，以驗證還原序列化代理程式的設定：

* `https://server:port/system/console/healthcheck?tags=deserialization`

存取URL後，會顯示與代理程式相關的健康情況檢查清單。 您可以透過驗證健康狀態檢查是否通過來判斷代理程式是否已正確啟動。 如果失敗，您必須手動載入代理程式。

如需疑難排解代理程式問題的詳細資訊，請參閱下方的[處理動態代理程式載入錯誤](#handling-errors-with-dynamic-agent-loading)。

>[!NOTE]
>
>如果您將`org.apache.commons.collections.functors`新增至允許清單，健康狀態檢查一律會失敗。

## 處理動態代理程式載入的錯誤 {#handling-errors-with-dynamic-agent-loading}

如果記錄中顯示錯誤，或驗證步驟偵測到載入代理程式的問題，請手動載入代理程式。 如果您使用JRE (Java™ Runtime Environment)而非JDK (Java™ Development Toolkit)，也建議使用此工作流程，因為動態載入的工具無法使用。

若要手動載入代理程式，請執行下列動作：

1. 編輯CQ jar的JVM啟動引數，新增下列選項：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >您也必須使用 — nofork CQ/AEM選項以及適當的JVM記憶體設定，因為代理程式並未在分支JVM上啟用。

   >[!NOTE]
   >
   >可以在AEM安裝的`crx-quickstart/opt/notsoserial/`資料夾中找到NotSoSerial代理程式jar的Adobe散發。

1. 停止並重新啟動JVM；

1. 請依照[驗證代理程式啟用](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)中所述步驟再次驗證代理程式的啟用。

## 其他考量 {#other-considerations}

如果您正在IBM® JVM上執行，請檢閱位於[此位置](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api)的Java™ Attach API支援檔案。
