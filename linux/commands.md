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

# Media

## Video Editing

- Embed subtitles to a video:

        mkvmerge -o output.mkv video.mp4 subtitles.srt

- Merge videos:

        mkvmerge -o output.mkv video1.mkv + video2.mkv

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
