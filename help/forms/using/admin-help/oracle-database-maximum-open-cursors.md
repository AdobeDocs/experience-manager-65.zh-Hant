---
title: Oracle資料庫最大開啟游標臨界值
description: 瞭解如何在Oracle中設定開啟游標的最大值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
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
source-wordcount: '88'
ht-degree: 0%
---
# Oracle資料庫最大開啟游標臨界值 {#oracle-database-maximum-open-cursors-threshold}

若要在Oracle中設定開啟游標的最大值，您可能必須將此值調整為適合您應用程式的數字。 很明顯，在中等負載下，平均開啟的游標為2700。 建議您從上限3000開始。 如需詳細資訊，請前往[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)。
