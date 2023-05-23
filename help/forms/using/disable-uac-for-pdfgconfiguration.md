---
title: 禁用適用於JEE和OSGI的PDFG配置的UAC
description: 為PDFG配置禁用UAC的步驟
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# 無法在Windows Server上將Word或Excel檔案轉換為PDF {#unable-to-convert-word-excel-files-PDF}

## 問題 {#issue}

當用戶嘗試將Word或Excel檔案轉換為MicrosoftWindows Server上的PDF時，會遇到以下錯誤：

*來自主轉換器的錯誤消息：ALC-PDG-015-003 — 系統無法開啟輸入檔案。 請再次提交檔案或與系統管理員聯繫。*


## 解決方案 {#solution}

請執行以下步驟來解決問題：
1. 要訪問系統配置實用程式，請轉至 **[!UICONTROL 開始>運行]** 然後輸入 **[!UICONTROL MSCONFIG]**。
1. 按一下 **[!UICONTROL 工具]** 向下滾動，選擇 **[!UICONTROL 更改UAC設定]**。 按一下 **[!UICONTROL 啟動]** 命令。
1. 將滑塊調整到「從不通知」級別。 完成後，關閉命令窗口並關閉「System Configuration（系統配置）」窗口。
1. 驗證UAC的註冊表設定是否設定為0（零）。 執行以下步驟驗證：

   1. Microsoft®建議在修改註冊表之前先備份它。 有關詳細步驟，請參見 [如何在Windows中備份和還原註冊表](https://support.microsoft.com/en-us/help/322756)。
   1. 開啟Microsoft® Windows註冊表編輯器。 要開啟註冊表編輯器，請轉到「開始」>「運行」，鍵入regedit，然後按一下「確定」。
   1. 導覽至 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。確保EnableLUA的值設定為0（零）。
   1. 確保 **啟用LUA** 設定為0（零）。 如果值不是0，請將值更改為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

## 應用於 {#appliesto}

此解決方案適用於以下方面：
* AEM Forms在JEE伺服器上
* AEM Forms在OSGi伺服器上
