<h1 align="center">
Bearshare Pot 🐻💰
</h1>

<div align="center">

[![Static Badge](https://img.shields.io/badge/GitHub-blue?style=flat&logo=github)](https://github.com/XternA/bearshare-reward)
[![Static Badge](https://img.shields.io/badge/License-purple?style=flat&logo=github)](https://github.com/XternA/bearshare-reward?tab=License-1-ov-file)
[![Docker Stars](https://img.shields.io/docker/stars/xterna/bearshare-pot?logo=docker&label=Docker%20Stars)](https://hub.docker.com/r/xterna/bearshare-pot)
[![GitHub Repo stars](https://img.shields.io/github/stars/XternA/bearshare-reward?style=flat&logo=github&label=Stars&color=orange)](https://github.com/XternA/bearshare-reward)
[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg?style=flat&logo=paypal)](https://www.paypal.com/donate/?hosted_button_id=32DCQ65QM5FNE)

If you like this project, don't forget to leave a star. ⭐

### Containerized Docker image for [Bearshare](https://bit.ly/4g7PmCs) daily reward 💰

>**Note:** This built image comes with no warranty of any kind. By using this image you agree this License Aggrement in addition with Honeygain's T&C.

This is a simple Docker image for installing Bearshare's daily reward auto-claim script as a container.

</div>

## Pulling Image 🐋
**64-Bit** architecture and **ARM64**:
```sh
docker pull ghcr.io/xterna/bearshare-pot
```

## Overview 🐻
[**Bearshare-Pot**](https://bit.ly/4g7PmCs) 🐻💰 is a script (bot) powered by NodeJS and JavaScript to automatically claim the daily reward from [**Bearshare**](https://bit.ly/4g7PmCs)🐻.

The script is designed to be run in a docker environment, allowing it to be deployed alongside the Bearshare docker container.

It uses very minimal resources, resulting in the CPU utilisation staying at idle **0%** the entire time unless logging into the website.
```
CONTAINER ID   NAME            CPU %     MEM USAGE / LIMIT   MEM %     NET I/O          BLOCK I/O      PIDS
702d98b1805b   bearshare-pot   0.00%     73.51MiB / 320MiB   22.97%    2.13MB / 149kB   58MB / 127MB   12
```
> This script comes pre-bundled with [**Income Generator**](https://github.com/XternA/income-generator). A tool which consolidates and earns passive income from multiple sources.

## Features 🚀
- Automatically log in and claim daily reward if threshold reached.
- Auto-wait until next event trigger.
- If error occurs, will auto restart the bot.

### Output 🖥️
This is what the script looks like when you inspect the output via `docker logs bearshare-pot`.
```
------------ Bearshare Reward Auto Claim ------------
Starting login process...
Logging in as example@abc.com
Logged into Bearshare 🐻
-----------------------------------------------------

Current Earnings:    $0.285 💵
Lifetime Earnings:   $0.285 💰
Reward Progress:     24.53/50 MB 🐻

Not earned enough to claim yet ❌
Current logged time is 13:01:53
Next event trigger at 16:00:00
Wait time is 2 hour 58 minute ⏱️
```

## Usage 📃
Define the following environment variable to bootstrap the image.

| Variable | Description | Mandatory |
| :--- | :--- | :---: |
| **EMAIL**     | Your Bearshare email address    | YES |
| **PASSWORD**  | Your Bearshare password         | YES |

Or supply credentials in a Dotenv `.env` file.
```markdown
EMAIL=<email_address>
PASSWORD=<password_credential>
```

## Docker Deployment 🐋
### Compose
File: `compose.yml`
```yaml
services:
  bearshare-pot:
    container_name: bearshare-pot
    image: xterna/bearshare-pot
    restart: unless-stopped
    environment:
      - EMAIL=$EMAIL
      - PASSWORD=$PASSWORD
    dns:
      - 1.1.1.1
      - 8.8.8.8
```

With Bearshare app docker image.
```yaml
services:
  bearshare:
    container_name: bearshare
  image: xterna/bearshare
    restart: always
    environment:
      - EMAIL=$EMAIL
      - PASSWORD=$PASSWORD
    dns:
      - 1.1.1.1
      - 8.8.8.8

  bearshare-pot:
    container_name: bearshare-pot
    image: ghcr.io/xterna/bearshare-pot
    restart: unless-stopped
    environment:
      - EMAIL=$EMAIL
      - PASSWORD=$PASSWORD
    dns:
      - 1.1.1.1
      - 8.8.8.8
    depends_on:
      - bearshare
```

Execute where compose file is located.
```yaml
docker compose up -d
```

ℹ️ **Note:** If you apply resource limits such as CPU and RAM you need to set the following bare minimum:
```
  - cpu=0.8
  - mem_limit=350m
```
The script won't be able to run properly and will constantly timeout if the CPU and RAM limit is set lower than recommended. This is only required during the boot-up phase where it needs to spin up a headless browser to connect to the site. Resource is most intensive only during this phase.

### CLI
Using environment variable or Dotenv `.env` defined e.g.
```sh
docker run -d --restart unless-stopped --name bearshare-pot -e EMAIL=$EMAIL -e PASSWORD=$PASSWORD ghcr.io/xterna/bearshare-pot
```

Directly passing credentials.
```sh
docker run -d --restart unless-stopped --name bearshare-pot -e EMAIL=example.gmail.com -e PASSWORD=pass123 ghcr.io/xterna/bearshare-pot
```
This will start the application in the background. The alias assigned is `bearshare-pot`.

## Like My Work? 🫶
Donations are warmly welcomed no matter how small and thank you very much. 😌
- **Bitcoin (BTC)** - `bc1qq993w3mxsf5aph5c362wjv3zaegk37tcvw7rl4`
- **Ethereum (ETH)** - `0x2601B9940F9594810DEDC44015491f0f9D6Dd1cA`
- **Binance Smart Chain (BSC)** - `0x2601B9940F9594810DEDC44015491f0f9D6Dd1cA`
- **Solana (SOL)** - `Ap5aiAbnsLtR2XVJB3sp37qdNP5VfqydAgUThvdEiL5i`
- **PayPal** - [@xterna](https://paypal.me/xterna)

## Disclaimer ⚠️
Disclaimer: This image is neither affiliated with nor endorsed by Honeygain. Use this image at your own risk and responsibility. By using this image, you agree to be automatically bound by the License Agreement associated with it.

The author does not provide any assurances, whether explicit or implicit, regarding the accuracy, completeness, or appropriateness of this image for specific purposes. The author shall not be held accountable for any damages, including but not limited to direct, indirect, incidental, consequential, or special damages, arising from the use or inability to use this image or its accompanying documentation, even if the possibility of such damages has been communicated.

By choosing to use this image, you acknowledge and assume all risks associated with its use. Additionally, you agree that the author cannot be held liable for any issues or consequences that may arise as a result of its usage.
