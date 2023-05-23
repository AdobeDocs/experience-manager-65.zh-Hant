---
title: 成員繳費限制
seo-title: Member Contribution Limits
description: 貢獻限制功能允許您限制用於防止垃圾郵件的貢獻
seo-description: Contribution limits feature lets you limit the contributions to protect against spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 成員繳費限制 {#member-contribution-limits}

## 概觀 {#overview}

貢獻限制功能提供了限制社區成員貢獻的能力，作為防止垃圾郵件的一種手段。

當成員受限時，任何超出允許的貢獻數的帖子都會導致警報超出限制並拒絕該帖子。 然後，社區成員可以轉到社區消息中心並聯繫社區經理，該經理可以在適當時刪除限制。

可以從 [成員控制台](members.md) 和/或配置為在站點訪問者成為新成員時自動啟用。

使用「成員」控制台，社區管理員可以隨時主動刪除成員的貢獻限制，或當成員向提出此類請求的社區管理員發送消息時主動刪除。

## AEM Communities用戶生成的內容貢獻限制配置 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 確定繳款限額的特點（一個時期內的員額數）。
* 標識當達到限制時，成員將能夠發送消息的對象。
* 標識不需要約束的域。

要訪問此OSGi配置：

* 在主發佈伺服器上：
* 使用管理員權限登錄。
* 訪問 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   * 比如說， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 定位 `AEM Communities User Generated Content Contribution Limits Configuration`。
* 選擇編輯表徵圖。

![配置限制](assets/configure-limits.png)

* **[!UICONTROL 自動應用UGC繳費限制]**

   如果選中，則在用戶註冊為社區成員時自動設定貢獻限制。 這反映在社區成員的配置檔案中，可從 [成員控制台](members.md)。 從域允許清單中包含電子郵件地址的新成員從不受約束。

   未選中預設值。

* **[!UICONTROL UGC限制]**

   最大捐款數。

   預設為10個帖子。

* **[!UICONTROL UGC限制頻率]**

   約束UGC限制的時段。

   預設值為60分鐘。

* **[!UICONTROL 域]**

   一個或多個電子郵件域的允許清單。 選擇+表徵圖以建立附加條目。

   當自動應用UGC貢獻限制時，在域允許清單中具有電子郵件地址的用戶不會受到影響。 例如，如果 `mycompany.com` 添加到域清單，然後是具有電子郵件地址的成員 `me@mycompany.com` 從不限制發佈。

   預設值為空允許清單。

* **[!UICONTROL 郵件收件人]**

   能夠修改成員貢獻限制的成員的一個或多個可授權ID的清單。 選擇+表徵圖以建立附加條目。

   成員只有在達到其限制時才能聯繫到指定的成員。

   預設為沒有消息接收者。

注：預設配置在1小時內限制10個帖子。
