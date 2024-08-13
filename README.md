# XOLANA-stuff

-----

## Xolana Validator Monitor

To monitor our validator we can use `solana-watchtower`. For greater reliability, a separate, simple VPS server is required to run this monitor. 
As a notification frontend we will use Telegram.

### Installation

Install solana on your VPS

```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.18.22/install)"
```

### Systemd unit

To create a `systemd` unit that will run `solana-watchtower` type:

```bash
sudo vi /etc/systemd/system/xolana-watchtower.service
```

and paste the content of [xolana-watchtower.service](https://github.com/DamianPala/XOLANA-stuff/blob/main/xolana-watchtower.service). 
Replace all `<fields>` with proper values.  
For `<user>` use your local username of the user under which you wnat to run the monitor. In most cases you will have the same user in `User` field and `ExecStart` of `systemd` unit.  
To get `bot-token` create Telegram Bot by chatting with `@BotFather`  
To get `chat-id` use this tutorial: [How to get Telegram Bot Chat ID](https://gist.github.com/nafiesl/4ad622f344cd1dc3bb1ecbe468ff9f8a)  
You can use direct chat with your bot or you can add your bot to a group. In this case adding an admin permision to this bot may be needed.

Enable and start services:

```bash
sudo systemctl daemon-reload
sudo systemctl enable xolana-watchtower.service
sudo systemctl start xolana-watchtower.service
```

To view monitor logs use:

```bash
journalctl -fu xolana-watchtower.service
```

You can set specific tresholds and other option. To check this, use `solana-watchtower --help`.

### Links
 - https://docs.solanalabs.com/operations/best-practices/monitoring#solana-watchtower
