---
title: 為啟用SSL的LDAP伺服器配置用戶管理
seo-title: Configure User Management for an SSL-enabled LDAP server
description: 瞭解如何為啟用SSL的LDAP伺服器配置用戶管理，以使同步能夠通過LDAPS正常工作。
seo-description: Learn how  to configure User Management for an SSL-enabled LDAP server to enable synchronization to work properly over LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 為啟用SSL的LDAP伺服器配置用戶管理 {#configure-user-management-for-an-ssl-enabled-ldap-server}

要使同步在LDAPS上正常工作，證書頒發機構(CA)頒發的LDAP證書必須存在於應用程式伺服器的Java運行時環境(JRE)中。 將證書導入應用程式伺服器的JRE cacerts檔案，該檔案通常位於 *[JAVA_HOME]*/jre/lib/security/cacerts目錄。

1. 在目錄伺服器上啟用SSL。 有關詳細資訊，請參閱目錄供應商提供的文檔。
1. 從目錄伺服器導出客戶端證書。
1. 使用keytool程式將客戶端證書檔案導入Forms應用程式伺服器的預設Java虛擬機(JVM™)證AEM書儲存中。 此任務的過程因JVM和客戶端安裝路徑而異。 例如，如果將BEA WebLogic Server與JDK 1.5一起使用，請在命令提示符下鍵入以下文本：

   `keytool -import -alias`*別名* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 出現提示時，鍵入密碼。 (對於Java，預設口令為 `changeit`。) 出現一條消息，表明已成功導入證書。
1. 出現提示時，鍵入 `Yes` 信任證書。
1. 在「用戶管理」中啟用SSL，並在配置目錄設定時，為SSL選項選擇「是」並相應更改埠設定。 預設埠號為636。

>[!NOTE]
>
>如果您在使用SSL時遇到任何問題，請使用LDAP瀏覽器檢查在使用SSL時是否可以訪問LDAP系統。 如果LDAP瀏覽器無法訪問，則您的證書或應用程式伺服器配置不正確。 如果LDAP瀏覽器工作正常，並且您仍然遇到問題，則用戶管理配置不正確。
