### Windows
#### Find charset of a file
```
file -i filename
```

#### Converting files to UTF-8
```
iconv -f original_charset -t utf-8 originalfile > newfile
```

#### List directories in a folder
```
dir /s /b /o:n /ad
```

#### List File names only
```
dir /b /a-d
```

#### List Folders and Sub folders
```
dir /s /b /o:n /ad
```

#### Mount to nfs on windows
```
mount -o anon \\<IPADDRESS>\<DRIVE> Z:
```

#### Get SSL Certificate
```
openssl s_client -connect <SERVER>:<PORT> < /dev/null | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > <SERVER>.crt
```


