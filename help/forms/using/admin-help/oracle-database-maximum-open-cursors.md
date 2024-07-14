---
title: oracle資料庫最大開啟游標臨界值
description: 瞭解如何在Oracle中設定開啟游標的最大值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# oracle資料庫最大開啟游標臨界值 {#oracle-database-maximum-open-cursors-threshold}

若要設定Oracle中開啟游標的最大值，您可能必須將此值調整為適合您應用程式的數字。 很明顯，在中等負載下，平均開啟的游標為2700。 建議您從上限3000開始。 如需詳細資訊，請前往[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)。
