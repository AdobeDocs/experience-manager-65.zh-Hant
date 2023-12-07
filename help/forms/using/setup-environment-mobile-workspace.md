---
title: 設定AEM Forms應用程式的環境
description: 建置和部署AEM Forms應用程式的硬體、軟體和授權。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 設定AEM Forms應用程式的環境{#set-up-environment-for-aem-forms-app}

您需要下列硬體、軟體和授權，才能建置和部署AEM Forms應用程式：

## Windows裝置 {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools for Apache Cordova

## 適用於iOS裝置 {#for-ios-devices}

* 執行macOS X 10.9.5或更新版本的Intel型Apple Mac
* iOS SDK 8.4或更新版本
* Xcode版本：適用於OS X或更新版本的Xcode 6.4
* iOS開發人員企業計畫會籍
* 用於發佈內部iOS應用程式的企業憑證
* Apple iPad搭配iOS 8.4或更新版本

## Android™裝置 {#for-android-devices}

* Android™ Development Toolkit （ADT套件），可從以下來源下載： [https://developer.android.com/studio](https://developer.android.com/studio)
* 若環境設定在Mac系統上，則ADT應安裝在「應用程式」資料夾中。
* 如果ADT安裝在Mac上的任何其他位置，或環境設定在Windows系統上，則必須在以下位置更新ADT SDK路徑： `local.properties` 檔案。 此檔案位於 `src\android` 資料夾（在已擷取的來源封存檔中） `mobileworkspace-src.zip`. 在此檔案中，指向 `sdk.dir` 變數來產生ADT SDK在案頭上的位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。請確定未預先安裝PhoneGap SDK。
