# Troubleshooting

Use this checklist when **YUKI LAB CAR AUDIO v1.0.2** does not behave as expected.

## Resource does not start

Check that these resources start first:

```cfg
ensure oxmysql
ensure ox_inventory
ensure yuki_car_audio
```

Also confirm that your framework is running before `yuki_car_audio`.

For Qbox, verify that the QBCore compatibility bridge required by the resource is available.

## Stereo item does nothing

Check:

- The item definitions were added to `ox_inventory/data/items.lua`.
- The item names match `Config.ItemName` and `Config.BusinessItemName`.
- The player is inside a vehicle.
- The vehicle is networked correctly.
- There are no client console errors.

## `/music` does not open

The `/music` command requires the standard stereo item by default.

Confirm the player owns:

```text
yuki_car_stereo
```

Also check that `Config.Command` is still set to the expected command name.

## Business stereo does not open

The business stereo requires:

1. A supported job
2. ON DUTY status
3. The business stereo item
4. The player to be inside a vehicle

Check your internal job name against:

```lua
Config.BusinessJobs
```

Default mappings are:

- PD: `police`
- EMS: `ambulance`, `ems`
- Mechanic: `mechanic`

## No music can be heard outside the vehicle

Check:

- `Config.MaxDistance`
- `Config.BusinessMaxDistance`
- Player distance from the vehicle
- The selected vehicle/personal volume levels
- Whether the vehicle still exists and is networked

The current system uses distance-based attenuation rather than full directional 3D positioning.

## Music is not perfectly aligned between players

Small playback-position differences may occur because synchronization is based on server time.

This is expected behavior within the current product specification.

## Newly added MP3 is missing

After adding audio:

1. Place the MP3 under `html/music/`.
2. Register it in `Config.Tracks`.
3. Confirm the path and filename are correct.
4. Confirm the track `id` is unique.
5. Restart `yuki_car_audio` or restart the server.

## Cover image is missing

Confirm the image is stored under:

```text
html/covers/
```

and the `cover` value in `Config.Tracks` is relative to the `html/` directory.

## Favorites or playlists are not saved

Check:

- `oxmysql` is running.
- The database connection is healthy.
- The `yuki_car_audio_users` table exists.
- The DB user had permission to create the table on first start.

If automatic creation failed, manually run:

```text
install/install.sql
```

## Resource download is large

MP3 files are included in the FiveM resource data delivered to clients.

More tracks = a larger initial resource download.

Remove unused audio or reduce the amount of bundled content if download size becomes a concern.

## Support Request Checklist

When contacting YUKI LAB support, include:

- QBCore or Qbox
- Resource version
- Relevant F8/client console error
- Relevant server console error
- Steps to reproduce
- Whether the problem affects standard stereo, business stereo, or both
- Any changes made to `config.lua`

Official store:

https://yuki-lab.tebex.store/

---

# 日本語

不具合時は以下を確認してください。

- `oxmysql` / `ox_inventory` が先に起動している
- 使用中のFrameworkと設定が一致している
- Qboxの場合は互換機能が利用できる
- ox_inventoryへ2つのアイテムが正しく追加されている
- 車内で使用している
- 業務用は対応ジョブ + ON DUTYになっている
- `Config.BusinessJobs` の内部ジョブ名が街の設定と一致している
- MP3追加後は `yuki_car_audio` を再起動している
- プレイリスト等が保存されない場合はDBテーブルを確認する

問い合わせ時はFramework、エラー内容、再現手順、設定変更内容を添えてください。
