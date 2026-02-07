**🚀 软件定位**

**次世代Emby优化架构** - 专为网盘媒体库设计的智能加速平台，彻底解决网盘直连播放限制与风控问题。<br>
（仅用于团队自制视频都分享，不得用于盗版传播。）
<br>
<br>

**🔄 核心播放流程详解**  
<br>
**Normal模式：基础秒传直链**

路径： 源网盘 → 用户网盘 → 用户直链
```
用户播放请求 → 检测用户网盘无文件 → 源网盘秒传至用户网盘 → 获取用户网盘直链 → 返回播放
```
<br>

**Pro模式：三级智能加速架构**<br>

● STEP 1：用户自有文件极速匹配 (50ms)
```
用户播放请求 → 检查播放用户自己的网盘 → SHA1文件存在？
    ├─ ✅ 存在 → 直接获取用户网盘直链 → 立即播放
    └─ ❌ 不存在 → 进入STEP 2
```
1次API调用，50毫秒完成<br>
<br>

● STEP 2：用户间智能秒传加速 (5ms)
```
STEP 1未命中 → 查询本地播放记录数据库 → 搜索最近播放过相同文件的用户
    ├─ ✅ 找到最近已播放用户 → 秒传到 → 播放用户网盘
    │        ↓
    │    获取播放用户的网盘直链 → 返回播放
    │
    └─ ❌ 未找到 → 进入STEP 3
```
利用历史播放数据毫秒级本地搜索（5ms）  
用户间秒传，零API消耗<br>
<br>

● STEP 3：源网盘兜底保障
```
启动Normal模式兜底 → 源网盘秒传到播放用户网盘
        ↓
    获取播放用户的网盘直链 → 返回播放
```
100%可用性，多重备份机制<br><br>
<br>

**🔐 智能用户管理体系**<br>

👤 **自主注册**：用户独立个人中心<br>
🔒 **Cookie加密**：用户自行设置网盘Cookie，二进制加密存储，隐私安全<br>
🎨 **品牌定制**：完全自定义团队名称、LOGO<br>
⚙️ **精细权限**：多级访问控制与管理<br>
☁️ **云端备份**：自动定时备份用户资料至安全网盘<br>
<br>
<br>

**🐳 一键部署**<br>
系统架构: X86_64 (AMD64)<br>
```
首次访问: http://你的服务器IP:8091
默认账号: admin
默认密码: password
```
<br>

```
docker run -d \
  --name nextemby \
  --restart=unless-stopped \
  --network host \
  -e TZ=Asia/Shanghai \
  -v <配置文件存放路径>:/Config \
  nextemby/nextemby:latest
```
<br>

```
version: '3.8'
services:
  nextemby:
    image: nextemby/nextemby:latest
    container_name: nextemby
    restart: unless-stopped
    network_mode: host
    environment:
      - TZ=Asia/Shanghai
    volumes:
      - <配置文件存放路径>:/Config
```
<br>

普通版和团队版的区别<br>
⚡超频模式禁用（个人家庭使用用不上）<br>
🤝邀请注册禁用（个人家庭使用用不上）<br>
🕐定时备份禁用（个人家庭使用用不上）<br>
👥人数限制5人（个人家庭使用已足够）<br>

团队版激活码可联系作者捐赠获取https://t.me/NextEmbyChat
