---
title: 緩解AEM Forms JEE中的序列化問題 |Adobe Experience Manager
description: 瞭解如何減少在JDK 8上執行的AEM Forms JEE中的Java還原序列化問題。
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# 緩解AEM Forms JEE中的序列化問題 {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEE包含還原序列化防火牆，可在任何嘗試還原序列化物件之前新增預檢檢查。 此檢查會針對防火牆樣式的允許清單、封鎖清單或兩者來測試類別名稱，並拒絕已知可透過Java™還原序列化攻擊攻擊的類別。 基礎代理程式是Adobe修改過的開放原始碼[NotSoSerial](https://github.com/kantega/notsoserial)專案的分發，根據[Apache 2授權](https://www.apache.org/licenses/LICENSE-2.0)授權。

在執行&#x200B;**JDK 11或更新版本**&#x200B;的安裝上，此保護是由平台的原生序列化篩選所啟動，不需要手動步驟。 在執行&#x200B;**JDK 8**&#x200B;的安裝上，原生序列化篩選無效，因此代理程式必須在啟動時明確附加至JVM。 本文會說明如何執行此操作。

>[!NOTE]
>
>如果還原序列化篩選器健康情況檢查已在您的伺服器上報告為作用中（請參閱[驗證代理程式的啟用](#verifying-the-agents-activation)），表示您的應用程式伺服器已受到保護，您可以略過本檔案中的其餘步驟。

## 開始之前 {#before-you-begin}

確認應用程式伺服器執行的Java™版本：

```shell
java -version
```

如果報告的版本為`1.8.x` (JDK 8)，則套用本文中的步驟。 如果是11或更新版本，則不需要手動動作；請使用[驗證代理程式的啟用](#verifying-the-agents-activation)中說明的健康狀態檢查來驗證保護。

在接下來的步驟中，`<jee-installation-directory>`會參照AEM Forms JEE安裝的根目錄。

## 套用代理程式 {#applying-the-agent}

>[!IMPORTANT]
>
>這些步驟需要重新啟動應用程式伺服器。 將它們套用到每個受影響的執行個體。

1. **驗證目前的狀態。** 瀏覽至還原序列化篩選器健康狀態檢查：

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   如果檢查報告為作用中，表示執行個體已受保護，無需進一步動作。 如果失敗，請繼續下列步驟。

1. **驗證代理程式JAR是否已存在。** 檢查下列位置下的`notsoserial.jar`：

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **如果缺少JAR，請新增它。** 下載[`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar)，並將其複製到每個執行個體上方的資料夾：

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >在發佈之前，請以代理程式的Adobe JEE分發的官方Forms下載位置取代此步驟。

1. **更新應用程式伺服器的JVM啟動引數**&#x200B;以附加代理程式。 將下列選項新增至Java™執行行：

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   Java™執行行的確切位置取決於您的應用程式伺服器（例如JBoss、WebLogic或WebSphere®）。 將選項新增至用來啟動AEM Forms JEE應用程式伺服器的JVM選項。

1. **重新啟動JEE伺服器**，以便在JVM啟動時載入代理程式。

1. **重新驗證。** 再次瀏覽健康狀態檢查：

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   健康情況檢查現在應該報告為健康。

## 正在驗證代理程式的啟用 {#verifying-the-agents-activation}

您可以瀏覽至下列URL，隨時驗證還原序列化代理程式的設定：

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

此時會顯示與代理程式相關的健康情況檢查清單。 如果檢查通過，代理程式將正確啟動。 如果它們在JDK 8執行個體上失敗，則代理程式尚未載入，您必須使用[套用代理程式](#applying-the-agent)中的步驟手動附加它。

## 設定代理程式 {#configuring-the-agent}

如果應用程式伺服器的Java™版本是以JDK 8執行，則適用下列步驟。 您可以在附加代理程式後設定代理程式，並使用[套用代理程式](#applying-the-agent)中的步驟載入它。

預設設定足以供大部分安裝使用。 它包含已知可遠端利用類別的封鎖清單，以及可安全還原序列化受信任資料的套件允許清單。 封鎖清單會在任何列入允許清單的專案之前套用。

防火牆設定是動態的，可以隨時變更：

1. 前往位於`https://<server>:<port>/system/console/configMgr`的Web主控台。

1. 搜尋並按一下&#x200B;**還原序列化防火牆組態**。

此設定包含允許清單、封鎖清單和診斷記錄選項：

* **允許清單** — 允許還原序列化的類別或套件首碼。 如果您將自己的類別還原序列化，請在此處新增相關的類別或套件。
* **封鎖清單** — 不允許還原序列化的類別。 初始集僅限於被發現容易遭受遠端執行攻擊的類別。
* **診斷記錄** — 進行還原序列化時要記錄的選項。 預設&#x200B;**class-name-only**&#x200B;報告正在還原序列化的類別。 **完整棧疊**&#x200B;選項會記錄第一次還原序列化嘗試的Java™棧疊，這有助於在您的使用中找出並移除不受信任的還原序列化。 這些選項僅在第一次使用時記錄。

## 其他考量 {#other-considerations}

* 此代理程式旨在緩解目前已知的脆弱類別。 如果您的專案還原序列化不受信任的資料，該資料可能仍會遭到拒絕服務、記憶體不足或未知的未來還原序列化攻擊。
* 如果您在JRE (Java™ Runtime Environment)而非JDK (Java™ Development Kit)上執行，則無法使用動態代理程式載入所需的工具，且必須在啟動時手動附加代理程式，如[套用代理程式](#applying-the-agent)中所述。
* 如果您在® JVM上執行，請檢閱有關Java™附加API支援的檔案。
