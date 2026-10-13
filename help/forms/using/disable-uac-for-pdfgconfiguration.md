---
title: 停用適用於JEE和OSGI之PDFG設定的UAC
description: 瞭解如何針對PDFG設定停用UAC以修正Word到PDF轉換的步驟。
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%
---
# 無法在Windows Server上將Word或Excel檔案轉換為PDF {#unable-to-convert-word-excel-files-PDF}

## 問題 {#issue}

當使用者嘗試在® Windows Server上將Word或Excel檔案轉換成PDF時，會發生下列錯誤：

*來自主要轉換器的錯誤訊息：*
*ALC-PDG-015-003 — 系統無法開啟輸入檔。 再次提交您的檔案或連絡您的系統管理員。*


## 解決方案 {#solution}

請執行下列動作：

1. 若要存取系統組態公用程式，請移至&#x200B;**[!UICONTROL 開始>執行]**，然後輸入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 按一下&#x200B;**[!UICONTROL 工具]**&#x200B;標籤，然後向下捲動並選取&#x200B;**[!UICONTROL 變更UAC設定]**。 按一下&#x200B;**[!UICONTROL 啟動]**，以便在新視窗中執行命令。
1. 將滑桿調整為「永不通知」等級。 完成後，關閉命令視窗並關閉「系統組態」視窗。
1. 確認UAC的登入設定設為0 （零）。 執行以下步驟以進行驗證：

   1. ®建議您在修改登入之前先備份登入。 如需詳細步驟，請參閱[如何在Windows](https://support.microsoft.com/en-us/help/322756)中備份及還原登入。
   1. 開啟® Windows登入編輯器。 若要開啟登入編輯程式，請前往[開始] > [執行]，輸入regedit，然後按一下[確定]。
   1. 導覽至 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。 請確定EnableLUA的值設為0 （零）。
   1. 請確定&#x200B;**EnableLUA**&#x200B;的值設為0 （零）。 如果值不是0，請將值變更為0。 關閉登錄檔編輯器。

1. 重新啟動電腦。

## 適用於 {#appliesto}

此解決方案適用於JEE伺服器上的AEM Forms和OSGi伺服器上的AEM Forms 。
