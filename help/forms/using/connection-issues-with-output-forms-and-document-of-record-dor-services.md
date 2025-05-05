---
title: 輸出、Forms和（記錄檔案） DoR服務的連線問題
description: 解決SP19之後的AEM Forms連線錯誤。 停止、安裝Microsoft Visual C++、重新啟動伺服器以取得順暢的解決方案。 疑難排解輸出、Forms、DoR服務。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---

# 無法使用輸出服務、Forms服務或記錄檔案(DoR)服務 {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 問題

安裝AEM Forms 6.5 Service Pack 19後，嘗試使用輸出服務、Forms服務或記錄檔案(DoR)服務可能會導致`Connection to failed service`錯誤。

## 解決方案

若要解決問題：

1. 停止AEM 6.5 Forms執行個體。
1. 在安裝AEM 6.5 Forms的電腦上，下載並安裝適用於Visual Studio 2015、2017、2019和2022[&#128279;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)的64位元版Microsoft Visual C++可轉散發套件。
1. 重新啟動AEM Forms伺服器。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。


>[!NOTE]
>
>
> 確保您安裝了可轉散發套件，即使安裝了舊版亦然。
