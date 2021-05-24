---
title: 移除Geometrixx網站
seo-title: 移除Geometrixx網站
description: 了解如何移除範例Geometrixx內容。
seo-description: 了解如何移除範例Geometrixx內容。
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# 刪除Geometrixx站點{#removing-the-geometrixx-sites}

AEM隨附一組範例Geometrixx網站。 您可以透過&#x200B;**封裝管理器**&#x200B;移除此範例內容。

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

要刪除單個包，只需按一下該包上的&#x200B;**卸載**&#x200B;即可。

此外還有一個超級包：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此套件包含上述所有個別套件。 若要一次移除所有與geometrixx相關的內容，請按一下此套件上的&#x200B;**Uninstall**。 超級包將進入卸載狀態，所有單個包將從包管理器視圖中消失。

您現在有「空白」AEM例項，沒有任何示範網站。

>[!NOTE]
>
>升級時，會自動重新安裝geometrixx sites。 如果您不想要這些範例，則升級後可能需要移除geometrixx網站。

