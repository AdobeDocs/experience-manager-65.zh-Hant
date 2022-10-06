---
title: 取得附件電子郵件的其他步驟
description: 取得附件電子郵件的其他步驟
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 無法在JEE平台上取得包含AEM Forms附件的電子郵件{#unable-to-get-email-with-attachments}

此問題適用於下列版本：
* Experience Manager6.5Forms

## 問題 {#issue}

使用者無法執行「透過電子郵件傳送PDF」或「包含附件」等具有提交設定的操作。

## 解決方案 {#solution}

1. 將jar下載為 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 並將下載的jar檔案解壓縮，以取得資訊清單檔案。

1. 使用的資訊清單檔案 `java.mail-1.0.jar` 從步驟1擷取以建立新的自訂jar檔案，如 `java.mail-1.5.jar`.

1. 開啟資訊清單檔案，並取代 `1.5.0` with `1.5.6` 和 `Bundle-Version: 1.0` with `Bundle-Version:1.5`

1. 建立新的自訂Jar(`java.mail-1.5.jar`)檔案， `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 資料夾如下：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中， *manifest.mf* 是資訊清單檔案的名稱， *java.mail-1.5.jar* 是執行上述命令後將建立的檔案的名稱。

1. 下載 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 導覽至 `http://<server name>:<port>/lc/system/console/bundles`並刪除名稱為的套件組合 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 安裝 `java.mail-1.5.jar` 從步驟3取得。  此步驟會重新啟動JEE部署的Sling屬性。 等待安裝的套件組合 `http://<server name>:<port>/lc/system/console/bundles` 狀態顯示為 **作用中**.

   >注意：若為，狀態仍為 **InActive**，重新啟動   **JBoss** 從 **服務控制台**.


1. 安裝 `javax.mail-1.5.6.redhat-1.jar`使用步驟5下載的檔案。

1. 停止 **JBoss** 從 **服務控制台** 並將下列屬性附加至 **Sling.properties** 檔案：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新啟動 **JBoss**.