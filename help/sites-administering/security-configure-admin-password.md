---
title: 安裝時設定管理員密碼
description: 瞭解如何在Adobe Experience Manager安裝時變更管理員密碼。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 安裝時設定管理員密碼{#configure-the-admin-password-on-installation}

## 概觀 {#overview}

自6.3版開始，Adobe Experience Manager (AEM)可在安裝新執行個體時，使用命令列設定管理員密碼。

使用舊版AEM時，在安裝後必須變更管理員帳戶的密碼以及各種其他主控台的密碼。

此功能新增在安裝AEM執行個體期間為存放庫和Servlet引擎設定新管理員密碼的功能，因此不需要在之後手動進行。

>[!CAUTION]
>
>功能未涵蓋Felix主控台，您必須手動變更其密碼。 如需詳細資訊，請參閱相關 [安全性檢查清單區段](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## 如何使用它？ {#how-do-i-use-it}

如果您選擇透過命令列安裝AEM，而不是從檔案系統總管連按兩下JAR，此功能會自動觸發。

從命令列執行AEM例項的一般語法為：

```shell
java -jar aem6.3.jar
```

從命令列執行執行個體後，您會看到可在安裝過程中變更管理員密碼的選項：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>只有在安裝新的AEM執行個體時，才會出現變更管理員密碼的提示。

## 使用 — nointeractive旗標 {#using-the-nointeractive-flag}

您也可以選擇從屬性檔案指定密碼。 這是透過使用 `-nointeractive` 標籤與 `-Dadmin.password.file` 系統屬性。

範例如下：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

內的密碼 `passwordfile.properties` 檔案的格式必須如下：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果您只使用 `-nointeractive` 引數不含 `-Dadmin.password.file` 系統屬性時，AEM會使用預設的管理密碼，而不會要求您進行變更，基本上會複製舊版的行為。 此非互動模式可用於在安裝指令碼中使用命令列的自動安裝。
