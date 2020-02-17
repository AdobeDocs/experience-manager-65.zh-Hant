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
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 設定AEM Forms應用程式的環境{#set-up-environment-for-aem-forms-app}

您需要下列硬體、軟體和授權才能建立和部署AEM Forms應用程式：

## 適用於Windows裝置 {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* 適用於Apache Cordova的Microsoft Visual studio工具

## 適用於iOS裝置 {#for-ios-devices}

* 執行Mac OS X 10.9.5或更新版本的Intel架構Apple Mac
* iOS SDK 8.4或更新版本
* Xcode版本：Xcode 6.4 for OS x或更新版本
* iOS Developer Enterprise計畫的會員資格
* 散發內建iOS應用程式的企業憑證
* 含iOS 8.4或更新版本的Apple iPad

## 適用於Android裝置 {#for-android-devices}

* Android開發工具套件（ADT套件），可從https://developer.android.com/sdk/index.html下 [載](https://developer.android.com/sdk/index.html)
* 如果環境是在MAC系統上設定的，則應將ADT安裝在Applications資料夾中。
* 如果ADT安裝在MAC的任何其他位置，或是在Windows系統上設定環境，則ADT SDK路徑必須更新在解壓縮來源封存檔的資料夾中 `local.properties``src\android` ，檔案中的檔案中 `mobileworkspace-src.zip`。 在此檔案中，將變 `sdk.dir` 數指向案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。請確定未預先安裝PhoneGap SDK。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
