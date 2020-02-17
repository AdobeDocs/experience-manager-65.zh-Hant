---
title: 會員繳費限制
seo-title: 會員繳費限制
description: 貢獻限制功能可讓您限制貢獻，以防垃圾郵件
seo-description: 貢獻限制功能可讓您限制貢獻，以防垃圾郵件
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 會員繳費限制 {#member-contribution-limits}

## 概覽 {#overview}

貢獻限制功能可限制社群成員的貢獻，以防垃圾郵件。

當會員受限時，任何超過允許之稿數的貼文，都會產生超出限制且貼文遭拒的警告。 然後，社群成員可前往社群訊息中心，並聯絡社群經理，如有需要，可移除限制。

貢獻限制可以從「成員」控制台 [單獨啟用](members.md) ，和／或設定為在網站訪客成為新成員時自動啟用。

使用「成員」控制台，社區管理員可以隨時主動為成員刪除貢獻限制，或在成員向提出此類請求的社區管理員發送消息時主動刪除貢獻限制。

## AEM Communities使用者產生的內容貢獻限制設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置

* 定義繳費限制的特點（一個時段內的員額數）
* 標識成員在達到限制時能夠向誰發送消息
* 識別不需要限制的網域

要訪問此OSGi配置：

* 在主要發行者上
* 以管理員權限登入
* 存取 [Web Console](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 尋找 `AEM Communities User Generated Content Contribution Limits Configuration`
* 選取編輯圖示

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL 自動套用UGC貢獻限制]**

   如果勾選，會在使用者註冊為社群成員時，自動設定其貢獻限制。 這反映在社區成員的配置檔案中，可以從成員控制台啟用／禁 [用](members.md)。 新成員的電子郵件位址來自白名單網域，不受限制。

   預設為未勾選。

* **[!UICONTROL UGC限制]**

   貢獻的最大數目。

   預設為10篇貼文。

* **[!UICONTROL UGC限制頻率]**

   限制UGC限制的時段。

   預設值為60分鐘。

* **[!UICONTROL 網域]**

   一或多個電子郵件網域的白名單。 選擇+表徵圖以進行其他條目。

   當自動套用UGC貢獻限制時，在白名單網域中擁有電子郵件地址的使用者不受影響。 例如，如果網域 `mycompany.com` 新增至網域清單，則永遠不會限制具有電子郵件地址 `me@mycompany.com` 的成員張貼。

   預設為空白清單。

* **[!UICONTROL 訊息收件者]**

   可修改成員貢獻限制的成員的一個或多個可授權ID的清單。 選擇+表徵圖以進行其他條目。

   成員只能在達到其限制時向指定成員伸出援手。

   預設為無訊息收件者。

注意：預設設定會在一小時內限制10篇貼文。
