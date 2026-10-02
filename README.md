# YUKI LAB CAR AUDIO

**Synchronized vehicle audio system for FiveM — QBCore / Qbox**

> Official documentation repository for **YUKI LAB CAR AUDIO v1.0.2**.  
> This public repository contains documentation only. The commercial resource itself is distributed through Tebex / Cfx.re.

[**🛒 YUKI LAB Tebex Store**](https://yuki-lab.tebex.store/) · [**🎬 5-minute Product Demo**](https://www.youtube.com/watch?v=F4-W9wXxPPQ) · [**🎬 80-second Gameplay Demo**](https://www.youtube.com/watch?v=RYH9IoM9eTo)

---

## Overview

**YUKI LAB CAR AUDIO** is a vehicle-following synchronized car stereo resource for FiveM servers using **QBCore** or **Qbox**.

It plays registered local MP3 files from the resource and synchronizes playback for occupants of the same vehicle and nearby players. Audio volume decreases with distance from the vehicle, creating a simple and lightweight vehicle-audio experience without requiring external audio URLs.

### Main Features

- Standard car stereo item: `yuki_car_stereo`
- Business car stereo item: `yuki_business_car_stereo`
- `/music` command with standard-item ownership check
- Vehicle-following synchronized playback
- Distance-based volume attenuation
- Track / artist / album browsing and search
- Favorites
- User-created playlists
- Playlist rename / delete
- Add / remove tracks from playlists
- Play / pause / previous / next controls
- Vehicle volume and personal volume controls
- Shuffle
- Repeat Off / Repeat All / Repeat One
- Japanese / English UI
- QBCore / Qbox support
- On-duty PD / EMS / Mechanic integration
- Automatic audio cleanup when a vehicle or the resource is removed

---

## Requirements

Before installing YUKI LAB CAR AUDIO, make sure your server has:

- **QBCore** or **Qbox**
- **ox_inventory**
- **oxmysql**
- **OneSync**

> Qbox installations must have the official QBCore compatibility bridge available for this resource.

---

## Quick Installation

### 1. Install the resource

Place the purchased `yuki_car_audio` folder inside your FiveM resources directory.

Example:

```text
resources/[yuki]/yuki_car_audio
```

### 2. Add the ox_inventory items

Open:

```text
yuki_car_audio/install/ox_inventory_item.txt
```

Add the two item definitions inside the `return { ... }` table in:

```text
ox_inventory/data/items.lua
```

Included items:

```text
yuki_car_stereo
yuki_business_car_stereo
```

If your inventory or shop displays item images, copy the bundled PNG files to the image directory used by your inventory/shop resource.

### 3. Add the items to your shop (optional)

A simple example is included at:

```text
yuki_car_audio/install/shop_product_example.txt
```

Adapt the schema and prices to the shop resource used by your server.

### 4. Add the resource to `server.cfg`

Start YUKI LAB CAR AUDIO after the framework and required dependencies.

**QBCore example**

```cfg
ensure qb-core
ensure oxmysql
ensure ox_inventory
ensure yuki_car_audio
```

**Qbox example**

```cfg
ensure qbx_core
ensure oxmysql
ensure ox_inventory
ensure yuki_car_audio
```

### 5. Database

The required database table is created automatically on first start.

Only if your database user does not have permission to create tables, run:

```text
yuki_car_audio/install/install.sql
```

### 6. Restart

Restart `yuki_car_audio` or restart the server after installation or audio/config changes.

For the full setup guide, see **[Installation Guide](docs/INSTALLATION.md)**.

---

## Usage

### Standard Car Stereo

Use the standard stereo in either of these ways:

- Use `yuki_car_stereo` while inside a vehicle
- Use `/music` while carrying the standard stereo item

### Business Car Stereo

The business stereo is designed for configured whitelist jobs.

By default:

| Type | Default internal job names |
|---|---|
| PD | `police` |
| EMS | `ambulance`, `ems` |
| Mechanic | `mechanic` |

A player must:

1. Belong to a supported job
2. Be **ON DUTY**
3. Use `yuki_business_car_stereo` inside a vehicle

Business-job mappings can be changed in `Config.BusinessJobs`.

---

## Configuration

Important settings are available in `config.lua`, including:

- Framework detection (`auto`, `qbcore`, `qbox`)
- UI language (`ja`, `en`)
- Item names
- `/music` command name
- Passenger control permission
- Standard and business audio distance
- Distance attenuation curve
- Default / maximum vehicle volume
- Default / maximum personal volume
- Playlist limits
- Business job mappings
- Business shared albums
- Track library

See **[Configuration Guide](docs/CONFIGURATION.md)** for details.

---

## Adding Your Own Tracks

YUKI LAB CAR AUDIO uses local MP3 files bundled with the FiveM resource.

1. Add MP3 files under:

```text
html/music/
```

2. Add cover artwork under:

```text
html/covers/
```

3. Register each track in `Config.Tracks`.

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

### Track Notes

- Every track `id` must be unique.
- Avoid changing an existing track ID after users have added it to playlists.
- `file` and `cover` paths are relative to the `html/` directory.
- ASCII letters, numbers and underscores are recommended for filenames.
- More bundled audio increases the initial resource download size for players.
- Only distribute audio and artwork that you are authorized to use and redistribute on your server.

---

## Current Audio Model

YUKI LAB CAR AUDIO currently uses **distance-based attenuation**, rather than full directional 3D audio positioning.

- Players closer to the vehicle hear louder audio.
- Players farther away hear reduced volume.
- Small playback-position differences between clients can occur because synchronization uses server time.
- Arbitrary seek / timeline scrubbing is not currently included.
- External audio URL input is not supported.

---

## Player Data

Favorites, playlists and user audio settings are stored per `citizenid` in the `yuki_car_audio_users` database table.

The table is automatically created on first start when the database account has the required permission.

---

## Troubleshooting

Common checks:

- Confirm `oxmysql` and `ox_inventory` start before `yuki_car_audio`.
- Confirm the correct framework is running.
- On Qbox, confirm QBCore compatibility is available.
- Confirm the stereo items were added correctly to `ox_inventory`.
- Confirm the player is inside a networked vehicle.
- For the business stereo, confirm the job name matches `Config.BusinessJobs` and the player is on duty.
- After adding or changing MP3 files, restart `yuki_car_audio`.

See **[Troubleshooting](docs/TROUBLESHOOTING.md)** for more checks.

---

## Support

Purchase and support information is available through the official YUKI LAB Tebex store:

**https://yuki-lab.tebex.store/**

When requesting support, please include:

- Framework: QBCore or Qbox
- Relevant server/client console error
- Steps to reproduce the problem
- Whether the issue affects the standard stereo, business stereo, or both

---

## License & Distribution

YUKI LAB CAR AUDIO is a **commercial resource**.

- Purchase does not grant permission to redistribute, resell, sublicense, leak or publicly upload the resource or modified copies.
- Configuration/source changes for use on the purchaser's own licensed FiveM server are allowed within the product license terms.
- Bundled audio and artwork may not be extracted and redistributed as a standalone asset pack unless separately permitted.
- QBCore, Qbox / qbx_core, ox_inventory, oxmysql, FiveM / Cfx.re and other third-party projects remain subject to their own licenses and terms.

The complete product license is included with the purchased package as `LICENSE.txt`.

---

# 日本語ドキュメント

## 概要

**YUKI LAB CAR AUDIO** は、QBCore / Qbox 対応の FiveM 向け車両追従型カーステレオMODです。

登録済みのローカルMP3を車内から再生し、同じ車両の乗員や車外の近距離プレイヤーへ音楽を同期します。車両との距離に応じて音量が減衰します。

### 主な機能

- 通常用カーステレオ
- 業務用カーステレオ
- `/music` コマンド
- 車両追従型の同期再生
- 距離による音量減衰
- 曲 / アーティスト / アルバム検索
- お気に入り
- プレイリスト作成・変更・削除
- 再生 / 一時停止 / 前の曲 / 次の曲
- 車両音量 / 個人音量
- シャッフル
- リピートなし / 全曲 / 1曲
- 日本語 / English UI
- PD / EMS / Mechanic のON DUTY連動

## 必要環境

- QBCore または Qbox
- ox_inventory
- oxmysql
- OneSync

## 基本導入

1. `yuki_car_audio` を `resources` 配下へ配置
2. `install/ox_inventory_item.txt` の2アイテムを ox_inventory に追加
3. 必要に応じてショップへ商品追加
4. 依存リソースより後に `ensure yuki_car_audio`
5. DBテーブルは初回起動時に自動作成
6. `config.lua` をサーバー環境に合わせて調整

詳細は **[Installation Guide](docs/INSTALLATION.md)** と **[Configuration Guide](docs/CONFIGURATION.md)** を参照してください。

---

## Official Links

- **Tebex:** https://yuki-lab.tebex.store/
- **Documentation:** https://github.com/yuckychannel-lgtm/yuki-lab-car-audio

© YUKI LAB
