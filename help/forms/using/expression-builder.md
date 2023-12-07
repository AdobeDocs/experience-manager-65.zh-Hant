---
title: 運算式產生器中的遠端函式
description: 通訊管理中的運算式產生器可讓您建立運算式和遠端函式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# 運算式產生器中的遠端函式{#remote-functions-in-expression-builder}

使用運算式產生器，您可以建立運算式或條件，對資料字典或一般使用者提供的資料值進行計算。 「通訊管理」使用運算式評估的結果來選取資產，例如文字、影像、清單和條件，並視需要將其插入通訊中。

## 使用運算式產生器建立運算式及遠端函式 {#creating-expressions-and-remote-functions-with-expression-builder}

運算式產生器內部使用JSP EL程式庫，因此運算式會遵循JSPEL語法。 如需詳細資訊，請參閱 [運算式範例](#exampleexpressions).

![運算式產生器](assets/expressionbuilder.png)

### 運算子 {#operators}

運算式產生器頂列的運運算元可用於運算式。

### 運算式範例 {#exampleexpressions}

以下是一些您可在通訊管理解決方案中使用的常用JSP EL範例：

* 若要新增兩個數字： ${number1 + number2}
* 若要串連兩個字串： ${str1} ${str2}
* 比較兩個數字： ${age &lt; 18}

如需詳細資訊，請參閱 [JSP EL規格](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). 使用者端運算式管理員不支援JSP EL規格中的某些變數和函式，特別是：

* 集合索引和對應索引鍵(使用 [] 表示法)的變數名稱中不支援在使用者端評估的運算式。
* 以下是運算式中使用的引數型別或函式的傳回型別：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布林值
   * java.lang.Integer
   * 整數
   * java.util.list
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精度
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮點數
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 遠端函式 {#remote-function}

遠端函式提供在運算式中使用自訂邏輯的功能。 您可以撰寫自訂邏輯，作為Java中的方法用於運算式中，而相同的函式可用於運算式中。 可用的遠端函式會列在運算式編輯器左側的「遠端函式」標籤下。

![remotefunction](assets/remotefunction.png)

#### 新增自訂遠端函式 {#adding-custom-remote-functions}

您可以建立自訂套件組合來匯出您自己的遠端函式，以便在運算式中使用。 若要建立自訂套件組合以匯出您自己的遠端函式，請執行下列工作。 它示範如何撰寫將輸入字串轉換為大寫的自訂函式。

1. 定義OSGi服務的介面，其中包含要匯出以供Expression Manager使用的方法。
1. 在介面A上宣告方法，並使用@ServiceMethod註解(com.adobe.exm.expeval.ServiceMethod)加上註解。 Expression Manager會忽略任何未加上註解的方法。 ServiceMethod註解具有下列可選屬性，也可以指定這些屬性：

   1. **已啟用**：判斷此方法是否已啟用。 Expression Manager會忽略停用的方法。
   1. **familyId**：指定方法的系列（群組）。 如果空白，Expression Manager會假設方法屬於預設系列。 沒有家族登入（預設家族除外），無法從中選擇函式。 Expression Manager會使用由各種組合匯出的所有函式所指定的所有系列ID的聯合，以動態建立登入。 請確定他們在此指定的ID可合理讀取，因為它也會顯示在運算式編寫使用者介面中。
   1. **顯示名稱**：人類看得懂的函式名稱。 此名稱用於製作使用者介面中的顯示目的。 如果空白，Expression Manager會使用函式的前置詞和local-name來建構預設名稱。
   1. **說明**：函式的詳細描述。 此說明用於製作使用者介面中的顯示目的。 如果空白，Expression Manager會使用函式的前置詞和local-name來建構預設描述。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   您也可以選擇使用@ServiceMethodParameter註解(com.adobe.exm.expeval.ServiceMethodParameter)標註方法的引數。 此註解僅用於指定在編寫使用者介面中使用的人類可讀名稱與方法引數說明。 確定介面方法的引數和傳回值屬於下列其中一種型別：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布林值
   * java.lang.Integer
   * 整數
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精度
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮點數
   * java.util.Calendar
   * java.util.Date
   * java.util.List

1. 定義介面的實作、將其設定為OSGI服務，並定義以下服務屬性：

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true專案會指示Expression Manager服務包含適合在運算式中使用的遠端函式。 此 &lt;service_id> 值必須為有效的Java識別碼（英數、$、_且不含其他特殊字元）。 此值的前置詞為REMOTE_關鍵字，會構成運算式內部使用的前置詞。 例如，如果介面在服務屬性中具有已註解的方法bar()和服務ID foo，則可在使用REMOTE_foo：bar()的運算式內參照。

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

以下是要使用的範例封存：

* **GoodFunctions.jar.zip** 是包含套件的jar檔案，套件包含範例遠端函式定義。 下載GoodFunctions.jar.zip檔案並將其解壓縮，以取得jar檔案。
* **GoodFunctions.zip** 是定義自訂遠端函式並為其建立套件組合的原始程式碼套件。

GoodFunctions.jar.zip

[取得檔案](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[取得檔案](assets/goodfunctions.zip)
