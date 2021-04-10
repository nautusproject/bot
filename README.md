# lichess-bot
This is the code for  [this](https://lichess.org/@/FS-Schach-Super) bot. The code is a fork of [ShailChoksi/lichess-bot](https://github.com/ShailChoksi/lichess-bot) with a few modifications. Thanks for the upstream effort.

## How to Install

### Linux:
- NOTE: Only Python 3 is supported!
- Download the repo into lichess-bot directory
- Navigate to the directory: `cd lichess-bot`
- Install virtualenv: `pip3 install virtualenv`
- Setup virtualenv:
```
virtualenv .venv -p python3 #if this fails you probably need to add Python3 to your PATH
source .venv/bin/activate
pip3 install -r requirements.txt
```
- Copy `config.yml.default` to `config.yml`
- Edit the variants: `supported_variants` and time controls: `supported_tc` from the config.yml as necessary


## Lichess OAuth
- Create an account for your bot on [Lichess.org](https://lichess.org/signup)
- NOTE: If you have previously played games on an existing account, you will not be able to use it as a bot account
- Once your account has been created and you are logged in, [create a personal OAuth2 token](https://lichess.org/account/oauth/token/create) with the "Play as a bot" selected and add a description
- A `token` e.g. `Xb0ddNrLabc0lGK2` will be displayed. Store this in `config.yml` as the `token` field
- NOTE: You won't see this token again on Lichess.


## Setup Engine
- Place your engine(s) in the `engine` directory
- In `config.yml`, enter the binary name as the `engine.name` field
- Leave the `weights` field empty or see LeelaChessZero section for Neural Nets


## Lichess Upgrade to Bot Account
**WARNING** This is irreversible. [Read more about upgrading to bot account](https://lichess.org/api#operation/botAccountUpgrade).
- run `python3 lichess-bot.py -u`

## To Quit
- Press CTRL+C
- It may take some time to quit


## Tips & Tricks
- You can specify a different config file with the `--config` argument.
- Here's an example systemd service definition:
```
[Unit]
Description=lichess-bot
After=network-online.target
Wants=network-online.target

[Service]
Environment="PYTHONUNBUFFERED=1"
ExecStart=/home/USER/lichess-bot/.venv/bin/activate /home/USER/lichess-bot/lichess-bot.py
WorkingDirectory=/home/USER/lichess-bot/
User=USER
Group=USER
Restart=always

[Install]
WantedBy=multi-user.target
```

# Acknowledgements
Thanks to the Lichess team, especially T. Alexander Lystad and Thibault Duplessis for working with the LeelaChessZero
team to get this API up. Thanks to the Niklas Fiekas and his [python-chess](https://github.com/niklasf/python-chess) code which allows engine communication seamlessly. And thanks to the original developers of that bot.

# License
lichess-bot is licensed under the AGPLv3 (or any later version at your option). Check out LICENSE.txt for the full text.
