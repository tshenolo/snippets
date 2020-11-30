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

### Java
coming soon

### Javascript
coming soon

### jQuery
coming soon

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

### Splunk
coming soon

### SQL
coming soon

### Windows
coming soon

### Wordpress
coming soon
