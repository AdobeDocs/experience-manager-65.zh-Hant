---
title: 停用適用於JEE和OSGI之PDFG設定的UAC
description: 瞭解如何針對PDFG設定停用UAC以修正Word到PDF轉換的步驟。
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# 無法在Windows Server上將Word或Excel檔案轉換為PDF {#unable-to-convert-word-excel-files-PDF}

## 問題 {#issue}

當使用者嘗試將Word或Excel檔案轉換成Microsoft® Windows Server上的PDF時，會發生下列錯誤：

*來自主要轉換器的錯誤訊息：*
*ALC-PDG-015-003 — 系統無法開啟輸入檔案。 再次提交您的檔案或聯絡您的系統管理員。*


## 解決方案 {#solution}

請執行下列動作：

1. 若要存取「系統組態公用程式」，請移至 **[!UICONTROL 開始>執行]** 然後輸入 **[!UICONTROL MSCONFIG]**.
1. 按一下 **[!UICONTROL 工具]** Tab鍵並向下捲動並選取 **[!UICONTROL 變更UAC設定]**. 按一下 **[!UICONTROL Launch]** 以便在新視窗中執行指令。
1. 將滑桿調整為「永不通知」等級。 完成後，關閉命令視窗並關閉「系統組態」視窗。
1. 確認UAC的登入設定設為0 （零）。 執行以下步驟以進行驗證：

   1. Microsoft®建議您在修改登入之前先備份登入。 如需詳細步驟，請參閱 [如何在Windows中備份及還原登入](https://support.microsoft.com/en-us/help/322756).
   1. 開啟Microsoft® Windows登入編輯器。 若要開啟登入編輯程式，請前往[開始] > [執行]，輸入regedit，然後按一下[確定]。
   1. 瀏覽至 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. 請確定EnableLUA的值設為0 （零）。
   1. 確認值 **EnableLUA** 設為0 （零）。 如果值不是0，請將值變更為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

## 套用至 {#appliesto}

此解決方案適用於JEE伺服器上的AEM Forms和OSGi伺服器上的AEM Forms 。
