---
title: 移除Geometrixx網站
seo-title: 移除Geometrixx網站
description: 瞭解如何移除範例Geometrixx內容。
seo-description: 瞭解如何移除範例Geometrixx內容。
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# 移除Geometrixx網站{#removing-the-geometrixx-sites}

AEM隨附一組範例Geometrixx網站。 您可以透過套件管理員移除此 **範例內容**。

個別geometrixx相關套件包括：

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

若要移除個別封裝，請按一下該封裝 **上的「解除** 安裝」。

此外還有一套超級套件：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此套件包含上述所有個別套件。 若要一次移除所有與geometrixxx相關的內容，請按一下 **此套件上的** 「解除安裝」。 super-package將進入解除安裝狀態，而所有個別封裝都會從封裝管理器檢視中消失。

您現在有一個「空」的AEM例項，沒有任何展示網站。

>[!NOTE]
>
>升級時，geometrixx網站會自動重新安裝。 如果您不想要這些範例，在升級後可能需要移除geometrixx網站。

