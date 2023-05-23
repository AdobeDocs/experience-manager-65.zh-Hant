---
title: 設定PDFG網路打印機（僅限Windows）
seo-title: Setting up a PDFG Network Printer (Windows only)
description: 瞭解如何設定PDFG網路打印機（僅限Windows）
seo-description: Learn how to set up a PDFG Network Printer ( Windows only )
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# 設定PDFG網路打印機（僅限Windows） {#setting-up-a-pdfg-network-printer-windows-only}

PDFG網路打印機允許用戶從支援打印的任何應用程式生成PDF文檔。 在用戶安裝PDFG網路打印機後，新打印機名為 *PDF發生器* 出現在Windows控制面板的「Printers（打印機）」部分。 如果已存在同名打印機，則系統會提示用戶提供其他名稱。

從任何應用程式打印到此打印機會將文檔（以PostScript格式）發送到PDF生成器，該生成器會將PostScript檔案轉換為PDF。 根據您配置PDF生成器的方式，它將PDF文檔作為電子郵件的附件發送給用戶，將PDF文檔轉發給指定的表單服務或進程AEM，或同時執行兩個操作。

設定PDFG網路打印機需要以下步驟：

1. 配置電子郵件設定。 (請參閱 [配置PDFG網路打印機的電子郵件設定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)。)
1. 在管理控制台中，配置PDFG網路打印機設定。 (請參閱 [配置PDFG網路打印機設定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)。)
1. 確保在表單資料庫中為用戶配置了有效的AEM電子郵件地址，並將PDFGUserPermission分配給每個用戶。 <!-- Fix broken link See Setting up and organizing users -->
1. 確保在用戶的電腦上安裝了32位JRE6。
1. 在用戶的電腦上安裝打印機。 (請參閱 [在用戶電腦上安裝PDFG網路打印機](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)。)

## 配置PDFG網路打印機的電子郵件設定 {#configure-email-settings-for-pdfg-network-printer}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 在「服務管理」頁上，按一下provider.email_sendmail_service，指定SMTP設定，然後按一下保存。

## 配置PDFG網路打印機設定 {#configure-the-pdfg-network-printer-settings}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「PDFG網路打印機」
1. 在「Adobe PDF設定」和「安全設定」清單中，選擇要應用於生成的PDF的選項。 有關這些設定的詳細資訊，請參閱 [配置Adobe PDF設定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) 和 [配置安全設定](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)。
1. 要將轉換的PDF發回給用戶，請選擇「將轉換的PDF檔案發回給用戶」選項，並指定以下資訊：

   * 用於向用戶發送PDF的電子郵件地址
   * 電子郵件的主題
   * 電子郵件的頁眉、正文和頁腳。 在電子郵件中， &lt;receivername> 替換為打印文檔的用戶的全名。

1. 要將轉換的PDF發送AEM到表單服務或流程，請選擇將轉換的PDF轉發到指定的表AEM單服務或流程選項並指定以下資訊：

   * 要調用的服務的名稱
   * 要調用的服務的操作的名稱
   * 在服務或進程的component.xml檔案中指定的輸入參數的名稱。 PDF文檔將用作該輸入參數的值。

1. 按一下「儲存」。

如果要還原為原始預設電子郵件文本，請按一下「還原電子郵件內容」。

## 在用戶電腦上安裝PDFG網路打印機 {#install-pdfg-network-printer-on-a-user-s-computer}

具有PDFG管理員或PDFG用戶角色的用戶可以安裝PDFG網路打印機。 電腦上必須安裝32位JDK。

1. （PDFG管理員）在管理控制台中，按一下「服務」>「PDF生成器」>「PDFG網路打印機」。

   （PDFG用戶）轉到 `http(s)://[host]:'port'/pdfgui` 然後按一下「PDFG Network Printer Installation（PDFG網路打印機安裝）」下的連結。

1. 在「PDFG Network Printer Installation（PDFG網路打印機安裝）」下，按一下連結。 當系統提示輸入用戶帳戶資訊時，指定您在步驟1中登錄時使用的用戶名和密碼。 出現一條消息，指出打印機已成功安裝。

   ***附註&#x200B;**:如果用戶的密碼更改，則用戶需要在其電腦上重新安裝PDFG網路打印機。 無法從管理控制台更新密碼。*

1. 按一下「確定」。
