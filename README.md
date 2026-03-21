# MegaByte Coin for Ubuntu

<p align="center">
  <img src=".github/assets/walletFrame_bg.png" alt="MegaByte Coin Ubuntu Build" width="100%">
</p>

<p align="center">
  <a href="https://github.com/MegaByteCoin/mbc-ubuntu/releases/tag/v1.0.0"><img src="https://img.shields.io/badge/platform-Ubuntu%2020.04%20%2F%20Linux-0f172a?style=for-the-badge&logo=ubuntu" alt="Ubuntu"></a>
  <img src="https://img.shields.io/badge/algorithm-Quark-2563eb?style=for-the-badge" alt="Quark">
  <img src="https://img.shields.io/badge/ticker-MBC-0ea5e9?style=for-the-badge" alt="MBC">
  <img src="https://img.shields.io/badge/staking-Yes-16a34a?style=for-the-badge" alt="Staking">
  <img src="https://img.shields.io/badge/masternodes-Yes-7c3aed?style=for-the-badge" alt="Masternodes">
  <img src="https://img.shields.io/badge/max_supply-1%2C000%2C000%20MBC-f59e0b?style=for-the-badge" alt="Supply">
</p>

<p align="center">
  <a href="https://megabytecoin.pp.ua"><img src="https://img.shields.io/badge/Website-megabytecoin.pp.ua-111827?style=for-the-badge"></a>
  <a href="https://explorer.megabytecoin.pp.ua"><img src="https://img.shields.io/badge/Explorer-Online-111827?style=for-the-badge"></a>
  <a href="https://github.com/MegaByteCoin/mbc-win/releases/tag/v1.0.0"><img src="https://img.shields.io/badge/Windows%20Wallet-v1.0.0-111827?style=for-the-badge"></a>
  <a href="https://ex.mbc.pp.ua"><img src="https://img.shields.io/badge/Exchange-Test%20Mode-111827?style=for-the-badge"></a>
</p>

---

## Overview

**MegaByte Coin (MBC)** is a Quark-based cryptocurrency with support for **staking** and **masternodes**.

This repository contains the **Ubuntu / Linux source tree and build environment** for compiling the MegaByte Coin daemon, CLI tools, and Qt wallet.

This README is focused on a **single regular mainnet wallet setup on Ubuntu 20.04**, built through the `depends/` system and installed into:

```bash
/root/.mbc
```

---

## Network Parameters

| Parameter | Value |
|---|---|
| Coin | MegaByte Coin |
| Ticker | MBC |
| Algorithm | Quark |
| Staking | Yes |
| Masternodes | Yes |
| Masternode Collateral | 1000 MBC |
| Max Supply | 1,000,000 MBC |
| Mainnet Port | 18777 |
| Mainnet RPC Port | 18778 |
| Block Time | 1 minute |
| Last POW Block | 1000 |
| Genesis Launch | 28.02.2026 01:00 UTC |

---

## Current Mainnet Nodes

The current mainnet layout used in this guide is:

- `31.131.21.71:18777`
- `31.131.21.71:18779`
- `31.131.21.71:18781`
- `41.138.197.2:18777`
- `41.138.197.3:18777`
- `41.138.197.4:18777`
- `41.138.197.5:18777`
- `41.138.197.6:18777`
- `41.138.197.7:18777`
- `41.138.197.8:18777`

Explorer:

- `https://explorer.megabytecoin.pp.ua`
- reserve direct URL: `http://31.131.21.71:3001/`

---

## Official Links

- **Website:** https://megabytecoin.pp.ua
- **Exchange:** https://ex.mbc.pp.ua
- **Explorer:** https://explorer.megabytecoin.pp.ua
- **Bitcointalk:** https://megabytecoin.pp.ua/bitcointalk.php
- **GitHub:** https://github.com/MegaByteCoin
- **Discord:** https://megabytecoin.pp.ua/discord.php
- **YouTube:** https://megabytecoin.pp.ua/youtube.php
- **News Feed:** https://megabytecoin.pp.ua/feed
- **Ubuntu/Linux release:** https://github.com/MegaByteCoin/mbc-ubuntu/releases/tag/v1.0.0
- **Windows release:** https://github.com/MegaByteCoin/mbc-win/releases/tag/v1.0.0

---

## Repository Layout

- `depends/` — dependency build system for Ubuntu / Linux
- `src/` — daemon, CLI, transaction tool, and core sources
- `src/qt/` — Qt wallet sources
- `contrib/` — helper scripts and extra tools
- `.github/assets/` — README assets such as banner images

---

## Build on Ubuntu 20.04 through `depends`

### 1. Install build dependencies

```bash
sudo apt-get update
sudo apt-get install -y build-essential libtool autotools-dev automake pkg-config bsdmainutils curl git cmake python3 ca-certificates
sudo apt-get install -y libssl-dev libevent-dev libboost-all-dev
sudo apt-get install -y qtbase5-dev qttools5-dev-tools libqt5svg5-dev libqrencode-dev
sudo apt-get install -y libdb++-dev libminiupnpc-dev libzmq3-dev
```

### 2. Build `depends` for Linux

```bash
cd /root/mbc-ubuntu/depends
make HOST=x86_64-pc-linux-gnu -j2
```

### 3. Generate `configure`

```bash
cd /root/mbc-ubuntu
./autogen.sh
```

### 4. Configure the project

```bash
cd /root/mbc-ubuntu
CONFIG_SITE=$PWD/depends/x86_64-pc-linux-gnu/share/config.site ./configure --prefix=$PWD/depends/x86_64-pc-linux-gnu
```

### 5. Build

```bash
cd /root/mbc-ubuntu
make -j2
```

---

## Expected Build Output

After a successful build, the binaries should be available here:

```bash
/root/mbc-ubuntu/src/mbcd
/root/mbc-ubuntu/src/mbc-cli
/root/mbc-ubuntu/src/mbc-tx
/root/mbc-ubuntu/src/qt/mbc-qt
```

---

## Install Binaries into `/root/.mbc`

```bash
mkdir -p /root/.mbc
install -m 755 /root/mbc-ubuntu/src/mbcd /root/.mbc/mbcd
install -m 755 /root/mbc-ubuntu/src/mbc-cli /root/.mbc/mbc-cli
install -m 755 /root/mbc-ubuntu/src/mbc-tx /root/.mbc/mbc-tx
install -m 755 /root/mbc-ubuntu/src/qt/mbc-qt /root/.mbc/mbc-qt
```

Check the installed files:

```bash
ls -lh /root/.mbc/mbcd /root/.mbc/mbc-cli /root/.mbc/mbc-tx /root/.mbc/mbc-qt
```

---

## Example `mbc.conf` for a Regular Mainnet Wallet

This example is for a **normal mainnet wallet / daemon** on Ubuntu 20.04.

It is **not** a three-wallet layout and **not** a testnet config.

File path:

```bash
/root/.mbc/mbc.conf
```

Example config:

```ini
rpcuser=mbcuser
rpcpassword=CHANGE_THIS_TO_A_LONG_RANDOM_PASSWORD

listen=1
daemon=1
server=1
txindex=1

port=18777
rpcport=18778

maxconnections=128
upnp=0

addnode=31.131.21.71:18777
addnode=31.131.21.71:18779
addnode=31.131.21.71:18781
addnode=41.138.197.2:18777
addnode=41.138.197.3:18777
addnode=41.138.197.4:18777
addnode=41.138.197.5:18777
addnode=41.138.197.6:18777
addnode=41.138.197.7:18777
addnode=41.138.197.8:18777
```

Notes:

- `rpcuser` and `rpcpassword` should be changed before first launch.
- Do not keep outdated nodes from `31.131.27.102`.
- This config is intended for a regular mainnet node or wallet user.
- Masternode-specific options should only be added on a real masternode server.

---

## Create `mbc.conf` from Terminal

```bash
cat > /root/.mbc/mbc.conf <<'EOF'
rpcuser=mbcuser
rpcpassword=CHANGE_THIS_TO_A_LONG_RANDOM_PASSWORD

listen=1
daemon=1
server=1
txindex=1

port=18777
rpcport=18778

maxconnections=128
upnp=0

addnode=31.131.21.71:18777
addnode=31.131.21.71:18779
addnode=31.131.21.71:18781
addnode=41.138.197.2:18777
addnode=41.138.197.3:18777
addnode=41.138.197.4:18777
addnode=41.138.197.5:18777
addnode=41.138.197.6:18777
addnode=41.138.197.7:18777
addnode=41.138.197.8:18777
EOF
```

---

## Start, Stop, and Check the Wallet

### Start daemon

```bash
/root/.mbc/mbcd -datadir=/root/.mbc -conf=/root/.mbc/mbc.conf -daemon
```

### Stop daemon

```bash
/root/.mbc/mbc-cli -datadir=/root/.mbc -conf=/root/.mbc/mbc.conf stop
```

### Basic info

```bash
/root/.mbc/mbc-cli -datadir=/root/.mbc -conf=/root/.mbc/mbc.conf getinfo
```

### Peer list

```bash
/root/.mbc/mbc-cli -datadir=/root/.mbc -conf=/root/.mbc/mbc.conf getpeerinfo
```

### Run Qt wallet

```bash
/root/.mbc/mbc-qt
```

---

## Notes

- Mainnet uses Quark and a 1 minute block target.
- Current Linux build path used in this project: `/root/mbc-ubuntu/`
- Current installed wallet path used in this guide: `/root/.mbc`
- The wallet news feed is configured to use the official project feed.
- This guide is written for Ubuntu 20.04 and a single regular wallet installation.

---

## Contributing

We welcome contributors who can help with:

- Linux wallet building
- node hosting
- network stability
- exchange testing
- wallet testing
- ecosystem development

---

## License

Distributed under the MIT software license. See `COPYING` for more information.
