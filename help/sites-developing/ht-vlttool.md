---
title: 如何使用VLT工具
seo-title: How to use the VLT Tool
description: Jackrabbit FileVault工具(VLT)由Apache Foundation開發，可將Jackrabbit/AEM例項的內容對應至您的檔案系統
seo-description: The Jackrabbit FileVault tool (VLT) is developed by The Apache Foundation that maps the content of a Jackrabbit/AEM instance to your file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 1%

---

# 如何使用VLT工具 {#how-to-use-the-vlt-tool}

Jackrabbit FileVault工具(VLT)是由 [Apache Foundation](https://www.apache.org/) 將Jackrabbit/AEM例項的內容對應至您的檔案系統。 VLT工具具有與原始碼控制系統客戶端(如Subversion(SVN)客戶端)類似的功能，提供正常的簽入、簽出和管理操作，以及用於靈活表示項目內容的配置選項。

從命令行運行VLT工具。 本檔案說明如何使用工具，包括如何開始使用及取得說明，以及列出所有 [命令](#vlt-commands) 可用 [選項](#vlt-global-options).

## 概念與架構 {#concepts-and-architecture}

請參閱 [Filevault概述](https://jackrabbit.apache.org/filevault/overview.html) 和 [保管庫FS](https://jackrabbit.apache.org/filevault/vaultfs.html) 來自官方 [Apache Jackrabbit Filevault檔案](https://jackrabbit.apache.org/filevault/index.html) 以全面了解Filevault工具的概念和結構。

## VLT快速入門 {#getting-started-with-vlt}

若要開始使用VLT，您必須執行下列操作：

1. 安裝VLT、更新環境變數和更新全局忽略的Subversion檔案。
1. 設定AEM存放庫（如果尚未這麼做）。
1. 查看AEM存放庫。
1. 與儲存庫同步。
1. 測試同步是否有效。

### 安裝VLT工具 {#installing-the-vlt-tool}

若要使用VLT工具，您必須先安裝它。 預設不會安裝它，因為它是其他工具。 此外，您還需要設定系統的環境變數。

1. 從 [Maven工件儲存庫。](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >VLT工具的來源是 [可在GitHub上使用。](https://github.com/apache/jackrabbit-filevault)
1. 解壓縮封存。
1. 新增 `<archive-dir>/vault-cli-<version>/bin` 環境 `PATH` 這樣命令檔案 `vlt` 或 `vlt.bat` 可視情況存取。 例如：

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. 開啟命令行shell並執行 `vlt --help`. 請確定輸出類似下列說明畫面：

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

安裝後，需要更新全局忽略的Subversion檔案。 編輯svn設定並新增下列內容：

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 設定行字元的結尾 {#configuring-the-end-of-line-character}

VLT根據以下規則自動處理行尾(EOF):

* 在Windows端簽出的檔案行 `CRLF`
* 在Linux/Unix端上以 `LF`
* 儲存庫的檔案行以 `LF`

為保證VLT和SVN配置匹配，應設定 `svn:eol-style` 屬性 `native` 用於儲存在儲存庫中的檔案的擴展。 編輯svn設定並新增下列內容：

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### 簽出儲存庫 {#checking-out-the-repository}

使用原始碼控制系統檢查儲存庫。 例如，在svn中，鍵入以下內容（用儲存庫替換URI和路徑）:

```shell
svn co https://svn.server.com/repos/myproject
```

### 與儲存庫同步 {#synchronizing-with-the-repository}

您需要將檔案與儲存庫同步。 要執行此操作：

1. 在命令列中，導覽至 `content/jcr_root`.
1. 鍵入以下內容(將埠號替換為 **4502** 和管理員密碼):

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >在您進行初始結帳時，只需指定一次憑證。 然後，這些檔案會儲存在您的主目錄中 `.vault/auth.xml`.

### 測試同步是否有效 {#testing-whether-the-synchronization-worked}

簽出儲存庫並同步後，您應進行測試，以確保所有功能都正常運行。 編輯 **.jsp** ，並查看是否在提交變更後反映變更。

要測試同步，請執行以下操作：

1. 導覽至 `.../jcr_content/libs/foundation/components/text`。
1. 編輯 `text.jsp`.
1. 通過鍵入 `vlt st`
1. 輸入 `vlt diff text.jsp`
1. 提交更改： `vlt ci test.jsp`.
1. 重新載入包含文字元件的頁面，並查看您的變更是否存在。

## 取得VLT工具的協助 {#getting-help-with-the-vlt-tool}

安裝VLT工具後，您可以從命令行訪問其幫助檔案：

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

有關特定命令的幫助，請鍵入help命令，後跟命令的名稱。 例如：

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## VLT中執行的常見任務 {#common-tasks-performed-in-vlt}

以下是在VLT中執行的一些常見任務。 有關每個命令的詳細資訊，請參見 [命令](#vlt-commands).

### 簽出子樹 {#checking-out-a-subtree}

例如，如果您只想簽出儲存庫的子樹狀結構， `/apps/geometrixx`，您可以輸入下列項目來執行此操作：

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

這樣會建立新的匯出根 `geo` 帶 `META-INF` 和 `jcr_root` 目錄，並將所有檔案放在 `/apps/geometrixx` in `geo/jcr_root`.

### 執行篩選的結帳 {#performing-a-filtered-checkout}

如果您有現有的工作區篩選條件，且想將其用於結帳，您可以先建立 `META-INF/vault` 將篩選器置於此處，或在命令列上指定，如下所示：

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

範例篩選器：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### 使用匯入/匯出，而非.vlt控制項 {#using-import-export-instead-of-vlt-control}

您可以在JCR存放庫和本機檔案系統之間匯入和匯出內容，而不需使用控制檔案。

若要匯入和匯出內容，不要使用 `.vlt` 控制：

1. 最初設定儲存庫：

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. 更改遠程副本並更新JCR:

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. 更改遠程副本並更新檔案伺服器：

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## 使用VLT {#using-vlt}

要在VLT中發出命令，請在命令行中鍵入以下命令：

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

以下各節將詳細說明選項和命令。

## VLT全局選項 {#vlt-global-options}

以下是VLT選項清單，所有命令均可用。 有關其他可用選項的資訊，請參見各個命令。

|  |  |
|--- |--- |
| 選項 | 說明 |
| `-Xjcrlog <arg>` | 擴展JcrLog選項 |
| `-Xdavex <arg>` | 擴展的JCR遠程選項 |
| `--credentials <arg>` | 要使用的預設憑據 |
| `--config <arg>` | 要使用的JcrFs配置 |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 盡可能少地打印 |
| `--version` | 打印版本資訊並退出VLT |
| `--log-level <level>` | 指示日誌級別，例如log4j日誌級別。 |
| `-h (--help) <command>` | 打印該特定命令的幫助 |

## VLT命令 {#vlt-commands}

下表介紹了所有可用的VLT命令。 有關語法、可用選項和示例的詳細資訊，請參閱各個命令。

|  |  |  |
|--- |--- |--- |
| 命令 | 縮寫命令 | 說明 |
| `export` |  | 從JCR儲存庫（保管庫檔案系統）導出到本地檔案系統，而不使用控制檔案。 |
| `import` |  | 將本地檔案系統導入到JCR儲存庫（保管庫檔案系統）。 |
| `checkout` | `co` | 檢出Vault檔案系統。 將此檔案用於本地檔案系統的初始JCR儲存庫。 (注意：您必須先簽出Subversion中的儲存庫。) |
| `analyze` |  | 分析包。 |
| `status` | `st` | 打印工作副本檔案和目錄的狀態。 |
| `update` | `up` | 將更改從儲存庫導入工作副本。 |
| `info` |  | 顯示有關本地檔案的資訊。 |
| `commit` | `ci` | 將更改從工作副本發送到儲存庫。 |
| `revert` | `rev` | 將工作副本檔案還原為原始狀態，並取消大部分的本機編輯。 |
| `resolved` | `res` | 刪除工作副本檔案或目錄上的衝突狀態。 |
| `propget` | `pg` | 在檔案或目錄上打印屬性的值。 |
| `proplist` | `pl` | 在檔案或目錄上打印屬性。 |
| `propset` | `ps` | 在檔案或目錄上設定屬性的值。 |
| `add` |  | 將檔案和目錄置於版本控制之下。 |
| `delete` | `del` 或 `rm` | 從版本控制中刪除檔案和目錄。 |
| `diff` | `di` | 顯示兩個路徑之間的差異。 |
| `console` |  | 執行互動式主控台。 |
| `rcp` |  | 將節點樹從一個遠程儲存庫複製到另一個。 |
| `sync` |  | 允許控制保管庫同步服務。 |

### 匯出 {#export}

導出裝載在的Vault檔案系統 &lt;uri> 到本地檔案系統(位於 &lt;local-path>. 可選 &lt;jcr-path> 可以指定，以便僅導出子樹。

#### 語法 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### 選項 {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-t (--type) <arg>` | 指定導出類型，可以是platform或jar。 |
| `-p (--prune-missing)` | 指定是否應刪除缺少的本地檔案 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR路徑 |
| `<localPath>` | 本地路徑 |

#### 範例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### 匯入 {#import}

導入本地檔案系統(從 `<local-path>` 在 `<uri>`. 您可以指定 `<jcr-path>` 作為導入根。 若 `--sync` 指定時，導入的檔案將自動置於保管庫控制下。

#### 語法 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### 選項 {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-s (-- sync)` | 將本地檔案置於保險庫控制下 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR路徑 |
| `<localPath>` | 本地路徑 |

#### 範例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### 結帳(co) {#checkout-co}

從JCR儲存庫到本地檔案系統執行初始檢出，從 &lt;uri> 到本地檔案系統(位於 &lt;local-path>. 您也可以新增 &lt;jcrpath> 用於簽出遠程樹的子目錄的參數。 可以指定將複製到META-INF目錄的工作區篩選器。

#### 語法 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### 選項 {#options-2}

|  |  |
|--- |--- |
| `--force` | 強制簽出，如果本地檔案已存在，則覆蓋 |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-f (--filter) <file>` | 如果未定義，則指定自動篩選 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | （可選）遠程路徑 |
| `<localPath>` | （可選）本地路徑 |

#### 範例 {#examples-2}

使用JCR遠程處理：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

使用預設工作區：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

如果URI不完整，則將展開：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 分析 {#analyze}

分析包。

#### 語法 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### 選項 {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | hotfix連結（例如名稱、id）的printf格式 `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `<localPaths> [<localPaths> ...]` | 本地路徑 |

### 狀態 {#status}

打印工作副本檔案和目錄的狀態。

若 `--show-update` 已指定，則會根據遠程版本檢查每個檔案。 然後，第二字母指定更新操作將執行哪些操作。

#### 語法 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### 選項 {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-u (--show-update)` | 顯示更新資訊 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 顯示狀態的檔案或目錄 |

### 更新 {#update}

將更改從儲存庫複製到工作副本中。

#### 語法 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### 選項 {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `--force` | 強制覆蓋本地檔案 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 要更新的檔案或目錄 |

### 資訊 {#info}

顯示有關本地檔案的資訊。

#### 語法 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### 選項 {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸 |
| `<file> [<file> ...]` | 顯示資訊的檔案或目錄 |

### 提交 {#commit}

將更改從工作副本發送到儲存庫。

#### 語法 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### 選項 {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `--force` | 即使修改了遠程副本，也強制提交 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 提交檔案或目錄 |

### 回復 {#revert}

將工作副本檔案還原為原始狀態，並取消大部分的本機編輯作業。

#### 語法 {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### 選項 {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸 |
| `<file> [<file> ...]` | 提交檔案或目錄 |

### 已解決 {#resolved}

移除 **衝突** 工作副本檔案或目錄的狀態。

>[!NOTE]
>
>此命令在語義上不解決衝突或刪除衝突標籤；它僅僅刪除與衝突相關的對象檔案，並允許重新提交PATH。

#### 語法 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### 選項 {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸 |
| `--force` | 解析，即使存在衝突標籤 |
| `<file> [<file> ...]` | 要解析的檔案或目錄 |

### 普羅佩特 {#propget}

在檔案或目錄上打印屬性的值。

#### 語法 {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### 選項 {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸 |
| `<propname>` | 屬性名稱 |
| `<file> [<file> ...]` | 從中獲取屬性的檔案或目錄 |

### Proplist {#proplist}

在檔案或目錄上打印屬性。

#### 語法 {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### 選項 {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸 |
| `<file> [<file> ...]` | 要列出屬性的檔案或目錄 |

### Propset {#propset}

在檔案或目錄上設定屬性的值。

>[!NOTE]
>
>VLT可識別以下特殊版本控制屬性：
>
>`vlt:mime-type`
>
>檔案的mimetype。 用於判斷是否要合併檔案。 以「text/」開頭的mimetype（或缺少的mimetype）被視為文本。 其他任何項目則視為二進位。

#### 語法 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### 選項 {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸 |
| `<propname>` | 屬性名稱 |
| `<propval>` | 屬性值 |
| `<file> [<file> ...]` | 將屬性設定為的檔案或目錄 |

### 新增 {#add}

將檔案和目錄置於版本控制之下，將其排程以添加到儲存庫。 將在下次提交時添加它們。

#### 語法 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### 選項 {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `--force` | 迫使行動進行 |
| `<file> [<file> ...]` | 添加本地檔案或目錄 |

### 刪除 {#delete}

從版本控制中刪除檔案和目錄。

#### 語法 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### 選項 {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `--force` | 迫使行動進行 |
| `<file> [<file> ...]` | 刪除本地檔案或目錄 |

### 差異 {#diff}

顯示兩個路徑之間的差異。

#### 語法 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### 選項 {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 檔案或目錄，以顯示 |

### 主控台 {#console}

執行互動式主控台。

#### 語法 {#syntax-16}

```shell
console -F <file>
```

#### 選項 {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | 指定控制台設定檔案。 預設檔案為console.properties。 |

### Rcp {#rcp}

將節點樹從一個遠程儲存庫複製到另一個。 `<src>` 指向源節點和 `<dst>` 指定必須存在父節點的目標路徑。 Rcp會透過串流資料來處理節點。

#### 語法 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### 選項 {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 盡可能少打印。 |
| `-r (--recursive)` | 遞歸下降。 |
| `-b (--batchSize) <size>` | 中間儲存之前要處理的節點數。 |
| `-t (--throttle) <seconds>` | 中間儲存後要等待的秒數。 |
| `-u (--update)` | 覆寫/刪除現有節點。 |
| `-n (--newer)` | 請遵照lastModified屬性進行更新。 |
| `-e (--exclude) <arg> [<arg> ...]` | 排除的源路徑的Regexp。 |
| `<src>` | 源樹的儲存庫地址。 |
| `<dst>` | 目標節點的儲存庫地址。 |

#### 範例 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>此 `--exclude` 選項後面接著另一個選項 `<src>` 和 `<dst>` 引數。 例如：
>
>`vlt rcp -e ".*\.txt" -r`

### 同步 {#sync}

允許控制保管庫同步服務。 在沒有任何參數的情況下，此命令將嘗試將當前工作目錄置於同步控制下。 如果在vlt結帳中執行，則會使用個別的篩選器和主機來設定同步。 如果在vlt簽出外執行，則只有當目錄為空時，它才註冊當前資料夾以進行同步。

#### 語法 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### 選項 {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出。 |
| `--force` | 強制執行某些命令。 |
| `-u (--uri) <uri>` | 指定同步主機的URI。 |
| `<command>` | 執行sync命令。 |
| `<localPath>` | 要同步的本地資料夾。 |

### 狀態代碼 {#status-codes}

VLT使用的狀態代碼為：

* 「 」沒有修改
* 新增「A」
* &#39;C&#39;衝突
* 已刪除&#39;D&#39;
* 「I」忽略
* 已修改&#39;M&#39;
* 已替換&#39;R&#39;
* &#39;?&#39; 項目不在版本控制下
* &#39;!&#39; 項缺失（由非svn命令刪除）或不完整
* 「~」版本化項目被不同類型的項目阻塞

## 設定FileVault同步 {#setting-up-filevault-sync}

保管庫同步服務用於將儲存庫內容與本地檔案系統表示同步，反之亦然。 這是通過安裝OSGi服務來實現的，該服務將監聽儲存庫更改並定期掃描檔案系統內容。 它使用與儲存庫相同的序列化格式將儲存庫內容映射到磁碟。

>[!NOTE]
>
>保管庫同步服務是一種開發工具，不建議在生產系統上使用它。 另請注意，服務只能與本地檔案系統同步，不能用於遠程開發。

### 使用vlt安裝服務 {#installing-the-service-using-vlt}

此 `vlt sync install` 命令可用於自動安裝保管庫同步服務包和配置。

套件組合安裝於下方 `/libs/crx/vault/install` 和設定節點建立於 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. 服務最初是啟用的，但未配置同步根。

以下範例將同步服務安裝至指定uri可存取的CRX執行個體。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### 顯示服務狀態 {#displaying-the-service-status}

此 `status` 命令可用於顯示有關正在運行的同步服務的資訊。&quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>此 `status` 命令不會從服務擷取任何即時資料，而會讀取設定，位於 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### 添加同步資料夾 {#adding-a-sync-folder}

此 `register` 命令用於添加要與配置同步的資料夾。

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>此 `register` 在配置 `sync-once` 設定。

### 刪除同步資料夾 {#removing-a-sync-folder}

此 `unregister` 命令用於從配置中刪除要同步的資料夾。

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>必須先註銷同步資料夾，然後才能刪除資料夾本身。

### 配置同步 {#configuring-synchronization}

#### 服務配置 {#service-configuration}

服務執行後，可使用下列參數進行設定：

* `vault.sync.syncroots`:定義同步根的一個或多個本地檔案系統路徑。

* `vault.sync.fscheckinterval`:應掃描檔案系統以進行更改的頻率（以秒為單位）。 預設為5秒。
* `vault.sync.enabled`:啟用/停用服務的一般標幟。

>[!NOTE]
>
>服務可以使用Web控制台或 `sling:OsgiConfig` 節點(具有名稱 `com.day.jcr.sync.impl.VaultSyncServiceImpl`)。
>
>使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

#### 同步資料夾配置 {#sync-folder-configuration}

每個同步資料夾都將配置和狀態儲存在三個檔案中：

* `.vlt-sync-config.properties`:設定檔。

* `.vlt-sync.log`:包含同步期間所執行操作相關資訊的記錄檔。
* `.vlt-sync-filter.xml`:定義要同步的儲存庫部分的篩選器。 此檔案的格式由 [執行篩選的結帳](#performing-a-filtered-checkout) 區段。

此 `.vlt-sync-config.properties` 檔案可讓您設定下列屬性：

**停用** 開啟或關閉同步。 預設情況下，此參數設為false以允許同步。

**同步一次** 如果非空白，則下次掃描會沿指定方向同步資料夾，則會清除參數。 支援兩個值：

* `JCR2FS`:將JCR儲存庫中的所有內容匯出並寫入本機磁碟。
* `FS2JCR`:將所有內容從磁碟匯入JCR存放庫。

**sync-log** 定義日誌檔案名。 預設情況下，值為.vlt-sync.log

### 使用VLT同步進行開發 {#using-vlt-sync-for-development}

若要根據同步資料夾來設定開發環境，請依照下列步驟進行：

1. 使用vlt命令列簽出儲存庫：

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >您可以使用篩選條件來僅結帳適當的路徑。 請參閱 [執行篩選的結帳](#performing-a-filtered-checkout) 一節。

1. 前往工作副本的根資料夾：

   ```shell
   $ cd dev/jcr_root/
   ```

1. 將同步服務安裝到儲存庫：

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. 初始化同步服務：

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. 編輯 `.vlt-sync-config.properties` 隱藏檔案並配置同步以同步儲存庫的內容：

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >此步驟會根據您的篩選設定下載整個存放庫。

1. 檢查日誌檔案 `.vlt-sync.log` 查看進度：

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

您的本機資料夾現在已與存放庫同步。 同步是雙向的，因此從儲存庫進行的修改將應用於本地同步資料夾，反之亦然。

>[!NOTE]
>
>「VLT同步」功能僅支援簡單檔案和資料夾，但檢測到特殊保管庫序列化檔案（.content.xml、dialog.xml等），並靜默忽略它們。 因此，可以在預設vlt結帳時使用保管庫同步。
