## New OSX Dev Environment

### Manually installed applications

### Homebrew packages
* git (much newer than OSX git)
* tmux
* reattach-to-user-namespace (for tmux)
* openssl
* python (installs `pip` also)

### Sublime Text packages
* [https://packagecontrol.io/installation](Package Control)
* GitGutter
* Theme - Spacegray

### Making sure openssl is using homebrew's
Check `/usr/local/bin` for `openssl` symlink. If it's not there:
```
brew link --force openssl
```
and open a new console (`which openssl`)

### Troubleshooting
#### iTerm2 <kbd>&#8997;</kbd><kbd>&larr;</kbd> and <kbd>&#8997;</kbd><kbd>&rarr;</kbd> keys not working
Set the iTerm2 profile keybindings to send the following hex codes:
* <kbd>&#8997;</kbd><kbd>&larr;</kbd>: `0x1b 0x62`
* <kbd>&#8997;</kbd><kbd>&rarr;</kbd>: `0x1b 0x66`

#### Failing to install eventmachine gem:
Make sure openssl is installed (homebrew command: `brew info openssl`)
```
gem install eventmachine -v '1.0.8' -- --with-cppflags=-I/usr/local/opt/openssl/include
```

Can check on where openssl put their include directory with `brew info openssl`

#### Installing an older version of postgresql (9.3.5 in this case)
```
brew install https://raw.githubusercontent.com/Homebrew/homebrew/11fcb57db1e915e8035b1c3bf6d4d634f32a226d/Library/Formula/postgresql.rb
```
This link was found by looking at the history: https://github.com/Homebrew/homebrew/commits/master/Library/Formula/postgresql.rb and using the version of the file where the bottle was updated.

If postgres has issues starting, check logs in `/usr/local/var/postgres`.  I've found that `/usr/local/var` may be owned by root so that has to be fixed to my user.  Can manually initialize and create a db with:
```
initdb /usr/local/var/postgres
createdb
```