---
title: 使用sendToPrinter API
seo-title: Using the sendToPrinter API
description: 使用sendToPrinter服務將文檔發送到打印機。
seo-description: Using the sendToPrinter service to send a document to printer.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%

---

# 使用sendToPrinter API {#using-the-sendtoprinter-api}

## 概觀 {#overview}

在AEM Forms，可以使用SendToPrinter服務將文檔發送到打印機。 SendToPrinter服務支援以下打印訪問機制：

* **可直接訪問的打印機** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **間接可訪問打印機** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   將文檔發送到打印機時，請指定以下打印協定之一：

   * **杯** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**直接IP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **共用打印機** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**:輸出服務支援通用Internet檔案系統(CIFS)打印協定。

## 使用SendToPrinter服務 {#using-sendtoprinter-service}

下表列出：

* 有關用於各種協定的printerName或printServer的資訊。
* 打印機為打印機伺服器URI和打印機名稱的各種組合返回的值或異常

| 協定（訪問機制） | 打印伺服器URI(PrinterSpec.printServer) | 打印機的名稱(PrinterSpec.printerName) | 結果 |
|--- |--- |--- |--- |
| SharedPrinter | 任何 | 空白 | 異常：必需參數sPrinterName不能為空。 |
| SharedPrinter | 任何 | 無效 | 出現異常，表示找不到打印機。 |
| SharedPrinter | 任何 | 有效 | 打印作業成功。 |
| LPD | 空白 | 任何 | 表示所需參數sPrintServerUri不能為空的異常。 |
| LPD | 無效 | 空白 | 表示所需參數sPrinterName不能為空的異常。 |
| LPD | 無效 | 非空 | 未找到sPrintServerUri的異常。 |
| LPD | 有效 | 無效 | 表示找不到打印機的異常。 |
| LPD | 有效 | 有效 | 打印作業成功。 |
| CUPS | 空白 | 任何 | 表示所需參數sPrintServerUri不能為空的異常。 |
| CUPS | 無效 | 任何 | 表示找不到打印機的異常。 |
| CUPS | 有效 | 任何 | 打印作業成功。 |
| DirectIP | 空白 | 任何 | 表示所需參數sPrintServerUri不能為空的異常。 |
| DirectIP | 無效 | 任何 | 表示找不到打印機的異常。 |
| DirectIP | 有效 | 任何 | 打印作業成功。 |
| CIFS | 有效 | 空白 | 打印作業成功。 |
| CIFS | 無效 | 任何 | 使用CIFS打印時出現未知錯誤。 |
| CIFS | 空白 | 任何 | 表示所需參數sPrintServerUri不能為空的異常。 |

## 身份驗證支援 {#authentication-support}

僅CIFS打印支援身份驗證。 要進行身份驗證，請在PrinterSpec中提供用戶名/密碼/域。 通過執行以下步驟，您AEM可以使用Granite CyprotoSupport Service加密密碼：

1. 請訪問https://&lt;server>:&lt;port>/system/console。

1. 轉到 **[!UICONTROL 主]** > **[!UICONTROL 加密支援]**。

1. 輸入一些純文字檔案，然後按一下 **[!UICONTROL Protect]**。
