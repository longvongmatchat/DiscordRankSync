# DiscordRankSync

Plugin Minecraft để đồng bộ rank từ Discord server sang Minecraft server.

**Tác giả:** NgHai

## Tính năng

### 🔗 **Hệ thống liên kết tài khoản**
- Liên kết tài khoản Discord với Minecraft thông qua Discord ID
- Hỗ trợ pending link system với timeout 60 giây
- Interactive Discord UI với buttons và dropdown menus
- Slash command `/lienket` để tạo panel quản lý

### 🔄 **Đồng bộ Rank thông minh**
- ⚙️ **LuckPerms Native Integration** - Đồng bộ groups trực tiếp với LuckPerms API
- 🔄 Tự động đồng bộ rank khi người chơi join server
- 📊 Đồng bộ định kỳ theo khoảng thời gian tùy chỉnh (mặc định: 30 giây)
- 🛡️ **Safe Sync Logic** - Chỉ thay đổi groups được map, không ảnh hưởng groups khác
- 🎯 **Precise Sync** - Thêm/xóa groups chính xác dựa trên Discord roles

### 🤖 **Discord Bot Integration**
- Bot Discord với đầy đủ quyền: Manage Roles, Read Messages, Send Messages
- Interactive embed panel với buttons: Link, Un-Link, Status
- Dropdown menu với các chức năng: View Links, Online Players, Discord Rank, Guide
- Real-time status checking và role verification

### 🚀 **Tối ưu hiệu suất**
- ⚡ **Advanced Caching System** - Cache roles, user info, permissions với TTL
- 🔄 **Smart Rate Limiting** - Có thể cấu hình hoặc vô hiệu hóa hoàn toàn
- 🧵 **Folia Full Support** - Tương thích hoàn hảo với Folia scheduler
- 📈 **Concurrent API Management** - Quản lý đồng thời API calls an toàn

### 🛠️ **Commands đầy đủ**
- `/link` - Liên kết tài khoản Discord
- `/discordunlink` - Hủy liên kết tài khoản
- `/discordinfo [player] [role_id]` - Xem thông tin Discord và kiểm tra role
- `/discordsync [player]` - Đồng bộ rank thủ công (admin)
- `/discordreload` - Reload cấu hình plugin (admin)

### 🔒 **Bảo mật và ổn định**
- 🛡️ **Comprehensive Error Handling** - Null checks và exception handling đầy đủ
- 🔒 **Stable & Reliable** - Không crash, hoạt động ổn định 24/7
- 🐛 **Advanced Debug System** - Debug logging chi tiết cho troubleshooting
- ⚙️ **Configurable Settings** - Tùy chỉnh mọi aspect qua config.yml

### 🎮 **Tương thích tối đa**
- 🌍 **Multi-Server Support** - Spigot, Paper, Folia
- 📋 **Permission Integration** - Hoạt động hoàn hảo với LuckPerms
- 🔧 **Plugin Dependencies** - Chỉ yêu cầu LuckPerms, không dependency khác
- 📊 **Real-time Monitoring** - Theo dõi active API calls và cache status

## Yêu cầu

- **Minecraft Server**: Spigot/Paper/Folia 1.13+
- **Java**: 8+
- **Dependencies** (bắt buộc):
  - **LuckPerms** - Modern permission management plugin (https://luckperms.net/)
- **Discord Bot Permissions**:
  - Manage Roles
  - Read Messages/View Channels
  - Send Messages
  - Use Slash Commands (tùy chọn)

## Cài đặt

### 1. Tải và cài đặt plugin

1. Tải file `DiscordRankSync.jar`
2. Copy vào thư mục `plugins/` của server
3. Restart server

### 2. Tạo Discord Bot

1. Truy cập [Discord Developer Portal](https://discord.com/developers/applications)
2. Tạo application mới
3. Vào tab "Bot" và tạo bot
4. **Quan trọng**: Bật các Intent:
   - ✅ Message Content Intent (cho đọc nội dung tin nhắn)
   - ✅ Server Members Intent (cho đọc thông tin member)
5. Copy Bot Token
6. Vào tab "OAuth2" > "URL Generator"
7. Chọn scopes: `bot` + `applications.commands` (cho slash commands)
8. Chọn permissions:
   - ✅ Manage Roles
   - ✅ Read Messages/View Channels
   - ✅ Send Messages
   - ✅ Use Slash Commands
   - ✅ Embed Links
9. Copy URL và invite bot vào server Discord của bạn

### 3. Cấu hình plugin

Chỉnh sửa file `plugins/DiscordRankSync/config.yml`:

```yaml
# Discord Bot Settings
Discord:
  BotToken: "YOUR_BOT_TOKEN_HERE"  # Thay bằng bot token của bạn
  GuildId: "YOUR_GUILD_ID_HERE"    # ID của Discord server
  NotificationChannel: ""          # ID channel để gửi thông báo (tùy chọn)

# Role Mappings - Map Discord Role ID -> Minecraft Group
RoleMappings:
  "123456789012345678": "vip"       # Thay bằng Role ID thực tế
  "987654321098765432": "premium"  # Thêm nhiều role tùy ý

# Settings
Settings:
  AutoSyncOnJoin: true      # Tự động sync khi join
  SyncInterval: 30          # Khoảng thời gian sync (giây)
  Debug: false              # Bật debug mode
```

### 4. Lấy Discord Role ID và Guild ID

1. **Guild ID**: Right-click server name > "Copy ID" (cần bật Developer Mode)
2. **Role ID**: Server Settings > Roles > Right-click role > "Copy ID"

## Cách sử dụng

### Liên kết tài khoản

#### Cách 1: Discord Interactive UI (Khuyến nghị)
1. Trong Discord, sử dụng slash command: `/lienket`
2. Bot sẽ tạo embed panel với buttons
3. Click **🔗 Link** button
4. Nhập tên Minecraft của bạn vào modal
5. Vào game và sử dụng lệnh `/link`

#### Cách 2: Manual (Cũ)
1. Người chơi lấy Discord ID của mình (User Settings > Advanced > Developer Mode > Right-click username > Copy ID)
2. Trong game: `/link <discord_id>`

### Commands

#### Minecraft Commands
- `/link` - Liên kết tài khoản Discord (không cần tham số khi dùng Discord UI)
- `/link <discord_id>` - Liên kết tài khoản Discord (manual mode)
- `/discordunlink` - Hủy liên kết tài khoản
- `/discordinfo [player]` - Xem thông tin Discord của người chơi
- `/discordinfo [player] [role_id]` - Kiểm tra role cụ thể của người chơi
- `/discordsync [player]` - Đồng bộ rank thủ công (admin only)
- `/discordreload` - Reload cấu hình plugin (admin only)

#### Discord Slash Commands
- `/lienket` - Tạo panel quản lý tài khoản với interactive UI

### Permissions

- `discordranksync.link` - Cho phép liên kết tài khoản (default: true)
- `discordranksync.unlink` - Cho phép hủy liên kết (default: true)
- `discordsync.info` - Cho phép xem thông tin Discord (default: true)
- `discordsync.admin` - Quyền admin để đồng bộ thủ công (default: op)

## Ví dụ cấu hình

```yaml
Discord:
  BotToken: "MTEyMzQ1Njc4OTAxMjM0NTY3OC5hijklmnop"
  GuildId: "987654321098765432"
  NotificationChannel: "112233445566778899"

RoleMappings:
  "112233445566778899": "vip"
  "998877665544332211": "premium"
  "776655443322110088": "legend"

Settings:
  AutoSyncOnJoin: true
  SyncInterval: 15      # Sync mỗi 15 giây
  Debug: true
```

## Ví dụ sử dụng Commands

### Liên kết tài khoản với Discord UI

1. **Trong Discord**: Gõ `/lienket` để tạo panel
2. **Bot tạo embed** với buttons: 🔗 Link | ❌ Un-Link | 📊 Status
3. **Click "🔗 Link"** → Nhập tên Minecraft → Tạo pending link
4. **Trong Minecraft**: `/link` (không cần tham số)
5. **Hoàn thành!** Tài khoản được liên kết và sync rank ngay lập tức

### Liên kết tài khoản Manual (Cũ)
```
/link 123456789012345678
# Liên kết với Discord ID của bạn

/discordlink 123456789012345678  # Cũng hoạt động
```

### Xem thông tin Discord
```
/discordinfo
# Xem thông tin Discord của chính mình

/discordinfo Notch
# Xem thông tin Discord của player khác

/discordinfo Notch 123456789012345678
# Kiểm tra xem Notch có role với ID cụ thể không
```

**Output mẫu:**
```
[DiscordSync] === Discord Info: PlayerName ===
Discord Tag: PlayerName#1234
Discord ID: 123456789012345678
Role cao nhất: VIP
Tất cả roles (3): VIP, Premium, Member
```

### Đồng bộ thủ công (Admin)
```
/discordsync
# Đồng bộ rank cho chính mình

/discordsync PlayerName
# Đồng bộ rank cho player khác
```

## Discord Interactive UI

Plugin cung cấp giao diện Discord tương tác đầy đủ:

### 🔗 **Link Button**
- Tạo modal nhập tên Minecraft
- Tạo pending link với timeout 60 giây
- Thông báo hướng dẫn hoàn thành liên kết

### ❌ **Un-Link Button**
- Yêu cầu xác nhận "CONFIRM" để tránh nhầm lẫn
- Tự động remove tất cả synced roles
- Thông báo thành công với cleanup

### 📊 **Status Button**
- Hiển thị thông tin liên kết hiện tại
- Show Discord roles và Minecraft username
- Trạng thái online/offline của player

### 📋 **Dropdown Menu**
- **Xem thông tin liên kết** - Chi tiết tài khoản đã link
- **Xem danh sách online** - Players đang online
- **Kiểm tra rank Discord** - Roles hiện tại của bạn
- **Hướng dẫn liên kết** - Guide chi tiết từng bước

## Cách nhận diện Role ID trong Discord

1. **Bật Developer Mode**: User Settings → Advanced → Developer Mode
2. **Copy Role ID**:
   - Server Settings → Roles
   - Right-click role → "Copy ID"
3. **Sử dụng trong lệnh**:
   ```
   /discordinfo PlayerName 123456789012345678
   ```

## Debug và Troubleshooting

### Kiểm tra role mappings
```yaml
# Trong config.yml
RoleMappings:
  "123456789012345678": "vip"      # Role ID -> Minecraft Group
  "987654321098765432": "premium"  # Role ID -> Minecraft Group
```

### Debug commands
```
/discordinfo PlayerName          # Xem tất cả roles
/discordinfo PlayerName <role_id> # Kiểm tra role cụ thể
```

### Xem logs
Bật debug mode trong config để xem chi tiết:
```yaml
Settings:
  Debug: true
```

## Troubleshooting

### Bot không kết nối
- Kiểm tra Bot Token có đúng không
- Đảm bảo bot đã được invite vào server với quyền phù hợp

### Permission không hoạt động
- **LuckPerms missing**: Plugin yêu cầu LuckPerms để hoạt động
- **Group names**: Kiểm tra tên group trong config khớp với group trong LuckPerms
- **Plugin load order**: Đảm bảo LuckPerms load trước DiscordRankSync

#### Cài đặt LuckPerms:
1. Tải từ: https://luckperms.net/
2. Copy vào thư mục `plugins/`
3. Restart server
4. Cấu hình groups theo ý muốn

### Role không sync
- **Kiểm tra Role Mappings**: Sử dụng `/discordreload` và xem console log
- **Kiểm tra Role ID**: Server Settings → Roles → Right-click → Copy ID (cần Developer Mode)
- **Kiểm tra Bot Permissions**: Bot cần quyền "Read Messages/View Channels" và "Manage Roles"
- **Debug Mode**: Bật `Debug: true` trong config để xem chi tiết sync process
- **Kiểm tra Links**: Xem file `links.yml` có lưu đúng Discord ID không
- **Safe Sync**: Plugin chỉ remove/add groups được map từ Discord roles, không ảnh hưởng groups khác

### Debug Steps
1. Bật debug mode trong config: `Debug: true`
2. Reload plugin: `/discordreload`
3. Join server và xem console log
4. Kiểm tra role mappings được load: `[DiscordRankSync] Loaded X role mappings`
5. Kiểm tra member roles: `[DiscordRankSync] Member roles:`
6. Kiểm tra sync result: `[DiscordRankSync] Synced roles for player: ...`

### Vấn đề với Discord Bot
- **Bot không phản hồi**: Kiểm tra bot permissions và token
- **Slash command không hoạt động**: Đảm bảo bot có quyền "Use Slash Commands"
- **Embed panel không hiện**: Kiểm tra quyền "Send Messages" và "Embed Links"

### Vấn đề với Caching & Performance
- **Rate limiting messages**: Có thể vô hiệu hóa rate limiting trong code
- **Cache không clear**: Plugin tự động cleanup cache mỗi 5 phút
- **API calls quá nhiều**: Điều chỉnh SyncInterval hoặc bật caching

### Vấn đề với Folia
- Plugin tự động phát hiện và sử dụng Folia scheduler khi chạy trên Folia
- Nếu gặp vấn đề về timing, thử điều chỉnh SyncInterval trong config
- GlobalRegionScheduler được sử dụng cho tasks toàn cục
- RegionScheduler được sử dụng cho player-specific tasks

## Support

Nếu gặp vấn đề:
1. **Bật Debug mode** trong config: `Debug: true`
2. **Kiểm tra console log** để xem chi tiết lỗi
3. **Test Discord bot** bằng cách sử dụng `/lienket` trong Discord
4. **Verify permissions** của bot trong Discord server
5. **Check LuckPerms** đã được cài đặt và hoạt động

### Liên hệ hỗ trợ:
- **Discord**: Tham gia server Discord để được hỗ trợ dsc.gg/frenzy-network
- **GitHub Issues**: Báo cáo bug và yêu cầu tính năng mới
- **Console Logs**: Chia sẻ logs khi gặp lỗi để debug nhanh hơn

## License

Plugin này được phát triển bởi NgHai.
## Discord
https://dsc.gg/frenzy-network
