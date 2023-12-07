---
title: 設定啟用SSL之LDAP伺服器的使用者管理
description: 瞭解如何為啟用SSL的LDAP伺服器設定「使用者管理」，讓同步化能夠透過LDAPS正常運作。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 設定啟用SSL之LDAP伺服器的使用者管理 {#configure-user-management-for-an-ssl-enabled-ldap-server}

為了使同步能夠透過LDAPS正常運作，憑證授權單位(CA)簽發的LDAP憑證必須存在於應用程式伺服器的Java執行階段環境(JRE)中。 將憑證匯入應用程式伺服器的JRE cacerts檔案，該檔案通常位於 *[JAVA_HOME]*/jre/lib/security/cacerts目錄。

1. 在目錄伺服器上啟用SSL。 如需詳細資訊，請參閱目錄廠商提供的檔案。
1. 從目錄伺服器匯出使用者端憑證。
1. 使用keytool程式將使用者端憑證檔案匯入AEM Forms應用程式伺服器的預設Java虛擬機器器(JVM™)憑證存放區。 此工作的程式會因您的JVM和使用者端安裝路徑而異。 例如，如果您使用BEA WebLogic Server搭配JDK 1.5，請從命令提示字元輸入以下文字：

   `keytool -import -alias`*別名* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 出現提示時，輸入密碼。 (Java的預設密碼為 `changeit`.) 系統會顯示訊息，指出憑證已成功匯入。
1. 出現提示時，鍵入 `Yes` 以信任憑證。
1. 在「使用者管理」中啟用SSL，並在設定目錄設定時，為SSL選項選取「是」，然後相應地變更連線埠設定。 預設連線埠號碼為636。

>[!NOTE]
>
>如果您在使用SSL時遇到任何問題，請使用LDAP瀏覽器來檢查在使用SSL時是否可以存取LDAP系統。 如果LDAP瀏覽器無法取得存取權，表示您的憑證或應用程式伺服器未正確設定。 如果LDAP瀏覽器正常運作，而您仍然遇到問題，則表示未正確設定「使用者管理」。
