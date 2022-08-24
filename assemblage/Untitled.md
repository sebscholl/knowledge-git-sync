202208241308

Status: #info
Tags: [[linux]] [[servers & networking]]

# Preventing sleep mode on Linux

## Turning off Sleep

On Ubuntu 16.04 LTS, I successfully used the following to disable suspend:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

And this to re-enable it:

```bash
sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

**Restart the computer after changes.**

## Turning off Sleep on Lid Close

1.  Open the file for editing.
```bash
sudo vim /etc/systemd/logind.conf
```
2.  Edit line **#HandleLidSwitch=suspend**.
    -   **HandleLidSwitch=poweroff** to shutdown computer when lid is closed
    -   **HandleLidSwitch=hibernate** to hibernate computer when lid is closed
    -   **HandleLidSwitch=suspend** to suspend computer when lid is closed
    -   **HandleLidSwitch=ignore** to do nothing to do nothing
3.  Save the file and restart the service to apply the changes.
```bash
systemctl restart systemd-logind
```

___

[StackOverflow on Preventing Sleep on Linux](https://askubuntu.com/questions/47311/how-do-i-disable-my-system-from-going-to-sleep)
[[setting up a remote SSH for Linux PC]]