---
title: 防止CSRF攻擊
description: 瞭解如何防止跨網站請求偽造(CSRF)攻擊，並保護使用者資料不被破壞。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# 防止CSRF攻擊 {#preventing-csrf-attacks}

## CSRF攻擊的運作方式 {#how-csrf-attacks-work}

跨網站請求偽造(CSRF)是一種網站漏洞，其中有效使用者的瀏覽器可能透過iFrame傳送惡意請求。 由於瀏覽器會以網域為基礎傳送Cookie，因此如果使用者已登入應用程式，該使用者的資料可能會受到危害。

例如，假設您登入瀏覽器中的管理主控台。 您會收到包含連結的電子郵件訊息。 按一下連結，即可在瀏覽器中開啟新標籤。 您開啟的頁面包含隱藏的iFrame，會使用已驗證的AEM表單工作階段的Cookie向Forms伺服器提出惡意請求。 由於「使用者管理」會收到有效的Cookie，因此會傳遞請求。

## CSRF相關辭彙 {#csrf-related-terms}

**Referer：**&#x200B;要求來源頁面的位址。 例如，site1.com上的網頁包含site2.com的連結。 按一下連結即可將要求張貼至site2.com。 此請求的反向連結為site1.com，因為此請求是從來源為site1.com的頁面發出的。

**已加入允許清單的URI：** URI會識別Forms伺服器上正在要求的資源，例如/adminui或/contentspace。 某些資源可能會允許請求從外部網站進入應用程式。 這些資源會視為已加入允許清單的URI。 Forms伺服器絕不會從加入允許清單的URI執行反向連結檢查。

**Null反向連結：**&#x200B;當您開啟新的瀏覽器視窗或Tab鍵，然後輸入地址並按Enter鍵時，反向連結為Null。 此請求是全新請求，並非源自上層網頁；因此，此請求沒有反向連結。 Forms伺服器可以從以下位置接收Null反向連結：

* 在SOAP或Acrobat的REST端點上提出的請求
* 在AEM forms SOAP或REST端點上提出HTTP請求的任何案頭使用者端
* 開啟新的瀏覽器視窗並輸入任何AEM forms web應用程式登入頁面的URL時

在SOAP和REST端點上允許Null反向連結。 在所有URI登入頁面（例如/adminui和/contentspace）及其對應的對應資源上也允許Null反向連結。 例如， /contentspace的對應servlet是/contentspace/faces/jsp/login.jsp，這應該是Null反向連結例外狀況。 只有在啟用Web應用程式的GET篩選時，才需要此例外。 您的應用程式可以指定是否允許空的反向連結。 請參閱[強化AEM表單及安全性](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)中的「防止跨網站要求偽造攻擊」。

**允許的反向連結例外狀況：**&#x200B;允許的反向連結例外狀況是允許的反向連結清單的子清單，會封鎖其要求。 允許的「參考例外」專屬於Web應用程式。 如果不允許允許的反向連結子集呼叫特定的Web應用程式，您可以透過「允許的反向連結例外」將反向連結加入封鎖清單。 在web.xml檔案中為您的應用程式指定允許的反向連結例外。 (請參閱「說明和Tutorials」頁面上「AEM表單的強化和安全性」中的「防止跨網站請求偽造攻擊」。)

## 允許的反向連結如何運作 {#how-allowed-referers-work}

AEM Forms提供反向連結篩選功能，可協助防止CSRF攻擊。 反向連結篩選的運作方式如下：

1. Forms伺服器會檢查用於叫用的HTTP方法：

   * 如果是POST，Forms伺服器會執行反向連結標題檢查。
   * 如果是GET，則Forms伺服器會略過反向連結檢查，除非CSRF_CHECK_GETS設定為true （在此情況下，會執行反向連結標題檢查）。 CSRF_CHECK_GETS是在web.xml檔案中為您的應用程式指定的。 （請參閱[強化與安全性指南](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)中的「防止跨網站請求偽造攻擊」。）

1. Forms伺服器會檢查要求的URI是否已加入允許清單：

   * 如果URI已加入允許清單，則伺服器會傳遞要求。
   * 如果請求的URI未被加入允許清單，則伺服器會擷取請求的反向連結。

1. 如果請求中有反向連結，伺服器會檢查其是否為允許的反向連結。 如果允許，伺服器會檢查反向連結例外狀況：

   * 若為例外狀況，則會封鎖要求。
   * 如果不是例外，則會傳遞要求。

1. 如果請求中沒有反向連結，則伺服器會檢查是否允許Null反向連結。

   * 如果允許空反向連結，則會傳遞請求。
   * 如果不允許空值反向連結，則伺服器會檢查請求的URI是否為Null反向連結的例外狀況，並據此處理請求。

## 設定允許的反向連結 {#configure-allowed-referers}

當您執行Configuration Manager時，預設主機和IP位址或Forms伺服器會新增至「允許的反向連結」清單中。 您可以在管理控制檯中編輯此清單。

1. 在管理控制檯中，按一下「設定>使用者管理>設定>設定允許的反向連結URL」。允許的反向連結清單會顯示在頁面底部。
1. 若要新增允許的反向連結：

   * 在允許的反向連結方塊中輸入主機名稱或IP位址。 若要一次新增多個允許的反向連結，請在新行中輸入每個主機名稱或IP位址。
   * 在「HTTP連線埠」和「HTTPS連線埠」方塊中，指定允許使用HTTP、HTTPS或兩者的連線埠。 如果您將這些方塊留空，則會使用預設連線埠（HTTP使用連線埠80，HTTPS使用連線埠443）。 如果您在方塊中輸入`0` （零），則該伺服器上的所有連線埠都會啟用。 您也可以輸入特定的連線埠號碼，以僅啟用該連線埠。
   * 按一下「新增」。

1. 若要從「允許的反向連結」清單中移除專案，請從清單中選取專案，然後按一下「刪除」。

   如果「允許的反向連結清單」是空的，CSRF功能會停止運作，系統就會變得不安全。

1. 變更允許的反向連結清單後，重新啟動AEM Forms伺服器。
