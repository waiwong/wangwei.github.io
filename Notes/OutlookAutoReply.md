# Note for outlook auto reply

Sample of source code.

<p>

```vbnet
Public WithEvents xlItems As Outlook.Items

Private Sub Application_Startup()
    Set xlItems = Session.GetDefaultFolder(olFolderInbox).Items
    
    'MsgBox xlItems.Count
    For Each myItem In xlItems
        If (myItem.Class = olMail) Then
            'myItem.Display
            'MsgBox myItem.FullName & ": " & myItem.LastModificationTime
            Exit For
        End If
    Next
    
End Sub

Private Sub xlItems_ItemAdd(ByVal objItem As Object)
    Dim xlReply As MailItem
    Dim xStr As String
    If objItem.Class <> olMail Then Exit Sub
    
    Set xlReply = objItem.ReplyAll
    With xlReply
         xStr = "<p>" & "Hi, Your email has been received. Thank you!" & "</p>"
         xStr = xStr & "<br />objItem.Subject: " & objItem.Subject
         xStr = xStr & "<br />objItem.Sender:" & objItem.Sender
         If objItem.CC <> Null Then
            xStr = xStr & "<br />objItem.CC:" & objItem.CC
         End If
         
         .HTMLBody = xStr & .HTMLBody
         '.Send
         .Save
    End With
End Sub

```
</p>

ref [source](https://www.datanumen.com/blogs/auto-reply-original-email-predefined-text-via-outlook-vba/)
and [microsoft vba](https://docs.microsoft.com/en-us/office/vba/api/outlook.mailitem)

### Run in Developer Mode
If you can see the Developer tab, you are running in developer mode. Otherwise, follow these steps to run in developer mode:
1. Click the File tab.
2. Click Options.
3. Click Customize Ribbon.
4. Select the Developer check box.