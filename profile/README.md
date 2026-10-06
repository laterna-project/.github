<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/logo-dark.png">
    <img alt="Laterna" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/logo-light.png" width="240">
  </picture>
</p>

<p align="center">
  A media server for the films, shows, music, books and photos you already have.<br>
  One binary, one SQLite file, and nothing that phones home.
</p>

<p align="center">
  <a href="https://github.com/laterna-project/laterna">Server</a> ·
  <a href="https://github.com/laterna-project/laterna-web">Web app</a> ·
  <a href="https://github.com/laterna-project/laterna/blob/develop/docs/install.md">Install</a> ·
  <a href="https://github.com/laterna-project/laterna/releases">Releases</a>
</p>

![The home page: films in progress, new arrivals per library](https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/home.jpg)

Laterna turns a few folders on a disk into something you actually want to open in the evening:
what you were watching, the next episode, the album you left halfway, the book you're reading,
last summer's photos. It's written from scratch in Go. It isn't a fork of Jellyfin, Emby or
Plex, and it doesn't speak their APIs: it has its own, and its own apps.

### Video that just plays

If the device can play the file, Laterna sends the file. If it can't, it switches to HLS and
only converts what has to be converted: when the sound is the problem, the picture goes through
untouched. Hardware encoders are found by actually trying them when the server starts, not by
guessing.

Subtitles keep the look their authors gave them. Styled ASS tracks are shown with their own
fonts, colors and positions, and since subtitles and fonts are pulled out of the file when it's
added, switching tracks never restarts the video. Intros and recaps can be skipped, the next
episode lines up during the credits, and scrubbing shows thumbnails.

<table>
  <tr>
    <td><img alt="A film's page" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/movie.jpg"></td>
    <td><img alt="The player with its subtitle menu" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/player.jpg"></td>
  </tr>
</table>

### And the rest of the shelf

Music is read from your tags, with ReplayGain and a queue that keeps playing while you browse.
Books open in the browser: EPUB with your choice of font and size, comics and manga page by page
(right to left when they should be), PDF too, and the page you stopped on is waiting on your
other devices. Photos are sorted by the day they were taken, with albums, EXIF details and a
slideshow.

<table>
  <tr>
    <td><img alt="An album" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/music.jpg"></td>
    <td><img alt="The photo viewer" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/photos.jpg"></td>
  </tr>
</table>

### For everyone in the house

Each person gets a profile with their own history, favorites and resume points. Profiles can
have a PIN, and parental controls are enforced by the server, so a kid can't get around them by
picking another app. You can sign in with a password, a passkey, your own OpenID Connect
provider, or a code shown on the TV. Friends with an account on your server can watch with you
from their own couch: playback, pauses and seeks stay in sync, and everyone can react.

The "Because you watched…" rows are computed on your server, from what your household watches.

<table>
  <tr>
    <td><img alt="Profile picker" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/profiles.jpg"></td>
    <td><img alt="Recommendations" src="https://raw.githubusercontent.com/laterna-project/.github/main/profile/images/discover.jpg"></td>
  </tr>
</table>

### Your files stay yours

Laterna reads the NFO files and artwork that sit next to your media, the ones Sonarr, Radarr,
Kodi or tinyMediaManager already write. It never looks anything up online, so nothing gets
matched to the wrong film, and it never writes into your folders. Rename or move a file and it
keeps its watch history. If a network share drops for a moment, your library doesn't vanish.

Running it is meant to be boring: no external database, a backup every night and another before
any upgrade that touches the database, a start in well under a second, under 60 MB of memory
when idle. Prometheus
metrics and OpenTelemetry traces are there if you want them. Coming from Jellyfin, you can bring
your users and what they've watched.

### Try it

```sh
docker run -d --name laterna -p 8096:8096 \
  -v laterna-config:/config -v laterna-cache:/cache \
  -v /path/to/media:/media:ro \
  ghcr.io/laterna-project/laterna:latest
```

Then open <http://localhost:8096> and create the first account. The image ships FFmpeg and the
web app. There are also `.deb` and `.rpm` packages, and archives for Linux, Windows, macOS and
FreeBSD, on the [releases page](https://github.com/laterna-project/laterna/releases).

| Repository | |
|---|---|
| [laterna](https://github.com/laterna-project/laterna) | The server, in Go. Its API is a Protobuf contract served with ConnectRPC, documented message by message. |
| [laterna-web](https://github.com/laterna-project/laterna-web) | The web app: every screen, administration included, in English, French, German and Spanish. |

### Where it stands

Laterna is young. The server is well tested, but it has only run on a handful of machines so
far, and until 1.0 a minor release may change the configuration or the API (the release notes
say how to upgrade). If you try it on a real library and something breaks, an issue is the most
useful thing you can send.

Laterna is free software, under the GNU GPL v3 or later.

<sub>The screenshots use free works: Sintel, Tears of Steel, Big Buck Bunny (CC BY 3.0),
Cosmos Laundromat, Spring (CC BY 4.0) and Elephants Dream and its soundtrack by Jan Morgenstern
(CC BY 2.5), by the Blender Foundation and Blender Animation Studio; Pepper&Carrot (after David
Revoy) and Marya Morevna by the Morevna Project (CC BY-SA 3.0 and 4.0); Lac Blanc in Chamonix by Tiia
Monto (CC BY-SA 3.0); and public domain films by the Lumière brothers, Georges Méliès and
F. W. Murnau. Full credits are in
[ATTRIBUTIONS.md](https://github.com/laterna-project/laterna-web/blob/develop/devtools/samples/ATTRIBUTIONS.md).</sub>
