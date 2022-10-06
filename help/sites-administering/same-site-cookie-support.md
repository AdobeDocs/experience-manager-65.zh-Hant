---
title: AEM 6.5的相同網站Cookie支援
description: AEM 6.5的相同網站Cookie支援
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: f7a4907ca6ce8ecaff9ef1fdf99ec0951ff497e0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# AEM 6.5的相同網站Cookie支援 {#same-site-cookie-support-for-aem-65}

自80版、Chrome和更新版Safari推出Cookie安全性新模型。 此模式的設計目的，是透過以下的設定，對協力廠商網站Cookie的可用性引入安全控制： `SameSite`. 如需詳細資訊，請參閱 [文章](https://web.dev/samesite-cookies-explained/).

此設定的預設值(`SameSite=Lax`)可能會導致AEM例項或服務之間的驗證無法運作。 這是因為這些服務的網域或URL結構可能不受此Cookie原則的限制。

為了避免此問題，您必須設定 `SameSite` cookie屬性至 `None` 登入Token。

>[!CAUTION]
>
>此 `SameSite=None` 只有在通訊協定安全(HTTPS)時，才會套用設定。
>
>如果通訊協定不安全(HTTP)，則會忽略設定，而伺服器會顯示此WARN訊息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以依照下列步驟來新增設定：

1. 前往Web主控台： `http://serveraddress:serverport/system/console/configMgr`
1. 搜尋並按一下 **AdobeGranite代號驗證處理常式**
1. 設定 **登入代號Cookie的SameSite屬性** to `None`，如下圖所示
   ![samesite](assets/samesite1.png)
1. 按一下儲存
1. 更新此設定並將使用者登出並重新登入後， `login-token` cookie會 `None` 屬性集和將包含在跨網站請求中。
