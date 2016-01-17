# Description
Purpose: when [Transmission](http://www.transmissionbt.com/) finishes downloading a torrent, auto-execute *"auto_download_subtitles.sh"*, which in turn will scan the torrent directory for any video files present, and download subtitles for each video file. 
By default the subtitles are in portuguese, but its possible to change them (see below)  

Install this script, configure Transmission, and all your finished torrents will automatically have subtitles for the videos (using [Filebot]https://www.filebot.net))  

NOTE: this script is made for Debian based linux distros. It will not work in Windows

# 1. Install 
```
## Dependencies: `Filebot`
cd /tmp && wget "http://filebot.sourceforge.net/download.php?type=deb&arch=i386" -O  filebot_latest_i386.deb
sudo dpkg -i filebot_latest_i386.deb
sudo apt-get -y -f install 
sudo dpkg -i filebot_latest_i386.deb
  # If you want to manually try filebot, do:
  #   MOVIE="/movie/some_movie.mkv"
  #   filebot --output srt --lang pt -get-subtitles $MOVIE

  
## Download the script `auto_download_subtitles.sh` 
cd $HOME
wget https://github.com/rjsteixeira/Transmission-torrent-subtitles/raw/master/auto_download_subtitles.sh 
chmod 777 auto_download_subtitles.sh
```

# 2. Configure filebot 

## 2.1 opensubtitles username and password for filebot
```
filebot -script fn:configure
```

If the above doesn't work because of permissions, set the credentials manually (assuming that /opt/filebot/ is filebot install dir):
```
 echo "net/filebot/osdb.user=OPENSUBS_USER\:OPENSUBS_PASSWORD" > /opt/filebot/prefs.properties
```

## 2.2 set the correct path of the filebot executable
Edit the `auto_download_subtitles.sh` file, changing the variable `FILEBOT`, example:
```
FILEBOT=/opt/filebot/filebot.sh
```

## 2.3 set the language you prefere
Edit the `auto_download_subtitles.sh` file, changing the variable `LANGUAGE_CODE`, example:
```
LANGUAGE_CODE="pt"
```

# 3. Configure Transmission
   - Open Transmission 
   - Edit / Preferences
   - Tab Torrents:
    + check: "Call script when torrent is completed" and point to => "auto_download_subtitles.sh"


# 4. All done - enjoy
  Download some torrent movie or TV show and check if the subtitles are automatically added :)

# Final notes
  + the downloading of subtitles is handled by [Filebot](http://filebot.sourceforge.net/), which fetches them from OpenSubtitles, Subscene and Sublight - these are community-made subtitles, and so may not exist for all movies/series. The more famous the movie, the more seeds/leechers the torrent will have, and therefore the more likely subtitles will exist.
  + if the subtitles downloaded automatically are not good, you can try to download other version of the subtitles (if available) manually, by opening yourself the `filebot` program, which is very easy to use

# Infos
  - Transmission scripts and environment variables: https://trac.transmissionbt.com/wiki/Scripts
  - Filebot usage from CLI: https://www.filebot.net/cli.html


