---
title: 配置SSL概述
seo-title: Overview of configuring SSL
description: 瞭解如何通過配置SSL來增強通信的安全性。
seo-description: Learn about how to enhance security of communication by configuring SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 配置SSL概述 {#overview-of-configuring-ssl}

您可以建立安全套接字層(SSL)憑據，並在應用程式伺服器上配置SSL以增強與應用程式伺服器通信的安全性。

作為安全產品，Rights Management需要配置SSL。 配置SSL證書時，請確保僅使用RSA密鑰。 不支援帶DSA密鑰的SSL證書。

所提供的資訊適用於全包式、自動和手動安裝。 它提供了配置SSL的方法的示例。 您還可以使用更適合您的網路或組織的其他方法。

>[!NOTE]
>
>建議您完成表單模組的安裝、配置和部AEM署，並確保產品在應用程式伺服器上配置SSL之前正確運行。

>[!NOTE]
>
>建立SSL安全證書和憑據時，使用與運行應用程式伺服器時使用的用戶帳戶權限相同。 如果應用程式伺服器是使用其他用戶權限運行的，則當ContentRootURI指向https時，表單可能無法正確呈現PDFForm格式副本。

如果您有啟用了SSL的LDAP伺服器，請配置「用戶管理」以使用它。 (請參閱 [為啟用SSL的LDAP伺服器配置用戶管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。)
