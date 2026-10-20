# Tiki Head Linux

[![Built with linuxlive](https://linuxlive.com/badge.svg)](https://linuxlive.com/library/tiki-head-linux/)

A geospatial workstation that starts from a USB stick and installs to a disk:
Ubuntu 26.04 LTS with GNOME, made with [linuxlive](https://linuxlive.com).

![The Tiki Head desktop](assets/wallpaper.png)

## What is inside

- **Desktop GIS:** QGIS, with GRASS in its Processing toolbox, and SAGA GIS,
  which runs on its own (`saga_gui`, `saga_cmd`): QGIS 3.40 has no SAGA
  provider.
- **The command line:** GDAL/OGR (which also writes PMTiles vector tiles),
  PROJ, SpatiaLite, osmium (OpenStreetMap), gpsbabel (GPS tracks) and NetCDF
  tools. [tippecanoe](https://github.com/felt/tippecanoe) is not included, but
  the compiler and libraries it needs are, so you can build it yourself.
- **A spatial database:** PostgreSQL with PostGIS. On an installed computer,
  each person gets a database of their own name with PostGIS in it.
- **Python:** GeoPandas, Rasterio, Shapely, PyProj, Fiona, xarray, Folium and
  SciPy, with IPython and Jupyter Notebook.
- **Maps and OpenStreetMap:** JOSM and GNOME Maps.
- **Apps from Flathub:** Firefox, Chromium and Visual Studio Code.
- **Sample data:** Natural Earth's world at 1:50 million (public domain) as one
  GeoPackage, and a QGIS project that opens it, in `~/GIS` for everyone.
- **`tiki-head-gis`:** lists the tools and their versions; `tiki-head-gis
  sample` opens the sample map.

## How it is put together

[linuxlive.yaml](linuxlive.yaml) lists the packages, the Flathub apps, three
files and three scripts:

| File | When it runs | What it does |
| --- | --- | --- |
| [files/](files/) | copied in | the guide (`/usr/share/tiki-head/README.md`), the login message (`/etc/motd`) and `tiki-head-gis` (`/usr/bin`) |
| [scripts/build.sh](scripts/build.sh) | while the image is built | downloads the sample data, makes the QGIS project, puts the GIS tools in GNOME's dock, dark style |
| [scripts/first-boot.sh](scripts/first-boot.sh) | once, on an installed computer | starts PostgreSQL and makes a PostGIS database for each person |
| [scripts/first-login.sh](scripts/first-login.sh) | once for each person | makes `~/GIS` with the sample data, the project and the guide |

Every push builds the ISO in GitHub Actions, boots it five ways, installs it to
a disk and checks every package, file and script above. Download it from the
run's Artifacts.

## Credits

Wallpaper and logo drawn in code for Tiki Head Linux, CC0. The islands come
from real elevation data: the Terrain Tiles on AWS Open Data (USGS on land,
NOAA ETOPO1 at sea, both public domain). Sample data from
[Natural Earth](https://www.naturalearthdata.com/), public domain. Not made or
endorsed by Canonical.
