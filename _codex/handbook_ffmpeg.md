# handbook ffmpeg

Generate the file list:

(for %f in (*.mp4) do @echo file '%f') > list.txt

Then merge:

ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4

Remove all original video audio
Add music.mp3 as the soundtrack

ffmpeg -f concat -safe 0 -i list.txt -stream_loop -1 -i music.mp3 -map 0:v -map 1:a -c:v copy -shortest final.mp4



overlay a GIF on top of a video and limit it to the first 5 seconds.

ffmpeg -i output.mp4 -ignore_loop 0 -i overlay.gif ^
-filter_complex "[0:v][1:v]overlay=(W-w)/2:(H-h)/2:enable='between(t,0,5)'" ^
-c:a copy final.mp4


ffmpeg -f concat -safe 0 -i list.txt -ignore_loop 0 -i skedit.gif -i "Yung Lean - Yoshi City.mp3" -filter_complex "[1:v]scale=iw*0.5:ih*0.5[gif];[0:v][gif]overlay=(W-w)/2:(H-h)/2:enable='between(t,0,5)'" -map 0:v -map 2:a -c:v libx264 -c:a aac -shortest final.mp4

ffmpeg -i output.mp4 -ignore_loop 0 -i skedit.gif ^
-filter_complex "[0:v][1:v]overlay=(W-w)/2:(H-h)/2:enable='between(t,0,5)'" ^
-c:a copy final.mp4


overlay a GIF on top of a video and limit it to the first 5 seconds and overlay a gif at each corner of screen at the 1/4 1/2 and 3/4 of video timeline.

for /f "tokens=1 delims=." %a in ('ffprobe -v error -show_entries format^=duration -of default^=nokey^=1:noprint_wrappers^=1 "OUTPUT_final.mp4"') do ffmpeg -i "OUTPUT_final.mp4" -ignore_loop 0 -i "C:\Users\6666666\Downloads\assets\skedit.gif" -i "C:\Users\6666666\Downloads\Yung Lean - Yoshi City.mp3" -filter_complex "[1:v]scale=iw*0.3:ih*0.3,split=13[start][c1][c2][c3][c4][c5][c6][c7][c8][c9][c10][c11][c12];[0:v][start]overlay=(W-w)/2:(H-h)/2:enable='between(t,0,5)'[v0];[v0][c1]overlay=10:10:enable='between(t,%a/4,%a/4+5)'[v1];[v1][c2]overlay=W-w-10:10:enable='between(t,%a/4,%a/4+5)'[v2];[v2][c3]overlay=10:H-h-10:enable='between(t,%a/4,%a/4+5)'[v3];[v3][c4]overlay=W-w-10:H-h-10:enable='between(t,%a/4,%a/4+5)'[v4];[v4][c5]overlay=10:10:enable='between(t,%a/2,%a/2+5)'[v5];[v5][c6]overlay=W-w-10:10:enable='between(t,%a/2,%a/2+5)'[v6];[v6][c7]overlay=10:H-h-10:enable='between(t,%a/2,%a/2+5)'[v7];[v7][c8]overlay=W-w-10:H-h-10:enable='between(t,%a/2,%a/2+5)'[v8];[v8][c9]overlay=10:10:enable='between(t,3*%a/4,3*%a/4+5)'[v9];[v9][c10]overlay=W-w-10:10:enable='between(t,3*%a/4,3*%a/4+5)'[v10];[v10][c11]overlay=10:H-h-10:enable='between(t,3*%a/4,3*%a/4+5)'[v11];[v11][c12]overlay=W-w-10:H-h-10:enable='between(t,3*%a/4,3*%a/4+5)'[v]" -map "[v]" -map 2:a -c:v libx264 -c:a aac -shortest final.mp4
