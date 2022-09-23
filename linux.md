### Linux
#### Convert jpg to PDF (3 steps)
#### Install the ImageMagick package (step 1)
```bash
sudo apt-get install imagemagick
```

#### List files as a single column (step 2)
```bash
ls -v --format single-column *.jpg
```

#### Convert images to PDF (step 3)
```bash
convert `ls -v --format single-column *.jpg` FileName.pdf
```

#### Reload .File (.bashrc , .profile)
```bash
source ~/.File
```

#### Create Bash Alias
```bash
alias workspace="cd /mnt/f/Users/username/Documents/workspace"
```
##### Usage:
```bash
workspace
```

#### Create Bash Function
```bash
function deployd4() { mvninstall; chmod 664 "$@"; scp "$@" SERVER04:~/.w;}
```
##### Usage:
```bash
deployd4 target/app.war
```

#### Copy Remote File
```bash
scp username@server:/tmp/filename.txt .
```

#### Copy Remote File (passing password to command)
```bash
sshpass -p 'password' scp username@server:/tmp/filename.txt .
```

#### Editing remote files via scp in vim
```bash
vim scp://remoteuser@server//absolute/path/to/document
```

#### ssh-keyscan
```bash
ssh-keyscan -t <dsa | rsa> <SERVER>
```