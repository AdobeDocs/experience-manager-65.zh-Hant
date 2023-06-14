---
title: 設定AEM Forms應用程式的環境
description: 建置和部署AEM Forms應用程式的硬體、軟體和授權。
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 設定AEM Forms應用程式的環境{#set-up-environment-for-aem-forms-app}

您需要下列硬體、軟體和授權，才能建置和部署AEM Forms應用程式：

## 適用於Windows裝置 {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools for Apache Cordova

## 適用於iOS裝置 {#for-ios-devices}

* 執行macOS X 10.9.5或更新版本的Intel型Apple Mac
* iOS SDK 8.4或更新版本
* Xcode版本：OS X或更新版本的Xcode 6.4
* iOS開發人員企業計畫會籍
* 用於發佈內部iOS應用程式的企業憑證
* Apple iPad搭配iOS 8.4或更新版本

## 適用於Android™裝置 {#for-android-devices}

* Android™ Development Toolkit （ADT套件），可從以下網址下載： [https://developer.android.com/studio](https://developer.android.com/studio)
* 如果環境設定在Mac系統上，則ADT應安裝在「應用程式」資料夾中。
* 如果ADT安裝在Mac上的任何其他位置，或環境設定在Windows系統上，則必須更新ADT SDK路徑： `local.properties` 檔案。 此檔案位於 `src\android` 在解壓縮的來源封存檔中的資料夾 `mobileworkspace-src.zip`. 在此檔案中，指向 `sdk.dir` 變數來識別案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。請確定未預先安裝PhoneGap SDK。
