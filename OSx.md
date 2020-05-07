# OSx Catalina

Set bandwidth restriction

```zsh
sudo dnctl pipe 1 config bw 400KByte/s
sudo pfctl -q -e
```

Unset bandwidth restriction

```zsh
sudo dnctl pipe 1 config bw 0
sudo pfctl -d
```

Check rules

```zsh
sudo dnctl list
```

Enable allow from anyware

```zsh
sudo spctl --master-disable
```
