---
title: 添加、啟用、修改或刪除端點
seo-title: 添加、啟用、修改或刪除端點
description: 瞭解如何新增、啟用、修改和移除端點。
seo-description: 瞭解如何新增、啟用、修改和移除端點。
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 添加、啟用、修改或刪除端點 {#adding-enabling-modifying-or-removing-endpoints}

## 向服務添加端點 {#add-an-endpoint-to-a-service}

端點只能新增至服務。 端點不能單獨存在；它必須與服務相關聯。

>[!NOTE]
>
>建議您在新增端點時使用唯一名稱。

1. 在管理控制台中，按一下「服務>應用程式與服務>服務管理」。
1. 在「服務管理」頁面上，按一下要配置的服務。
1. 在「端點」(Endpoints)頁籤的清單中，選擇要添加的端點類型，然後按一下「添加」(Add)。
1. 根據端點類型，配置其他端點設定。

   [Watched資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

   [電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

   [配置任務管理器端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

   [刪除端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 按一下「新增」。

## 啟用或禁用端點 {#enable-or-disable-an-endpoint}

依預設，會自動啟用新端點。 但是，如果您已禁用端點，則需要啟用該端點才能使其正常運行。

如果您遇到服務問題，請停用相關端點，以便更好地疑難排解問題。 您可能還希望在定期系統維護或升級服務期間禁用端點。

1. 在管理控制台中，按一下「服務>應用程式與服務>端點管理」。
1. 在「端點管理」頁面上，選中要啟用或禁用端點的複選框，然後按一下啟用或禁用。

## 修改端點 {#modify-an-endpoint}

>[!NOTE]
>
>您使用管理控制台對端點設定所做的變更不會反映在應用程式的設計時間副本中。 如果您重新部署應用程式，您使用管理控制台對其端點所做的任何變更都將遺失。

1. 在管理控制台中，按一下「服務>應用程式與服務>端點管理」。
1. 在「端點管理」頁上，按一下要修改的端點。
1. 在「更新端點」頁上，修改端點名稱、說明和設定。

   >[!NOTE]
   >
   >不要在名稱或說明中包含&lt;字元，因為它將截斷Workspace中顯示的名稱或說明。

1. 若要儲存變更，請按一下「更新」。

您也可以從「服務管理」頁中執行此任務，方法是選擇服務，然後按一下「端點」頁籤。

## 移除端點 {#remove-an-endpoint}

1. 在管理控制台中，按一下「服務>應用程式與服務>端點管理」。
1. 在「端點管理」(Endpoint Management)頁面上，選中要刪除的端點的複選框，然後按一下「刪除」(Remove)。 不再顯示端點。

