---
title: 瞭解建立行銷活動時的分段
description: 細分是建立行銷活動時的關鍵考量。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---

# 了解分段{#understanding-segmentation}

細分是建立行銷活動時的關鍵考量。 通常，在開始行銷活動之前，您必須先定義區段。

網站訪客造訪網站時，有不同的興趣和目標。 瞭解這些目標並達到預期是線上行銷的重要成功因素。

區段可透過分析和描述訪客的以下專案來協助實現此目標：

* 網站上的活動
* 側面像
* 其他網站上的活動

接著，內容就可以鎖定至訪客的需求和興趣，實際取決於他們相符的區段。

## 使用分段 {#using-segmentation}

區段是在[設定分段](/help/sites-administering/campaign-segmentation.md)中定義。 它們可用來控管特定目標對象看到的實際內容。

## 區段術語 {#segmentation-terminology}

在討論區段時，會使用下列術語：

**訪客** — 訪客是造訪網站的人。 該人員的造訪通常從反向連結頁面開始，然後進入您自己的網站上的一或多個頁面檢視。 可從該人員造訪的詳細資訊建立行為設定檔。

**使用者** — 使用者是在網站註冊以接收帳戶設定檔的訪客。 為了產生設定檔，他們提供額外的身分識別，例如電子郵件地址和性別等。 您也可以收集其他資訊，包括社群活動和購買模式等。 根據設定檔中提供的資訊，可以建立人口統計設定檔。

**特徵** — 特徵是訪客的特徵或屬性，可用來判斷特定區段中的成員資格。

**區段** — 區段是共用特定特徵的訪客集合。 區段應該與眾不同，與其他區段至少要有重疊。

**行為特徵** — 行為特徵是與訪客在網站上的行為相關的特徵。 這些類別包括：

* 您網站中的興趣；包括瀏覽的頁面和購買的產品。
* 在反向連結網站上的興趣；包括使用的搜尋詞或點選的廣告。
* 在其他網站上的興趣；使用Spyjax之類的工具來決定。
* 訪客忠誠度；造訪持續時間、造訪頻率。

**人口統計特徵** — 這些是選取的母體特徵，包括：

* 年齡
* 收入
* 系列大小
* 婚姻狀況
* 性別
* 位置

**衍生特徵** — 某些人口統計特徵在未註冊的情況下很難判斷，但可透過結合行為和人口統計特徵來衍生。

例如，將反向連結URL （作為行為特徵）與人口統計資料(從例如[Google Ad Planner](https://www.google.com/adplanner/)之類的工具取得)結合，網站擁有者便可匯出其訪客的人口統計特徵。

**子區段** — 一個區段可以劃分為幾個子區段。 可透過定義其他特徵來達成此目的。

**Teaser頁面** - Teaser頁面已導向特定對象。 它包含可以在Teaser段落中使用的可重複使用內容。

**行銷活動** — 行銷活動是Teaser頁面和電子郵件行銷頁面的集合，例如電子報或邀請。 通常，行銷活動會執行一段有限的時間，並由其他行銷活動取代。

**Teaser段落** — 這是從另一個相依於選取策略的頁面提取內容的段落。 此選擇策略可考慮區段和行銷活動。

**清單** — 已從已註冊使用者的區段中擷取清單。 例如，用來控制Teaser段落內容的位置。

>[!NOTE]
>
>如需Adobe Experience Manager中區段的詳細資訊，請參閱[區段](/help/sites-administering/campaign-segmentation.md)。
