---
title: AEM Communities發行說明
description: Adobe Experience Manager 6.5 Communities專屬發行說明。
exl-id: 8eeaf917-aac8-4f5c-be12-d2a6783c5c5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# AEM Communities發行說明{#aem-communities-release-notes}

閱讀AEM Communities 6.4版以來的改善項目。 若要深入了解新功能，請參閱[AEM 6.5 Communities使用手冊](https://helpx.adobe.com/experience-manager/6-4/communities/user-guide.html)。

若要取得最新版本，請參閱檔案的[ Deploying Communities](https://helpx.adobe.com/in/experience-manager/6-4/help/communities/deploy-communities.html#LatestReleases)區段。

## 主要增強功能{#major-enhancements}

### 增強社群參與{#enhancements-to-community-engagement}

**@Mentions支**
援AEM Communities現在可讓註冊使用者在「使用者產生的內容」中標籤（提及）其他已註冊成員，以吸引其注意。接著會通知標籤（提及的）成員，並附上對應使用者產生內容的深層連結。 不過，使用者可以選擇停用/啟用網路和電子郵件通知。

![提及次數支援](assets/at-mentions.png)

社群使用者不需要搜尋其名字、姓氏或使用者名稱，即可查看是否有任何人與他們取得聯繫或需要他們注意。 此外，它允許UGC作者尋求特定註冊用戶的回應，這些註冊用戶能夠最好地解決問題並添加輸入。

社群管理員需要在社群元件上&#x200B;**啟用提及**，讓已註冊的使用者能夠在這些元件上使用功能。

**群組訊息**

已註冊的社群成員現在可以透過單一電子郵件組合大量傳送直接訊息給群組，而非個別傳送相同的訊息給群組成員。 要允許[組消息傳送](/help/communities/configure-messaging.md)，請啟用[消息傳送操作服務](/help/communities/messaging.md#group-messaging)的兩個實例。

![群組訊息](assets/group-messaging.png)

### 大量協調{#enhancements-to-bulk-moderation}的增強功能

大量協調中的自訂篩選器

[自訂](/help/communities/moderation.md#custom-filters) 篩選器現在可開發，並新增至「大量協調」UI。

[Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)中提供[示範透過標籤篩選的範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)。 此專案可作為開發類似自訂篩選器的基礎。

![自訂篩選器](assets/custom-tag-filter.png)

**大量協調中的清單檢視**

已提供新的「清單檢視」，並改善UI，以大量協調顯示「使用者產生的內容」項目。

![清單檢視中的大量協調](assets/list-view-moderation.png)

### 增強網站和群組管理{#enhancements-to-site-and-group-management}

**作者端網站和群組管理員**

AEM 6.5以後的Communities允許對不同的社群網站和群組/巢狀群組進行分散管理（和管理）。 托管多個社群網站和巢狀群組的組織現在可以在建立網站（和群組）時，為作者端的管理員角色選取成員。

![站點管理員](assets/site-admin.png)

網站管理員可以在任何階層層級建立群組，並成為預設管理員。 其他群組管理員稍後可移除這些管理員。 群組管理員可以管理其群組G1，並在G1下建立巢狀子群組。

### 啟用{#enhancements-to-enablement}的增強功能

**SCORM 2017.1支援**

AEM 6.5 Communities的啟用功能支援「可共用內容物件參考模型」 [(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)引擎。

* 啟用元件的鍵盤導覽支援
* AEM Communities中的啟用元件（例如目錄和課程播放、工作總攬、檔案程式庫）支援鍵盤導覽，以改善協助工具。

### 其他增強功能 {#other-enhancements}

* Solr 7支援
* AEM 6.5社群在設定MSRP和DSRP時，支援Apache Solr 7.0版的搜尋平台。
