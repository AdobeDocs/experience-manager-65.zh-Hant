---
title: 6.5版的同AEM一站點Cookie支援
description: 6.5版的同AEM一站點Cookie支援
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: f7a4907ca6ce8ecaff9ef1fdf99ec0951ff497e0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 6.5版的同AEM一站點Cookie支援 {#same-site-cookie-support-for-aem-65}

自80版、Chrome和更新版Safari以來，Cookie安全性引入了新型號。 此模式旨在通過名為 `SameSite`。 有關詳細資訊，請參閱 [文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值(`SameSite=Lax`)可能導致實例AEM或服務之間的身份驗證無效。 這是因為這些服務的域或URL結構可能不在此cookie策略的約束下。

為了繞過這個，你需要設定 `SameSite` cookie屬性 `None` 的下界。

>[!CAUTION]
>
>的 `SameSite=None` 僅當協定安全(HTTPS)時才應用設定。
>
>如果協定不安全(HTTP)，則忽略該設定，伺服器將顯示以下WARN消息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以通過以下步驟添加設定：

1. 轉到Web控制台，位於 `http://serveraddress:serverport/system/console/configMgr`
1. 搜索並按一下 **Adobe花崗岩令牌驗證處理程式**
1. 設定 **登錄令牌Cookie的SameSite屬性** 至 `None`，如下圖所示
   ![三元](assets/samesite1.png)
1. 按一下「保存」
1. 更新此設定並重新註銷用戶後， `login-token` 曲奇餅 `None` 屬性集，並將包含在跨站點請求中。
