---
title: 參考信函模板
seo-title: Reference letter templates
description: AEM Forms提供了信件管理佈局模板，您可以使用這些模板快速建立信件。
seo-description: AEM Forms provides Correspondence Management letter layout templates that you can use to create letters quickly.
uuid: 3b2312d9-daa0-435b-976f-4969b54c5056
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
discoiquuid: afeb9f4d-3feb-4a0e-8884-e3ec1309b33b
exl-id: 40d127b5-1ce6-41fb-ac4c-2bf7ae79da82
source-git-commit: 1def8ff7bc90e2ab82ce8b50277a97da9709c78c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# 參考信函模板 {#reference-letter-templates}

在Oracle Tergement中，信件模板包含典型的表單域、頁眉和頁腳等佈局功能以及用於內容放置的空「目標區域」。

Oracle Tergement在 [AEM Forms附加包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)。 您可以根據品牌和業務需求在設計器中自定義模板。 該包包括以下模板：

* 經典
* 經典簡單
* 平衡左
* 平衡右
* 左視
* 視覺頂部
* 視覺頂部 — 經典

安裝軟體包後，佈局模板(XDP)將列在templates-folder中的以下位置：

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

以下是此包中所有模板中的常用欄位：

* 日期
* 致敬
* 關閉文本
* 簽名文本

![列出所有CM字母模板](assets/templatescorrespondence.png)

安裝AEM-FORMS.-6.3-REFERENCE-LAYOUT-TEMPLATES包後，模板將列在templates-folder中

## 經典 {#classic}

Classic模板頂部有標識，適合寫一封簡單的專業信件。

![經典](assets/classic.png)

PDF預覽使用「傳統型」模板建立的信件

## 經典簡單 {#classic-simple}

包括用於捕獲電話號碼和電子郵件地址的欄位。 「標準簡單」模板與「標準簡單」模板類似，只是它沒有可以輸入收件人地址的欄位。

![聯繫資訊片段](assets/classicsimple.png)

PDF預覽使用「傳統型簡單」模板建立的字母

## 平衡左 {#balanced-left}

「平衡左」模板包含字母左側的徽標。

![平衡左](assets/balancedleft.png)

PDF預覽使用「平衡左」模板建立的信件

## 平衡右 {#balanced-right}

「平衡右」模板左側有公司徽標，並為在信件本身上輸入收件人地址提供了空間。 「平衡右側」模板還包含一個頁腳，當字母具有多個頁面時，該頁腳會重新流動。

![平衡](assets/balancedright.png)

PDF預覽使用「平衡右側」模板建立的信件

## 左視 {#visual-left}

「可視左側」模板在頁面左側有一個側頭，在側頭上放置了公司徽標。 可視左模板具有主題欄位，但沒有頁腳。

![可視化左](assets/visualleft.png)

PDF預覽使用可視左模板建立的字母

## 視覺頂部 {#visual-top}

「可視頂部」模板頂部有可視邊距。 「可視頂部」模板包含一個欄位，用於在頁面本身上輸入收件人地址。 「可視頂部」模板具有主題欄位和頁腳，該頁腳會為延伸到多頁的字母重排。

![視覺頂部](assets/visualtop.png)

PDF使用「可視頂部」模板建立的信件預覽

## 視覺頂部 — 經典 {#visual-top-classic}

Visual Top - Classic模板的頁面頂部有一個帶有公司徽標的標題。 Visual Top - Classic模板有一個欄位可輸入主題，但沒有頁腳。

![視覺經典](assets/visualtopclassic.png)

PDF預覽使用「可視頂部 — 經典」模板建立的字母
