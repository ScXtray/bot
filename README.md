# Discord Moderation Bot

Bot Discord dengan fitur moderasi + utility: kick, ban, mute, timeout (TO), afk, react role, update list, welcome & out, anti-link, anti-promosi, anti kata tertentu.

## 🚀 Cara Install & Jalankan

### 1. Install Node.js
Pastikan sudah install [Node.js](https://nodejs.org/) versi 18 ke atas.

### 2. Install dependencies
```bash
npm install
```

### 3. Setup Discord Application
1. Buka https://discord.com/developers/applications → **New Application**
2. Tab **Bot** → **Reset Token** → salin tokennya
3. Di tab **Bot**, aktifkan 3 **Privileged Gateway Intents**: `PRESENCE INTENT`, `SERVER MEMBERS INTENT`, `MESSAGE CONTENT INTENT`
4. Tab **OAuth2 → URL Generator**: centang scope `bot` + `applications.commands`, lalu centang permission: `Kick Members`, `Ban Members`, `Moderate Members`, `Manage Roles`, `Manage Messages`, `Send Messages`, `Read Message History`, `Add Reactions`, `View Channels`
5. Buka link yang muncul di bawah, invite bot ke server-mu

### 4. Isi konfigurasi
- Copy `.env.example` jadi `.env`, isi `DISCORD_TOKEN`, `CLIENT_ID`, dan `GUILD_ID`
  - `CLIENT_ID` ada di tab **General Information** (Application ID)
  - `GUILD_ID` didapat dengan klik kanan nama server di Discord (aktifkan Developer Mode dulu: Settings → Advanced → Developer Mode)
- Edit `config.json` sesuai kebutuhan:
  - `welcomeChannelId` / `leaveChannelId`: ID channel buat pesan welcome & out
  - `antiKata.bannedWords`: daftar kata yang mau diblokir
  - `reactRole.emojiRoleMap`: pasangan emoji → ID role

### 5. Daftarkan slash command
```bash
npm run deploy
```

### 6. Jalankan bot
```bash
npm start
```

## 📜 Daftar Command

| Command | Fungsi |
|---|---|
| `/kick` | Kick member |
| `/ban` | Ban member |
| `/mute` | Mute member (role "Muted", permanen sampai di-unmute) |
| `/unmute` | Lepas mute |
| `/to` | Timeout member (native Discord, otomatis lepas sendiri) |
| `/afk` | Set status AFK |
| `/reactrole` | Bikin pesan react-role baru di channel saat ini |
| `/updatelist` | Refresh pesan react-role setelah `emojiRoleMap` diubah |
| `/badword tambah\|hapus\|list` | Kelola daftar kata terlarang |

## 🛡️ Auto-moderasi
Otomatis aktif, tidak perlu command — bisa diatur di `config.json`:
- **Anti-link**: hapus pesan yang mengandung URL (kecuali domain di `allowedDomains`)
- **Anti-promosi**: hapus pesan yang mengandung link invite Discord
- **Anti kata tertentu**: hapus pesan yang mengandung kata di `bannedWords`

Member dengan izin **Manage Messages** (moderator) otomatis dikecualikan dari auto-moderasi.

## 📁 Struktur Folder
```
discord-bot/
├── index.js              # entry point
├── deploy-commands.js    # daftarin slash command
├── config.json           # pengaturan (role, channel, kata terlarang)
├── .env                  # token & ID rahasia (JANGAN commit)
├── commands/              # semua slash command
├── events/                 # semua event handler
└── utils/afkStore.js       # penyimpanan status AFK
```

## ⚠️ Catatan
- Role bot harus **di atas** role "Muted" dan role member yang mau dikelola (urutan role di Server Settings → Roles)
- Kalau mau host 24/7, bisa pakai VPS, Railway, Render, atau platform hosting Node.js lain
- Status AFK saat ini disimpan di memori (reset kalau bot restart) — bisa diupgrade ke database kalau perlu persist
