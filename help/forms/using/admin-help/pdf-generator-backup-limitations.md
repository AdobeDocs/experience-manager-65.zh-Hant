---
title: PDF Generator備份限制
description: 瞭解PDF Generator備份限制。 PDF Generator使用的暫存目錄無法備份，因為它以設定的間隔清除內容。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# PDF Generator備份限制 {#pdf-generator-backup-limitations}

無法備份PDF Generator用來轉換檔案的暫存目錄。 即使服務已正確還原，資料仍可能會遺失，因為PDF Generator會以設定的間隔檢視及清除暫存目錄的內容。
