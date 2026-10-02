# Configuration Guide

This guide summarizes the main public configuration options for **YUKI LAB CAR AUDIO v1.0.2**.

## Framework

```lua
Config.Framework = 'auto'
```

Supported values:

- `auto`
- `qbcore`
- `qbox`

`auto` is recommended unless you have a specific reason to force a framework.

## Language

```lua
Config.Locale = 'ja'
```

Available values:

- `ja` — Japanese
- `en` — English

## Item Names

```lua
Config.ItemName = 'yuki_car_stereo'
Config.BusinessItemName = 'yuki_business_car_stereo'
```

Change these only if you also update the corresponding inventory definitions.

## Command

```lua
Config.Command = 'music'
```

The standard stereo can be opened with `/music` when the player carries the required standard stereo item.

## Passenger Controls

```lua
Config.AllowPassengers = true
```

Controls whether passengers may operate the stereo UI.

## Audio Distance

```lua
Config.MaxDistance = 10.0
Config.BusinessMaxDistance = 50.0
Config.DistanceCurve = 1.6
```

- `MaxDistance` — hearing range for the standard stereo
- `BusinessMaxDistance` — hearing range for the business stereo
- `DistanceCurve` — attenuation behavior as distance increases

## Volume

```lua
Config.CabinVolumeMultiplier = 1.0
Config.DefaultVolume = 0.30
Config.MaxVolume = 0.80
Config.DefaultPersonalVolume = 1.00
Config.MaxPersonalVolume = 1.00
```

These values control default and maximum vehicle/personal volume behavior.

## Update / Cleanup Timing

```lua
Config.SpatialUpdateMs = 200
Config.VehicleCleanupMs = 5000
```

Avoid aggressive changes unless you understand the performance impact.

## Queue / Playlist Limits

```lua
Config.MaxQueueTracks = 250
Config.MaxPlaylists = 20
Config.MaxTracksPerPlaylist = 200
Config.MaxPlaylistNameLength = 32
```

Use these limits to control user-created playlist size and naming.

## Business Shared Albums

```lua
Config.BusinessBaseAlbums = { 'YUKI LAB' }
```

Albums listed here are available to all configured business jobs.

## Business Jobs

```lua
Config.BusinessJobs = {
    pd = { jobs = { 'police' } },
    ems = { jobs = { 'ambulance', 'ems' } },
    mechanic = { jobs = { 'mechanic' } }
}
```

Change internal job names to match your server.

Example:

```lua
Config.BusinessJobs = {
    pd = { jobs = { 'lspd' } },
    ems = { jobs = { 'ambulance' } },
    mechanic = { jobs = { 'mechanic' } }
}
```

The business stereo requires both:

- a supported job
- ON DUTY status

## Adding Tracks

Add MP3 files under:

```text
html/music/
```

Add cover art under:

```text
html/covers/
```

Then register the track in `Config.Tracks`.

Example:

```lua
{
    id = 'my_track_01',
    title = 'My Track',
    artist = 'My Artist',
    album = 'My Album',
    file = 'music/My_Album/my_track_01.mp3',
    cover = 'covers/my_album.png',
    enabled = true
}
```

For business-job-only tracks, add a job category:

```lua
job = 'pd'
```

Supported product categories include:

- `pd`
- `ems`
- `mechanic`

## Track ID Rules

- Every track `id` must be unique.
- Avoid changing IDs after release if players already use those tracks in playlists.
- `file` and `cover` are relative to the `html/` directory.
- ASCII filenames with underscores are recommended.

## Audio Distribution Reminder

MP3 files are delivered to players as FiveM resource data. Adding more tracks increases the resource download size.

Only add audio and artwork you are authorized to distribute and use on your server.

---

# 日本語メモ

主な設定箇所は `config.lua` にあります。

- `Config.Framework`：フレームワーク自動判定 / 固定
- `Config.Locale`：日本語 / English
- `Config.ItemName`：通常用アイテム名
- `Config.BusinessItemName`：業務用アイテム名
- `Config.Command`：`/music` のコマンド名
- `Config.AllowPassengers`：同乗者操作
- `Config.MaxDistance`：通常用の音が届く距離
- `Config.BusinessMaxDistance`：業務用の音が届く距離
- `Config.BusinessJobs`：PD / EMS / Mechanic の内部ジョブ名
- `Config.BusinessBaseAlbums`：業務用で共通表示するアルバム
- `Config.Tracks`：曲ライブラリ

サーバーごとのジョブ内部名が違う場合は、必ず `Config.BusinessJobs` を合わせてください。
