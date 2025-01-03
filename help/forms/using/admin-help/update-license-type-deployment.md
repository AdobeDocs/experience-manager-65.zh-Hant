---
title: 更新部署的授權型別
description: 使用管理主控台中的「變更授權」頁面，更新部署的授權型別。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 更新部署的授權型別 {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

在AEM表單安裝過程中，您使用Configuration Manager來設定及部署所需的AEM表單模組。 預設情況下，這些模組會設定60天的評估授權。 使用管理主控台中的「變更授權」頁面來變更部署的授權型別。 目前部署的模組會顯示在「變更許可證」頁面上。

「變更許可證」頁面會顯示有關您的許可證的資訊：

* 目前的授權型別
* 上次更新授權的日期和時間
* 上次更新的執行者
* 授權的目前狀態
* AEM表單的安裝日期
* 目前授權到期的日期

>[!NOTE]
>
>授權變更適用於所有已部署的模組。 在變更授權型別之前，請取消部署任何未授權的模組。 如果部署的模組清單包含您從Adobe購買的模組以外的模組，請勿選取生產授權型別。

## 更新授權型別 {#update-the-license-type}

1. 在管理控制檯中，按一下授權。
1. 閱讀AEM Forms一般使用者授權合約，如果您同意合約條款，請選取「我接受」，然後按一下「下一步」。
1. 在「變更許可證」頁面上，選取許可證型別：

   * **評估：** 60天評估授權
   * **開發：**&#x200B;永久開發授權
   * **NFR：** 2年評估授權
   * **IDEV：** Adobe Developer方案的1年訂閱
   * **生產：**&#x200B;永久授權

1. 選取「是，授權變更對所有已部署的模組都有效」。
1. 按一下「確認許可證變更」。 系統會顯示訊息，指出授權已成功更新。
