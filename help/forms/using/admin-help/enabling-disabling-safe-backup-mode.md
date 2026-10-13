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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%
---
# 啟用和停用安全備份模式 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

在「備份設定值」頁面上，您可以在安全的備份模式中操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。

AEM表單處於安全備份模式時，除了不會主動從GDS目錄移除檔案外，其他功能仍會正常運作。

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
