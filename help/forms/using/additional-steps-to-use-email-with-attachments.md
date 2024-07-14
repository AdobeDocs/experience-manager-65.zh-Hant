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

1. 將jar下載為[java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar)，並將下載的jar檔案解壓縮，以取得資訊清單檔案。

1. 使用從步驟1擷取的`java.mail-1.0.jar`資訊清單檔案，建立自訂jar檔案，例如`java.mail-1.5.jar`。

1. 開啟資訊清單檔案，並將所有出現的`1.5.0`取代為`1.5.6`，`Bundle-Version: 1.0`取代為`Bundle-Version:1.5`

1. 在`C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin`資料夾中使用下列命令，建立自訂jar (`java.mail-1.5.jar`)檔案：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中，*manifest.mf*&#x200B;是資訊清單檔案的名稱，而&#x200B;*java.mail-1.5.jar*&#x200B;是執行上述命令後所建立之檔案的名稱。

1. 下載[javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1)。

1. 瀏覽至`http://<server name>:<port>/lc/system/console/bundles`並刪除名稱為`JavaMail API (com.sun.mail.javax.mail) version 1.6.2`的組合。

1. 安裝從步驟3取得的`java.mail-1.5.jar`。 此步驟會重新啟動JEE部署的sling屬性。 等候在`http://<server name>:<port>/lc/system/console/bundles`安裝的組合將狀態顯示為&#x200B;**作用中**。

   >如果狀態仍為&#x200B;**InActive**，請重新啟動   來自&#x200B;**服務主控台**&#x200B;的&#x200B;**JBoss®**。


1. 安裝使用步驟5下載的`javax.mail-1.5.6.redhat-1.jar`檔案。

1. 從&#x200B;**服務主控台**&#x200B;停止&#x200B;**JBoss®**，並將下列屬性附加至&#x200B;**Sling.properties**&#x200B;檔案：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新啟動&#x200B;**JBoss®**。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。
