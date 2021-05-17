## How to Use Math AutoCorrect in Excel



**Summary**

**Use Math AutoCorrect Outside of Math Regions in Excel**

Excel does not have Word's native option available within the Excel Options ► Proofing ► AutoCorrect Options ► Math AutoCorrect for *Use Math AutoCorrect rules outside of math regions*. Likewise, much of the VBA functionality within Excel's VBE for the OMathAutoCorrect or OMathAutoCorrectEntries collection objects has been disabled. When Excel is within its own math editor, a different interface is being exchanged with and all symbols can be properly displayed but using AutoCorrect for the math symbols in regular worksheet operations is not available.

**Intended for Excel 2010 and 2013 (and other Office programs of the same versions)**

**Details**

How to get Math AutoCorrect into Everyday Excel Worksheet Operations

In my (admittedly uninformed) opinion, Excel's separation of standard and mathematical autocorrect and the subsequent crippling of the latter most likely has to do with several common math symbols being used for reserved purposes within Excel. The single quote (e.g. *tick* or ASCII 0×039) character being the most obvious one as it is used to force Excel to consider a number or date as text when used as a prefix. Suffice to say that there are legitimate reasons why the decision to isolate Excel's Math AutoCorrect was made while Word's was not.

This just means that we have to work around the limitation and accept any shortcomings. While Excel's VBA use of the OMathAutoCorrect object is somewhat crippled, the equivalent VBA in Word is not. If we take all of the entries from the OMathAutoCorrectEntries collection and convert them as additions to the standard AutoCorrectEntries collection, then they will be available within all Office programs including Excel. The end results in each of the Office programs may vary.

**Normalizing the Math AutoCorrect Entries with a Macro**

Close Excel and all other Office programs then open Word to a new blank document and tap Alt+F11 to enter the VBE. Use the pull-down menus to Insert ► Module (or Alt+I, M). Paste the following into the new pane titled something like *Normal - NewMacros (Code)* or *Normal - Module1 (Code)*.



Sub Normalize_Math_AutoCorrect_Entries()
   Dim acm As Long, ac As Long, yn As Long, cACEs As AutoCorrectEntries
   Set cACEs = Application.AutoCorrect.Entries
   With Application.OMathAutoCorrect
     .UseOutsideOMath = False   'no longer necessary
     For acm = 1 To .Entries.Count
       yn = vbYes
       For ac = 1 To cACEs.Count
         If cACEs(ac).Name = .Entries(acm).Name Then
            yn = MsgBox(cACEs(ac).Name & " is currently assigned to " & cACEs(ac).Value & _
             Chr(46) & Chr(10) & Chr(10) & "Are you sure you want to replace it?", _
             vbYesNo + vbQuestion, "Duplication")
           If yn = vbYes Then cACEs(ac).Delete
           Exit For
         End If
       Next ac
       If yn = vbYes Then
         Application.AutoCorrect.Entries.Add Name:=.Entries(acm).Name, _
​         Value:=.Entries(acm).Value
​      End If
​    Next acm
   End With
   Set cACEs = Nothing
 End Sub



With that in place, tap Alt+Q to return to your blank document. Tap Alt+F8 to open the Macros dialog and run the macro. If a duplicate entry is encountered, the process will be paused and you will be presented with something like the following.


                  ![Image](figures/2908ba3f-7915-4cb4-8286-14d47a76772a)

 Note that I have chosen to demonstrate one duplication that can actually be displayed. Many of the Unicode characters will only be represented by a **?** since a standard VBA message box cannot display Unicode. This does not mean that the symbol will be added incorrectly; like Excel this is simply a display limitation.

 Accept or reject the overwrites. Anything not already found within the standard AutoCorrectEntries collection will be added without asking.

 When this process is complete, all of the OMathAutoCorrect entries will have been normalized as standard AutoCorrect entries. If you open Excel, they should be available immediately. Here are some before and after screenshots first initiating the auto-correction process by typing the keyword then typing the space that forces the auto-correction event after \beta.



​      ![Image](figures/bc14d581-485c-41cc-a5e1-64c376fb5a40)      ![Image](figures/ff34ea1a-bb27-4bef-9fcd-8683c8aac227)





That is all there is to it. By converting the special Math AutoCorrect Entries to standard ones,  the limitation on using the special math symbol through auto-correction has been bypassed.



**References**



I've prepared a full listing of the Math AutoCorrect symbols on my OneDrive [here](http://1drv.ms/1vzWVmZ) for you to reference.

- [Excel_2013_OMathAutoCorrectEntries.xlsx](http://1drv.ms/1vzWVmZ)

On a related note, I wrote a local Wiki article a while back on a similar topic on the use of stylized fractions within Office programs through additions to the standard AutoCorrect collection. Here is a link to that:

- [Styled Fractions in Windows](http://answers.microsoft.com/en-us/office/wiki/office_2013_release-word/styled-fractions-in-windows/4a07d5fa-2484-4e39-b1f3-70bb3eb0c332)