---
title: 為AEM Forms應用設定環境
seo-title: Set up environment for AEM Forms app
description: 構建和部署AEM Forms應用的硬體、軟體和許可證。
seo-description: Hardware, software, and licenses to build and deploy the AEM Forms app.
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
source-wordcount: '209'
ht-degree: 0%

---

# 為AEM Forms應用設定環境{#set-up-environment-for-aem-forms-app}

您需要以下硬體、軟體和許可證來構建和部署AEM Forms應用：

## 對於Windows設備 {#for-windows-devices}

* MicrosoftWindows 10
* MicrosoftVisual Studio 2015
* MicrosoftApache Cordova的Visual Studio工具

## 對於iOS設備 {#for-ios-devices}

* 基於英特爾的AppleMac運行MacOS X 10.9.5或更高版本
* iOSSDK 8.4或更高版本
* Xcode版本：OS X或更高版本的Xcode 6.4
* iOS開發商企業方案成員
* 用於分發內部iOS應用的企業證書
* AppleiPad與iOS8.4或更高版本

## 對於Android設備 {#for-android-devices}

* Android開發工具包（ADT捆綁包），可從 [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* 如果在MAC系統上設定環境，則ADT應安裝在「應用程式」資料夾中。
* 如果ADT安裝在MAC的任何其他位置，或者環境設定在Windows系統上，則需要在中更新ADT SDK路徑 `local.properties` 中可用的檔案 `src\android` 已提取的源存檔中的資料夾 `mobileworkspace-src.zip`。 在此檔案中，指出 `sdk.dir` 變數到案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。確保未預安裝PhoneGap SDK。
