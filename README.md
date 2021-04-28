## Snippets
These are some of my favorite code snippets.


### CakePHP
#### Create a CakePHP Project
```bash
composer create-project --prefer-dist cakephp/app:^3.9 my_app_name
```

#### Create a controller for a table called users
```bash
bin/cake bake controller Users
```

#### Create a model (and entity) for a table called users
```bash
bin/cake bake model Users
```

#### Create the default template files for a table (add/edit/view/index)
```bash
bin/cake bake template Users
```

#### Bake add/edit/view/index using one command
```bash
bin/cake bake all Users
```

#### Bake just the index template file
```bash
bin/cake bake template Users index
```

### Ionic
#### Install Ionic
```bash
npm install -g @ionic/cli
```

#### Create a Ionic Project
```bash
ionic start   <my_app_name>  <template> [options]
```

| Template	  | Description                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------|
| tabs	      | A starting project with a simple tabbed interface                                                        |
| blank	      | A blank starter project                                                                                  |
| sidemenu    |	A starting project with a side menu with navigation in the content area                                  |
| super	      | A starting project complete with pre-built pages, providers and best practices for Ionic development.    |
| conference  |	A project that demonstrates a realworld application                                                      |
| tutorial	  | A tutorial based project that goes along with the Ionic documentation                                    |
| aws	        | AWS Mobile Hub Starter                                                                                   |


#### Run Locally in a Web Browser
```bash
ionic serve
```

#### Adding a new page
```bash
ionic g page login
```

#### Routing to another page
```TypeScript
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-gamelevels',
  templateUrl: './gamelevels.page.html',
  styleUrls: ['./gamelevels.page.scss'],
})
export class GamelevelsPage implements OnInit {

  constructor(private router: Router) {}

  ngOnInit() {
  }

  playgame(level:number){
    this.router.navigate(['gameplay', level ]);
  }

}
```

#### Integrating JQuery
```bash
npm install jquery --save
npm install @types/jquery
```

#### Import jquery on your page like this
```TypeScript
import * as $ from "jquery";
```


### Linux
#### Convert jpg to PDF (3 steps)
#### Install the ImageMagick package (step 1)
```bash
sudo apt-get install imagemagick
```

#### List files as a single column (step 2)
```bash
ls -v --format single-column *.jpg
```

#### Convert images to PDF (step 3)
```bash
convert `ls -v --format single-column *.jpg` FileName.pdf
```

#### Reload .File (.bashrc , .profile)
```bash
source ~/.File
```

#### Create Bash Alias
```bash
alias workspace="cd /mnt/f/Users/username/Documents/workspace"
```
##### Usage:
```bash
workspace
```

#### Create Bash Function
```bash
function deployd4() { mvninstall; chmod 664 "$@"; scp "$@" SERVER04:~/.w;}
```
##### Usage:
```bash
deployd4 target/app.war
```

#### Copy Remote File
```bash
scp username@server:/tmp/filename.txt .
```

#### Copy Remote File (passing password to command)
```bash
sshpass -p 'password' scp username@server:/tmp/filename.txt .
```

#### Editing remote files via scp in vim
```bash
vim scp://remoteuser@server//absolute/path/to/document
```

#### ssh-keyscan
```bash
ssh-keyscan -t <dsa | rsa> <SERVER>
```


### PeopleCode
#### Select a single row of data
```
/* Read class name and parameter record name from the database. */ 
SQLExec("SELECT RECNAME, FIELDNAME, PC_EVENT_TYPE, PC_FUNCTION_NAME FROM PSROLEDEFN WHERE ROLENAME= :1", &ROLENAME, &rec, &fld, &pce, &pcf);
```

#### Select Multiple rows of data
```
Local SQL &SQL; 
Local Record &REC; 
  
&REC = CreateRecord(RECORD.TRANS_TBL); 
&SQL = CreateSQL("%SelectAll(:1) WHERE PROCESSED <> 'Y'");  
  
&SQL.Execute(&REC); 
While &SQL.Fetch(&REC) 
/* do processing */ 
...  
End-While;
```

#### Run BI Publisher Report via PSXP_RPTDEFNMANAGER
```
import PSXP_RPTDEFNMANAGER:*;

/*Create Report*/
Function CreateReport(&reportDefnId, &templateName, &reportName)
    
    MessageBox(0, "", 0, 0, "Processing Report: %1", &reportName);
    
    Local string &languageCode = "ENG";
    Local string &outputFormat = "PDF";
    Local date &AsOfDate = %Date;
    Local string &folderName = "General";
    Local number &PID = MCM_GRDADM_AET.PROCESS_INSTANCE;
    
    /* Initializing Report Def class Object */
    Local PSXP_RPTDEFNMANAGER:ReportDefn &rptDefn = create PSXP_RPTDEFNMANAGER:ReportDefn(&reportDefnId);
    &rptDefn.Get();
    rem &rptDefn.OutDestination = %FilePath;
    &rptDefn.ReportFileName = &reportName;
    &rptDefn.ProcessReport(&templateName, &languageCode, &AsOfDate, &outputFormat);
    rem CommitWork();
    rem &rptDefn.DisplayOutput();
    &rptDefn.Publish("", "", &folderName, &PID);
    
    MessageBox(0, "", 0, 0, "Posted Report: %1", &reportName);
    
End-Function;

/*Declare and Initialize Variables/
Local string &reportDefnId = "<Report_Defition_Id>";
Local string &templateName = "<Template_Name>";
Local string &reportName = "<Report_Name>";

/*Call Create Report Function*/
CreateReport(&reportDefnId, &templateName, &reportName);
```

#### Run BI Publisher Via PSXPQRYRPT App Engine
```
/*Create Report*/
Function CreateReport(&runctrl)
   
  Local string &AppEngineName;
  Local ProcessRequest &RQST;
  &AppEngineName = "PSXPQRYRPT";
  &RQST = CreateProcessRequest("XML Publisher", &AppEngineName);
  &RQST.OutDestType = "Web";
  &RQST.OutDestFormat = "PDF";
  &RQST.RunControlID = &runctrl;
  rem &RQST.RunLocation = "PSUNX";
  &RQST.Schedule();
  
End-Function;

/*Declare and Initialize Run Control ID variable/
Local string &runctrl = "<RunControlID>";

/*Call Create Report Function*/
CreateReport(&runctrl);

```

#### Run PS Job
```
/*Function name : Run Process*/
Function RunProcess(&ProcessName)
    MessageBox(0, "", 0, 0, "Run %1", &ProcessName);
    
    /* Create the ProcessRequest Object & Run the Scheduled JobSet Now */
    Local ProcessRequest &JobRQST;
    Local integer &instanceList;
    
    /* SetupScheduleDefnItem(ScheduleName, JobName)*/
    &JobRQST = SetupScheduleDefnItem(&ProcessName, &ProcessName);
    &JobRQST.RunJobSetNow();
    &PRCSINSTANCE = &JobRQST.ProcessInstance;
    &PRCSSTATUS = &JobRQST.Status;
    If &PRCSSTATUS = 0 Then
      MessageBox(0, "", 0, 0, "Process Instance: %1", &PRCSINSTANCE);
    Else
      MessageBox(0, "", 0, 0, "Process Not submitted");
    End-If;
    
End-Function;

/*Declare and Initialize Process Name Variable*/
Local string &processName = "<Process_Name>";

/*Call Run Process Function */
RunProcess(&processName);
```

#### Scaling FLUID pages for iPhone
```
Declare Function GetDefaultViewportSetting PeopleCode PTLAYOUT.FUNCLIB FieldFormula;
Declare Function SetViewport PeopleCode PTLAYOUT.FUNCLIB FieldFormula;

Local string &Viewport;
Local number &Pos;

&Viewport = GetDefaultViewportSetting();

If %Request.BrowserDeviceFormFactor = 0 And
      %Request.BrowserPlatformClass = "ios" Then
    &Pos = Find("minimal-ui", &Viewport);
    If &Pos = 0 Then
      &Viewport = &Viewport | ", minimal-ui";
    End-If;
End-If;

SetViewport(&Viewport);
AddMetaTag("format-detection", "telephone=no");
```

#### File Layout Line Break
```
Local string &CRLF = Char(13) | Char(10);

&FILE.SetFileLayout(FileLayout.MCM_PER_UPSYNC);
&FILE.SetRecTerminator(&CRLF); 
```

#### CREF Date Change
```
Local ApiObject &Portal;
Local string &PORTAL_NAME = "EMPLOYEE";
Local string &CRefName = "MCM_TILE_TOGGLE";

&Portal = %Session.GetPortalRegistry();
&Portal.Open(&PORTAL_NAME);
rem &CRef = &Portal.FindCRefByName(&CRefName);
&CRefLink = &Portal.FindCRefLinkByName(&CRefName);

MessageBox(0, "", 0, 0, "ValidFrom: %1", &CRefLink.ValidFrom);
MessageBox(0, "", 0, 0, "ValidTo: %1", &CRefLink.ValidTo);

Local date &newDate = AddToDate(%Date, 0, 0, 10);
&CRefLink.ValidTo = &newDate;

MessageBox(0, "", 0, 0, "New ValidTo: %1", &CRefLink.ValidTo);

&CRefLink.Save();
```

#### Create a File
```
Local string &sFileName = "triggerfile.txt";
Local File &exportFile = GetFile(GetURL(URL.FILE_REPO) | "/OUT/" | &sFileName, "W", %FilePath_Absolute);

If &exportFile.IsOpen Then
  &exportFile.WriteLine("");
  &exportFile.Close();
Else
  MessageBox(0, "", 0, 0, "Error cannot open file %1", &sFileName);
  Exit (0);
End-If;
```

#### Read a File
```
Local File &MYFILE;
Local array of string &MYARRAY;
Local string &TEXT;
&MYFILE = GetFile("names.txt", "R", "UTF8BOM");
&MYARRAY = CreateArrayRept("", 0);
While &MYFILE.ReadLine(&TEXT);
    &MYARRAY.Push(&TEXT);
End-While;
&MYFILE.Close();
```

#### IB Publish Message
PeopleCode used to publish the LOCATION_SYNC service operation. This code has been placed in the SavePostChange event in the SETID field in the LOCATION_TBL record.
```
Local Message &MSG;

&MSG = CreateMessage(Operation.LOCATION_SYNC, %IntBroker_Request);
&MSG.CopyRowsetDelta(GetLevel0()(1).GetRowset(Scroll.LOCATION_TBL));
%IntBroker.Publish(&MSG);
```

#### Call an App Engine program immediately
```
/* Set the state record for the App Engine */
Local Record &stateRec;

&stateRec = CreateRecord(Record.STATE_REC_AET);
&stateRec.EMPLID.Value = <EMPLID>;
&stateRec.ITEM_TYPE.Value = <ITEM_TYPE>;

CallAppEngine("<APP_ENGINE_NAME>", &stateRec);
  
```

#### Using SQLExec and Record Objects
```
Local Record &recO;
&recO = CreateRecord(Record.PSOPRDEFN);
SQLExec("%selectall(:1) WHERE PSOPRDEFN.EMPLID = :2", &recO, "EE2343", &recO);  
```

#### Calculate SHA-256 Checksum for an Input String 
```
SQLExec("SELECT CAST(STANDARD_HASH ( '<INPUT>', 'SHA256') AS CHAR(100)) FROM DUAL;", &SHAHex);
MessageBox(0, "", 0, 0, "" | &SHAHex);  
```

#### Left-pad and right-pad string functions
```
/*Left Pad Function*/
Function lpad(&in_string As string, &length As number, &pad_char As string) Returns string

  If Len(&in_string) < &length Then
  &in_string = Rept(&pad_char, &length - Len(&in_string)) |
        &in_string;
  End-If;

  Return &in_string;

End-Function;

/*Right Pad Function*/
Function rpad(&in_string As string, &length As number, &pad_char As string) Returns string

  If Len(&in_string) < &length Then
  &in_string = &in_string |
        Rept(&pad_char, &length - Len(&in_string));
  End-If;

  Return &in_string;

End-Function;

Local string &num_char = "123";
&num_char = lpad(&num_char, 10, "0");
MessageBox(0, "", 0, "" | &num_char);
  
```

#### Copy File
```
/*Copy File*/
Function copyFile(&filePath, &destinationPath) Returns boolean;
   
    try
       
       Local JavaObject &file = CreateJavaObject("java.io.File", &filePath);
       Local JavaObject &dest = CreateJavaObject("java.io.File", &destinationPath);
       Local boolean &success = &file.renameTo(&dest);
       If Not &success Then
          throw CreateException(0, 0, "Unable to move file " | &filePath | " to " | &destinationPath | ".");
       Else
          Return True;
       End-If;
       
    catch Exception &Err
       Warning (&Err.ToString());
       Return False;
    end-try;
    
End-Function;

/*Declare variables*/
Local string &file1 = "H:\temp\test1\mcmaps-extract.csv";
Local string &file2 = "H:\temp\test2\mcmaps-extract.csv";

/*Copy Files*/
If copyFileTo(&file1, &file2) Then
  MessageBox(0, "", 0, 0, "Success");
Else
  MessageBox(0, "", 0, 0, "fail");
End-If;
   
```

#### Set the root log4j level
Where standard levels are ALL < TRACE < DEBUG < INFO < WARN < ERROR < FATAL < OFF
```
Function SetTraceOn
   
   GetJavaClass("org.apache.logging.log4j.core.config.Configurator").initialize(CreateJavaObject("org.apache.logging.log4j.core.config.DefaultConfiguration"));
   GetJavaClass("org.apache.logging.log4j.core.config.Configurator").setRootLevel(GetJavaClass("org.apache.logging.log4j.Level").INFO);
   
End-Function;
```

### SQL
#### Alter Session
```
ALTER SESSION SET CURRENT_SCHEMA=SYSADM;
```

#### Unlock Account
```
ALTER USER oracledbuser ACCOUNT UNLOCK;
```

#### Create User with User Permissions
```
CREATE USER oracledbuser IDENTIFIED BY password
QUOTA UNLIMITED ON SYSTEM
QUOTA UNLIMITED ON SYSAUX;

GRANT CREATE SESSION TO oracledbuser;

GRANT CREATE TABLE TO oracledbuser;

GRANT SELECT_CATALOG_ROLE TO oracledbuser; 

GRANT EXECUTE_CATALOG_ROLE TO oracledbuser;

EXECUTE DBMS_STREAMS_AUTH.GRANT_ADMIN_PRIVILEGE(grantee => 'oracledbuser');

GRANT UNLIMITED TABLESPACE TO oracledbuser;

GRANT RESOURCE TO oracledbuser;

ALTER USER oracledbuser QUOTA unlimited ON system;

GRANT UNLIMITED TABLESPACE TO oracledbuser;
```

#### Create table, Sequence, Trigger
```
CREATE TABLE "SOFTWARE" (
"SOFTWARE_ID"      NUMBER(10,0) NOT NULL ENABLE,
"SOFTWARE_VERSION" VARCHAR2(255 BYTE),
"SOFTWARE_TITLE"   VARCHAR2(255 BYTE),
"COMP_LAB"         NUMBER(10,0),
PRIMARY KEY ("SOFTWARE_ID"));

CREATE SEQUENCE SOFTWARE_SEQUENCE START WITH 1 INCREMENT BY 1;

CREATE OR REPLACE TRIGGER SOFTWARE_trigger
BEFORE INSERT
ON SOFTWARE
REFERENCING NEW AS NEW
FOR EACH ROW
BEGIN
SELECT SOFTWARE_SEQUENCE.nextval INTO :NEW.software_id FROM dual;
END;
```

#### Drop all tables, constraints, and sequences in a Schema
```
BEGIN

FOR c IN (SELECT table_name FROM user_tables) LOOP
EXECUTE IMMEDIATE ('DROP TABLE ' || c.table_name || ' CASCADE CONSTRAINTS');
END LOOP;

FOR s IN (SELECT sequence_name FROM user_sequences) LOOP
EXECUTE IMMEDIATE ('DROP SEQUENCE ' || s.sequence_name);
END LOOP;

END;
```

#### Grant select, insert, update, delete
```
GRANT SELECT, INSERT, UPDATE, DELETE ON SYSADM.TABLENAME TO PUBLIC;
```

#### How to Find PeopleSoft Processes/PSJobs in a Recurrence
```
SELECT PROCESS_JOB_NAME,
  DESCRIPTION,
  RECURNAME
FROM PS_PRCSRECUR A,
  (SELECT P.PRCSNAME AS PROCESS_JOB_NAME,
    P.DESCR          AS DESCRIPTION,
    P.RECURNAME      AS RECURNAME
  FROM PS_PRCSDEFN P
  UNION
  SELECT JP.PRCSJOBAME AS PROCESS_JOB_NAME,
    (SELECT J.DESCR FROM PS_PRCSDEFN J WHERE J.PRCSNAME = JP.PRCSNAME
    )            AS DESCRIPTION,
    JP.RECURNAME AS RECURNAME
  FROM PS_PRCSJOBDEFN J,
    PS_PRCSJOBITEM JP
  WHERE J.PRCSJOBNAME = JP.PRCSJOBNAME
  ) B
WHERE B.RECURNAME = A.RECURNAME
AND A.RECURNAME   = :1
ORDER BY 1;
```

#### Find/Unlock PeopleSoft Objects
```
-- Find locked PeopleSoft Object
SELECT * FROM PSCHGCTLLOCK WHERE OPRID = :UserId;

-- Delete locked PeopleSoft Object
DELETE FROM PSCHGCTLLOCK WHERE OPRID = :userId AND OBJECTVALUE1 = :ObjectName; 
```

#### Find navigations where a process is attached
```
SELECT A.PORTAL_URI_SEG2,
    RTRIM(E.PORTAL_LABEL)
    || ' >> '
    || RTRIM(D.PORTAL_LABEL)
    || ' >> '
    || RTRIM(C.PORTAL_LABEL)
    || ' >> '
    || RTRIM(B.PORTAL_LABEL)
    || ' >> '
    || RTRIM(A.PORTAL_LABEL)
  FROM PSPRSMDEFN A
  LEFT JOIN PSPRSMDEFN B
  ON B.PORTAL_NAME     = A.PORTAL_NAME
  AND B.PORTAL_OBJNAME = A.PORTAL_PRNTOBJNAME
  LEFT JOIN PSPRSMDEFN C
  ON C.PORTAL_NAME     = B.PORTAL_NAME
  AND C.PORTAL_OBJNAME = B.PORTAL_PRNTOBJNAME
  LEFT JOIN PSPRSMDEFN D
  ON D.PORTAL_NAME     = C.PORTAL_NAME
  AND D.PORTAL_OBJNAME = C.PORTAL_PRNTOBJNAME
  LEFT JOIN PSPRSMDEFN E
  ON E.PORTAL_NAME         = D.PORTAL_NAME
  AND E.PORTAL_OBJNAME     = D.PORTAL_PRNTOBJNAME
  WHERE A.PORTAL_URI_SEG2 IN
    (SELECT PNLGRPNAME FROM PS_PRCSDEFNPNL P WHERE P.PRCSNAME = :PROCESS_NAME );
```

#### Find Records and Fields used in a PeopleSoft Page
```
-- SQL Query to find all the Records and Fields used in a PeopleSoft page:
SELECT RECNAME,
  FIELDNAME
FROM PSPNLFIELD
WHERE PNLNAME = :PAGENAME;

-- SQL Query to find all the Records where a particular PeopleSoft field is used:
SELECT DISTINCT RECNAME,
  FIELDNAME
FROM PSRECFIELD
WHERE FIELDNAME = :FIELDNAME;

-- SQL query to find all the page names where a field is used from a particular record:
SELECT PNLNAME
FROM PSPNLFIELD
WHERE RECNAME = :RECORDNAME
AND FIELDNAME = :FIELDNAME;
```

#### Optional Prompts/Criteria
```
SELECT * FROM TABLENAME WHERE FIELDNAME = :1 OR TRIM(:1) IS NULL;
```

### Windows
#### Find charset of a file
```
file -i filename
```

#### Converting files to UTF-8
```
iconv -f original_charset -t utf-8 originalfile > newfile
```

#### List directories in a folder
```
dir /s /b /o:n /ad
```

#### List File names only
```
dir /b /a-d
```

#### List Folders and Sub folders
```
dir /s /b /o:n /ad
```

#### Mount to nfs on windows
```
mount -o anon \\<IPADDRESS>\<DRIVE> Z:
```

#### Get SSL Certificate
```
openssl s_client -connect <SERVER>:<PORT> < /dev/null | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > <SERVER>.crt
```














