# ebookmap

Create maps optimized for [eBook readers](https://en.wikipedia.org/wiki/E-reader) using the data from [OpenStreetMap](https://www.openstreetmap.org/).

## Screenshots

A map of [Upper West Side, New York](https://www.openstreetmap.org/relation/8398085):

<img alt="Sceenshot 1" src="https://user-images.githubusercontent.com/142021/42083860-c4a1257a-7b94-11e8-8ef6-e122985722dc.png" width="200"> <img alt="Sceenshot 2" src="https://user-images.githubusercontent.com/142021/42083861-c4d2ad84-7b94-11e8-94ef-71865989db1f.png" width="200"> <img alt="Sceenshot 3" src="https://user-images.githubusercontent.com/142021/42083863-c504c4a4-7b94-11e8-96d4-984dcb5afd46.png" width="200"> <img alt="Sceenshot 4" src="https://user-images.githubusercontent.com/142021/42083864-c53760da-7b94-11e8-8ef2-e7f698656196.png" width="200">

The original PDF file (paper size A5): https://www.scribd.com/document/382852184/upper-west-side-new-york.

## Features

- All dependencies are encapsulated in a container which can be easily bootstrapped and used on almost any Linux system.
- Resolution-independent scalable vector images.
- The clickable overview page to quickly navigate to an area of interest.
- Clickable page edges to navigate to adjacent pages.
- The clickable Index page with a list of streets and objects.
- Table of contents.

## Requirements

- A [systemd](https://en.wikipedia.org/wiki/Systemd)-based Linux system ([Debian](https://www.debian.org/)/[Ubuntu](https://www.ubuntu.com/) and derivatives, [Arch Linux](https://www.archlinux.org/), etc.)
- Minimum free 2GB of disk space.
- These packages need to be installed manually unless your system is not Debian, Ubuntu, or Arch Linux: `debootstrap`, `systemd-nspawn`.

## Usage

- Clone or download this repository and `cd` into the directory:

```shell
git clone https://github.com/sgtpep/ebookmap.git
cd ./ebookmap
```

- Setup a container with all dependencies (it will be stored at `/var/lib/machines/ocitysmap`): `./setup-container`
- The next step can be omitted if you want to use OcitySMaps and the default Mapnik stylesheet as is. Otherwise, for better results on eBook readers apply customizations (you can read comments, lines started with `#`, in `./customize-ocitysmap` to learn about them): `./customize-ocitysmap`
- Import some data from OpenStreetMap to the container's database providing a URL to it (the `.osm.pbf` format is recommended; see [this section](#openstreetmap-data-extracts) for a list of known data sources): `./import-data https://download.bbbike.org/osm/bbbike/NewYork/NewYork.osm.pbf`. For huge datasets you can also pass additional arguments for `osm2pgsql` (for example, `-s|--slim` activates the slim mode which is slower, but uses less memory, `-C|--cache 10000` enables to use up to 10000MB of RAM for the cache; read [Usage of `osm2pgsql`](http://www.volkerschatz.com/net/osm/osm2pgsql-usage.html) and [OpenStreetMap Wiki](https://wiki.openstreetmap.org/wiki/Osm2pgsql) to learn about them): `./import-data [url] -s -C 10000`
- Default object names in the OpenStreetMap data are provided in local languages. If you want to see names in English run (note: not all objects on OpenStreetMap may have been translated to English, it depends on efforts of OpenStreetMap contributors): `./translate-data`.

## OpenStreetMap data extracts

- https://download.bbbike.org/osm/bbbike/
- https://download.geofabrik.de/
- http://download.openstreetmap.fr/extracts/

## Resources

- MapOSMatic, a web service that allows you to generate maps of cities using the OpenStreetMap data: https://maposmatic.osm-baustelle.de/
- Source code of OcitySMaps, a command-line tool behind the MapOSMatic web service: http://git.savannah.gnu.org/cgit/maposmatic/ocitysmap.git, https://github.com/hholzgra/ocitysmap
- MapOSMatic on OpenStreetMap Wiki: https://wiki.openstreetmap.org/wiki/MapOSMatic
- Other tools to generate printable maps from OpenStreetMap: https://wiki.openstreetmap.org/wiki/OSM_on_Paper
