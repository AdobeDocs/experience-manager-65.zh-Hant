---
title: PDF產生器備份限制
seo-title: PDF產生器備份限制
description: 了解PDF產生器備份限制。
seo-description: 了解PDF產生器備份限制。
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# PDF生成器備份限制{#pdf-generator-backup-limitations}

無法備份PDF生成器用於轉換檔案的臨時目錄。 即使服務會正確還原，資料仍會遺失，因為PDF產生器會以設定的間隔檢閱並清除暫時目錄的內容。
