# 🚀 Installation Guide - Meross LAN (MSH400 Support)

## ⚠️ Domain Name: `meross_lan_msh400`

This fork uses a **different domain** to avoid conflicts with the original integration.

| Original | This Fork |
|----------|-----------|
| Domain: `meross_lan` | Domain: `meross_lan_msh400` |
| Name: "Meross LAN" | Name: "Meross LAN (MSH400 Support)" |

**Benefits**:
- ✅ Both integrations can coexist
- ✅ No need to uninstall the original
- ✅ Easy to switch between versions
- ✅ Clear identification in UI

---

## Installation Methods

### Method 1: HACS (Recommended)

#### Step 1: Add Custom Repository

1. Open **Home Assistant** → **HACS** → **Integrations**
2. Click the **⋮** menu (top right) → **Custom repositories**
3. Add:
   - **Repository**: `https://github.com/vAugagneur/meross_lan`
   - **Category**: `Integration`
4. Click **Add**

#### Step 2: Install

1. In HACS → Integrations, search for **"Meross LAN"**
2. Select **"Meross LAN (MSH400 Support)"** (from vAugagneur)
3. Click **Download**
4. **Restart Home Assistant**

#### Step 3: Configure

1. Go to **Settings** → **Devices & Services**
2. Click **+ Add Integration**
3. Search for **"Meross LAN (MSH400 Support)"**
4. Follow the configuration wizard

---

### Method 2: Manual Installation

#### On the Home Assistant Server

```bash
# 1. Navigate to custom_components
cd /config/custom_components

# 2. Clone the repository
git clone https://github.com/vAugagneur/meross_lan.git temp_install

# 3. Copy integration folder
cp -r temp_install/custom_components/meross_lan_msh400 ./

# 4. Clean up
rm -rf temp_install

# 5. Set permissions (if needed)
chown -R homeassistant:homeassistant meross_lan_msh400
```

#### Via SSH (for Docker/Supervised)

```bash
# 1. Connect to your Home Assistant server
ssh user@homeassistant-ip

# 2. Navigate to config directory
cd /path/to/homeassistant/config/custom_components

# 3. Clone and install
git clone https://github.com/vAugagneur/meross_lan.git temp
cp -r temp/custom_components/meross_lan_msh400 ./
rm -rf temp

# 4. Restart Home Assistant container
docker restart homeassistant
# OR for docker-compose:
cd /path/to/homeassistant
docker-compose restart homeassistant
```

---

## Verification

### Check Installation

1. **Settings** → **System** → **Logs**
2. Filter for `meross_lan_msh400`
3. You should see:
   ```
   INFO Successfully loaded custom_components.meross_lan_msh400
   ```

### Check Available Integration

1. **Settings** → **Devices & Services**
2. Click **+ Add Integration**
3. Search for **"MSH400"** or **"Meross"**
4. You should see: **"Meross LAN (MSH400 Support)"**

---

## Configuration

### First Time Setup

1. **Add Integration**:
   - Settings → Devices & Services → + Add Integration
   - Search: "Meross LAN (MSH400 Support)"

2. **Choose Configuration Method**:
   - **HTTP (Device IP)**: For devices on local network
   - **MQTT**: For MQTT-configured devices
   - **Meross Cloud**: To import devices from cloud account

3. **For MSH400 Hub**:
   - Enter Hub IP address
   - Enter device key (or recover from Meross cloud)
   - Hub and all subdevices will be discovered automatically

### Expected Entities (MSH400)

After setup, you should see:

**Hub Device**:
- `sensor.msh400_XXXXXX_hub`

**MS100 Sensors** (Temperature/Humidity):
- 🌡️ `sensor.ms100_39000e5d6b50_temperature`
- 💧 `sensor.ms100_39000e5d6b50_humidity`

**MS200 Sensors** (Door/Window):
- 🚪 `binary_sensor.ms200_39000e5d69eb_window`

---

## Side-by-Side Installation

### Running Both Versions

You can have **both** integrations installed:

| Integration | Domain | Devices |
|-------------|--------|---------|
| **Original** | `meross_lan` | MSH300 + other devices |
| **This Fork** | `meross_lan_msh400` | MSH400 + sensors |

**No conflicts!** Each uses a different domain.

### Migration Strategy

1. **Install this fork** (keep original installed)
2. **Configure MSH400** in the new integration
3. **Test** for a few days
4. **Optionally remove** the original if you prefer this version

---

## Troubleshooting

### Integration Not Found

**Problem**: Can't find "Meross LAN (MSH400 Support)" in Add Integration

**Solution**:
```bash
# Check if files are correctly installed
ls -la /config/custom_components/meross_lan_msh400/

# Should show:
# __init__.py
# manifest.json
# const.py
# ... (many other files)

# Restart Home Assistant
ha core restart
```

---

### HACS Shows Original Integration

**Problem**: HACS shows original "Meross LAN" instead of MSH400 version

**Solution**:
1. Remove the original repository from HACS custom repos
2. Re-add: `https://github.com/vAugagneur/meross_lan`
3. Ensure Category is **Integration**
4. Reload HACS

---

### Conflict with Original Integration

**Problem**: Errors like "Domain meross_lan already configured"

**This should NOT happen!** The fork uses `meross_lan_msh400`.

If you see this:
1. Check `manifest.json` in installed folder
2. Verify `"domain": "meross_lan_msh400"`
3. If incorrect, reinstall from this fork

---

### Permission Errors

**Problem**: "Permission denied" when accessing integration

**Solution**:
```bash
# On Home Assistant OS/Supervised:
chown -R root:root /config/custom_components/meross_lan_msh400

# On Docker with custom user:
chown -R 1000:1000 /config/custom_components/meross_lan_msh400
```

---

## Updating

### Via HACS

1. HACS → Integrations
2. Find "Meross LAN (MSH400 Support)"
3. Click **Update**
4. Restart Home Assistant

### Manual Update

```bash
cd /config/custom_components
rm -rf meross_lan_msh400
git clone https://github.com/vAugagneur/meross_lan.git temp
cp -r temp/custom_components/meross_lan_msh400 ./
rm -rf temp
# Restart Home Assistant
```

---

## Uninstallation

### Remove Integration

1. **Settings** → **Devices & Services**
2. Find **"Meross LAN (MSH400 Support)"**
3. Click **⋮** → **Delete**
4. Confirm deletion

### Remove Files

```bash
rm -rf /config/custom_components/meross_lan_msh400
# Restart Home Assistant
```

---

## Support

- **Issues**: https://github.com/vAugagneur/meross_lan/issues
- **Original Integration**: https://github.com/krahabb/meross_lan
- **Documentation**: [MSH400_SUPPORT.md](MSH400_SUPPORT.md)

---

## FAQ

**Q: Can I use this with MSH300?**  
A: Yes! MSH300 is fully supported (same as original integration)

**Q: Will my devices migrate automatically?**  
A: No. This is a separate integration. You need to configure devices again.

**Q: Can I switch back to original meross_lan?**  
A: Yes! Just uninstall this fork and configure devices in the original.

**Q: Why a different domain name?**  
A: To avoid conflicts and allow side-by-side installation for testing.

**Q: Will this be merged into original meross_lan?**  
A: That's the goal! Once thoroughly tested, we'll submit a PR.

---

**Repository**: https://github.com/vAugagneur/meross_lan  
**Version**: Based on meross_lan 5.8.0 + MSH400 support  
**Last Updated**: 2026-01-27
