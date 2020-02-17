---
title: 在安裝時設定管理員密碼
seo-title: 在安裝時設定管理員密碼
description: 瞭解如何變更AEM安裝的管理員密碼。
seo-description: 瞭解如何變更AEM安裝的管理員密碼。
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 在安裝時設定管理員密碼{#configure-the-admin-password-on-installation}

## 概覽 {#overview}

自6.3版起，AEM允許在安裝新例項時使用命令列來設定管理員密碼。

在舊版AEM中，管理員帳戶的密碼，以及各種其他主控台的密碼，必須在安裝後加以變更。

此功能新增了在安裝AEM例項期間為儲存庫和Servlet引擎設定新管理員密碼的功能，因此不需在安裝後手動執行。

>[!CAUTION]
>
>請注意，Felix Console不包含此功能，需手動變更密碼。 如需詳細資訊，請參閱相關的安 [全性檢查清單一節](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)。

## 我要如何使用它？ {#how-do-i-use-it}

如果您選擇透過命令列安裝AEM，而不是從檔案系統檔案總管連按兩下JAR，此功能將會自動觸發。

從命令列執行AEM例項的一般合成是：

```shell
java -jar aem6.3.jar
```

從命令行運行實例時，將顯示一個選項，用於在安裝過程中更改管理員密碼：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>只有在安裝新AEM例項時，才會出現變更管理員密碼的提示。

## 使用-nointeractive標籤 {#using-the-nointeractive-flag}

您也可以選擇從屬性檔案指定密碼。 這是使用與系統屬性 `-nointeractive` 結合的標誌`-Dadmin.password.file` 。

以下是範例：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

檔案內的密 `passwordfile.properties` 碼必須具備下列格式：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果您只是使用參 `-nointeractive` 數而不使用系統屬性 `-Dadmin.password.file` ,AEM會使用預設的管理員密碼，而不會要求您變更它，實際上是從舊版複製行為。 此非互動模式可用於使用安裝指令碼中的命令行進行自動安裝。

