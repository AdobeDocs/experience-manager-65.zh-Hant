---
title: 使用JSON結構描述建立最適化表單
seo-title: 使用JSON結構描述建立最適化表單
description: 最適化表單可以使用JSON結構描述做為表單模型，讓您運用現有的JSON結構描述來建立最適化表單。
seo-description: 最適化表單可以使用JSON結構描述做為表單模型，讓您運用現有的JSON結構描述來建立最適化表單。
uuid: bdeaeae8-65a3-4c46-b27d-fe68481e31f1
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 375ba8fc-3152-4564-aec5-fcff2a95cf4c
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# 使用JSON結構描述建立最適化表單{#creating-adaptive-forms-using-json-schema}

## 必備條件 {#prerequisites}

使用JSON結構描述製作最適化表單作為表單模型，需要基本瞭解JSON結構描述。 建議在本文之前閱讀下列內容。

* [建立最適化表單](../../forms/using/creating-adaptive-form.md)
* [JSON結構描述](https://json-schema.org/)

## 使用JSON結構描述做為表單模型 {#using-a-json-schema-as-form-model}

AEM Forms支援使用現有的JSON結構描述來建立最適化表單。 此JSON結構描述組織中後端系統產生或使用資料的結構。 您使用的JSON結構描述應符合 [v4規範](https://json-schema.org/draft-04/schema)。

使用JSON結構描述的主要功能包括：

* JSON的結構會在最適化表單的製作模式中，在「內容搜尋器」索引標籤中顯示為樹狀結構。 您可以從JSON階層將元素拖放並新增至最適化表單。
* 您可以使用與相關結構符合的JSON預先填入表單。
* 提交時，使用者輸入的資料會以與相關結構相符的JSON形式提交。

JSON結構描述由簡單和複雜的元素類型組成。 這些元素具有向元素添加規則的屬性。 當這些元素和屬性拖曳至最適化表單時，它們會自動映射至對應的最適化表單元件。

此JSON元素與最適化表單元件的對應如下：

```
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON元素、屬性或屬性</strong></th>
   <th><strong>最適化表單元件</strong></th>
  </tr>
  <tr>
   <td><p>具有enum和enumNames約束的字串屬性。</p> <p>語法、</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>下拉式元件：</p>
    <ul>
     <li>enumNames中列出的值會顯示在下拉方塊中。</li>
     <li>枚舉中列出的值用於計算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>具有格式約束的字串屬性。 例如，電子郵件和日期。</p> <p>語法、</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>當類型為字串且格式為電子郵件時，會映射電子郵件元件。</li>
     <li>當類型為字串且格式為hostname時，會映射具有驗證的Textbox元件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>{</p> <p>「類型」:"字串",</p> <p>}</p> </td>
   <td><br /> <br /> 文字欄位<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>數字屬性<br /> </td>
   <td>子類型設為float的數值欄位<br /> </td>
  </tr>
  <tr>
   <td>整數屬性<br /> </td>
   <td>子類型設定為整數的數值欄位<br /> </td>
  </tr>
  <tr>
   <td>布爾型屬性<br /> </td>
   <td>切換<br /> </td>
  </tr>
  <tr>
   <td>object property<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>array屬性</td>
   <td>最小值和最大值分別等於最小值和最大值的可重複面板。 僅支援同構陣列。 因此項目約束必須是對象而不是陣列。<br /> </td>
  </tr>
 </tbody>
</table>

### 通用架構屬性 {#common-schema-properties}

最適化表單使用JSON結構描述中的可用資訊來對應每個產生的欄位。 特別是：

* title屬性用作最適化表單元件的標籤。
* description屬性設定為自適應表單元件的詳細說明。
* 預設屬性用作最適化表單域的初始值。
* maxLength屬性被設定為文本欄位元件的maxlength屬性。
* 「數值」框元件使用minimum、maximum、exclusiveMinimum和exclusiveMaximum屬性。
* 若要支援DatePicker元件的範圍，請提供額外的JSON結構描述屬性minDate和maxDate。
* minItems和maxItems屬性用於限制可從面板元件中添加或刪除的項目／欄位數。
* readOnly屬性設定自適應表單元件的只讀屬性。
* 必要屬性會將最適化表單欄位標示為必填，而如果是面板（其中type為object），則最終提交的JSON資料會包含與該物件對應之空值的欄位。
* pattern屬性設定為自適應形式的驗證模式（規則運算式）。
* JSON結構描述檔副檔名必須保留為。schema.json。 例如，&lt;filename>.schema.json。

## 範例JSON結構描述 {#sample-json-schema}

以下是JSON結構描述的範例。

```
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### 可重複使用的架構定義 {#reusable-schema-definitions}

定義索引鍵用於識別可重複使用的結構描述。 可重複使用的架構定義用於建立片段。 它類似於在XSD中識別複雜類型。 以下提供含定義的範例JSON結構描述：

```
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上例定義了客戶記錄，其中每個客戶都具有發運地址和開單地址。 兩個地址的結構相同——地址有街道地址、城市地址和州地址。 所以最好不要複製地址。 此外，還可輕鬆新增和刪除欄位，以便日後進行任何變更。

## JSON結構描述定義中的預先設定欄位 {#pre-configuring-fields-in-json-schema-definition}

您可以使用 **aem:afProperties** 屬性來預先設定JSON結構描述欄位，以對應至自訂最適化表單元件。 以下列出範例：

```
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## 為表單對象配置指令碼或表達式 {#configure-scripts-or-expressions-for-form-objects}

JavaScript是最適化表單的運算式語言。 所有運算式都是有效的JavaScript運算式，並使用最適化表單指令碼模型API。 您可以預先設定表單物件，以 [評估表單事件](../../forms/using/adaptive-form-expressions.md) 上的運算式。

使用aem:afproperties屬性來預先設定最適化表單運算式或指令碼，以用於最適化表單元件。 例如，觸發初始化事件時，下列程式碼會設定電話欄位的值，並列印值至記錄檔：

```
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

您應是Forms-power-user [群組的成員](/help/forms/using/forms-groups-privileges-tasks.md) ，以設定Form物件的指令碼或運算式。 下表列出最適化表單元件支援的所有指令碼事件。

<table>
 <tbody>
  <tr>
   <th><strong></strong>元件\事件</th>
   <th>initialize <br /> </th>
   <td>計算</td>
   <td>可見性</td>
   <td>驗證</td>
   <td>已啟用</td>
   <td>提交值</td>
   <td>按一下 </td>
   <td>選項</td>
  </tr>
  <tr>
   <td>文字欄位</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>數值欄位</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>數值步進器</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電話</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>切換</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>按鈕</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>核取方塊</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>下拉式清單</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>影像選擇</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>資料輸入欄位</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>日期挑選器</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電子郵件</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>影像</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>面板</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

在JSON中使用事件的一些範例是，在初始化事件時隱藏欄位，並在值提交事件時設定其他欄位的值。 如需建立指令碼事件運算式的詳細資訊，請參 [閱最適化表單運算式](../../forms/using/adaptive-form-expressions.md)。

以下是前述範例的範例JSON程式碼。

### 隱藏初始化事件上的欄位 {#hiding-a-field-on-initialize-event}

```
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### 在值提交事件上配置另一個欄位的值 {#configure-value-of-another-field-on-value-commit-event}

```
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## 限制最適化表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以將下列限制新增至JSON結構描述元素，以限制最適化表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 架構屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>元件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上界。 預設會包含最大值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器<br /> </li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的下界。 預設會包含最小值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值 (Boolean)</p> </td>
   <td><p>如果為true，則在表單元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，表單元件中指定的數字值或日期必須小於或等於為maximum屬性指定的數字值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值 (Boolean)</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須大於最小屬性指定的數值或日期。</p> <p>如果為false，表單元件中指定的數值或日期必須大於或等於為最小屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的字元數目下限。 最小長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>字串</td>
   <td>指定元件中允許的最大字元數。 最大長度必須等於或大於零。</td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元的順序。 如果字元符合指定的模式，則元件接受字元。</p> <p>該模式屬性映射到相應自適應表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>映射至XSD架構的所有最適化表單元件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxItems</td>
   <td>字串</td>
   <td>指定陣列中項目的最大數目。 最大項目必須等於或大於零。</td>
   <td> </td>
  </tr>
  <tr>
   <td>minItems</td>
   <td>字串</td>
   <td>指定陣列中項目的最小數量。 最小項目必須等於或大於零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 不支援的構造 {#non-supported-constructs}

最適化表單不支援下列JSON結構：

* 空類型
* 聯合類型（如任何）和
* OneOf、AnyOf、AllOf和NOT
* 僅支援同構陣列。 因此，項目約束必須是對象而不是陣列。

## Frequently asked questions {#frequently-asked-questions}

**為什麼我無法將子表單的個別元素（從任何複雜類型產生的結構）拖曳至可重複的子表單（minOccours或maxOccuns值大於1）?**

在可重複的子表單中，您必須使用完整的子表單。 如果您只想要選擇欄位，請使用整個結構並刪除不要的欄位。

**我在Content Finder中有很長的複雜結構。 如何尋找特定元素？**

您有兩個選項：

* 捲動樹狀結構
* 使用「搜尋」方塊尋找元素

**JSON結構描述檔的副檔名為何？**

JSON結構描述檔的副檔名必須為。schema.json。 例如，&lt;filename>.schema.json。
