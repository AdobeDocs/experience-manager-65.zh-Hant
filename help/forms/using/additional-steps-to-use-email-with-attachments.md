---
title: 取得含附件的電子郵件的其他步驟
description: 瞭解當您無法在JEE平台上擷取AEM Forms的電子郵件附件時，如何修正錯誤。
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 無法取得JEE平台上AEM Forms的電子郵件（含附件）{#unable-to-get-email-with-attachments}

此問題適用於下列版本：

* Experience Manager6.5 Forms

## 問題 {#issue}

使用者無法執行操作，例如透過電子郵件傳送PDF或包含附件的提交設定。

## 解決方案 {#solution}

1. 將jar下載為 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 並解壓縮下載的jar檔案以取得資訊清單檔案。

1. 使用資訊清單檔案： `java.mail-1.0.jar` 從步驟1擷取以建立自訂jar檔案，例如 `java.mail-1.5.jar`.

1. 開啟資訊清單檔案並取代所有出現的 `1.5.0` 替換為 `1.5.6` 和 `Bundle-Version: 1.0` 替換為 `Bundle-Version:1.5`

1. 建立自訂jar (`java.mail-1.5.jar`)檔案，使用下列指令 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 資料夾為：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中， *manifest.mf* 是資訊清單檔案的名稱，並且 *java.mail-1.5.jar* 是在執行上述命令後建立的檔案名稱。

1. 下載 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 瀏覽至 `http://<server name>:<port>/lc/system/console/bundles`並刪除名稱為 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 安裝 `java.mail-1.5.jar` 取得自步驟3。 此步驟會重新啟動JEE部署的sling屬性。 等待已安裝的套件組合： `http://<server name>:<port>/lc/system/console/bundles` 將狀態顯示為 **作用中**.

   >如果狀態仍為 **非作用中**，重新啟動   **JBoss®** 從 **服務主控台**.


1. 安裝 `javax.mail-1.5.6.redhat-1.jar`使用步驟5下載的檔案。

1. 停止 **JBoss®** 從 **服務主控台** 並將下列屬性附加至 **Sling.properties** 檔案：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新啟動 **JBoss®**.

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。
