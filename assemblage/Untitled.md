202208241308

Status: #info
Tags: [[linux]] [[servers & networking]]

# Preventing sleep mode on Linux

On Ubuntu 16.04 LTS, I successfully used the following to disable suspend:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

And this to re-enable it:

```bash
sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

**Restart the computer after changes.**
___

[StackOverflow on Preventing Sleep on Linux](https://askubuntu.com/questions/47311/how-do-i-disable-my-system-from-going-to-sleep)
[[setting up a remote SSH for Linux PC]]