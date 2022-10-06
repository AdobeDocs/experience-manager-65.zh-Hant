---
title: 新增網域
seo-title: Adding domains
description: 了解如何使用網域管理設定和網域名稱和ID的一般考量，新增企業、本機或混合式網域。
seo-description: Learn how to add an enterprise, local, or hybrid domain using Domain Management settings and general considerations for domain names and IDs.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# 新增網域 {#adding-domains}

## 新增企業網域 {#add-an-enterprise-domain}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建企業域」。
1. 在ID框中，鍵入域的唯一標識符，在「名稱」框中，為域鍵入描述性名稱。 (請參閱 [網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 指定是否啟用帳戶鎖定。 (請參閱 [配置帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 預設情況下，將選中「啟用帳戶鎖定」。
1. 按一下「添加身份驗證」 ，然後在「身份驗證提供程式」清單中，根據您的組織使用的身份驗證機制選擇一個提供程式。 可能的值是LDAP、Kerberos、SAML或自定義身份驗證提供程式。

   如果選擇LDAP，則可以使用目錄配置中指定的LDAP伺服器，也可以選擇不同的LDAP伺服器以用於身份驗證。 如果選擇不同的伺服器，則您的用戶必須存在於兩個LDAP伺服器上。

1. 提供頁面上需要的任何其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 添加目錄或自定義服務提供程式介面(SPI)。 (請參閱 [添加目錄或自定義SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 按一下「完成」，然後按一下「確定」。

建立企業域後，請手動同步目錄或建立觸發器以執行同步，然後「用戶管理」才能使用它。 然後，您可以設定目錄同步計畫，並根據需要執行手動同步。 (請參閱 [同步目錄](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## 新增本機網域 {#add-a-local-domain}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建本地域」。
1. 在ID框中，鍵入域的唯一標識符，並在「名稱」框中鍵入域的描述性名稱。 (請參閱 [網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 指定是否啟用帳戶鎖定，然後按一下「確定」。 (請參閱 [配置帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 預設情況下，將選中「啟用帳戶鎖定」。

## 新增混合網域 {#add-a-hybrid-domain}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新增混合網域」 。
1. 在ID框中，鍵入域的唯一標識符，並在「名稱」框中鍵入域的描述性名稱。 (請參閱 [網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 按一下「添加身份驗證」 ，然後在「身份驗證提供程式」清單中，根據您的組織使用的身份驗證機制選擇一個提供程式。 可能的值是LDAP、Kerberos、SAML或自定義身份驗證提供程式。
1. 提供頁面上需要的任何其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 按一下「確定」，然後再次按一下「確定」。

## 網域名稱和ID的重要考量 {#important-considerations-for-domain-names-and-ids}

選擇網域名稱和ID時，請謹記下列事項：

### 一般考量 {#general-considerations}

* 使用DB2以外的資料庫提供程式時，域ID最多可以包含50個位元組。 如果您使用單位元組ASCII字元，上限為50個字元。 如果域標識符包含多位元組字元，則此限制會降低。 例如，如果您建立的網域的識別碼包含3個位元組字元，則上限為16個字元。 此外，您也無法建立包含4個位元組字元的網域。 如果您建立的網域ID超過此限制，AEM表單將會處於不穩定狀態。 要從此不穩定狀態中恢復，請參見 [刪除包含擴展字元或多位元組字元的域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」。
* 可在AEM表單中建立的企業網域和本機網域數目，取決於每個網域ID的長度。 當您新增企業或混合網域時，「使用者管理」會更新AEM表單設定檔案(config.xml)的AuthProviders節點中的configInstance字串。 configInstance字串包含與授權提供程式關聯的所有域的絕對路徑的冒號分隔清單。 此字串的大小限制為8192個字元。 達到此限制時，您無法建立其他網域。

### 使用DB2時的考量事項 {#considerations-when-using-db2}

為AEM表單資料庫使用DB2時，網域ID的允許長度上限取決於使用的字元類型：

* 100個單位元組(ASCII)（例如英文、法文或德文使用的字元）
* 50個雙位元組（例如中文、日文或韓文使用的字元）
* 25個四位元組（例如，繁體中文使用的字元）

### 使用MySQL時的考量事項 {#considerations-when-using-mysql}

使用MySQL作為AEM表單資料庫時，會套用下列限制：

* 網域ID和網域名稱僅使用單位元組(ASCII)字元。 如果您使用延伸ASCII字元，AEM表單會處於不穩定狀態，如果您嘗試刪除網域，則可能會擲回例外狀況。 要從此不穩定狀態中恢復，請參見 [刪除包含擴展字元或多位元組字元的域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」主題。
* 您無法建立兩個名稱相同但大小寫不同的網域。 例如，嘗試建立名為 *Adobe* 當名為 *adobe* 已存在導致錯誤。
* 「使用者管理」無法區分兩個網域名稱，這兩個網域名稱僅因使用延伸字元而異。 例如，如果您建立的網域名為 *abcde* 和名為 *阿布奇*，則會視為相同。

### 刪除包含擴展字元或多位元組字元的域 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 導出配置檔案，如 [匯入和匯出設定檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. 開啟配置檔案，在「域」節點下，找到名稱屬性與使用擴展字元或多位元組字元建立的域名稱相匹配的節點。 刪除與該域相關的整個節點。
1. 在資料庫中，在edcprincipaldomainentity表中搜索域：

   * 選擇 `*` 從edcprincipaldomainentity。
   * 查找包含擴展字元或多位元組字元的域名，並將其狀態設定為OBSOLETE。

1. 匯入更新的設定檔，如 [匯入和匯出設定檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
