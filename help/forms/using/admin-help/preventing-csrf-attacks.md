---
title: 防止CSRF攻擊
seo-title: Preventing CSRF attacks
description: 了解如何防止跨網站請求偽造(CSRF)攻擊，並防止使用者資料受到損害。
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

## CSRF攻擊如何運作 {#how-csrf-attacks-work}

跨網站請求偽造(CSRF)是一個網站漏洞，使用有效使用者的瀏覽器來傳送惡意請求（可能是透過iFrame）。 由於瀏覽器會依網域傳送Cookie，若使用者目前已登入應用程式，則使用者的資料可能會受到損害。

例如，假設您登入瀏覽器的管理控制台。 您會收到包含連結的電子郵件訊息。 按一下連結，即會在瀏覽器中開啟新索引標籤。 您開啟的頁面包含隱藏的iFrame，該iFrame會使用已驗證AEM表單工作階段的Cookie，向表單伺服器提出惡意請求。 由於使用者管理會收到有效的Cookie，因此會傳遞請求。

## CSRF相關術語 {#csrf-related-terms}

**引用者：** 要求來源頁面的位址。 例如，site1.com上的網頁包含site2.com的連結。 按一下連結會向site2.com發佈請求。 此請求的引用者為site1.com，因為請求來自源為site1.com的頁面。

**允許的URI:** URI可標識正在請求的表單伺服器上的資源，例如/adminui或/contentspace。 某些資源可能允許請求從外部站點輸入應用程式。 這些資源被視為允許列出的URI。 表單伺服器從未從允許列出的URI執行反向連結檢查。

**Null引用：** 開啟新的瀏覽器窗口或頁簽，然後鍵入地址並按Enter鍵時，引用為null。 此要求為全新請求，並非源自上層網頁；因此，請求沒有反向連結。 表單伺服器可接收來自以下網址的空反向連結：

* 在來自Acrobat的SOAP或REST端點上提出的請求
* 在AEM表單SOAP或REST端點上提出HTTP要求的任何案頭用戶端
* 開啟新瀏覽器視窗且輸入任何AEM表單網頁應用程式登入頁面的URL時

在SOAP和REST端點上允許空引用。 還允許在所有URI登入頁面（如/adminui和/contentspace）及其對應的映射資源上使用null引用。 例如， /contentspace的映射servlet為/contentspace/faces/jsp/login.jsp，這應為Null引用者例外。 只有當您為Web應用程式啟用GET篩選時，才需要此例外。 您的應用程式可以指定是否允許空引用。 請參閱以下主題中的「防止跨網站請求偽造攻擊」： [AEM表單的強化與安全性](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**允許的反向連結例外狀況：** 允許的引用異常是允許的引用的清單的子清單，從中阻止請求。 允許的引用異常對Web應用程式是特定的。 如果不允許允許的引用的子集調用特定的Web應用程式，則可以通過允許的引用異常來阻止引用。 允許的引用異常在應用程式的web.xml檔案中指定。 (請參閱「說明和Tutorials」頁面上AEM表單的強化與安全性中的「防止跨網站請求偽造攻擊」)。

## 允許的反向連結如何運作 {#how-allowed-referers-work}

AEM forms提供反向連結篩選功能，可協助防止CSRF攻擊。 以下是反向連結篩選的運作方式：

1. 表單伺服器會檢查用於呼叫的HTTP方法：

   * 如果是POST，表單伺服器會執行反向連結標題檢查。
   * 如果為GET，則表單伺服器會繞過引用檢查，除非將CSRF_CHECK_GETS設定為true，否則它將執行引用頭檢查。 CSRF_CHECK_GETS在應用程式的web.xml檔案中指定。 (請參閱以下主題中的「防止跨網站請求偽造攻擊」： [強化與安全指南](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. 表單伺服器會檢查請求的URI是否允許列出：

   * 如果允許列出URI，則伺服器會傳遞請求。
   * 如果未允許列出請求的URI，則伺服器將檢索請求的引用。

1. 如果請求中有反向連結，則伺服器會檢查其是否為允許的反向連結。 如果允許，伺服器會檢查是否有反向連結例外狀況：

   * 如果是例外，則會封鎖要求。
   * 如果不是例外，則會傳送要求。

1. 如果請求中沒有反向連結，則伺服器會檢查是否允許空的反向連結。

   * 如果允許空的引用，則會傳遞請求。
   * 如果不允許空引用，則伺服器將檢查所請求的URI是否為空引用的例外，並相應地處理該請求。

## 設定允許的反向連結 {#configure-allowed-referers}

當您運行Configuration Manager時，預設主機和IP地址或表單伺服器將添加到「允許的引用」清單中。 您可以在管理控制台中編輯此清單。

1. 在管理控制台中，按一下「設定>使用者管理>設定>設定允許的反向連結URL」 。「允許的反向連結」(Allowed Referer)清單出現在頁面底部。
1. 若要新增允許的反向連結：

   * 在「允許的引用」框中鍵入主機名或IP地址。 若要一次新增多個允許的反向連結，請在新的一行上輸入每個主機名稱或IP位址。
   * 在「HTTP埠」和「HTTPS埠」框中，指定允許HTTP、HTTPS或兩者的埠。 如果這些框為空，則使用預設埠（HTTP為埠80,HTTPS為埠443）。 如果您輸入 `0` （零）框中，該伺服器上的所有埠都已啟用。 您也可以輸入特定的埠號，以僅啟用該埠。
   * 按一下「新增」。

1. 要從「允許的引用」清單中刪除條目，請從清單中選擇項，然後按一下「刪除」。

   如果「允許的引用清單」為空，CSRF功能將停止工作，系統將變得不安全。

1. 變更允許的反向連結清單後，請重新啟動AEM表單伺服器。
