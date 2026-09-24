# List all file
dir /b

# List all file except a specific folder
dir /b /s | findstr /v /i "\\FolderName\\"

# List files and folder in a tree structure
tree /F

## Files + folders, using ASCII characters:
tree /F /A
