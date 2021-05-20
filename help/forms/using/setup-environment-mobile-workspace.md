---
title: 設定AEM Forms應用程式的環境
seo-title: 設定AEM Forms應用程式的環境
description: 建置和部署AEM Forms應用程式的硬體、軟體和授權。
seo-description: 建置和部署AEM Forms應用程式的硬體、軟體和授權。
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 設定AEM Forms應用程式的環境{#set-up-environment-for-aem-forms-app}

您需要下列硬體、軟體和授權才能建置和部署AEM Forms應用程式：

## 對於Windows設備{#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* 適用於Apache Cordova的Microsoft Visual Studio Tools

## 對於iOS設備{#for-ios-devices}

* 運行Mac OS X 10.9.5或更高版本的基於Intel的Apple Mac
* iOS SDK 8.4或更新版本
* Xcode版本：適用於OS X或更新版本的Xcode 6.4
* iOS開發人員企業計畫會員資格
* 用於發佈內部iOS應用程式的企業憑證
* 使用iOS 8.4或更新版本的Apple iPad

## 針對Android裝置{#for-android-devices}

* 可從[https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)下載的Android開發工具套件（ADT套件組合）
* 如果環境是在MAC系統上設定的，則應將ADT安裝在Applications資料夾中。
* 如果ADT安裝在MAC上的任何其他位置，或者環境是在Windows系統上設定的，則ADT SDK路徑需要在`local.properties`檔案中更新，該檔案位於已提取的源歸檔檔案`mobileworkspace-src.zip`的`src\android`資料夾中。 在此檔案中，將`sdk.dir`變數指向案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。請確定未預先安裝PhoneGap SDK。
