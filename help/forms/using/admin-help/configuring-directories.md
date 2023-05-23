---
title: 配置目錄
seo-title: Configuring directories
description: 瞭解如何添加、編輯和刪除目錄以及配置用戶管理以使用虛擬清單視圖。
seo-description: Learn how to add, edit and delete directories and configure user management to use virtual list view.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 0%

---

# 配置目錄 {#configuring-directories}

對於您配置的每個企業域，指定驗證提供程式查詢用戶資訊的目錄。 可以為域配置多個目錄。

## 添加目錄或自定義SPI {#adding-directories-or-custom-spis}

對於您配置的每個企業域，指定驗證提供程式查詢用戶資訊的目錄。 您可以將目錄添加到現有企業域或添加到新企業域。 可以為域配置多個目錄。 您還可以配置域以使用自定義服務提供商介面(SPI)進行同步。

### 添加目錄 {#add-a-directory}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下新建企業域或選擇現有企業域。
1. 按一下「添加目錄」。
1. 在「配置檔案名稱」框中，鍵入一個名稱以區分此目錄，然後按一下「下一步」。
1. 配置目錄伺服器設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings)。)
1. 要驗證是否可以連接到LDAP伺服器，請按一下Test。 如果test失敗，請查看應用程式伺服器日誌檔案中的異常以確定失敗的根本原因。 按一下「Close（關閉）」 ，然後按一下「Next（下一步）」。
1. 選擇「用戶設定」並根據需要配置設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings)。)
1. 要驗證基本DN和其他配置的屬性是否收集了正確的用戶批，請按一下「Test」。 LDAP嘗試使用提供的設定（如基本DN、搜索篩選器和所有屬性）來檢索前200條記錄。

   如果返回用戶，則結果將顯示根據屬性集分配給每個欄位的值。 如果test因不存在的伺服器名稱、不正確的授權資訊或屬性而失敗，則會出現以下錯誤消息：&quot;指定的搜索條件未返回任何結果&quot;。 要確定故障的根本原因，請查看應用程式伺服器日誌檔案中的異常。 按一下「Close（關閉）」 ，然後按一下「Next（下一步）」。

1. 選擇「組設定」並根據需要配置設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings)。)
1. 要驗證基本DN和其他配置的屬性是否收集了正確的組批，請按一下「Test」。 如果返回組，則結果將顯示根據屬性集分配給每個欄位的值。 按一下關閉。

### 添加自定義SPI {#add-a-custom-spi}

有關建立自定義SPI的資訊，請參閱中的「開發AEM表單的SPI」 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63)。 要使新部署的自定義SPI可用於與域關聯，請重新啟動伺服器。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下新建企業域或選擇現有企業域。
1. 按一下「添加目錄」。
1. 在「配置檔案名稱」框中鍵入名稱，選擇「自定義SPI提供程式」，然後按一下「下一步」。
1. 從清單中選擇自定義用戶提供程式，然後按一下「下一步」。
1. 從清單中選擇自定義組提供程式，然後按一下「完成」。

## 編輯目錄 {#edit-a-directory}

您可以編輯先前配置的目錄的詳細資訊。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下清單中的相應域，然後在顯示的頁面上，從清單中選擇相應的目錄。
1. 根據需要配置目錄、用戶和組設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings)。)
1. 按一下「確定」。

## 刪除目錄 {#delete-a-directory}

在刪除目錄後同步域時，該目錄中的所有用戶和組在資料庫中都被標籤為已過時。 不會在Administration Console的任何搜索中返回它們。

>[!NOTE]
>
>企業域至少需要一個身份驗證提供程式和目錄提供程式。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下清單中的相應域。
1. 選中相應目錄的複選框，然後按一下「刪除」。
1. 在顯示的確認頁面上按一下「確定」，然後再次按一下「確定」。

## 目錄設定 {#directory-settings}

將目錄添加到域時，請指定以下目錄設定。

**伺服器：** （必需）目錄伺服器的完全限定域名(FQDN)。 例如，對於adobe.com網路上名為x的電腦，FQDN為x.adobe.com。 可以使用IP地址代替FQDN伺服器名。

**埠：** （必需）目錄伺服器使用的埠。 通常為389或636(如果安全套接字層(SSL)協定用於通過網路發送驗證資訊)。

**SSL:** （必需）指定在通過網路發送資料時目錄伺服器是否使用SSL。 預設值為No。 如果設定為「是」，則應用程式伺服器的Java™運行時環境(JRE)必須信任相應的LDAP伺服器證書。

**綁定** （必需）指定如何訪問目錄。

**匿名：** 不需要用戶名或密碼。 匿名用戶可以只能讀取有限量的資料。 此選項對初始測試可能非常有用。

**用戶：** 需要身份驗證。 在「名稱」框中，指定可以訪問目錄的用戶記錄的名稱。 最好輸入用戶帳戶的完整可分辨名稱(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」框中，指定關聯的密碼。 選擇「用戶」作為「綁定」選項時，需要這些設定。

**名稱：** 未啟用匿名訪問時可用於連接到LDAP資料庫的名稱。 對於Active Directory 2003，請指定 `[domain name]\[userid]`。 對於Sun™ One、eDirectory或IBMTivoli Directory Server，請指定用戶的完全限定名稱，如uid=lcuser、ou=it、o=company.com。

**密碼：** 在未啟用匿名訪問時，與指定連接到LDAP資料庫的名稱對應的密碼。

**填充頁面：** 選中後，使用相應的預設LDAP值填充「用戶」和「組」設定頁上的屬性。

**檢索基本DN:** 檢索基本DN並在下拉清單中顯示它們。 當您有多個基本DN且需要選擇值時，此設定非常有用。

**啟用推薦：** 當您的組織使用以層次結構組織的多個Active Directory域且您僅為父域指定了目錄設定時，此設定適用。 在這種情況下，當您選擇此選項時，用戶管理可以訪問子域中的用戶和組詳細資訊。

>[!NOTE]
>
>按一下「Test」以驗證是否可以連接到LDAP伺服器。 要確定任何故障的根本原因，請在應用程式伺服器日誌檔案中查看異常。

### 用戶設定 {#user-settings}

**唯一標識符：** （必需）用於標識用戶的唯一且常數屬性。 使用非DN屬性作為唯一標識符，因為如果用戶的DN移到組織的其他部分，則其DN可能會更改。 此設定取決於目錄伺服器。 該值是Active Directory 2003的objectGUID、Sun™ One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>確保輸入的屬性在組織中保證唯一。 輸入不正確的值可能會導致嚴重的系統問題。

**基本DN:** 設定為從LDAP層次結構同步用戶和組的起點。 最好在層次結構的最低級別指定一個基本DN，該DN包括需要同步服務的所有用戶和組。

如果在「目錄」設定中選擇了「啟用引用」選項，請將「基本DN」選項設定為 *直流* DN的一部分。 要使推薦工作，搜索範圍必須同時包括父域和子域。

>[!NOTE]
>
>不要在此設定中包括用戶的DN。 要同步特定用戶，請使用「搜索篩選器」設定。

雖然Base DN是管理控制台中的強制設定，但某些目錄伺服器(如IBMDomino Enterprise Server)可能需要空的BaseDN。 要指定空的基本DN，請導出config.xml檔案，在config.xml檔案中編輯設定，然後重新導入它。 (請參閱 [導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。)

**搜索篩選器：** （必需）用於查找與用戶關聯的記錄的搜索篩選器。 您可以執行一級搜索或子級搜索。 （請參閱搜索篩選器語法或RFC 2254。） 有關MicrosoftAD架構的其他資訊，請參見Active Directory架構。

**描述：** 用戶說明的架構屬性

**全名：** （必需）用戶全名的架構屬性

**登錄ID:** （必需）用戶登錄ID的架構屬性

**姓氏：** （必需）用戶姓的架構屬性

**給定名稱：** （必需）用戶名的架構屬性

**縮寫：** 用戶首字母的架構屬性

**業務日曆：** 允許您根據此設定（業務日曆鍵）的值將業務日曆映射到用戶。 業務日曆定義業務日和非業務日。 在計AEM算提醒、截止日期和升級等事件的將來日期和時間時，表單可以使用業務日曆。 您為用戶分配業務日曆密鑰的方式取決於您是使用企業域、本地域還是混合域。 （請參閱配置業務日曆。）

如果使用的是企業域，則可以將「業務日曆」設定映射到LDAP目錄中的欄位。 例如，如果目錄中的每個用戶記錄都包含 *鄉* 欄位，並且您要根據用戶所在的國家/地區分配業務日曆，請指定 *鄉* 欄位名稱作為業務日曆設定的值。 然後，您可以映射業務日曆鍵(為 *鄉* 欄位)到表單工作流中的業務日曆。

用於在表單工作流頁中顯示業務日曆鍵名稱的空間量是有限的。 將業務日曆鍵的名稱限制為少於53個字元，以避免在這些頁面上截斷該鍵。

**修改時間戳：** 要啟用增量目錄同步，請設定此值以修改TimeStamp。 （請參閱啟用增量目錄同步。）

**組織：** 用戶所屬組織名稱的架構屬性。

**主電子郵件：** 用戶主電子郵件地址的架構屬性。

**輔助電子郵件：** 用戶的輔助電子郵件地址的架構屬性。

**電話：** 用戶電話號碼的架構屬性。

**郵政地址：** 用戶郵件地址的架構屬性。

**區域設定：** 包含ISO區域設定資訊的架構屬性。 值是雙字母語言代碼或語言和國家/地區代碼。

**時區：** 包含用戶所在時區的架構屬性。 該值是字串，如City/Country。

**啟用虛擬清單視圖(VLV)控制項：** 一種LDAP控制項，它AEM使表單能夠從目錄伺服器成批檢索資料。 如果將Sun One用作LDAP目錄，並且該目錄包含許多用戶，則啟用VLV將建立用戶管理在搜索用戶時可以使用的索引。 此功能在使用普通用戶帳戶時非常有用，該帳戶只能同步有限數量的資料。 您還可以為組啟用VLV。 如果選擇啟用虛擬清單視圖(VLV)控制項，請在排序欄位框中指定名稱。

>[!NOTE]
>
>要啟用VLV，請配置Sun One。 請參閱 [配置用戶管理以使用虛擬清單視圖(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)。

**排序欄位：** 如果選擇了「啟用虛擬清單視圖(VLV)控制項」，請指定用於對索引進行排序的屬性名稱。 此屬性名稱（如uid）是在目錄伺服器上為VLV建立索引時指定的屬性名稱。

### 組設定 {#group-settings}

**唯一標識符：** （必需）用於標識組的唯一且常數屬性。 使用非DN屬性作為唯一標識符。 此設定取決於目錄伺服器。 該值是Active Directory 2003的objectGUID、Sun One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>確保輸入的屬性在組織中保證唯一。 輸入不正確的值可能會導致嚴重的系統問題。

**基本DN:** （必需）目錄的基本可分辨名稱。

雖然Base DN是管理控制台中的強制設定，但是一些目錄伺服器(如IBMDomino Enterprise Server)需要空的BaseDN。 要指定空的基本DN，請導出config.xml檔案，在config.xml檔案中編輯設定，然後重新導入它。 (請參閱 [導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。)

**搜索篩選器：** （必選）用於查找與組關聯的記錄的搜索篩選器。 您可以執行一級搜索或子級搜索。

**描述：** 組說明的架構屬性

**全名：** （必需）組全名的架構屬性

**成員DN:** （必需）組內成員可分辨名稱的架構屬性

**成員唯一標識符：** 作為選定組成員的用戶或組的唯一標識符。 此值取決於目錄伺服器。 該值是AD2003的objectSID、Sun One的nsuniqueID和eDirectory的guid。

如果使用非DN屬性指定了成員DN，則用戶管理使用成員唯一標識符查詢LDAP以收集用戶的DN，因為它對應於唯一標識符值。

如果將DN指定為唯一標識符，則無需配置成員唯一標識符。

**組織：** 組所屬組織名稱的架構屬性

**主電子郵件：** 組的主電子郵件地址的架構屬性

**輔助電子郵件：** 組的輔助電子郵件地址的架構屬性

**修改時間戳：** 要啟用增量目錄同步，請設定此值以修改TimeStamp。 （請參閱啟用增量目錄同步。）

**啟用虛擬清單視圖(VLV)控制項：** 一種LDAP控制項，它AEM使表單能夠從目錄伺服器成批檢索資料。 如果將Sun One用作LDAP目錄，並且該目錄包含許多組，則啟用VLV將建立用戶管理在搜索組時可以使用的索引。 此功能在使用普通用戶帳戶時非常有用，該帳戶只能同步有限數量的資料。 您還可以為用戶啟用VLV。 如果選擇啟用虛擬清單視圖(VLV)控制項，請指定排序欄位名稱。

>[!NOTE]
>
>要啟用VLV，請配置Sun One。 請參閱 [配置用戶管理以使用虛擬清單視圖(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)。

**排序欄位名稱：** 如果選擇了「啟用虛擬清單視圖(VLV)控制項」，請指定用於對索引進行排序的屬性名稱。 此屬性名稱是在目錄伺服器上為VLV建立索引時指定的屬性名稱。

>[!NOTE]
>
>按一下「Test」以驗證是否根據基本DN和搜索標準收集了用戶和組設定。

如果返回用戶和組，則結果將顯示根據屬性集分配給每個欄位的值。

>[!NOTE]
>
>用戶管理不支援域內的重複用戶ID;只同步一個用戶ID。

## 配置用戶管理以使用虛擬清單視圖(VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

目錄同步是用戶管理的重要要求。 用戶和組將從企業目錄同步到表單數AEM據庫以分配角色和權限。 用戶數在100到1000000個以內，這取決於需求，而且對高效同步資料提出了工程難題。

LDAP協定提供了一種機制，通過使用請求控制以分頁方式查詢大資料集。 使用MicrosoftActive Directory時，LDAPAEM表單資料庫同步使用PagedResultsControl以按特定大小的批檢索資料。 Sun ONE目錄伺服器不支援此控制項。 要針對Sun ONE Directory Server完成分頁查詢，請使用「虛擬清單視圖」(VLV)控制項。 此控制項既包括目錄伺服器端配置，也包括客戶端實現。

>[!NOTE]
>
>本節介紹如何使用Sun ONE Directory Server的VLV控制項。 但是，您可以將此控制項用於任何支援VLV控制項的目錄伺服器。

1. 配置目錄時，在「用戶設定」頁和「組設定」頁上選擇「啟用虛擬清單視圖(VLV)控制」。 選中該複選框後，還必須在「排序欄位」框中指定排序名稱。 預設值為uid。 (請參閱 [添加目錄或自定義SPI](configuring-directories.md#adding-directories-or-custom-spis) 或 [編輯目錄](configuring-directories.md#edit-a-directory)。)
1. 使用Sun ONE管理控制台或命令行指令碼為用戶和組建立LDAP VLV項。 如果使用命令行指令碼，則可以使用示例用戶和組LDIF檔案。 (請參閱 [為VLV配置Sun ONE Directory Server](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)。)
1. 停止伺服器並建立所需的索引。 (請參閱 [為VLV建立目錄伺服器索引](configuring-directories.md#create-the-directory-server-index-for-vlv)。)

### 為VLV配置Sun ONE Directory Server {#configuring-the-sun-one-directory-server-for-vlv}

建立VLV需要包含 `vlvSearch` 和 `vlvIndex` 對象類。 vlvSearch條目包括搜索基， `vlvFilter` 屬性，它指定包含要排序的屬性的對象類。 的 `vlvIndex` 對象類包括 `vlvSort` 屬性，它指定要排序的一個或多個屬性以及排序順序。 (減號(-)表示反字母順序)。 將VLV與表單AEM配合使用需要用戶和組單獨的條目。

>[!NOTE]
>
>可以使用Sun ONE圖形用戶介面(GUI)或通過命令行指令碼建立對象條目。 有關使用GUI建立對象項的說明，請參見Sun ONE文檔。

以下是用戶VLV項的示例指令碼LDIF:

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**使用指令碼建立對象條目**

1. 示例指令碼具有名為 `lcuser`。 此條目用於與VLV相關的配置，用於表單中的用戶AEM同步。 相應地修改以下屬性：

   **條目名稱：** 此示例中的條目名稱為 `lcuser`。 如果 `lcuser` 在示例指令碼的所有區域中都必須更改。

   **vlvBase:** 在「用戶設定」頁上指定的基本DN。

   **vlvFilter:** 在「用戶設定」頁上指定的搜索篩選器。

   **vlvSort:** 在「用戶設定」頁的「VLV設定」部分中指定的「排序欄位」。 VLV控制項要求您指定排序控制項。 此欄位用作建立的vlv索引的排序參數。

   **aci:** 示例指令碼中指定的訪問控制授予任何經過驗證的用戶訪問VLV索引以執行讀取、搜索和比較操作的權限。 管理員可以限制對綁定用戶的訪問，該用戶在「用戶管理」用戶介面中指定的「目錄伺服器設定」頁中配置。 如果未授予權限，則用戶搜索無法使用VLV，並且LDAP伺服器引發權限異常。

   >[!NOTE]
   >
   >作為慣例，vlvIndex條目名稱也設定為 `lcuser`但你可以給它取個不同的名字。 在vlvindex工具中使用相同的名稱。 (請參閱 [為VLV建立目錄伺服器索引&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*。)*

1. 使用 `ldapmodify` 工具，分別使用組的「基本DN」、「搜索篩選器」和「排序欄位」為組建立類似條目：

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例如，鍵入以下文本：

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### 為VLV建立目錄伺服器索引 {#create-the-directory-server-index-for-vlv}

配置目錄設定並為用戶和組建立LDAP VLV項後，請停止伺服器並建立所需的索引。

1. 建立對象項後，停止Sun ONE Server。
1. 使用vlvindex工具，通過鍵入以下文本來生成索引：

   *目錄伺服器實例* `\vlvindex.bat -n userRoot -T lcuser`

   將生成以下輸出：

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex工具存在於目錄伺服器實例目錄中。 如果Sun ONE Server有兩個運行server1和server2的實例，則vlvindex工具位於 *Sun ONE伺服器目錄*\server1目錄。 參數的值 `-T` 是 `cn` 先前在示例LDIF中建立的vlvindex條目的屬性。 在這個例子中， `lcuser`。

1. 如果還為組啟用了VLV，請為組建立相應的索引。 驗證是否通過運行以下命令建立索引：

   *sun one server目錄* `\shared\bin>ldapsearch -h`*主機名* `-p`*埠no* `-s base -b "" objectclass=*`

   將生成以下示例資料等輸出：

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
