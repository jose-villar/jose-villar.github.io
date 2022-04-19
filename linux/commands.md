# General Commands

- `df`: Report file system disk space usage.
- `find / -iname <nombreabuscar>`: Search in the root of the file system
- `tar -xzf *.tar.gz/zip`: Extract a .zip or .tar.gz
- `du -chs --exclude="*.txt" .`: Report file space usage in the current
  directory, excluding .txt files
- `ip r | grep default`: get gateway ip
- `find . -name '*.srt' -delete`: Find and delete recursively all .srt files in
  the current directory
- `fc-list : family style:` list available fonts.

# Media

## Video Editing

- Embed subtitles to a video:

    mkvmerge -o output.mkv video.mp4 subtitles.srt
