---
title: 提取字串以進行翻譯
seo-title: 提取字串以進行翻譯
description: 使用xgettext-maven-plugin從需要翻譯的原始碼擷取字串
seo-description: 使用xgettext-maven-plugin從需要翻譯的原始碼擷取字串
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 提取字串以進行翻譯{#extracting-strings-for-translating}

使用xgettext-maven-plugin從需要翻譯的原始碼擷取字串。 Maven增效模組會將字串擷取至您傳送以進行轉譯的XLIFF檔案。 字串會從下列位置擷取：

* Java源檔案
* Javascript來源檔案
* SVN資源（JCR節點）的XML表示

## 設定字串擷取 {#configuring-string-extraction}

設定xgettext-maven-plugin工具擷取專案字串的方式。

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| 章節 | 說明 |
|---|---|
| /filter | 標識要解析的檔案。 |
| /parsers/vaultxml | 配置Vault檔案的解析。 標識包含外部字串和本地化提示的JCR節點。 也標識要忽略的JCR節點。 |
| /parsers/javascript | 識別將字串外部化的Javascript函式。 您不需要變更本節。 |
| /parsers/regexp | 配置Java、JSP和ExtJS範本檔案的剖析。 您不需要變更本節。 |
| /potement | 偵測要國際化的字串的公式。 |

### 標識要解析的檔案 {#identifying-the-files-to-parse}

i18n.any檔案的/filter區段可識別xgettext-maven-plugin工具所剖析的檔案。 新增數個包含和排除規則，用以分別識別已剖析和忽略的檔案。 您應包含所有檔案，然後排除您不想解析的檔案。 通常，您會排除不會對UI貢獻的檔案類型，或是定義UI但未翻譯的檔案。 包含和排除規則具有下列格式：

```
{ /include "pattern" }
{ /exclude "pattern" }
```

規則的陣列部分用於匹配要包括或排除的檔案的名稱。 模式前置詞指示您是要匹配JCR節點（其在Vault中的表示法）還是檔案系統。

| 首碼 | 效果 |
|---|---|
| / | 表示JCR路徑。 因此，此前置詞與jcr_root目錄下的檔案匹配。 |
| &amp;ast; | 表示檔案系統上的常規檔案。 |
| 無 | 沒有前置詞，或以資料夾或檔案名開頭的模式，表示檔案系統上的常規檔案。 |

在模式中使用時， /字元表示子目錄和&amp;ast;字元符合所有。 下表列出數個範例規則。

<table>
 <tbody>
  <tr>
   <th>範例規則</th>
   <th>效果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>包含所有檔案。</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>排除所有PDF檔案。</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>排除POM檔案。</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>排除/content節點下的所有檔案。</p> <p>包含/content/catalogs/geometrixx/templatepages節點。</p> <p>包含/content/catalogs/geometrixx/templatepages的所有子節點。</p> </td>
  </tr>
 </tbody>
</table>

### 擷取字串 {#extracting-the-strings}

無POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

使用POM:將此添加到POM:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

命令：

```shell
mvn xgettext:extract
```

### 輸出檔案 {#output-files}

* `raw.xliff`:提取的字串
* `warn.log`:警告（如果有），如果 `CQ.I18n.getMessage()` API使用不正確。 這些應用程式總需要修正，然後再重新執行。

* `parserwarn.log`:解析器警告（如果有），例如js解析器發出
* `potentials.xliff`:「潛在」候選項，但可能是需要翻譯的人類可讀字串（可以忽略，仍然會產生大量誤報）
* `strings.xliff`:平面化xliff檔案，要導入到ALF
* `backrefs.txt`:允許快速查找指定字串的原始碼位置

