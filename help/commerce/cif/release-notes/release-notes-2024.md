---
title: AEM內容與Commerce 2024年發行說明
description: Adobe Experience Manager內容和Commerce 2024年發行說明。
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 25%

---

# Commerce integration framework GitHub版本總覽

## 系統需求概觀

請檢閱下表中，您目前使用或計畫未來使用的CIF版本的最低系統需求。

| 元件 | 系統需求 |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF附加元件 | 最低： AEM 6.5.18、Adobe Commerce 2.3.5 GraphQL結構描述 |
| CIF Core Components | [系統需求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 專案原型 | [系統需求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 發行日期： 2024年10月

| 元件 | 版本 | 詳細資料 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF Core Components | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### 錯誤修正 {#bug-fixes-October}

* 修正UI測試，使其可正確搭配核心CIF元件運作。
* 已解決類別URL格式在雲端例項中無法如預期運作的問題。

## 發行日期： 2024年9月

| 元件 | 版本 | 詳細資料 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF Core Components | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### 改善功能 {#improvements-September}

* 將類別限制設為可自訂。

### 錯誤修正 {#bug-fixes-September}

* Commerce 的欄位未與資產中繼資料結構編輯器妥善整合。
* 輪播產品多欄位供拖放的問題。
* 拖放的輪播類別多欄位問題
* 在類別和產品編輯器頁面的頁面資訊中，按一下無法用於功能表。
* 訂單號碼不會顯示在訂單確認頁面內。

## 發行日期： 2024年1月

| 元件 | 版本 | 詳細資料 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF Core Components | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### 錯誤修正 {#bug-fixes-january}

* 修正產品集合元件中的「加入購物車」按鈕和「加入願望清單」按鈕
