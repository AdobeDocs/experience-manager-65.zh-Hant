---
title: 停用JEE和OSGI皆適用之PDFG設定的UAC
description: 為PDFG配置禁用UAC的步驟
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# 無法在Windows Server上將Word或Excel檔案轉換為PDF {#unable-to-convert-word-excel-files-PDF}

## 問題 {#issue}

當使用者嘗試在Microsoft Windows Server上將Word或Excel檔案轉換為PDF時，會發生下列錯誤：

*來自主轉換器的錯誤消息：ALC-PDG-015-003-The系統無法開啟輸入檔案。 請再次提交您的檔案，或聯繫您的系統管理員。*


## 解決方案 {#solution}

執行下列步驟以解決問題：
1. 要訪問系統配置實用程式，請轉至 **[!UICONTROL 開始>運行]** 然後輸入 **[!UICONTROL MSCONFIG]**.
1. 按一下 **[!UICONTROL 工具]** 向下捲動並選取 **[!UICONTROL 更改UAC設定]**. 按一下 **[!UICONTROL Launch]** 在新窗口中運行命令。
1. 將滑桿調整到「永不通知」級別。 完成後，關閉命令窗口並關閉「系統配置」窗口。
1. 驗證UAC的註冊表設定是否設定為0（零）。 執行下列步驟以驗證：

   1. Microsoft®建議您先備份註冊表，然後再修改它。 如需詳細步驟，請參閱 [如何在Windows中備份和還原註冊表](https://support.microsoft.com/en-us/help/322756).
   1. 開啟Microsoft® Windows Registry編輯器。 要開啟註冊表編輯器，請轉至「開始」>「運行」，鍵入regedit，然後按一下「確定」。
   1. 導覽至 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。確保將EnableLUA的值設定為0（零）。
   1. 確保 **EnableLUA** 設為0（零）。 如果值不是0，請將值變更為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

## 套用至 {#appliesto}

此解決方案適用於下列項目：
* JEE伺服器上的AEM Forms
* AEM Forms on OSGi Server
