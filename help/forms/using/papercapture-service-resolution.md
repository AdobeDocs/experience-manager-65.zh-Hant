---
title: 疑難排解文章，解決PaperCapture服務無法對PDF執行OCR （光學字元辨識）作業的問題。
description: 瞭解如何解決PaperCapture服務無法對PDF執行OCR （光學字元辨識）作業的問題。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 18005ba060954151df126789496c81f7238e32f6
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# PaperCature服務無法對PDF執行OCR

## 問題

升級至AEM Forms Service Pack 6.5.21.0後， `PaperCapture` 服務無法在PDF上執行OCR （光學字元辨識）作業。 此服務不會產生PDF或記錄檔形式的輸出。

## 解決方案

1. 下載 [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Ca285aedf27094c9e8d9b08dc91e26aa7%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545648843177070%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=uWk0PsSSDjLRxqEMGMW%2BbD%2Fv4egR4vWL%2B0mfKpXdrKQ%3D&amp;reserved=0) 從軟體發佈入口網站。
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
1. 取代現有的內容 `PaperCaptureSvc` 包含已複製內容的資料夾。
1. [重新啟動AEM執行個體](/help/forms/using/restart-aem-sdk.md).


