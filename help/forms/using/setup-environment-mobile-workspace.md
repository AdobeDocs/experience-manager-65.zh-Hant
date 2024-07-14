---
title: 設定AEM Forms應用程式的環境
description: 建置和部署AEM Forms應用程式的硬體、軟體和授權。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
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

## 若為Android™裝置 {#for-android-devices}

* 可從[https://developer.android.com/studio](https://developer.android.com/studio)下載的Android™ Development Toolkit （ADT套件）
* 若環境設定在Mac系統上，則ADT應安裝在「應用程式」資料夾中。
* 如果ADT安裝在Mac上的任何其他位置，或環境設定在Windows系統上，則必須在`local.properties`檔案中更新ADT SDK路徑。 此檔案位於已解壓縮來源封存檔`mobileworkspace-src.zip`的`src\android`資料夾中。 在此檔案中，將`sdk.dir`變數指向案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。請確定未預先安裝PhoneGap SDK。
