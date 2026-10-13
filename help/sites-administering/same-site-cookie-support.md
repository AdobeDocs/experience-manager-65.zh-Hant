---
title: AEM 6.5的同網站Cookie支援
description: 瞭解AEM 6.5的同網站Cookie支援。
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 78%
---
# AEM 6.5的同網站Cookie支援 {#same-site-cookie-support-for-aem-65}

從 80 版本開始，Chrome 和之後的 Safari 引入了一種新的 cookie 安全性模型。 此模式旨在透過稱為 `SameSite` 的設定在第三方網站的 Cookie 可用性方面引入安全性控制項。 如需詳細資訊，請參閱此[web.dev - SameSite Cookie說明](https://web.dev/samesite-cookies-explained/)文章。

此設定的預設值 (`SameSite=Lax`) 可能會導致 AEM 執行個體或服務之間的驗證無法運作。 這是因為這些服務的網域或 URL 結構可能不受此 cookie 原則的約束。

若要解決此問題，您必須將登入權杖的`SameSite` Cookie屬性設定為`None`。

>[!CAUTION]
>
>`SameSite=None` 設定僅在通訊協定安全 (HTTPS) 時套用。
>
>如果通訊協定不安全 (HTTP)，則將忽略該設定並且伺服器將顯示此警告訊息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以依照下列步驟新增設定：

1. 前往 Web 主控台，位於 `http://serveraddress:serverport/system/console/configMgr`
1. 搜尋並按一下 **Adobe Granite 權杖驗證處理常式**
1. 將&#x200B;**登入權杖 cookie 的 SameSite 屬性**&#x200B;設定為 `None`，如下圖所示
   ![samesite](assets/samesite1.png)
1. 按一下「儲存」
1. 此設定一更新且使用者登出並再次登入後，`login-token` cookie 就會有 `None` 屬性集，並將包含在跨網站請求中。
