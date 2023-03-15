---
title: 會員供款限制
seo-title: Member Contribution Limits
description: 貢獻限制功能可讓您限制貢獻內容，以防垃圾郵件
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

# 會員供款限制 {#member-contribution-limits}

## 概觀 {#overview}

貢獻限制功能可限制社群成員的貢獻，作為防止垃圾郵件的工具。

當成員受限時，超過允許的貢獻數的任何帖子都會導致超出限制且帖子被拒絕的警報。 然後，社區成員可以前往社區消息中心並聯繫社區管理員，該管理員可以在適當時移除限制。

貢獻限制可從 [成員控制台](members.md) 和/或設為當網站訪客成為新成員時自動啟用。

使用「成員」控制台，社區管理員可以隨時主動為成員刪除貢獻限制，或者在成員向提出此請求的社區管理員發送消息時主動刪除。

## AEM Communities使用者產生的內容貢獻限制設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 定義供款限制的特點（一個時段內的員額數）。
* 標識當達到限制時，成員將能夠發送消息的對象。
* 識別永遠不需要限制的網域。

要達到此OSGi配置：

* 在主要發佈者上：
* 以管理員權限登入。
* 存取 [Web主控台](../../help/sites-deploying/configuring-osgi.md).

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找出 `AEM Communities User Generated Content Contribution Limits Configuration`.
* 選取編輯圖示。

![設定限制](assets/configure-limits.png)

* **[!UICONTROL 自動套用UGC貢獻限制]**

   如果勾選此選項，當使用者註冊為社群成員時，會自動對使用者設定貢獻限制。 這會反映在社群成員的設定檔中，並可從 [成員控制台](members.md). 從允許的網域清單中取得電子郵件地址的新成員永不受限。

   預設為未勾選。

* **[!UICONTROL UGC限制]**

   最大貢獻數。

   預設為10篇貼文。

* **[!UICONTROL UGC限制頻率]**

   限制UGC限制的時段。

   預設為60分鐘。

* **[!UICONTROL 網域]**

   一或多個電子郵件網域的允許清單。 選取+圖示以進行其他項目。

   自動套用UGC貢獻限制時，網域允許清單中含有電子郵件地址的使用者不受影響。 例如，如果網域 `mycompany.com` 會新增至網域清單，然後是具有電子郵件地址的成員 `me@mycompany.com` 從不限制發佈。

   預設為空的允許清單。

* **[!UICONTROL 傳訊收件者]**

   可修改成員貢獻限制的成員的一個或多個可授權ID的清單。 選取+圖示以進行其他項目。

   成員只能在達到其限制時與指定成員聯繫。

   預設值為無訊息收件者。

注意：預設設定會導致1小時內限制為10篇貼文。
