# List all file
dir /b

# List all file except a specific folder
dir /b /s | findstr /v /i "\\FolderName\\"
