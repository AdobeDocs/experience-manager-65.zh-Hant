---
title: 為啟用SSL的LDAP伺服器配置用戶管理
seo-title: 為啟用SSL的LDAP伺服器配置用戶管理
description: 瞭解如何為啟用SSL的LDAP伺服器配置用戶管理，以使同步能夠在LDAPS上正常工作。
seo-description: 瞭解如何為啟用SSL的LDAP伺服器配置用戶管理，以使同步能夠在LDAPS上正常工作。
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 為啟用SSL的LDAP伺服器配置用戶管理 {#configure-user-management-for-an-ssl-enabled-ldap-server}

為了同步才能在LDAPS上正常運作，認證授權機構(CA)核發的LDAP憑證必須存在於應用程式伺服器的Java執行階段環境(JRE)中。 將憑證匯入應用程式伺服器的JRE cacerts檔案，此檔案通常位於 *[JAVA_HOME]*/jre/lib/security/cacerts目錄中。

1. 在目錄伺服器上啟用SSL。 如需詳細資訊，請參閱目錄廠商提供的檔案。
1. 從目錄伺服器導出客戶機證書。
1. 使用keytool程式將用戶端憑證檔案匯入AEM Forms應用程式伺服器的預設Java虛擬機器(JVM™)憑證存放區。 此任務的過程會因JVM和客戶端安裝路徑而異。 例如，如果您使用BEA webLogic Server與JDK 1.5，請從命令提示符下鍵入以下文本：

   `keytool -import -alias`*別名&#x200B;*`-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 出現提示時，鍵入密碼。 (對於Java，預設密碼為 `changeit`。)出現一則訊息，指出憑證已成功匯入。
1. 出現提示時，鍵 `Yes` 入以信任憑證。
1. 在「用戶管理」中啟用SSL，並在配置目錄設定時，為SSL選項選擇「是」，並相應更改埠設定。 預設埠號為636。

>[!NOTE]
>
>如果您使用SSL時遇到任何問題，請使用LDAP瀏覽器來檢查它在使用SSL時是否可以訪問LDAP系統。 如果LDAP瀏覽器無法獲得訪問權，則您的證書或應用程式伺服器配置不正確。 如果LDAP瀏覽器工作正常，而您仍然遇到問題，則用戶管理未正確配置。

