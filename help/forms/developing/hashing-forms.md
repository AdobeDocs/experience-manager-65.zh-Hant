---
title: 如何在動態PDF forms中生成和使用散列？
description: 在動態PDF forms中生成和使用哈希
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 在動態PDF forms中生成和使用哈希 {#generate-work-with-hashes-dynamic-pdf-forms}


## 先決知識 {#prerequisite-knowledge}

JEE設計器上需要一些AEM Forms經驗，以及訪問和調用指令碼對象中的函式的能力。

## 用戶級別 {#user-level}

開始

如果要在PDF表單中隱藏密碼，而不希望在原始碼或PDF文檔中的其他任何位置以明文形式隱藏密碼，則知道如何生成和使用MD4、MD5、SHA-1和SHA-256散列是關鍵。

其思想是通過生成唯一的哈希值來模糊口令，並將此哈希值儲存在PDF文檔中。 這種唯一的哈希函式可以由不同的哈希函式生成，在本文中，我將向您介紹如何在PDF表內生成這些哈希函式以及如何使用它們。

散列函式將任意長度的長字串（或消息）作為輸入，並生成固定長度的字串作為輸出，有時稱為消息摘要或數字指紋。

AEM Forms在JEE設計器上允許您將指令碼對象中的不同哈希函式作為JavaScript實現，並在動態PDF文檔中運行這些函式。 本文示例檔案中包含的示例PDF使用以下哈希函式的開源實現：

* MD4和MD5 — 由Ronald Rivest設計

* SHA-1和SHA-256 — 由NIST定義

使用散列的最大好處是不必通過比較明文字串直接比較密碼；相反，您可以比較兩個密碼的兩個散列。 因為兩個不同的字串將具有相同的哈希的可能性很小，如果這兩個哈希都相同，則您可以假設比較的字串（在本例中是口令）也相同。

>[!NOTE]
>
>MD4或MD5存在一些眾所周知的安全問題（稱為哈希衝突）。 由於這些哈希衝突和其他SHA-1哈希（包括彩虹表），我決定在第二個示例中集中討論SHA-256哈希函式。  有關詳細資訊，請參見 [衝突](https://en.wikipedia.org/wiki/Hash_collision) 和 [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table) 維基百科的頁面。

## 檢查指令碼對象 {#examining-script-objects}

在JEE Designer的AEM Forms中開啟提供的兩個示例中的一個時，將在「層次結構」調色板中找到四個指令碼對象（請參閱下圖）。

![變數](assets/variables.jpg)

要查看這些指令碼對象中哈希函式的JavaScript實現，請選擇指令碼對象並在指令碼編輯器中瀏覽代碼。  您可以看到以下每個哈希函式是如何實現的：

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1()
* soHASHING_SHA1.str_sha1()
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

如您從此清單中所看到的，哈希的不同輸出類型有不同的函式。 您可以選擇 `hex_` 十六進位數字， `b64_` 對於Base64編碼輸出，或 `str_` 以便進行簡單字串編碼。

根據您選擇的哈希函式，哈希的長度會有所不同：

* MD4:128位
* MD5:128位
* SHA-1:160位
* SHA-256:256位

## 正在嘗試示例PDF forms {#try-sample-pdf-forms}

本文的示例檔案包括兩個PDF forms。 第一個示例允許您鍵入字串，然後為字串生成MD4、MD5、SHA-1和SHA-256哈希值。  第二個示例是一個簡單的表單，如果輸入了正確的密碼，則會解鎖文本欄位。

### 示例1:生成哈希 {#generating-dashes}

按照以下步驟嘗試第一個示例：

1. 下載和解壓縮示例檔案後，在JEE Designer上使用AEM Forms開啟hashing_forms_sample1.pdf。 或者，您可以使用Adobe Reader或Adobe Acrobat專業版來開啟和查看示例，但是您將無法查看原始碼。
1. 在標籤為 [!UICONTROL 清除文本] 鍵入密碼或要散列的任何其他消息。
1. 按一下四個按鈕中的一個按鈕以生成MD4、MD5、SHA-1或SHA-256哈希。 根據您按的按鈕，將調用產生十六進位輸出的四個哈希函式之一，並對字串或消息進行哈希處理。

散列操作的結果顯示在標籤為 [!UICONTROL 散列]。 散列的長度會因您選擇的散列函式而異。

所有示例都使用十六進位數字作為輸出類型。 可以使用指令碼編輯器修改示例並將輸出類型更改為Base64或簡單字串。

### 示例2:匹配密碼 {#matching-passwords}

第二個示例演示了如何在後台比較散列，而不必公開真實密碼。 您輸入的密碼已散列。 儲存在不可見欄位中的真實密碼也被散列。 密碼是安全的，不是因為它不可見，而是因為它已被散列。 由於無法從散列值中重構密碼，因此以散列形式公開密碼是安全的。 只在散列之間進行比較，而不是在明文中的密碼之間進行比較。 如果兩個散列相同，則可以假定密碼相同。

按照以下步驟嘗試第二個示例：

1. 開啟 `hashing_forms_sample2.pdf` 和AEM Forms一起。 或者，您可以使用Adobe Reader或Adobe Acrobat專業版來開啟和查看示例，但是您將無法查看原始碼。
1. 選擇兩個標有密碼欄位之一 [!UICONTROL 密碼MAN] 或 [!UICONTROL 密碼WOMAN] 並鍵入密碼：
   1. 他的密碼是 `bob`
   1. 女人的密碼是 `alice`
1. 當您將焦點移出密碼欄位或按Enter鍵時，輸入的密碼的哈希值將自動生成，並與後台儲存的正確密碼的哈希值進行比較。 正確的散列密碼儲存在標有不可見文本欄位中 `passwd_man_hashed` 和 `passwd_woman_hashed`。 如果為人鍵入正確的密碼，則文本欄位將標籤為 `Man 1` 和 `Man 2` 可訪問，以便您在其中鍵入文本。 同樣的行為也適用於婦女的田地。
1. 或者，您可以按一下標有「刪除密碼」的按鈕，該按鈕將禁用文本欄位並更改其邊框。

比較兩個散列值並啟用文本欄位的代碼非常簡單：

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 從這兒去哪裡 {#next-steps}

你哪裡需要這種東西？ 請考慮一個PDF表單，該表單包含只應由授權個人填寫的欄位。 通過使用密碼保護這些欄位，可確保只有知道密碼的用戶才能訪問這些欄位。

我鼓勵您繼續瀏覽兩個示例PDF檔案。  可以使用Sample_1.pdf生成新的哈希值，並使用生成的值更改Sample_2.pdf中使用的密碼或哈希函式。  「屬性」部分中列出的資源還提供了有關散列和本文中使用的特定JavaScript實現的其他資訊。

## 屬性 {#attributions}

* [羅納德·里韋斯特](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [哈希衝突](https://en.wikipedia.org/wiki/Hash_collision)
* [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)
* [JavaScript MD5項目首頁](https://pajhome.org.uk/crypt/md5/)
* [jsSHA2項目首頁](https://anmar.eu.org/projects/jssha2/)
