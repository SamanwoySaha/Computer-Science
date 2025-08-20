---
title: yt-dlp
draft: false
tags: 
date: 11-Aug-2025
---
# References
1. https://github.com/yt-dlp/yt-dlp

# Notes
```bash
# options
-S = video format
-P = download path
-o = output file format

# Download a youtube playlist
$ yt-dlp -S "res:720,fps" -P "<absolute-download-path>" -o "%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s" "<youtube-playlist-link>"

# Download all playlists of YouTube channel/user keeping each playlist in separate directory:
$ yt-dlp -o "%(uploader)s/%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s" "https://www.youtube.com/user/TheLinuxFoundation/playlists"

# Download a youtube video
$ yt-dlp -S "res:720,fps" -P "<download-path>" "<youtube-video-link>"
```



