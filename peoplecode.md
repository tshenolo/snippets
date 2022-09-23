### PeopleCode
#### Compress Files
```
Function AddFileToZip(&zipInternalPath, &fileNameToZip, &zip)
   Local JavaObject &file = CreateJavaObject("java.io.File", &fileNameToZip);
   REM ** We will read &fileNameToZip into a buffer and write it out to &zip;
   Local JavaObject &buf = CreateJavaArray("byte[]", 1024);
   
   Local number &byteCount;
   Local JavaObject &in = CreateJavaObject("java.io.FileInputStream", &fileNameToZip);
   
   rem Local JavaObject &zipEntry = CreateJavaObject("java.util.zip.ZipEntry", &zipInternalPath | "/" | &file.getName());
   Local JavaObject &zipEntry = CreateJavaObject("java.util.zip.ZipEntry", &file.getName());
   
   REM ** Make sure zip entry retains original modified date;
   &zipEntry.setTime(&file.lastModified());
   
   &zip.putNextEntry(&zipEntry);
   
   &byteCount = &in.read(&buf);
   
   While &byteCount > 0
      &zip.write(&buf, 0, &byteCount);
      &byteCount = &in.read(&buf);
   End-While;
   
   &in.close();
   
   If &file.delete() Then
      MessageBox(0, "", 0, 0, "File Deleted: " | &file.getName());
   Else
      MessageBox(0, "", 0, 0, "File Not Deleted: " | &file.getName());
   End-If;
   
End-Function;


Local JavaObject &zip = CreateJavaObject("java.util.zip.ZipOutputStream", CreateJavaObject("java.io.FileOutputStream", "/temp/testfiles.zip", True));

AddFileToZip("folder1", "/temp/test1.txt", &zip);
AddFileToZip("folder1", "/temp/test2.txt", &zip);

&zip.flush();
&zip.close();
```


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