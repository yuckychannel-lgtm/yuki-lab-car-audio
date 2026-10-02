# Installation Guide

This guide covers the standard installation of **YUKI LAB CAR AUDIO v1.0.2**.

## Requirements

- QBCore or Qbox
- ox_inventory
- oxmysql
- OneSync

Qbox servers must provide the official QBCore compatibility bridge required by this resource.

## 1. Install the Resource

Place the purchased `yuki_car_audio` folder inside your FiveM resources directory.

Example:

```text
resources/[yuki]/yuki_car_audio
```

## 2. Add ox_inventory Items

Open:

```text
yuki_car_audio/install/ox_inventory_item.txt
```

Add both entries inside the `return { ... }` table in:

```text
ox_inventory/data/items.lua
```

The two items are:

```text
yuki_car_stereo
yuki_business_car_stereo
```

The resource package also includes product images for the two stereo items. If your inventory or shop displays item images, copy those PNG files into the image directory used by that resource.

## 3. Add Shop Products (Optional)

If you want players to buy the stereo items from an in-game shop, adapt the included example:

```text
yuki_car_audio/install/shop_product_example.txt
```

The included prices are examples only. Match the format and pricing to your own shop resource.

## 4. Configure server.cfg

Start YUKI LAB CAR AUDIO after its dependencies.

### QBCore

```cfg
ensure qb-core
ensure oxmysql
ensure ox_inventory
ensure yuki_car_audio
```

### Qbox

```cfg
ensure qbx_core
ensure oxmysql
ensure ox_inventory
ensure yuki_car_audio
```

## 5. Database

The required table is created automatically on first resource start.

If your database account cannot create tables, manually execute:

```text
yuki_car_audio/install/install.sql
```

The resource stores favorites, playlists and user settings in:

```text
yuki_car_audio_users
```

## 6. Choose UI Language

Open `config.lua` and set:

```lua
Config.Locale = 'ja'
```

for Japanese, or:

```lua
Config.Locale = 'en'
```

for English.

## 7. Configure Business Jobs

Business stereo access is restricted to supported jobs while the player is ON DUTY.

Defaults:

```lua
Config.BusinessJobs = {
    pd = { jobs = { 'police' } },
    ems = { jobs = { 'ambulance', 'ems' } },
    mechanic = { jobs = { 'mechanic' } }
}
```

Change the internal job names to match your server.

Example, if your police job is `lspd`:

```lua
pd = { jobs = { 'lspd' } }
```

## 8. Test the Standard Stereo

Inside a vehicle:

- Use the `yuki_car_stereo` item, or
- Carry the item and use `/music`

## 9. Test the Business Stereo

1. Join a configured business job.
2. Go ON DUTY.
3. Enter a vehicle.
4. Use `yuki_business_car_stereo`.

## 10. Restart After Changes

After changing audio files or major configuration values, use:

```text
restart yuki_car_audio
```

or restart the server.

---

# 日本語

## 必要リソース

- QBCore または Qbox
- ox_inventory
- oxmysql
- OneSync

## 基本手順

1. `yuki_car_audio` を `resources` 配下へ配置
2. `install/ox_inventory_item.txt` の2アイテムを ox_inventory に追加
3. 必要ならショップへ追加
4. 依存リソースより後に `ensure yuki_car_audio`
5. DBテーブルは初回起動時に自動作成
6. `Config.Locale` と `Config.BusinessJobs` をサーバー環境に合わせて変更

通常用は車内で `yuki_car_stereo` を使用、またはアイテム所持状態で `/music` を使用します。

業務用は対応ジョブ + ON DUTY の状態で `yuki_business_car_stereo` を使用してください。
