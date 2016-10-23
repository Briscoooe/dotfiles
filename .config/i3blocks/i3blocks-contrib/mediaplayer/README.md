# Media player

Generic media player support

![Example screenshot](mediaplayer.png)

This displays "ARTIST - SONG" if music is playing.
Supported players are:
- spotify, vlc, audacious, xmms2, mplayer and others that
use MPRIS DBus Interface Specification
- mpd
- cmus

mpd is supported through mpc (music player client).

For MPRIS support you need to have playerctl binary in your path.
See: https://github.com/acrisci/playerctl

If you leave the instance empty it will try to find an
active player used on it's own.

``` ini
[mediaplayer]
command=$SCRIPT_DIR/mediaplayer
instance=spotify
interval=5
signal=10
```
