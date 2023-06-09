# General Commands

- `df`: Report file system disk space usage.
- `find / -iname <nombreabuscar>`: Search in the root of the file system
- `tar -xzf *.tar.gz/zip`: Extract a .zip or .tar.gz
- `tar -czf compressed_archive.tar.gz *`: Create a compressed archive out of
  all the files in the current directory
- `du -chs --exclude="*.txt" .`: Report file space usage in the current
  directory, excluding .txt files
- `ip r | grep default`: get gateway ip
- `find . -name '*.srt' -delete`: Find and delete recursively all .srt files in
  the current directory
- `fc-list : family style:` List available fonts.
- `grep -rl <string>`: List files with a given string, recursively.
- `cat input.txt | tr "\n" " " | rg --pcre2 "\b(\w+)\s+\1\b"`: Print out
  repeated consecutive words.
- `inxi -F`: Display system information

# Media

## Video Editing

- Embed subtitles to a video:

        mkvmerge -o output.mkv video.mp4 subtitles.srt

- Merge videos:

        # these 2 ways are equivalent
        mkvmerge -o output.mkv video1.mkv + video2.mkv
        mkvmerge -o output.mkv '[' video1.mkv video2.mkv ']'

        mkvmerge -o output.mkv 1.mkv + 2.mkv --generate-chapters when-appending

        # join all the videos together
        mkvmerge -o output.mkv '[' * ']'


- Get information of a video:

        mkvmerge --identify input.mkv

- Get audio:

        ffmpeg -i video.mp4 audio.mp3

        mkvmerge -D input.mkv -o audio.aac

        # mkvmerge options:
        -A, --no-audio
        -D, --no-video
        -S, --no-subtitles
        -B, --no-buttons
        -T, --no-track-tags
        --no-chapters
        -M, --no-attachments
        --no-global-tags

- Remove audio

        mkvmerge -A input.mkv -o output.mkv

- Add audio to video:

        mkvmerge input.mkv audio.mp3 -o output.mkv

- Record audio:

        # Pick the name of a source and use it instead of default
        pactl list sources
        ffmpeg -f pulse -i default output.wav

- Trim audio:

        ffmpeg -i input.wav -ss 20 -to 40 -c copy out.wav

- Trim a video

        # The output will last 20 seconds
        ffmpeg -ss 00:00:10 -to 00:00:30 -i input.mkv -c copy output.mkv

- Split a video

        # Split video into a part of 7 seconds and the rest
        ffmpeg -i input.mkv -to 07 -c copy p1.mkv -ss 07 -c copy p2.mkv

- Decrease image resolution

        # Generate an image 20px wide, keeping its aspect ratio
        ffmpeg -i img.jpg -vf scale=20:-1 img-small.jpg

