
# Convert TS ke MP4

Saya membuat ini bertujuan untuk mengonversi video dalam format `.ts` (Transport Stream) menjadi format `.mp4` yang lebih umum digunakan.


## Gunakan Jupyter untuk konversi video

```py
import moviepy.editor as mpe
import glob, os

files = []
for pattern in ['*.ts', '**/*.ts', '**/**/*.ts', '**/**/**/*.ts']:
    files.extend(glob.glob(pattern))

for video in files:
    if video in files:
        filename = video
        input_file = video
        output_file = f"converted_{os.path.splitext(filename)[0]}.mp4"
    else:
        path = os.path.dirname(video)
        filename = os.path.basename(video)
        input_file = video
        output_file = os.path.join(path, os.path.splitext(filename)[0] + '.mp4')

    clip = mpe.VideoFileClip(input_file)
    clip.write_videofile(output_file)

    print(f"Video {filename} telah dikonversi menjadi {os.path.splitext(filename)[0]}.mp4") 
    
print("\nSemua video Anda telah berhasil dikonversi!")
```
Jika mempunyai CUDA dari NVIDIA, silakan gunakan untuk meningkatkan kecepatan dan efisiensi proses.

Sebagian besar proyek ini bergantung pada [FFmpeg](https://ffmpeg.org/download.html), jadi pastikan Anda telah menginstal FFmpeg di sistem Anda sebelum menggunakannya.






ubah bagian ini :
```
clip = mpe.VideoFileClip(input_file)
clip.write_videofile(output_file)
```
Menjadi :
```
ffmpeg_cmd = f'ffmpeg -hwaccel cuda -i "{input_file}" -c:v h264_nvenc "{output_file}"'
os.system(ffmpeg_cmd)
```

## Authors

- [@Zivalez](https://www.github.com/Zivalez)
