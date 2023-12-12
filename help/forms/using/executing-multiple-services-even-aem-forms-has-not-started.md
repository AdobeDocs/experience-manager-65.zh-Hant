---
title: 無論AEM Forms是否尚未啟動，仍執行多項服務。
description: 即使AEM Forms尚未完全啟動，仍會處理多項服務。
exl-id: 4ec40412-15b1-434b-a919-2cf23f48077c
source-git-commit: faa628ac4a4631564141f68f3efc9d69a67e5c40
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 4%

---

# 無論AEM Forms是否尚未完全啟動，仍要執行多項服務{#steps-to-resolve-error-after-installing-service-pack}


## 問題 {#issue}

當使用者重新啟動AEM Forms時，目前的呼叫程式仍會繼續進行，例如轉譯PDF檔案等。 這會導致AEM Forms伺服器的重新啟動無法正確啟動。

## 套用至 {#applies-to}

此解決方案適用於JEE伺服器上的AEM Forms和OSGi伺服器上的AEM Forms 。

## 解決方案 {#solution}

若要解決此問題，請新增引數 `Dcom.adobe.livecycle.dsc.deferServiceStart=true` 至 [批次檔](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) 在伺服器啟動期間。
