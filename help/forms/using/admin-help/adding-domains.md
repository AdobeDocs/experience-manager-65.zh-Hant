---
title: 添加域
seo-title: Adding domains
description: 瞭解如何使用域管理設定和域名和ID的一般注意事項來添加企業域、本地域或混合域。
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

# 添加域 {#adding-domains}

## 添加企業域 {#add-an-enterprise-domain}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下新建企業域。
1. 在ID框中，鍵入域的唯一標識符，在「名稱」框中，鍵入域的描述性名稱。 (請參閱 [域名和ID的重要注意事項](adding-domains.md#important-considerations-for-domain-names-and-ids)。)
1. 指定是否啟用帳戶鎖定。 (請參閱 [配置帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)。) 預設情況下，會選擇「啟用帳戶鎖定」。
1. 按一下添加驗證，然後在驗證提供程式清單中，根據您的組織使用的驗證機制選擇一個提供程式。 可能的值是LDAP、Kerberos、SAML或自定義身份驗證提供程式。

   如果選擇LDAP，則可以使用目錄配置中指定的LDAP伺服器，或者可以選擇其他LDAP伺服器來進行身份驗證。 如果您選擇其他伺服器，則用戶必須同時存在於兩個LDAP伺服器上。

1. 提供頁面上所需的任何其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。)
1. 添加目錄或自定義服務提供程式介面(SPI)。 (請參閱 [添加目錄或自定義SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)。)
1. 按一下「Finish（完成）」 ，然後按一下「OK（確定）」。

建立企業域後，請手動同步目錄或建立觸發器以在用戶管理可以使用該目錄之前執行同步。 然後，可以設定目錄同步計畫並根據需要執行手動同步。 (請參閱 [正在同步目錄](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories)。)

## 添加本地域 {#add-a-local-domain}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下新建本地域。
1. 在ID框中，鍵入域的唯一標識符，並在「名稱」框中，鍵入域的描述性名稱。 (請參閱 [域名和ID的重要注意事項](adding-domains.md#important-considerations-for-domain-names-and-ids)。)
1. 指定是否啟用帳戶鎖定，然後按一下確定。 (請參閱 [配置帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)。) 預設情況下，會選擇「啟用帳戶鎖定」。

## 添加混合域 {#add-a-hybrid-domain}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下「新建混合域」。
1. 在ID框中，鍵入域的唯一標識符，並在「名稱」框中，鍵入域的描述性名稱。 (請參閱 [域名和ID的重要注意事項](adding-domains.md#important-considerations-for-domain-names-and-ids)。)
1. 按一下添加驗證，然後在驗證提供程式清單中，根據您的組織使用的驗證機制選擇一個提供程式。 可能的值是LDAP、Kerberos、SAML或自定義身份驗證提供程式。
1. 提供頁面上所需的任何其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。)
1. 按一下「OK（確定）」 ，然後再次按一下「OK（確定）」。

## 域名和ID的重要注意事項 {#important-considerations-for-domain-names-and-ids}

在選擇域名和ID時，請記住以下注意事項：

### 一般考慮事項 {#general-considerations}

* 使用除DB2外的資料庫提供程式時，域ID最多可包含50個位元組。 如果使用單位元組ASCII字元，則限制為50個字元。 如果域標識符包含多位元組字元，則此限制會減少。 例如，如果建立的域的標識符包含3個位元組的字元，則限制為16個字元。 此外，您不能建立包含4位元組字元的域。 如果建立的域ID超過此限制，AEM表單將處於不穩定狀態。 要從此不穩定狀態恢復，請參見 [刪除包含擴展或多位元組字元的域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」。
* 可在表單中建立的企業域和本AEM地域的數量取決於每個域ID的長度。 添加企業域或混合域時，用戶管理會更新表單配置檔案(config.xml)的AuthProviders節AEM點中的configInstance字串。 configInstance字串包含與授權提供程式關聯的所有域的絕對路徑的冒號分隔清單。 此字串的大小限制為8192個字元。 當達到此限制時，無法建立其他域。

### 使用DB2時的注意事項 {#considerations-when-using-db2}

當將DB2用AEM於表單資料庫時，域ID的最大允許長度取決於使用的字元類型：

* 100個單位元組(ASCII)（例如，英語、法語或德語中使用的字元）
* 50個雙位元組（例如，中文、日文或韓文使用的字元）
* 25個四位元組（例如，繁體中文使用的字元）

### 使用MySQL時的注意事項 {#considerations-when-using-mysql}

當將MySQL用作表單數AEM據庫時，會應用以下限制：

* 域ID和域名只使用單位元組(ASCII)字元。 如果使用擴展ASCII字AEM符，表單將處於不穩定狀態，如果嘗試刪除域，則可能會引發異常。 要從此不穩定狀態恢復，請參見 [刪除包含擴展或多位元組字元的域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」。
* 不能建立兩個具有相同名稱但大小寫不同的域。 例如，嘗試建立名為 *Adobe* 當命名為 *adobe* 已存在導致錯誤的結果。
* 用戶管理不能區分兩個域名，這兩個域名僅在使用擴展字元時不同。 例如，如果建立的域名為 *禁用* 和名為 *布克德*，它們被認為是相同的。

### 刪除包含擴展或多位元組字元的域 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 導出配置檔案，如中所述 [導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。
1. 開啟配置檔案，在「域」節點下，找到名稱屬性與使用擴展或多位元組字元建立的域名稱匹配的節點。 刪除與該域相關的整個節點。
1. 在資料庫中，在edcprincipaldomainentity表中搜索域：

   * 選擇 `*` 從edcprincipaldomainentity中。
   * 查找包含擴展或多位元組字元的域名，並將其狀態設定為OBSOLETE。

1. 導入更新的配置檔案，如中所述 [導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。
