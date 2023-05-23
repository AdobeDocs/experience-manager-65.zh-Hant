---
title: 備份和恢復EMC Documentum儲存庫
seo-title: Backing up and recovering the EMC Documentum repository
description: 本文檔介紹了備份和恢復為您的表單環境配置的EMC Documentum儲存庫所需AEM的任務。
seo-description: This document describes the tasks required to back up and recover the EMC Documentum repository configured for your AEM forms environment.
uuid: ab3b1fb1-25b3-4c95-801f-82d4b58f05ff
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f146202f-25f1-46a0-9943-c483f5f09f9f
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# 備份和恢復EMC Documentum儲存庫 {#backing-up-and-recovering-the-emc-documentum-repository}

本節介紹備份和恢復為您的表單環境配置的EMC Documentum儲存庫所需AEM的任務。

>[!NOTE]
>
>這些說明假定AEM已根據需要安裝並配置帶Connectors for ECM和EMC Documentum Content Server的表單。

對於備份和還原過程，有兩項主要任務：

* 備份（或恢復）表單AEM環境。
* 備份（或恢復）EMC Documentum Content Server。

>[!NOTE]
>
>在備份AEMEMC Documentum系統之前備份您的表單資料，然後在恢復表單環境之前恢復EMC DocumentumAEM系統。

## 軟體要求 {#software-requirements}

要在您的EMC Documentum Content Server上執行必要的備份任務，請從EMC購買適當的第三方應用工具，如EMC NetWorker或從CYA購買EMC Documentum的CYA SmartRecovery for EMC Documentum。 以下說明介紹了使用EMC NetWorker Module 7.2.2版的步驟。

您需要以下EMC NetWorker模組：

* NetWorker模組
* NetWorker配置嚮導
* NetWorker設備配置嚮導
* Content Server使用的資料庫類型的NetWorker Module
* NetWorker Module for Documentum

## 準備EMC Document Content Server以進行備份和恢復 {#preparing-the-emc-document-content-server-for-backup-and-recovery}

本節介紹在Content Server上安裝和配置EMC NetWorker軟體。

**準備EMC Documentum伺服器進行備份**

1. 在EMC Documentum Content Server上，安裝EMC NetWorker模組，接受所有預設值。

   在安裝過程中，系統會提示您輸入Content Server電腦的伺服器名稱， *NetWorker伺服器名稱*。 為資料庫安裝EMC NetWorker Module時，請選擇「完成」安裝。

1. 使用下面的示例內容，建立名為 *nsrnmd_win_cfg* 並將其保存到Content Server上的可訪問位置。 此檔案將由備份和還原命令調用。

   以下文本包含換行符的格式字元。 如果將此文本複製到此文檔之外的某個位置，則每次複製一部分，並在將其貼上到新位置時刪除格式字元。

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # Please refer to the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   保留配置檔案密碼欄位 `NMDDE_DM_PASSWD` 空白。 您將在下一步中設定密碼。

1. 按如下方式設定配置檔案密碼：

   * 開啟命令提示符，然後更改為 `[NetWorker_root]\Legato\nsr\bin`。
   * 運行以下命令： `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. 建立用於備份資料庫的可執行批處理(.bat)檔案。 （請參見NetWorker文檔。） 根據您的安裝設定批處理檔案中的詳細資訊。

   * 完整資料庫備份(nsrnmddbf.bat):

      `NetWorker_database_module_root` `-s`*&lt;networker_server_name>* `-U``[username]` `-P`*[密碼&#x200B;]*`-l full`*&lt;database_name>*

   * 增量資料庫備份(nsrnmddbi.bat):

      `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * 資料庫日誌備份(nsrnmddbl.bat):

      `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

      其中：

      `[NetWorker_database_module_root]` 是NetWorker模組的安裝目錄。 例如，NetWorker Module for SQL Server的預設安裝目錄為C:\Program Files\Legato\nsr\bin\nsrsqlsv。

      `NetWorker_Server_Name` 是NetWorker安裝的伺服器。

      `username` &amp; `password` 是資料庫管理員用戶的用戶名和密碼。

      `database_name` 是要備份的資料庫的名稱。

**建立備份設備**

1. 在EMC Documentum伺服器上建立新目錄，並通過向所有用戶授予完全權限來共用資料夾。
1. 啟動EMC NetWorker Administrator，然後按一下「介質管理」>「設備」。
1. 按一下右鍵「設備」，然後選擇「建立」。
1. 輸入以下值，然後按一下「確定」：

   **名稱：** 共用目錄的完整路徑

   **媒體類型：** `File`

1. 按一下右鍵新設備，然後選擇「操作」。
1. 按一下「標籤」，輸入名稱，按一下「確定」，然後按一下「裝載」。

將添加一個設備，備份的檔案將保存到該設備。 您可以添加多種不同格式的設備。

## 備份EMC Documentum Content Server {#back-up-the-emc-documentum-content-server}

完成表單資料的完整備份後，請執AEM行以下任務。 (請參閱 [備份表AEM單資料](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data)。)

>[!NOTE]
>
>命令指令碼需要在中建立的nsrnmd_win.cfg檔案的完整路徑 [準備EMC Document Content Server以進行備份和恢復](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery)。

1. 開啟命令提示符，然後更改為 `[NetWorker_root]\Legato\nsr\bin`。
1. 運行以下命令：

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## 恢復EMC Documentum Content Server {#restore-the-emc-documentum-content-server}

在還原表單資料之前，請執AEM行以下任務。 (請參閱 [恢復表AEM單資料](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data)。)

>[!NOTE]
>
>命令指令碼需要在中建立的nsrnmd_win.cfg檔案的完整路徑 [準備EMC Document Content Server以進行備份和恢復](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery)。

1. 停止要恢復的Docbase服務。
1. 啟動資料庫模組的NetWorker User Utility(例如， *NetWorker User for SQL Server*)。
1. 按一下「還原」工具，然後選擇「正常」。
1. 在螢幕的左側，選擇Docbase的資料庫，然後按一下工具欄上的「開始」按鈕。
1. 恢復資料庫後，重新啟動Docbase服務。
1. 開啟命令提示符，然後更改為 *[NetWorker_root]*\Legato\nsr\bin
1. 運行以下命令：

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
