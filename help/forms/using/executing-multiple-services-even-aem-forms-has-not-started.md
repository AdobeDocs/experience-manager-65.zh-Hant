---
title: 無論AEM Forms是否尚未啟動，仍執行多項服務。
description: 即使AEM Forms尚未完全啟動，仍會處理多項服務。
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# 無論AEM Forms是否尚未完全啟動，仍要執行多項服務{#steps-to-resolve-error-after-installing-service-pack}


## 問題 {#issue}

當使用者重新啟動AEM Forms時，目前的呼叫程式仍會繼續進行，例如轉譯PDF檔案等。 這會導致AEM Forms伺服器的重新啟動無法正確啟動。

## 套用至 {#applies-to}

此解決方案適用於JEE伺服器上的AEM Forms和OSGi伺服器上的AEM Forms 。

## 解決方案 {#solution}

若要解決此問題，使用者需新增引數 `Dcom.adobe.livecycle.dsc.deferServiceStart=true` 至 [批次檔](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) 在伺服器啟動期間。





