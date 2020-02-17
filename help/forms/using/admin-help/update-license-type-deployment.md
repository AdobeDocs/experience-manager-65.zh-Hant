---
title: 更新部署的授權類型
seo-title: 更新部署的授權類型
description: 使用管理控制台中的「變更授權」頁面，更新部署的授權類型。
seo-description: 使用管理控制台中的「變更授權」頁面，更新部署的授權類型。
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更新部署的授權類型 {#update-the-license-type-for-the-deployment}

在AEM表單安裝程式中，您使用Configuration manager來設定和部署您需要的AEM表單模組。 依預設，這些模組已設定60天試用授權。 使用管理控制台中的「變更授權」頁面，變更部署的授權類型。 當前部署的模組顯示在「更改許可證」頁上。

「變更授權」頁面會顯示您的授權的相關資訊：

* 目前的授權類型
* 上次更新授權的日期和時間
* 執行上次更新的人員
* 授權的目前狀態
* 安裝AEM表單的日期
* 目前授權的到期日

>[!NOTE]
>
>許可證更改適用於所有已部署的模組。 在您變更授權類型之前，請先解除部署任何未授權的模組。 如果部署的模組清單中包含的模組不是您從Adobe購買的模組，請勿選取「生產」授權類型。

## 更新授權類型 {#update-the-license-type}

1. 在管理控制台中，按一下「授權」。
1. 閱讀AEM表單使用者授權合約，如果您同意合約條款，請選取「我接受」，然後按「下一步」。
1. 在「變更授權」頁面上，選取授權類型：

   * **** EVAL:60天試用授權
   * **** 開發人員：永久開發授權
   * **** NFR:2年評估授權
   * **** IDEV:Adobe開發人員計畫的1年訂閱
   * **** 生產：永久授權

1. 選擇「是」,「許可證更改」對所有已部署模組有效。
1. 按一下「確認授權變更」。 出現訊息，指出授權已成功更新。

