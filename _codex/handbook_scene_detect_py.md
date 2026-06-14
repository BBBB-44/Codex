# sceneDetect

## split video in a folder
cd /d C:\Users\6666666\Downloads\video1
for %f in (*.webm) do scenedetect -i "%f" detect-content split-video 

## Delete original only if SceneDetect succeeds
for %f in (*.webm *.mkv) do scenedetect -i "%f" detect-content split-video && del "%f"
