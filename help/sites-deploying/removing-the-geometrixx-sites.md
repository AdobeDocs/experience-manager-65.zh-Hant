---
title: 移除Geometrixx網站
description: 瞭解如何移除範例Geometrixx內容。
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 移除Geometrixx網站{#removing-the-geometrixx-sites}

AEM隨附一組範例Geometrixx網站。 您可以透過以下方式移除此範例內容： **封裝管理員**.

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

若要移除個別套件，只要按一下 **解除安裝** 在該套件上。

此外，還有超級套件：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此套件包含上述所有個別套件。 若要一次移除所有geometrixx相關內容，請按一下 **解除安裝** 在此封裝上。 超級套件會進入解除安裝狀態，而所有個別套件會從「套件管理員」檢視中消失。

您現在有「空白」AEM執行個體，沒有任何示範網站。

>[!NOTE]
>
>升級時，會自動重新安裝Geometrixx網站。 如果您不想要這些範例，請在升級後移除Geometrixx網站。

