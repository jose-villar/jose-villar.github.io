# General Commands

- `find / -iname <nombreabuscar>`: Search in the root of the file system
- `tar -xzf *.tar.gz/zip`: Extract a .zip or .tar.gz
- `tar -czf compressed_archive.tar.gz *`: Create a compressed archive out of
  all the files in the current directory
- `ip r | grep default`: get gateway ip
- `find . -name '*.srt' -delete`: Find and delete recursively all .srt files in
  the current directory
- `fc-list : family style:` List available fonts.
- `grep -rl <string>`: List files with a given string, recursively.
- `cat input.txt | tr "\n" " " | rg --pcre2 "\b(\w+)\s+\1\b"`: Print out
  repeated consecutive words.
- `inxi -F`: Display system information
- `locale`: Get locale-specific information. For example:

```
LANG=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME=es_CL.UTF-8
LC_ADDRESS=es_CL.UTF-8
LC_TELEPHONE=es_CL.UTF-8
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION=es_CL.UTF-8
LC_ALL=
```

Use `localectl set-locale` to change any of the variables listed above. For
example:

`sudo localectl set-locale LANG=en_US.UTF-8`

# Disks

- `du -chs --exclude="*.txt" .`: Report file space usage in the current
  directory, excluding .txt files
- `df`: Report file system disk space usage.

- `lsblk`: list information about block devices, which typically include hard
  drives, solid-state drives, and other storage devices, as well as partitions on
  those devices.
- `sudo umount /dev/sdX`: Unmount device `sdX`.
- `sudo dd if=/path/to/iso of=/dev/sdX bs=4M status=progress`: write image to
  the USB drive. `if` stands for _input file_, `of` stands for _output file_,
  `bs=4M` means the _block size_ of _4M_ and `status=progress` is to show the
  progress. After the `dd` command finishes, run the following command to ensure
  that all data is written to the USB drive and it's safe to remove: `sync`
- `eject /dev/sdX`: Safely eject the USB drive from your system.

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

