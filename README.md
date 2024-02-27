# docker-vietnam

> **⚠️ BASED ON THE GREAT WORK OF**
> [timche/docker-csgo](https://github.com/timche/docker-csgo)

<p>
  <a href="https://hub.docker.com/r/timche/csgo">
    <img alt="Docker Image Version" src="https://img.shields.io/docker/v/maxaucube/docker-vietnam/latest">
  </a>
  <a href="https://hub.docker.com/r/timche/csgo">
    <img alt="Docker Image Size" src="https://img.shields.io/docker/image-size/maxaucube/docker-vietnam/latest">
  </a>
  <a href="https://hub.docker.com/r/timche/csgo">
    <img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/maxaucube/docker-vietnam" />
  </a>
  <a href="https://hub.docker.com/r/timche/csgo">
    <img alt="Docker Stars" src="https://img.shields.io/docker/stars/maxaucube/docker-vietnam" />
  </a>
</p>

> [Military Conflict: Vietnam](https://store.steampowered.com/app/1012110/Military_Conflict_Vietnam/) with automated/manual updating.


## Table of Contents

- [How to Use This Image](#how-to-use-this-image)
- [Image Variants](#image-variants)
- [Environment Variables](#environment-variables)
  - [General](#general)
  - [Mods](#mods)
  - [Other](#other)
- [Populating with Own Server Files](#populating-with-own-server-files)
- [Updating the Server](#updating-the-server)
  - [Automated ( Coming SOON )](#automated-recommended)
  - [Manually](#manually)

## How to Use This Image

```sh
$ docker run \
  -v=vietnam:/home/vietnam/server \
  --net=host \
  maxaucube/docker-vietnam
```

This is a bare minimum example and the server will be:

- installed on a volume named `vietnam` to [ensure persistence of server files](https://docs.docker.com/storage/).
- running on the default port `27015` on the `host` network for [optimal network performance](https://docs.docker.com/network/host/)

To configure the server with more advanced settings, set [environment variables](#environment-variables).

## Image Variants

Each variant refers to a tag, e.g. `maxaucube/docker-vietnam:<tag>`.

##### [`latest`](https://github.com/maxaucube/docker-vietnam/blob/master/base/Dockerfile) / [`<version>`](https://github.com/maxaucube/docker-vietnam/blob/master/base/Dockerfile)

#### More variants in the future, Contribute if you want !

## Environment Variables

### General

##### `VIETNAM_WS_API_KEY`

Default: None

Your [Steam Web API Key](https://steamcommunity.com/dev/apikey) to download workshop maps. ( DON'T SUPPORTED NOW )

Sets `-authkey` in `srcds_run` parameters.

##### `VIETNAM_IP`

Default: `0.0.0.0`

Internet IP the server is accessible from. In most cases the default value is sufficient, but if you want to run a [GOTV server](https://developer.valvesoftware.com/wiki/SourceTV) or have issues connecting to the server, setting the IP can help.

Sets `+ip` in `srcds_run` parameters.

##### `VIETNAM_PORT`

Default: `27015`

Port the server is listening to.

Sets `-port` in `srcds_run` parameters.

##### `VIETNAM_MAP`

Default: `mcv_port`

Start the server with a specific map.

Sets `+map` in `srcds_run` parameters.

##### `VIETNAM_MAX_PLAYERS`

Default: `16`

Maximum players allowed to join the server.

Sets `-maxplayers_override` in `srcds_run` parameters.

##### `VIETNAM_HOSTNAME`

The server name. [It can't contain spaces](https://developer.valvesoftware.com/wiki/Command_Line_Options#Some_useful_console_variables_2), so if you need a server name with spaces, set `hostname` in a config instead, e.g. `server.cfg`.

Sets `+hostname` in `srcds_run` parameters.

##### `VIETNAM_RCON_PW`

Default: `changeme`

RCON password to administrate the server.

Sets `+rcon_password` in `srcds_run` parameters.

##### `VIETNAM_PW`

Default: None

Password to join the server.

Sets `+sv_password` in `srcds_run` parameters.

##### `VIETNAM_TICKRATE`

Default: `64`

Server tick rate which can be `64` or `128`. The default value gives the best game experience, but also requires most server hardware resources.

Sets `-tickrate` in `srcds_run` parameters.

##### `VIETNAM_GAME_TYPE`

Default: `0`

Game Type

Sets `+game_type` in `srcds_run` parameters.

##### `VIETNAM_GAME_MODE`

Default: `0`

Game Mode

Sets `+game_mode` in `srcds_run` parameters.

##### `VIETNAM_MAP_GROUP`

Default: `0`

Map group.

Sets `+mapgroup` in `srcds_run` parameters.

##### `VIETNAM_TV_ENABLE`

Default: `false`

Enable SourceTV. Can be enabled with `true`. ( NOT TESTED)

##### `VIETNAM_TV_NAME`

Default: `GOTV`

Set GOTV name. ( NOT TESTED)

##### `VIETNAM_TV_PASSWORD`

Default: None

Set GOTV password. ( NOT TESTED)

##### `VIETNAM_TV_DELAY`

Default: `45`

Set GOTV broadcast delay in seconds. ( NOT TESTED)

##### `VIETNAM_TV_PORT`

Default: `27020`

Set GOTV port. ( NOT TESTED)

##### `VIETNAM_TV_DELAYMAPCHANGE`

Default: `1`

Delay the map change on game server until rest of buffered game has been broadcasted. ( NOT TESTED)

##### `VIETNAM_TV_DELTACACHE`

Default: `2`

 ( NOT TESTED)

##### `VIETNAM_TV_DISPATCHMODE`

Default: `1`

 ( NOT TESTED)

##### `VIETNAM_TV_MAXCLIENTS`

Default: `10`

Maximum client number for GOTV. ( NOT TESTED)

##### `VIETNAM_TV_MAXRATE`

Default: `0`

Maximum bandwidth spend per client in bytes/second. ( NOT TESTED)

##### `VIETNAM_TV_OVERRIDEMASTER`

Default: `0`

 ( NOT TESTED)

##### `VIETNAM_TV_SNAPSHOTRATE`

Default: `64`

World snapshots broadcasted per second by GOTV. ( NOT TESTED)

##### `VIETNAM_TV_TIMEOUT`

Default: `60`

 ( NOT TESTED)

##### `VIETNAM_TV_TRANSMITALL`

Default: `1`

By default entities and events outside of the auto-director view are removed from GOTV broadcasts to save bandwidth. If `tv_transmitall` is enabled, the whole game is transmitted and spectators can switch their view to any player they want. This option increases bandwidth requirement per spectator client by factor 2 to 3.  ( NOT TESTED)

##### `VIETNAM_FORCE_NETSETTINGS`

Default: `false`

Force client netsettings to highest `rate` (`786432`), `cmdrate` (`128`) and `updaterate` (`128`). This ensures optimal gameplay experience. Requires 128 [tick rate](#csgo_tickrate).

Sets `+sv_minrate`, `+sv_mincmdrate` and `+sv_minupdaterate` in `srcds` parameters.

##### `VIETNAM_PARAMS`

Additional `srcds_run` [parameters](https://developer.valvesoftware.com/wiki/Command_Line_Options#Command-line_parameters).

##### `VIETNAM_CUSTOM_FILES_DIR`

Default: `/usr/vietnam`

Absolute path to a directory in the container containing custom server files. Changing this is not recommended in order to follow the documentation. See more at "[Populating with Own Server Files](#populating-with-own-server-files)".


### Mods

> Coming very soon <3

### Other

##### `VALIDATE_SERVER_FILES`

Default: `false`

Validate and restore missing/fix broken server files on container start. Can be enabled with `true`.

This should especially be used whenever custom server files have been deleted and have overwritten files before, and you want to restore the original files.

##### `DEBUG`

Default: `false`

Print all executed commands for better debugging.

## Populating with Own Server Files

The server can be populated with your own custom server files (e.g. configs and maps) through a mounted directory that has the same folder structure as the server `csgo` folder in order to add or overwrite the files at their respective paths. Deleted custom server files, which have been added or have overwritten files before, are also removed from the `csgo` folder. The directory must be mounted at [`VIETNAM_CUSTOM_FILES_DIR`](#csgo_custom_files_dir) (default: `/usr/csgo`) and will be synced with the server `csgo` folder at each start of the container.

**Note:** See [`VALIDATE_SERVER_FILES`](#validate_server_files) on how to restore original files if they've been overwritten before but are removed now.

### Example

#### Host

Custom server files in `/home/user/custom-files`:

<!-- prettier-ignore-start -->
```sh
custom-files
├── addons
│   └── sourcemod
│       └── configs
│           └── admins_simple.ini # Will be overwritten
└── cfg
    └── server.cfg # Will be added
```
<!-- prettier-ignore-end -->

#### Container

`/home/user/custom-files` mounted to [`VIETNAM_CUSTOM_FILES_DIR`](#vietnam_custom_files_dir) (default: `/usr/vietnam`) in the container:

<!-- prettier-ignore-start -->
```sh
$ docker run \
  -v=csgo:/home/vietnam/server \
  -v=/home/user/custom-files:/usr/vietnam \ # Mount the custom files directory
  --net=host \
  maxaucube/docker-vietnam
```
<!-- prettier-ignore-end -->

## Updating the Server

Once the server has been installed, the container will check for a server update at every container start.

### Automated

> Coming very soon ! ()

### Manuallygame_type

Restart the container with [`docker restart`](https://docs.docker.com/engine/reference/commandline/restart/).

#### Example

Container named `vietnam`:

```sh
$ docker restart vietnam
```
