---
title: 設定AEM Forms應用程式的環境
seo-title: 設定AEM Forms應用程式的環境
description: 建立和部署AEM Forms應用程式的硬體、軟體和授權。
seo-description: 建立和部署AEM Forms應用程式的硬體、軟體和授權。
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 設定AEM Forms應用程式的環境{#set-up-environment-for-aem-forms-app}

您需要下列硬體、軟體和授權才能建立和部署AEM Forms應用程式：

## 對於Windows設備{#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* 適用於Apache Cordova的Microsoft Visual Studio工具

## 對於iOS裝置{#for-ios-devices}

* 執行Mac OS X 10.9.5或更新版本的Intel架構Apple Mac
* iOS SDK 8.4或更新版本
* Xcode版本：Xcode 6.4 for OS X或更新版本
* iOS Developer Enterprise計畫的會員資格
* 散發內建iOS應用程式的企業憑證
* 含iOS 8.4或更新版本的Apple iPad

## 對於Android裝置{#for-android-devices}

* Android開發工具套件（ADT套件），可從[https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)下載
* 如果環境是在MAC系統上設定的，則ADT應安裝在Applications資料夾中。
* 如果ADT安裝在MAC的任何其他位置，或者如果環境是在Windows系統上設定，則ADT SDK路徑必須更新在`local.properties`檔案中，此檔案位於解壓縮之來源封存檔`mobileworkspace-src.zip`的`src\android`檔案夾中。 在此檔案中，將`sdk.dir`變數指向案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。請確定未預先安裝PhoneGap SDK。
