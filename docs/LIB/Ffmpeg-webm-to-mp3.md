# Extract Audio from .WEBM to .MP3 using `ffmpeg`

Soruce: 

- <https://bytefreaks.net/gnulinux/bash/ffmpeg-extract-audio-from-webm-to-mp3>
- <https://computingforgeeks.com/how-to-convert-mp4-to-mp3-on-linux/>

## Install `ffmpeg` and tools

Arch:

```sh
sudo pacman -S lame ffmpeg
```

Debian:

```sh
sudo apt -y install ffmpeg lame
```

## Convert a Single file from `.webm` to `.mp3` using `ffmpeg`

If you need to extract the audio from an `.WEBM` movie file to an `.MP3` audio 
file you can  execute the following:

```sh
FILE="the-file-you-want-to-process.webm";
ffmpeg -i "${FILE}" -vn -ab 128k -ar 44100 -y "${FILE%.webm}.mp3";
```

The first command will assign the file name to a variable, we do this to avoid 
typing errors in the second command where we might want to use the same name 
for the audio file.

The second command, will use ffmpeg to extract the audio. The -i flag, indicates the file name of the input. We used the flag -vn that will instruct ffmpeg to disable video recording. The -ab flag will set the bit rate to 128k. The -ar flag will set the audio sample rate to 441000 Hz.  The -y flag will overwrite output file without asking, so be careful when you use it.

## Convert All Files in a Directory from `.webm` to `.mp3` using `ffmpeg`

```sh
find . -type f -iname "*.webm" \
	-exec bash -c 'FILE="$1"; ffmpeg -i "${FILE}" -vn -ab 128k -ar 44100 -y "${FILE%.webm}.mp3";' _ '{}' \;
```

The filename of the audio file will be the same as the webm video with 
the correct extension. The `webm` extension will be removed and replaced by 
the `mp3` extension e.g `hi.webm` will become `hi.mp3`.

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)


