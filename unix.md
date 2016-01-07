Change all directory permissions
```bash
find . -type d -exec chmod 755 {} +
```

Get octal file permissions
```bash
stat -c "%a %n" *
```

Get disk usage
```bash
df -h
```