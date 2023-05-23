---
title: 獲取附件電子郵件的其他步驟
description: 獲取附件電子郵件的其他步驟
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 無法在JEE平台上獲取AEM Forms的附件電子郵件{#unable-to-get-email-with-attachments}

此問題適用於以下版本：
* Experience Manager六點五Forms

## 問題 {#issue}

用戶無法執行諸如「通過電子郵件發送PDF」或「包含附件」等操作，並配置「提交」。

## 解決方案 {#solution}

1. 將jar下載為 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 並解壓縮下載的jar檔案以獲取清單檔案。

1. 使用的清單檔案 `java.mail-1.0.jar` 從步驟1中檢索以建立新的自定義jar檔案，如 `java.mail-1.5.jar`。

1. 開啟清單檔案並替換 `1.5.0` 與 `1.5.6` 和 `Bundle-Version: 1.0` 與 `Bundle-Version:1.5`

1. 建立新的自定義jar(`java.mail-1.5.jar`使用以下命令 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 資料夾：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中， *manifest.mf* 是清單檔案的名稱， *java.mail-1.5.jar* 是執行上述命令後將建立的檔案的名稱。

1. 下載 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1)。

1. 導航到 `http://<server name>:<port>/lc/system/console/bundles`並刪除名稱為 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`。

1. 安裝 `java.mail-1.5.jar` 從步驟3獲得。  此步驟將重新啟動JEE部署的sling屬性。 等待安裝的捆綁包 `http://<server name>:<port>/lc/system/console/bundles` 顯示狀態為 **活動**。

   >注：以防萬一，狀態仍然 **活動**&#x200B;重新啟動   **JBoss** 從 **服務控制台**。


1. 安裝 `javax.mail-1.5.6.redhat-1.jar`使用步驟5下載的檔案。

1. 停止 **JBoss** 從 **服務控制台** 並將以下屬性添加到 **Sling.properties** 檔案：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新啟動 **JBoss**。
