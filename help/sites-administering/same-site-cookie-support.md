---
title: AEM 6.5的相同網站Cookie支援
description: AEM 6.5的相同網站Cookie支援
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# AEM 6.5 {#same-site-cookie-support-for-aem-65}的相同網站Cookie支援

自80版、Chrome和更新版Safari推出Cookie安全性新模型。 此模式旨在透過名為`SameSite`的設定，對協力廠商網站Cookie的可用性引入安全控制。 如需詳細資訊，請參閱這篇[文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值(`SameSite=Lax`)可能會導致AEM執行個體或服務之間的驗證無法運作。 這是因為這些服務的網域或URL結構可能不受此Cookie原則的限制。

為了解決此問題，您需要為登入Token將SameSite Cookie部落設定為`None`。

您可以依照下列步驟來執行此操作：

1. 前往`http://serveraddress:serverport/system/console/configMgr`的Web主控台
1. 搜尋並按一下&#x200B;**AdobeGranite代號驗證處理常式**
1. 將登入代號Cookie **的** SameSite屬性設為`None`，如下圖所示
   ![samesite](assets/samesite1.png)
1. 按一下儲存
1. 更新此設定並重新登出使用者後，`login-token` Cookie即會設定`None`屬性，並納入跨網站請求中。
