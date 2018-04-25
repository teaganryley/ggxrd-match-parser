![Example output html screenshot](https://raw.githubusercontent.com/nxths/ggxrd-match-parser/master/screenshots/example.jpg)

# Overview
This project is for parsing out matches from youtube videos for Guilty Gear Xrd. Specifically, these scripts will generate an html file containing match start times with character names. See example screenshot above, each match is a timestamped youtube video link.

* ``ggxrd-match-parser.py``: Main script for downloading and parsing youtube videos, run with ``--help`` for more details. See comment towards top of source file, should edit variable for the masks/ path before running.
* ``ggxrd-rss-match-parser.py``: Utility script to run the match parser over a series of videos from a youtube RSS feed. See comment towards top of source file, should edit variables for the RSS url and paths before running.

The scripts should be cross platform but have only been tested on linux and windows.

# Dependencies
* [python 3.x](https://www.python.org/)
* [moviepy](https://zulko.github.io/moviepy/) (may need to upgrade pip itself first before installing through pip)
  * [ffmpeg](https://www.ffmpeg.org/)
* [youtube-dl](https://rg3.github.io/youtube-dl/) (needs to be in PATH)

# Limitations
The image analysis is comically simple so there's a number of limitations:
* Videos must be raw gameplay footage, any picture-in-picture which shifts/resizes the game screen will break the image analysis. Video overlays should be ok if they don't obscure the top or center of the screen.
* Live streaming videos are unsupported.
* The 144p format must be available for the youtube video. Unclear if this is guaranteed, but haven't found any contrary examples.
* The demo, training, and MOM mode detection is crappy so they may show up in the processed matches.

# Errors
* ``ERROR: requested format not available`` typically caused by trying to download a live streaming video. These can show up in youtube RSS feeds as the most recent video, should be ok to ignore when running ``ggxrd-rss-match-parser.py`` since older videos are processed first and there won't be any newer videos.

# Further work (none of these are planned, but would be nice)
* OCR out the player names on the VS splash screen (would need to download videos in higher quality format)
* Detect when matches actually begin (skip over VS splash screen and character intros), and adjust the timestamp forwards accordingly
* Make the image analysis not terrible and train machine learning model to recognize character names/splashes properly
* Make the demo, training, MOM mode detection less crappy