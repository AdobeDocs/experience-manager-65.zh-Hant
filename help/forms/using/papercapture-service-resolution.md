---
title: 疑難排解文章，解決當紙張擷取服務無法對PDF執行OCR （光學字元辨識）作業時的問題。
description: 瞭解解決PaperCapture服務無法對PDF執行OCR （光學字元辨識）作業問題的步驟。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
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
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%
---

# PaperCature服務無法對PDF執行OCR作業

## 問題

升級至AEM Forms Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0後，`PaperCapture`服務無法在PDF上執行OCR （光學字元辨識）作業。 此服務不會產生PDF或記錄檔形式的輸出。

## 套用至

此解決方案適用於：

* 所有(JBoss、Weblogic、Websphere) JEE伺服器上的AEM Forms
* OSGi伺服器上的AEM Forms

## 解決方案

1. 從軟體發佈入口網站下載[Hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0)。
1. 擷取並複製下載資料夾的內容。
1. 導覽至下列對應應用程式伺服器的路徑：
   * **jboss**：
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**：
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**：\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **OSGi設定**：\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. 停止AEM應用程式伺服器。
1. 將`PaperCaptureSvc`資料夾的現有內容取代為複製的內容。
1. 重新啟動AEM應用程式伺服器。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。
