+++
title = "Shell script for battery Notification"
date = 2022-01-04
+++

# Dependencies
These are the application you need in Arch Linux. You can try with same applications in any other distro as well

- Cron

    `sudo pacman -S cronie`

- Dunst

    `sudo pacman -S dunst`


# Process

## Step 1 : Bash script

[Download from Github](https://github.com/pavanbhat1999/bin/blob/master/scripts/battery_notification.sh)
```bash
#!/usr/bin/bash
STATUS=$(cat /sys/class/power_supply/BAT0/status)
CURRENT_BAT=$(cat /sys/class/power_supply/BAT0/capacity)
UPPER_LIMIT=60
LOWER_LIMIT=30
if [ "$STATUS" = "Charging" ]; then
    echo 'Charging'
    if [ $CURRENT_BAT -gt $UPPER_LIMIT ]
    then
        notify-send "Above limit Please Unplug the Charger" -u critical
    fi
else
    echo "Not Charging"
    if [ $CURRENT_BAT -gt $LOWER_LIMIT ]
    then
        echo 'Optimum Charge'
    fi
    if [ $CURRENT_BAT -lt $LOWER_LIMIT ]
    then
        notify-send "Gone below Lower Limit. Charge Me Please" -u critical
    fi
fi

```

## Step 2 : Dunsrc for sound

[Download from Github](aaa)

```bash
[global]
monitor = 0
follow = mouse
geometry = "1000x1000-20+48"
indicate_hidden = yes
shrink = no
separator_height = 0
padding = 32
horizontal_padding = 32
frame_width = 2
sort = no
idle_threshold = 120
font = Fira Code 14
line_height = 4
markup = full
format = %s\n%b
alignment = center
show_age_threshold = 60
word_wrap = yes
ignore_newline = no
stack_duplicates = false
hide_duplicate_count = yes
show_indicators = no
icon_position = off
sticky_history = yes
history_length = 20
browser = /usr/bin/brave
always_run_script = true
title = Dunst
class = Dunst
mouse_middle_click = do_action
[shortcuts]
close = ctrl+space
close_all = ctrl+shift+space
history = ctrl+grave
context = ctrl+shift+period

[urgency_low]
timeout = 4
background = "#141c21"
foreground = "#93a1a1"
frame_color = "#8bc34a"

[urgency_normal]
timeout = 8
background = "#141c21"
foreground = "#93a1a1"
frame_color = "#ba68c8"

[urgency_critical]
timeout = 5
background = "#B10F29"
foreground = "#93a1a1"
frame_color = "#ff7043"
[play_sound]
    summary="*"
    # sound file which you want
    script= paplay sound.ogg
```

## Step 3 : Add Cron

After installing cron and enabling it run the following command

`crontab -e`


Then add these lines of code

`* * * * *  XDG_RUNTIME_DIR=/run/user/$(id -u) sh battery_notification.sh`
