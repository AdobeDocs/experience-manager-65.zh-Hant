---
title: 配置LDAP綁定密碼
seo-title: 配置LDAP綁定密碼
description: 了解如何先配置綁定密碼欄位，然後再將配置檔案導入其他系統。
seo-description: 了解如何先配置綁定密碼欄位，然後再將配置檔案導入其他系統。
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# 配置LDAP綁定密碼{#configure-the-ldap-bind-password}

為避免安全風險，未配置導出的配置檔案(config.xml)中的綁定密碼欄位。 將配置檔案導入其他系統之前，請確保配置此密碼。 此密碼將覆蓋儲存在資料庫中的現有密碼。 空密碼不會覆蓋現有的非空密碼值。

1. 在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔」。
1. 要將當前配置設定導出到檔案，請按一下「導出」並將配置檔案保存到其他位置。
1. 在檔案中，找到`Domains` > *[您的網域名稱]* > `DirectoryConfigs` > `LDAPGroupConfig`節點。 以下是範例：

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   鍵入`bindpassword`的值，並保存更改。

1. 在檔案中，找到`Domains` > *[您的網域名稱]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`節點。 以下是範例：

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   鍵入`bindpassword`的值，並保存更改。

1. 若要匯入更新的檔案，請在「使用者管理」中按一下「設定>匯入和匯出設定檔」。
1. 按一下「瀏覽」以查找檔案，按一下「導入」，然後按一下「確定」。
