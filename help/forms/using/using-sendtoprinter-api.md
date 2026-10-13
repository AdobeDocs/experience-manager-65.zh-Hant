---
title: 使用sendToPrint API
description: 使用sendToPrinter服務將檔案傳送至印表機。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,APIs & Integrations
exl-id: 585d4053-1056-4d2b-a9df-9516775afe50
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%
---
# 使用sendToPrint API {#using-the-sendtoprinter-api}

## 概觀 {#overview}

在AEM Forms中，您可以使用SendToPrinter服務將檔案傳送至印表機。 SendToPrinter服務支援下列列印存取機制：

* **可直接存取的印表機** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **可間接存取的印表機** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  當您將檔案傳送至印表機時，請指定下列其中一個列印通訊協定：

  * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
  * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
  * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
  * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
  * **CIFS**： Output服務支援一般網際網路檔案系統(CIFS)列印通訊協定。

## 使用SendToPrinter服務 {#using-sendtoprinter-service}

下表列出：

* 有關用於各種通訊協定的printerName或printServer的資訊。
* 印表機傳回各種印表機伺服器URI和印表機名稱組合的值或例外狀況

| 通訊協定（存取機制） | 列印伺服器URI (PrinterSpec.printServer) | 印表機名稱(PrinterSpec.printerName) | 結果 |
|--- |--- |--- |--- |
| SharedPrinter | 任何 | 空 | 例外：必要的引數sPrinterName不得為空白。 |
| SharedPrinter | 任何 | 無效 | 例外狀況指出找不到印表機。 |
| SharedPrinter | 任何 | 有效 | 列印工作成功。 |
| LPD | 空 | 任何 | 例外狀況，指出必要的引數sPrintServerUri不得為空白。 |
| LPD | 無效 | 空 | 例外狀況，指出必要的引數sPrinterName不得為空白。 |
| LPD | 無效 | 非空白 | 例外狀況指出找不到sPrintServerUri。 |
| LPD | 有效 | 無效 | 例外狀況指出找不到印表機。 |
| LPD | 有效 | 有效 | 成功的列印工作。 |
| CUPS | 空 | 任何 | 例外狀況，指出必要的引數sPrintServerUri不得為空白。 |
| CUPS | 無效 | 任何 | 例外狀況指出找不到印表機。 |
| CUPS | 有效 | 任何 | 列印工作成功。 |
| DirectIP | 空 | 任何 | 例外狀況，指出必要的引數sPrintServerUri不得為空白。 |
| DirectIP | 無效 | 任何 | 例外狀況指出找不到印表機。 |
| DirectIP | 有效 | 任何 | 列印工作成功。 |
| CIFS | 有效 | 空 | 列印工作成功。 |
| CIFS | 無效 | 任何 | 使用CIFS列印時出現未知錯誤。 |
| CIFS | 空 | 任何 | 例外狀況，指出必要的引數sPrintServerUri不得為空白。 |

## 驗證支援 {#authentication-support}

只有CIFS列印支援驗證。 若要驗證，請在PrinterSpec中提供使用者名稱/密碼/網域。 若要使用AEM Granite CyprtoSupport Service加密密碼，請執行下列步驟：

1. 請前往https://&lt;server>：&lt;port>/system/console。

1. 移至&#x200B;**[!UICONTROL 主要]** > **[!UICONTROL 密碼編譯支援]**。

1. 輸入一些純文字，然後按一下&#x200B;**[!UICONTROL 保護]**。
