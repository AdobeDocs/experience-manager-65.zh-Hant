---
title: 添加、啟用、修改或刪除端點
seo-title: Adding, enabling, modifying, or removing endpoints
description: 了解如何新增、啟用、修改和移除端點。
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 添加、啟用、修改或刪除端點 {#adding-enabling-modifying-or-removing-endpoints}

## 將端點新增至服務 {#add-an-endpoint-to-a-service}

端點只能新增至服務。 端點不能單獨存在；它必須與服務相關聯。

>[!NOTE]
>
>建議您在新增端點時使用唯一的名稱。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 在「服務管理」頁上，按一下要配置的服務。
1. 在「端點」頁簽的清單中，選擇要添加的端點類型，然後按一下「添加」。
1. 視端點類型而定，請配置其他端點設定。

[已監看資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[配置Task Manager端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[遠程處理端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 按一下「新增」。

## 啟用或停用端點 {#enable-or-disable-an-endpoint}

預設會自動啟用新端點。 但是，如果已禁用某個端點，則需要啟用該端點，使其可運行。

如果您遇到服務問題，請停用相關端點以更妥善地疑難排解問題。 在常規系統維護期間或升級服務時，您也可能希望禁用端點。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「端點管理」。
1. 在「端點管理」頁上，選擇要啟用或禁用的端點的複選框，然後按一下啟用或禁用。

## 修改端點 {#modify-an-endpoint}

>[!NOTE]
>
>使用管理控制台對端點配置所做的更改不會反映在應用程式的設計時間副本中。 如果您重新部署應用程式，則您使用管理控制台對其端點所做的任何更改都將丟失。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「端點管理」。
1. 在「端點管理」頁上，按一下要修改的端點。
1. 在「更新端點」頁上，修改端點名稱、說明和設定。

   >[!NOTE]
   >
   >請勿在名稱或說明中加入&lt;字元，因為這會截斷工作區中顯示的名稱或說明。

1. 要保存更改，請按一下「更新」。

您也可以從「服務管理」頁中選擇服務，然後按一下「端點」頁簽執行此任務。

## 移除端點 {#remove-an-endpoint}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「端點管理」。
1. 在「端點管理」頁上，選中要刪除的端點的複選框，然後按一下「刪除」。 不再顯示端點。
