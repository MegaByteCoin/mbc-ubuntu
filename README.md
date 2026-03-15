# MegaByte Coin for Ubuntu

<p align="center">
  <img src=".github/assets/walletFrame_bg.png" alt="MegaByte Coin Ubuntu Build" width="100%">

</p>

<p align="center">
  <a href="https://github.com/MegaByteCoin/mbc-ubuntu/releases/tag/v1.0.0"><img src="https://img.shields.io/badge/platform-Ubuntu%20%2F%20Linux-0f172a?style=for-the-badge&logo=ubuntu" alt="Ubuntu">
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

**MegaByte Coin (MBC)** is a Quark-based cryptocurrency with support for **staking**, **masternodes**, and a growing ecosystem around the project.

This repository contains the **Ubuntu / Linux build environment and source tree** for compiling the MegaByte Coin wallet and daemon.

---

## Network Parameters

| Parameter | Value |
|---|---|
| Coin | MegaByte Coin |
| Ticker | MBC |
| Algorithm | Quark |
| Staking | Yes |
| Masternodes | Yes = 1000 Coin|
| Max Supply | 1,000,000 MBC |
| Mainnet Port | 18777 |
| Block Time | 1 minute |
| Last POW Block | 1000 |
| Genesis Launch | 28.02.2026 01:00 UTC |
| Masternode Collateral | fill in after final confirmation |

---

## Official Links

- **Website:** https://megabytecoin.pp.ua
- **Exchange:** https://ex.mbc.pp.ua
- **Explorer:** https://explorer.megabytecoin.pp.ua
- **Bitcointalk:** https://megabytecoin.pp.ua/bitcointalk.php
- **GitHub:** https://github.com/MegaByteCoin
- **Discord:** https://megabytecoin.pp.ua/discord.php
- **YouTube:** https://megabytecoin.pp.ua/youtube.php
- **News Feed:** https://megabytecoin.pp.ua/feed/

---

## Repository Layout

- `depends/` — dependency build system for Ubuntu / Linux
- `src/` — daemon, CLI, and core sources
- `src/qt/` — Qt wallet sources
- `contrib/` — helper scripts and extra tools
- `.github/assets/` — README assets such as banner images

---

## Build on Ubuntu



1. Install dependencies

#bash

sudo apt-get update
sudo apt-get install -y build-essential libtool autotools-dev automake pkg-config bsdmainutils curl git cmake python3
sudo apt-get install -y libssl-dev libevent-dev libboost-all-dev
sudo apt-get install -y qtbase5-dev qttools5-dev-tools libqt5svg5-dev libqrencode-dev
sudo apt-get install -y libdb++-dev libminiupnpc-dev libzmq3-dev

2. Build depends for Linux
cd /root/mbc-ubuntu/depends
make HOST=x86_64-pc-linux-gnu -j2
3. Generate configure
cd /root/mbc-ubuntu
./autogen.sh
4. Configure
CONFIG_SITE=$PWD/depends/x86_64-pc-linux-gnu/share/config.site ./configure --prefix=/
5. Build
make -j2
Expected Output

After a successful build, the main binaries are expected here:

src/megabyted

src/megabyte-cli

src/qt/megabyte-qt

Notes

Mainnet uses Quark and a 1 minute block target.

Current Linux build path used in this project: /root/mbc-ubuntu/

The wallet news feed is configured to use the official project feed.

Contributing

We welcome contributors who can help with:

Linux wallet building

node hosting

network stability

exchange testing

wallet testing

ecosystem development

License

Distributed under the MIT software license. See COPYING for more information.
