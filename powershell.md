You can create an alias in PowerShell by adding a function to your profile. Here’s how to make touch behave like the New-Item command for file creation:

Open your PowerShell profile. You can edit it by running:

```
notepad $PROFILE
```

If the profile file doesn’t exist, this command will create it.

Add the following function to your profile file:

```
function touch {
    param (
        [string]$Path
    )

    if (Test-Path $Path) {
        # If the file exists, update its last write time
        (Get-Item -Path $Path).LastWriteTime = Get-Date
    } else {
        # If the file doesn't exist, create a new file
        New-Item -Path $Path -ItemType File | Out-Null
    }
}
```

Save and close the file, then reload your profile to apply the change:

```
. $PROFILE
```

Now you can use touch "filename.txt" in PowerShell to create a new file or update the timestamp of an existing file.
