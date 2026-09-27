# List all file
dir /b

# List all file except a specific folder
dir /b /s | findstr /v /i "\\FolderName\\"

# List files and folder in a tree structure
tree /F

## Files + folders, using ASCII characters:
tree /F /A

# Create and open a new text file directly in Notepad+
*Notice: To create and open a text file directly using the notepad++ file_name.txt command, you must first add Notepad++ to your system's Environment Variables.

notepad++ file_name.txt



----------------------------

# Environment variable modification

## Step 1: Copy the Notepad++ Installation Path

   1. Open File Explorer.
   2. Navigate to C:\Program Files\Notepad++ (or C:\Program Files (x86)\Notepad++).
   3. Click inside the address bar at the top and copy the text path (Ctrl + C).

## Step 2: Add Notepad++ to Environment Variables

   1. Press the Windows Key, type sysdm.cpl, and press Enter to open System Properties.
   2. Navigate to the Advanced tab.
   3. Click the Environment Variables... button at the bottom.
   4. Under the System variables section (bottom pane), scroll down to find the variable named Path, select it, and click Edit....
   5. Click the New button on the right, then paste (Ctrl + V) the folder path copied in Step 1.
   6. Click OK on all open windows to save the changes.

## Step 3: Verify and Test the Setup

   1. Close any active Command Prompt (CMD) windows.
   2. Open a new Command Prompt window to reload the updated path settings.
   3. Run the following command to test the integration:
   
   notepad++ file_name.txt
   
   

