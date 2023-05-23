---
title: 在安裝時配置管理員密碼
seo-title: Configure the Admin Password on Installation
description: 瞭解如何在安裝時更改管理AEM員密碼。
seo-description: Learn how to change the Admin Password on AEM Installation.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 在安裝時配置管理員密碼{#configure-the-admin-password-on-installation}

## 概觀 {#overview}

自6.3版以AEM來，允許在安裝新實例時使用命令行設定管理員密碼。

使用的早期版本AEM後，必須在安裝後更改管理帳戶的密碼以及其他各種控制台的密碼。

此功能增加了在實例安裝期間為儲存庫和Servlet引擎設定新管理員密碼的功能AEM，因此無需在安裝後手動執行。

>[!CAUTION]
>
>請注意，功能不包括需要手動更改密碼的Felix控制台。 有關詳細資訊，請參閱相關 [「安全核對清單」部分](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)。

## 如何使用它？ {#how-do-i-use-it}

如果您選擇通過命令行安裝，則此功AEM能將自動觸發，而不是從檔案系統資源管理器中按兩下JAR。

從命令行運行實AEM例的常規合成為：

```shell
java -jar aem6.3.jar
```

從命令行運行實例時，將顯示在安裝過程中更改管理員密碼的選項：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>只有在安裝新實例時才會出現更改管理員密碼的提AEM示。

## 使用 — nointeractive標誌 {#using-the-nointeractive-flag}

也可以選擇從屬性檔案中指定密碼。 這是通過 `-nointeractive` 組合旗`-Dadmin.password.file` 系統屬性。

下面是一個示例：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

密碼 `passwordfile.properties` 檔案需要具有以下格式：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果你只是使用 `-nointeractive` 參數 `-Dadmin.password.file` system屬性，AEM將使用預設的admin密碼，而不要求您更改它，實際上是從早期版本複製行為。 此非交互模式可用於使用安裝指令碼中的命令行進行自動安裝。
