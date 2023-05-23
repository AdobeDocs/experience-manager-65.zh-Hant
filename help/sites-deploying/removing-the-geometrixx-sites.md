---
title: 刪除Geometrixx站點
seo-title: Removing the Geometrixx Sites
description: 瞭解如何刪除示例Geometrixx內容。
seo-description: Learn how to remove the sample Geometrixx content.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 刪除Geometrixx站點{#removing-the-geometrixx-sites}

附AEM帶一組樣本Geometrixx網站。 您可以通過 **包管理器**。

與幾何相關的單個包包括：

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

要刪除單個包，請按一下 **卸載** 包上的。

還有一個超級包：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此包包含上述所有單個包。 要同時刪除與幾何相關的所有內容，請按一下 **卸載** 在這包里。 超級軟體包將進入卸載狀態，所有單個軟體包都將從軟體包管理器視圖中消失。

您現在有一個「空」實AEM例，沒有任何演示站點。

>[!NOTE]
>
>升級時，將自動重新安裝geometrix站點。 如果不需要這些示例，則升級後可能需要刪除geometrixx網站。

