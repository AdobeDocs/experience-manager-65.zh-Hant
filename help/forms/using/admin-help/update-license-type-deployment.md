---
title: 更新部署的許可證類型
seo-title: Update the license type for the deployment
description: 使用管理控制台中的「更改許可證」頁更新部署的許可證類型。
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 更新部署的許可證類型 {#update-the-license-type-for-the-deployment}

在AEM表單安裝程式中，您使用Configuration Manager來設定和部署您需要的AEM表單模組。 預設情況下，這些模組配置了60天評估許可證。 使用管理控制台中的「更改許可證」頁可更改部署的許可證類型。 當前部署的模組將顯示在「更改許可證」頁上。

「更改許可證」頁顯示有關許可證的資訊：

* 當前許可證類型
* 上次更新許可證的日期和時間
* 執行上次更新的人員
* 許可證的當前狀態
* 安裝AEM表單的日期
* 當前許可證的到期日

>[!NOTE]
>
>許可證更改適用於所有已部署的模組。 在更改許可類型之前，請取消部署任何未獲許可的模組。 如果部署的模組清單包含您從Adobe購買的模組以外的模組，則不要選擇生產許可證類型。

## 更新許可證類型 {#update-the-license-type}

1. 在管理控制台中，按一下「授權」。
1. 閱讀AEM Forms最終用戶許可協定，如果您同意協定的條款，請選擇「我接受」，然後按一下「下一步」。
1. 在「更改許可證」頁上，選擇許可證類型：

   * **EVAL:** 60天評估許可證
   * **開發：** 永久開發授權
   * **NFR:** 2年評估許可
   * **IDEV:** 訂購Adobe Developer計畫1年
   * **生產：** 永久授權

1. 選擇是，許可證更改對所有已部署的模組有效。
1. 按一下「確認許可證更改」。 此時會出現一則訊息，指出授權已成功更新。
