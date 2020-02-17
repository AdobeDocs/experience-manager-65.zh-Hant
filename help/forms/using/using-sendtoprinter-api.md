---
title: 使用sendToPrinter API
seo-title: 使用sendToPrinter API
description: 使用sendToPrinter服務將文檔發送到打印機。
seo-description: 使用sendToPrinter服務將文檔發送到打印機。
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用sendToPrinter API {#using-the-sendtoprinter-api}

## 概覽 {#overview}

在AEM Forms中，您可以使用SendToPrinter服務將檔案傳送至印表機。 SendToPrinter服務支援以下打印訪問機制：

* **可直接存取的印表機**`: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **間接可存取的印表機**`: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   將文檔發送到打印機時，請指定以下打印協定之一：

   * **CUPS**`: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter**`: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**:Output服務支援通用Internet檔案系統(CIFS)打印協定。

## 使用SendToPrinter服務 {#using-sendtoprinter-service}

下表列出：

* 用於各種協定的printerName或printServer的相關資訊。
* 打印機返回的打印機伺服器URI和打印機名稱的各種組合的值或例外

| 協定（訪問機制） | 打印伺服器URI(PrinterSpec.printServer) | 打印機的名稱(PrinterSpec.printerName) | 結果 |
|--- |--- |--- |--- |
| SharedPrinter | 任何 | 空白 | 例外：必要引數sPrinterName不能為空。 |
| SharedPrinter | 任何 | 無效 | 出現異常，表示找不到打印機。 |
| SharedPrinter | 任何 | 有效 | 成功的列印工作。 |
| LPD | 空白 | 任何 | 表示必要參數sPrintServerUri不能為空的例外。 |
| LPD | 無效 | 空白 | 表示必要參數sPrinterName不能為空的例外。 |
| LPD | 無效 | 非空白 | 未找到sPrintServerUri的例外。 |
| LPD | 有效 | 無效 | 表示找不到打印機的例外。 |
| LPD | 有效 | 有效 | 成功的列印工作。 |
| CUPS | 空白 | 任何 | 表示必要參數sPrintServerUri不能為空的例外。 |
| CUPS | 無效 | 任何 | 表示找不到打印機的例外。 |
| CUPS | 有效 | 任何 | 成功的列印工作。 |
| DirectIP | 空白 | 任何 | 表示必要參數sPrintServerUri不能為空的例外。 |
| DirectIP | 無效 | 任何 | 表示找不到打印機的例外。 |
| DirectIP | 有效 | 任何 | 成功的列印工作。 |
| CIFS | 有效 | 空白 | 成功的列印工作。 |
| CIFS | 無效 | 任何 | 使用CIFS打印時出現未知錯誤。 |
| CIFS | 空白 | 任何 | 表示必要參數sPrintServerUri不能為空的例外。 |

## 驗證支援 {#authentication-support}

身份驗證僅支援CIFS打印。 要驗證，請在PrinterSpec中提供用戶名／密碼／域。 您可以使用AEM Granite CyprotoSupport service來加密密碼，方法是執行下列步驟：

1. 前往https://&lt;server>:&lt;port>/system/console。

1. 轉至「 **[!UICONTROL 主]** > **[!UICONTROL 加密支援」]**。

1. 輸入某些純文字檔案，然後按一下「保 **[!UICONTROL 護」]**。

