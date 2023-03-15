---
title: AEM 6.5的相同網站Cookie支援
description: AEM 6.5的相同網站Cookie支援
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: f7a4907ca6ce8ecaff9ef1fdf99ec0951ff497e0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 74%

---

# AEM 6.5的相同網站Cookie支援 {#same-site-cookie-support-for-aem-65}

從 80 版本開始，Chrome 和之後的 Safari 引入了一種新的 cookie 安全性模型。 此模式的設計目的，是透過以下的設定，對協力廠商網站Cookie的可用性引入安全控制： `SameSite`. 如需詳細資訊，請參閱本[文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值 (`SameSite=Lax`) 可能會導致 AEM 執行個體或服務之間的驗證無法運作。這是因為這些服務的網域或 URL 結構可能不受此 cookie 原則的約束。

為了避免此問題，您必須設定 `SameSite` cookie屬性至 `None` 登入Token。

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
