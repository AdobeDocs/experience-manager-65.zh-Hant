---
title: 防止CSRF攻擊
seo-title: Preventing CSRF attacks
description: 瞭解如何防止跨站點請求偽造(CSRF)攻擊並保護用戶資料不受破壞。
seo-description: Learn how to prevent Cross-site request forgery (CSRF) attacks and safeguard user data from being compromised.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 防止CSRF攻擊 {#preventing-csrf-attacks}

## CSRF攻擊的工作原理 {#how-csrf-attacks-work}

跨站點請求偽造(CSRF)是一個網站漏洞，其中使用有效用戶的瀏覽器發送惡意請求，可能是通過iFrame。 因為瀏覽器基於域發送cookie ，所以如果用戶當前已登錄到應用程式，則用戶的資料可能會受到損害。

例如，考慮您登錄到瀏覽器管理控制台的情形。 您會收到包含連結的電子郵件。 按一下連結，該連結將在瀏覽器中開啟一個新頁籤。 您開啟的頁面包含隱藏的iFrame，該iFrame使用通過身份驗證的表單會話中的cookie向表單伺服器發出AEM惡意請求。 由於用戶管理接收有效的cookie，因此它會傳遞請求。

## CSRF相關術語 {#csrf-related-terms}

**參考者：** 從中發出請求的源頁的地址。 例如，site1.com上的網頁包含指向site2.com的連結。 按一下連結將請求發佈到site2.com。 此請求的引用者是site1.com，因為該請求是從源為site1.com的頁面發出的。

**允許列出的URI:** URI標識正在請求的表單伺服器上的資源，例如/adminui或/contentspace。 某些資源可能允許請求從外部站點輸入應用程式。 這些資源被視為允許列出的URI。 表單伺服器從不從允許列出的URI執行引用檢查。

**空引用者：** 開啟新的瀏覽器窗口或頁籤後，鍵入地址並按Enter鍵，引用者為空。 該請求是全新的，不是源於父網頁；因此，該請求沒有引用者。 表單伺服器可以從以下位置接收空引用：

* 在Acrobat的SOAP或REST端點上發出的請求
* 在表單SOAP或REST終結點上發出HTTPAEM請求的任何案頭客戶端
* 開啟新瀏覽器窗口並輸入任何表單Web應用AEM程式登錄頁的URL時

允許在SOAP和REST端點上使用空引用器。 還允許對所有URI登錄頁（如/adminui和/contentspace）及其對應的映射資源使用空引用。 例如，/contentspace的映射servlet為/contentspace/faces/jsp/login.jsp，這應為空引用器異常。 僅當您為Web應用程式啟用GET篩選時，才需要此異常。 您的應用程式可以指定是否允許空引用器。 請參閱中的「防止跨站點請求偽造攻擊」 [表單的強化和安AEM全](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)。

**允許的引用例外：** 允許引用例外是允許引用者清單的子清單，從中阻止請求。 允許的引用例外是Web應用程式特有的。 如果不允許允許引用者的子集調用特定的Web應用程式，則可以通過允許引用者例外來阻止引用者清單。 允許的引用例外在應用程式的web.xml檔案中指定。 (請參閱幫助和Tutorials頁上表單的強化和安全中的「防止跨站點請求偽造AEM攻擊」。)

## 如何允許參考者工作 {#how-allowed-referers-work}

表AEM單提供引用過濾，有助於防止CSRF攻擊。 以下是引用過濾的工作原理：

1. 表單伺服器檢查用於調用的HTTP方法：

   * 如果是POST，則表單伺服器執行引用器頭檢查。
   * 如果是GET，則表單伺服器會繞過參照器檢查，除非CSRF_CHECK_GETS設定為true，在這種情況下它會執行參照器頭檢查。 CSRF_CHECK_GETS是在應用程式的web.xml檔案中指定的。 (請參閱中的「防止跨站點請求偽造攻擊」 [加固和安全導向](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)。)

1. 表單伺服器檢查是否允許列出請求的URI:

   * 如果允許列出URI，則伺服器會傳遞該請求。
   * 如果未允許列出請求的URI，則伺服器將檢索請求的引用者。

1. 如果請求中有引用者，伺服器將檢查它是否是允許的引用者。 如果允許，伺服器將檢查引用者異常：

   * 如果是異常，則會阻止請求。
   * 如果不是例外，則會傳遞請求。

1. 如果請求中沒有引用器，伺服器將檢查是否允許空引用器。

   * 如果允許空引用器，則會傳遞該請求。
   * 如果不允許空引用器，伺服器將檢查所請求的URI是否是空引用器的異常，並相應地處理該請求。

## 配置允許的引用者 {#configure-allowed-referers}

運行Configuration Manager時，預設主機和IP地址或表單伺服器將添加到允許的引用清單中。 可以在管理控制台中編輯此清單。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「配置允許的引用URL」。「允許的引用」清單出現在頁面底部。
1. 要添加允許的引用：

   * 在「允許的引用者」框中鍵入主機名或IP地址。 要一次添加多個允許的引用，請在新行上鍵入每個主機名或IP地址。
   * 在「HTTP埠」和「HTTPS埠」框中，指定允許HTTP、HTTPS或兩者的埠。 如果將這些框留空，則使用預設埠（HTTP的埠80和HTTPS的埠443）。 如果輸入 `0` （零）框中，該伺服器上的所有埠都已啟用。 您也可以輸入特定的埠號以僅啟用該埠。
   * 按一下「新增」。

1. 要從「允許的引用」(Allowed Referer)清單中刪除條目，請從清單中選擇項目，然後按一下「刪除」(Delete)。

   如果「允許的參照者清單」為空，則CSRF功能將停止工作，系統將變得不安全。

1. 更改「允許引用」清單後，重新啟AEM動表單伺服器。
