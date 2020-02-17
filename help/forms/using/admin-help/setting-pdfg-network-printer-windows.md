---
title: 設定PDFG網路打印機（僅限Windows）
seo-title: 設定PDFG網路打印機（僅限Windows）
description: 瞭解如何設定PDFG網路打印機（僅限Windows）
seo-description: 瞭解如何設定PDFG網路打印機（僅限Windows）
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定PDFG網路打印機（僅限Windows） {#setting-up-a-pdfg-network-printer-windows-only}

PDFG網路印表機可讓使用者從支援列印的任何應用程式產生PDF檔案。 當用戶安裝PDFG網路打印機後，名為 ** PDF生成器的新打印機將出現在Windows控制面板的「打印機」部分。 如果已存在同名打印機，則提示用戶提供其他名稱。

從任何應用程式列印至此印表機，會將檔案（以PostScript格式）傳送至PDF產生器，將PostScript檔案轉換為PDF。 視您設定PDF產生器的方式而定，它會將PDF檔案以電子郵件訊息附件的形式傳送給使用者、將PDF檔案轉送至指定的AEM表單服務或程式，或同時執行兩個動作。

要設定PDFG網路打印機，需要執行以下步驟：

1. 設定電子郵件設定。 (請參 [閱「為PDFG網路印表機設定電子郵件設定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)」)。
1. 在管理控制台中，配置PDFG網路打印機設定。 (請參 [閱配置PDFG網路打印機設定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)。)
1. 請確定您的使用者已在AEM Forms資料庫中設定有效的電子郵件地址，並將PDFGUserPermission指派給每位使用者。 <!-- Fix broken link See Setting up and organizing users -->
1. 請確定32位元JRE6已安裝在使用者的電腦上。
1. 在用戶的電腦上安裝打印機。 (請參 [閱在使用者的電腦上安裝PDFG網路印表機](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)。)

## 為PDFG網路打印機配置電子郵件設定 {#configure-email-settings-for-pdfg-network-printer}

1. 在管理控制台中，按一下「服務>應用程式與服務>服務管理」。
1. 在「服務管理」頁上，按一下provider.email_sendmail_service ，指定SMTP設定，然後按一下保存。

## 配置PDFG網路打印機設定 {#configure-the-pdfg-network-printer-settings}

1. 在管理控制台中，按一下「服務> PDF產生器> PDFG網路印表機」
1. 在「Adobe PDF設定」和「保全設定」清單中，選取要套用至產生之PDF的選項。 如需這些設定的詳細資訊，請參 [閱「設定Adobe PDF設定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) 」 [和「設定保全設定」](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)。
1. 若要將轉換的PDF傳回給使用者，請選取「以電子郵件將轉換的PDF檔案傳回給使用者」選項，並指定下列資訊：

   * 用來傳送PDF給使用者的電子郵件地址
   * 電子郵件的主旨
   * 電子郵件的頁首、內文和頁尾。 在電子郵件訊息中，&lt;receiverName>會以列印檔案之使用者的完整名稱取代。

1. 若要將轉換的PDF傳送至AEM表單服務或程式，請選取「將轉換的PDF轉送至指定的AEM表單服務或程式」選項，並指定下列資訊：

   * 要調用的服務的名稱
   * 要調用的服務的操作名稱
   * 輸入參數的名稱，如服務或進程的component.xml檔案中所指定。 PDF檔案將用作該輸入參數的值。

1. 按一下「儲存」。

如果要回復為原始的預設電子郵件文本，請按一下「恢復電子郵件內容」。

## 在使用者的電腦上安裝PDFG網路印表機 {#install-pdfg-network-printer-on-a-user-s-computer}

具有PDFG管理員或PDFG用戶角色的用戶可以安裝PDFG網路打印機。 電腦上必須安裝32位JDK。

1. （PDFG管理員）在管理控制台中，按一下「服務> PDF產生器> PDFG網路印表機」。

   （PDFG用戶）轉至「PDFG Network Printer Installation(PDFG網路打印 `http(s)://[host]:[port]/pdfgui` 機安裝)」下，並按一下該連結。

1. 在「PDFG Network Printer Installation（PDFG網路打印機安裝）」下，按一下該連結。 當提示輸入使用者帳戶資訊時，請指定您在步驟1中用來登入的使用者名稱和密碼。 出現一條消息，指出打印機已成功安裝。

   ***注意&#x200B;**:如果用戶密碼更改，則用戶需要在其電腦上重新安裝PDFG網路打印機。 無法從管理控制台更新密碼。*

1. 按一下「確定」。

