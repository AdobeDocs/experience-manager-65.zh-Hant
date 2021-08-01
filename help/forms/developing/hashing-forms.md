---
title: 如何在動態PDF forms中產生和使用雜湊？
description: 在動態PDF forms中產生和使用雜湊
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 在動態PDF forms中產生和使用雜湊 {#generate-work-with-hashes-dynamic-pdf-forms}


## 必備知識 {#prerequisite-knowledge}

JEE Designer上需要一些AEM Forms的使用體驗，存取和呼叫指令碼物件中函式的功能亦然。

## 使用者層級 {#user-level}

開始

當您想要隱藏PDF表單中的密碼，但不想在原始碼內或PDF檔案的其他任何位置以明文格式隱藏密碼時，知道如何產生和使用MD4、MD5、SHA-1和SHA-256雜湊是關鍵。

其思想是透過產生唯一雜湊來模糊化密碼，並將此雜湊儲存在PDF檔案中。 這個唯一的雜湊可以由不同的雜湊函式產生，在本文中，我將示範如何在PDF表單內產生，以及如何搭配使用。

哈希函式將任意長度的長字串（或消息）作為輸入，並產生固定長度的字串作為輸出，有時稱為消息摘要或數字指紋。

AEM Forms on JEE Designer可讓您以JavaScript在指令碼物件中實作不同的雜湊函式，並在動態PDF檔案中執行。 本文範例檔案包含的範例PDF會使用下列雜湊函式的開放原始碼實作：

* MD4和MD5 — 由Ronald Rivest設計

* SHA-1和SHA-256 — 如NIST所定義

使用雜湊的最大好處是，您不必透過比較明文字字串來直接比較密碼；反之，您可以比較這兩個密碼的兩個雜湊。 因為兩個不同的字串不太可能有相同的雜湊，如果兩個雜湊都相同，您就可以假設比較的字串（在此例中是密碼）也相同。

>[!NOTE]
>
>MD4或MD5有一些眾所周知的安全問題（稱為雜湊衝突）。 由於這些雜湊碰撞和其他SHA-1攻擊（包括彩虹表），我決定在第二個範例中集中處理SHA-256雜湊函式。  如需詳細資訊，請參閱Wikipedia的[碰撞](https://en.wikipedia.org/wiki/Hash_collision)和[彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)頁面。

## 檢查指令碼對象 {#examining-script-objects}

當您在JEE Designer上開啟AEM Forms中提供的兩個範例之一時，會在階層浮動視窗中找到四個指令碼物件（請參閱下圖）。

![變數](assets/variables.jpg)

若要查看這些指令碼物件中雜湊函式的JavaScript實作，請選取指令碼物件，並在指令碼編輯器中探索程式碼。  您可以查看下列各雜湊函式的實作方式：

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASH_SHA1.b64_sha1()
* soHASH_SHA1.str_sha1()
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

如您從此清單中所見，不同的雜湊輸出類型可使用不同的函式。 您可以選擇十六進位數字`hex_`、Base64編碼輸出`b64_`或簡單字串編碼`str_`。

雜湊長度會依您選擇的雜湊函式而異：

* MD4:128位
* MD5:128位
* SHA-1:160位
* SHA-256:256位

## 嘗試範例PDF forms {#try-sample-pdf-forms}

本文的範例檔案包含兩個PDF forms。 第一個範例可讓您輸入字串，然後為字串產生MD4、MD5、SHA-1和SHA-256雜湊值。  第二個示例是一種簡單的形式，如果輸入了正確的密碼，則可解除文本欄位的鎖定。

### 範例1: 產生雜湊 {#generating-dashes}

請依照下列步驟，嘗試第一個範例：

1. 下載和解壓縮範例檔案後，請在JEE Designer上使用AEM Forms開啟hash_forms_sample1.pdf。 或者，您也可以使用Adobe Reader或Adobe Acrobat Professional來開啟和檢視範例，但您將看不到原始碼。
1. 在標示為[!UICONTROL 清除文字]的文字欄位中，輸入密碼或您要雜湊的任何其他訊息。
1. 按一下四個按鈕之一以產生MD4、MD5、SHA-1或SHA-256雜湊。 根據您按下的按鈕，將調用產生十六進位輸出的四個哈希函式之一，並對字串或消息進行哈希處理。

雜湊操作的結果顯示在標示為[!UICONTROL hash]的欄位中。 雜湊的長度會根據您選擇的雜湊函式而有所不同。

所有示例都使用十六進位數字作為輸出類型。 可以使用指令碼編輯器修改示例並將輸出類型更改為Base64或簡單字串。

### 範例2: 匹配密碼 {#matching-passwords}

第二個範例示範如何在背景比較雜湊，而不需揭示真實密碼。 您輸入的密碼是雜湊的。 儲存在不可見欄位中的真實密碼也經過雜湊處理。 密碼是安全的，不是因為密碼是不可見的，而是因為密碼是雜湊的。 由於無法從雜湊值重構密碼，因此以雜湊形式公開密碼是安全的。 只會在雜湊之間進行比較，不會在明文的密碼之間進行比較。 如果兩個雜湊相同，則可以假設密碼相同。

請依照下列步驟，嘗試第二個範例：

1. 在JEE Designer上使用AEM Forms開啟`hashing_forms_sample2.pdf`。 或者，您也可以使用Adobe Reader或Adobe Acrobat Professional來開啟和檢視範例，但您將看不到原始碼。
1. 選擇標籤為[!UICONTROL 密碼MAN]或[!UICONTROL 密碼WOMAN]的兩個密碼欄位之一，並鍵入密碼：
   1. 該人的密碼為`bob`
   1. 女人的密碼為`alice`
1. 當您將焦點移出密碼欄位或按Enter鍵時，您輸入的密碼的哈希將自動生成，並與後台儲存的正確密碼的哈希進行比較。 正確的雜湊密碼儲存在標有`passwd_man_hashed`和`passwd_woman_hashed`的不可見文本欄位中。 如果為人鍵入正確的密碼，則標籤為`Man 1`和`Man 2`的文本欄位將可供訪問，以便您在其中鍵入文本。 同樣的行為也適用於女性的田地。
1. 您可以選擇按一下標示為「刪除密碼」的按鈕，這會停用文字欄位並變更其邊框。

比較兩個雜湊值並啟用文字欄位的程式碼相當簡單：

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 從這裡到哪裡 {#next-steps}

你在哪裡需要這樣的東西？ 請考慮使用PDF表單，該表單中的欄位應僅由授權個人填寫。 使用密碼保護這些欄位（在文檔中的任何位置都不能以明文顯示，如在Sample_2.pdf中），您可以確保只有知道密碼的用戶才能訪問這些欄位。

建議您繼續探索兩個範例PDF檔案。  您可以使用Sample_1.pdf產生新的雜湊值，並使用產生的值來變更Sample_2.pdf中使用的密碼或雜湊函式。  「歸因」區段中列出的資源也提供雜湊和本文中使用之特定JavaScript實作的其他資訊。

## 歸因 {#attributions}

* [羅納德·里韋斯特](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [雜湊碰撞](https://en.wikipedia.org/wiki/Hash_collision)
* [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)
* [JavaScript MD5專案首頁](http://pajhome.org.uk/crypt/md5/)
* [jsSHA2專案首頁](https://anmar.eu.org/projects/jssha2/)


