---
---

# how to download yt video via url with cmd command

1. download yt dlp
```powershell
powershell -Command "Invoke-WebRequest https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp.exe -OutFile yt-dlp.exe"
```

2. Verify it downloaded correctly:
```powershell
yt-dlp.exe --version
```

3. To install it globally (so you can run yt-dlp from any folder):

```powershell
mkdir C:\Tools
move yt-dlp.exe C:\Tools\
setx PATH "%PATH%;C:\Tools"
```

4. Close the CMD window and open a new Command Prompt, then try:
```powershell
yt-dlp --version
```

5. Download ffmpeg (for thumbnail)
```powershell
winget install -e --id Gyan.ffmpeg
```

# Different download options :

## Download audio + thumbnail to a specific folder
```powershell
````

## Download youtube video to a specific folder:
```powershell
yt-dlp -P "C:\Users\6666666\Downloads\Video2" "https://www.youtube.com/watch?v=RkAv9L8naMI"
```

## Download only audio in a specific folder
```powershell
yt-dlp -f bestaudio -x -P "C:\Users\6666666\Downloads\Video2" --audio-format mp3 "https://www.youtube.com/watch?v=YWyHZNBz6FE"
```

## Download only audio
```powershell
yt-dlp -x --audio-format mp3 "URL_DE_LA_VIDÉO"
```
