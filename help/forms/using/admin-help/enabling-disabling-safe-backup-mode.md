---
title: 啟用和禁用安全備份模式
seo-title: Enabling and disabling safe backup mode
description: 在「備份設定」頁上，您可以以安全備份模式操作AEM表單，以便可靠地備份資料庫和全局文檔儲存(GDS)(GDS)目錄。 了解如何啟用和禁用安全備份模式。
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 啟用和禁用安全備份模式 {#enabling-and-disabling-safe-backup-mode}

在「備份設定」頁上，您可以以安全備份模式操作AEM表單，以便可靠地備份資料庫和全局文檔儲存(GDS)(GDS)目錄。

雖然AEM表單處於安全備份模式，但它正常運行，只是它沒有主動從GDS目錄中刪除檔案。

>[!NOTE]
>
>設定此選項不會備份您的系統；它為備份準備了系統。

## 啟用安全備份模式 {#enable-safe-backup-mode}

1. 在管理控制台中，按一下「設定」>「核心繫統設定」>「備份設定」。
1. 在「備份設定」頁上，選擇「在安全備份模式下操作」 ，然後按一下「確定」。

>[!NOTE]
>
>如果系統已在安全備份模式下運行，則按一下「確定」時將不會建立新保留。

## 禁用安全備份模式 {#disable-safe-backup-mode}

1. 在管理控制台中，按一下「設定」>「核心繫統設定」>「備份設定」。
1. 在「備份設定」頁上，取消選擇「在安全備份模式下操作」，然後按一下「確定」。
