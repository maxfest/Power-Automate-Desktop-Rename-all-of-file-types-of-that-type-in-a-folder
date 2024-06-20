Did you know Power Automate Desktop flow can be copied and pasted as text? Now you know!
Copy the text bellow into a new flow to use:



/# Creator: Max Festersen Hansen
A flow that renames all file-names of a single type to another.
This has many use cases. Like bulk renaming zip to apk.
Note: This is only a renaming, there is no file conversion.#/
IF ReplaceUserWithWindowsUserName = $'''True''' THEN
    System.GetEnvironmentVariable.GetEnvironmentVariable Name: $'''USERNAME''' Value=> Username
    Text.Replace Text: Mappe TextToFind: $'''\\USER\\''' IsRegEx: False IgnoreCase: False ReplaceWith: $'''\\%Username%\\''' ActivateEscapeSequences: False Result=> Mappe
END
Folder.GetFiles Folder: Mappe FileFilter: $'''*.%FromFileType%''' IncludeSubfolders: False FailOnAccessDenied: True SortBy1: Folder.SortBy.NoSort SortDescending1: False SortBy2: Folder.SortBy.NoSort SortDescending2: False SortBy3: Folder.SortBy.NoSort SortDescending3: False Files=> Files
File.RenameFiles.RenameChangeExtension Files: Files NewExtension: ToFileType IfFileExists: File.IfExists.DoNothing RenamedFiles=> RenamedFiles
