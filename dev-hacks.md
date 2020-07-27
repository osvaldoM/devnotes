## Add pt/ any language to php storm 

- Download the UNICODE version fo the file (possible source [www.winedt.org](http://www.winedt.org/dict.html))
- Convert it from unicode-16 to utf-8 with iconv, e. g.:
- `$ iconv -f UTF-16 -t UTF-8 pt.dic > pt.utf-8.dic`
- Move the converted file back to its original name (or remove the original, just to avoid confusion).
- Move the file to one of the folders scanned by phpstorm( will be at __settings >> editor >> spelling dictionary tab__ )
- Restart phpStorm

### Start android emulator as _.root._ with writable _.fs._
credits to [answer one](https://stackoverflow.com/a/49427040/4043487) and [answer two](https://stackoverflow.com/a/49511666/4043487) 

- properly setup environemnt variables as described in answer two

list devices

    $ emulator -list-avds
    output: Nexus_5X_API_28_x86
    
    $ emulator -avd @Nexus_5X_API_26_x86 -writable-system 
    $ adb root
    $ adb remount
    
Generate public url for aws S3 file and copy to clipboard

    $ aws s3 presign s3://mybucket/myfile  --expires-in 90000 | clipcopy

### Replace text in multiple word documents

[https://www.extendoffice.com/documents/word/1002-word-replace-multiple-files.html]()

Sub CommandButton1_Click()
'Updated by Extendoffice 20180625
Dim xFileDialog As FileDialog, GetStr(1 To 100) As String '100 files is the maximum applying this code
Dim xFindStr As String
Dim xReplaceStr As String
Dim xDoc As Document
On Error Resume Next
Set xFileDialog = Application.FileDialog(msoFileDialogFilePicker)
With xFileDialog
    .Filters.Clear
    .Filters.Add "All WORD File ", "*.docx", 1
    .AllowMultiSelect = True
    i = 1
    If .Show = -1 Then
        For Each stiSelectedItem In .SelectedItems
            GetStr(i) = stiSelectedItem
            i = i + 1
        Next
        i = i - 1
    End If
    Application.ScreenUpdating = False
    xFindStr = InputBox("Find what:", "Kutools for Word", xFindStr)
    xReplaceStr = InputBox("Replace with:", "Kutools for Word", xReplaceStr)
    For j = 1 To i Step 1
        Set xDoc = Documents.Open(FileName:=GetStr(j), Visible:=True)
        Windows(GetStr(j)).Activate
        Selection.Find.ClearFormatting
        Selection.Find.Replacement.ClearFormatting
        With Selection.Find
            .Text = xFindStr  'Find What
            .Replacement.Text = xReplaceStr  'Replace With
            .Forward = True
            .Wrap = wdFindAsk
            .Format = False
            .MatchCase = False
            .MatchWholeWord = False
            .MatchByte = True
            .MatchWildcards = False
            .MatchSoundsLike = False
            .MatchAllWordForms = False
        End With
        Selection.Find.Execute Replace:=wdReplaceAll
        Application.Run macroname:="NEWMACROS"
        ActiveDocument.Save
        ActiveWindow.Close
    Next
    Application.ScreenUpdating = True
End With
MsgBox "Operation end, please view", vbInformation
End Sub

