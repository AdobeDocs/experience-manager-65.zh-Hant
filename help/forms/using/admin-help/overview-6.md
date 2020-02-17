---
title: 設定SSL的概述
seo-title: 設定SSL的概述
description: 瞭解如何設定SSL來增強通訊的安全性。
seo-description: 瞭解如何設定SSL來增強通訊的安全性。
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定SSL的概述 {#overview-of-configuring-ssl}

您可以建立安全通訊端層(SSL)憑證，並在應用程式伺服器上設定SSL，以增強與應用程式伺服器通訊的安全性。

身為安全產品，Rights Management需要設定SSL。 在配置SSL證書時，請確保只使用RSA密鑰。 不支援具有DSA金鑰的SSL憑證。

提供的資訊適用於統包、自動和手動安裝。 它提供了配置SSL的方法示例。 您也可以使用更適合您網路或組織的其他方法。

>[!NOTE]
>
>建議您完成AEM表單模組的安裝、設定和部署，並在應用程式伺服器上設定SSL之前，確定產品已正確執行。

>[!NOTE]
>
>建立SSL安全憑證和憑證時，請使用與您用來執行應用程式伺服器相同的使用者帳戶權限。 如果應用程式伺服器是使用其他使用者權限執行，當ContentRootURI指向https時，表單可能無法正確呈現PDFForm轉譯。

如果您有啟用SSL的LDAP伺服器，請設定「使用者管理」以搭配使用。 (請參 [閱為啟用SSL的LDAP伺服器配置用戶管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。)
