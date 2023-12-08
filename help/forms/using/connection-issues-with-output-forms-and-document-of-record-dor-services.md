---
title: 輸出、Forms和（記錄檔案） DoR服務的連線問題
description: 解決SP19之後的AEM Forms連線錯誤。 停止、安裝Microsoft Visual C++、重新啟動伺服器以取得順暢的解決方案。 疑難排解輸出、Forms、DoR服務。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
source-git-commit: cf5da092fabbc7834108dc54d65eb97e160984ce
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# 無法使用輸出服務、Forms服務或記錄檔案(DoR)服務 {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 問題

安裝AEM Forms 6.5 Service Pack 19後，嘗試使用輸出服務、Forms服務或記錄檔案(DoR)服務可能會導致 `Connection to failed service` 錯誤。

## 解決方案

若要解決問題：

1. 停止AEM 6.5 Forms執行個體。
1. 下載並安裝 [適用於Visual Studio 2015、2017、2019和2022的64位元版Microsoft Visual C++可轉散發套件](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) 在安裝AEM 6.5 Forms的電腦上。
1. 重新啟動AEM Forms伺服器。


>[!NOTE]
>
>
> 確保您安裝了可轉散發套件，即使安裝了舊版亦然。
