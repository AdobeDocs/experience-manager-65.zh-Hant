---
title: 設定SSL概述
seo-title: Overview of configuring SSL
description: 了解如何設定SSL以增強通訊安全性。
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

# 設定SSL概述 {#overview-of-configuring-ssl}

您可以建立安全套接字層(SSL)憑據，並在應用程式伺服器上配置SSL以增強與應用程式伺服器通信的安全性。

作為安全產品，Rights Management需要配置SSL。 設定SSL憑證時，請確定您只使用RSA金鑰。 不支援具有DSA金鑰的SSL憑證。

提供的資訊適用於統包、自動和手動安裝。 此範例提供設定SSL的方法。 您也可以使用其他更適合您的網路或組織的方法。

>[!NOTE]
>
>建議您完成AEM表單模組的安裝、設定和部署，並在應用程式伺服器上設定SSL之前，確定產品正確運作。

>[!NOTE]
>
>建立SSL安全證書和憑據時，請使用與運行應用程式伺服器時相同的用戶帳戶權限。 如果應用程式伺服器是使用其他用戶權限運行的，則當ContentRootURI指向https時，表單可能無法正確呈現PDFForm格式轉譯。

如果您有啟用SSL的LDAP伺服器，請配置「用戶管理」以使用它。 (請參閱 [為啟用SSL的LDAP伺服器配置用戶管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
