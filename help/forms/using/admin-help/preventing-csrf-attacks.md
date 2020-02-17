---
title: 防止CSRF攻擊
seo-title: 防止CSRF攻擊
description: 瞭解如何防止跨網站偽造要求(CSRF)攻擊，並保護使用者資料不受侵害。
seo-description: 瞭解如何防止跨網站偽造要求(CSRF)攻擊，並保護使用者資料不受侵害。
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 防止CSRF攻擊 {#preventing-csrf-attacks}

## CSRF攻擊的運作方式 {#how-csrf-attacks-work}

跨網站要求偽造(CSRF)是一項網站弱點，有效使用者的瀏覽器可用來傳送惡意要求（可能是透過iFrame）。 由於瀏覽器會依網域傳送Cookie，因此，如果使用者目前已登入應用程式，使用者的資料可能會受到危害。

例如，假設您在瀏覽器中登入管理主控台。 您會收到包含連結的電子郵件訊息。 您按一下連結，會在瀏覽器中開啟新的標籤。 您開啟的頁面包含隱藏的iFrame，會使用已驗證的AEM表單工作階段中的Cookie，對表單伺服器提出惡意要求。 由於「使用者管理」會收到有效的Cookie，因此會傳遞請求。

## CSRF相關術語 {#csrf-related-terms}

**** 參考：來自要求的來源頁面地址。 例如，site1.com的網頁包含site2.com的連結。 按一下連結會將要求張貼至site2.com。 此請求的參考者為site1.com，因為此請求是從來源為site1.com的頁面提出。

**** 白名單URI:URI可識別所請求表單伺服器上的資源，例如/adminui或/contentspace。 某些資源可能允許請求從外部站點輸入應用程式。 這些資源被視為白名單URI。 表單伺服器絕不會從白名單URI執行反向連結檢查。

**** 空引用器：當您開啟新的瀏覽器視窗或標籤時，輸入位址並按Enter，則反向連結為null。 這項要求是全新的，並非源自父網頁；因此，沒有請求的參考。 表單伺服器可接收來自下列網站的空值參考者：

* 在SOAP或REST端點上從Acrobat提出的要求
* 對AEM表單SOAP或REST端點進行HTTP要求的任何案頭用戶端
* 開啟新的瀏覽器視窗，並輸入任何AEM表單網頁應用程式登入頁面的URL時

允許在SOAP和REST端點上使用空值引用器。 也允許所有URI登入頁面（例如/adminui和/contentspace）及其對應的映射資源上有空引用器。 例如，/contentspace的映射servlet為/contentspace/faces/jsp/login.jsp，這應為空引用器異常。 只有在您為Web應用程式啟用GET篩選時，才需要此例外。 您的應用程式可以指定是否允許空值參照器。 請參閱「AEM表單的強化與安全性」中的「防止跨 [網站要求偽造攻擊」](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)。

**** 允許的引用例外：允許的引用例外是允許的引用的清單的子清單，從中阻止請求。 允許參考例外是Web應用程式的特定情況。 如果不允許允許的引用程式的子集調用特定Web應用程式，則可以通過允許的引用例外將引用程式列入黑名單。 允許的引用例外是在您應用程式的web.xml檔案中指定。 （請參閱「說明與教學課程」頁面上「AEM表單的強化與安全性」中的「防止跨網站要求偽造攻擊」）。

## 如何允許參考者運作 {#how-allowed-referers-work}

AEM表格提供反向連結篩選，可協助防止CSRF攻擊。 以下是反向連結篩選的運作方式：

1. Forms伺服器檢查用於調用的HTTP方法：

   * 如果是POST，表單伺服器將執行反向連結標題檢查。
   * 如果是GET，表單伺服器會繞過參考者檢查，除非CSRF_CHECK_GETS設定為true，在此情況下，它會執行參考者標頭檢查。 CSRF_CHECK_GETS是在應用程式的web.xml檔案中指定。 (請參閱「強化與安全性指南」中的「防止跨網站要求偽造 [攻擊」](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html))。

1. Forms伺服器檢查請求的URI是否為白名單：

   * 如果URI已列入白名單，則伺服器會傳遞請求。
   * 如果請求的URI未列入白名單，則伺服器將檢索請求的引用器。

1. 如果請求中有參考，伺服器會檢查它是否為允許的參考。 如果允許，則伺服器會檢查是否有引用者例外：

   * 如果是例外，則會封鎖請求。
   * 如果不是例外，則會傳遞請求。

1. 如果請求中沒有引用器，伺服器會檢查是否允許空引用器。

   * 如果允許空引用，則會傳遞請求。
   * 如果不允許空引用，伺服器會檢查請求的URI是否為空引用的例外，並相應地處理請求。

## 設定允許的參考者 {#configure-allowed-referers}

運行Configuration Manager時，預設主機和IP地址或表單伺服器將添加到「允許的引用」清單中。 您可以在管理控制台中編輯此清單。

1. 在管理控制台中，按一下「設定>使用者管理>設定>設定允許的參考URL」。「允許的參考」清單會顯示在頁面底部。
1. 若要新增允許的參考者：

   * 在「允許的參考」方塊中輸入主機名稱或IP位址。 要一次添加多個允許的引用器，請在新行上鍵入每個主機名或IP地址。
   * 在「HTTP埠」和「HTTPS埠」框中，指定允許HTTP、HTTPS或兩者的埠。 如果保留這些框為空，則使用預設埠（HTTP的埠80和HTTPS的埠443）。 如果在框 `0` 中輸入（零），則該伺服器上的所有埠都將啟用。 您也可以輸入特定的埠號，以僅啟用該埠。
   * 按一下「新增」。

1. 要從「允許的引用」清單中刪除條目，請從清單中選擇項，然後按一下「刪除」。

   如果「允許的參考者清單」為空白，CSRF功能就會停止運作，而且系統會變得不安全。

1. 變更「允許的參考者」清單後，請重新啟動AEM表單伺服器。

