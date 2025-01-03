---
title: 啟用和停用安全備份模式
description: 在「備份設定值」頁面上，您可以在安全的備份模式中操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。 瞭解如何啟用和停用安全備份模式。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 啟用和停用安全備份模式 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

在「備份設定值」頁面上，您可以在安全的備份模式中操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。

當AEM表單處於安全備份模式時，它會正常運作，只是它不會主動從GDS目錄中移除檔案。

>[!NOTE]
>
>設定這個選項不會備份您的系統；它會將您的系統準備好，以進行備份。

## 啟用安全備份模式 {#enable-safe-backup-mode}

1. 在管理控制檯中，按一下「設定>核心系統設定>備份設定」。
1. 在「備份設定值」頁面上，選取「在安全備份模式下作業」，然後按一下「確定」。

>[!NOTE]
>
>如果系統已經在安全備份模式下執行，當您按一下「確定」時，將不會建立新的保留。

## 停用安全備份模式 {#disable-safe-backup-mode}

1. 在管理控制檯中，按一下「設定>核心系統設定>備份設定」。
1. 在「備份設定值」頁面上，取消選取「在安全備份模式下作業」，然後按一下「確定」。
