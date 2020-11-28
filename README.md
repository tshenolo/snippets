## Snippets
These are some of my favorite code snippets.


### CakePHP
#### Create a CakePHP Project
```bash
composer create-project --prefer-dist cakephp/app:^3.9 my_app_name
```

#### Create a controller for a table called users
```bash
bin/cake bake controller Users
```

#### Create a model (and entity) for a table called users
```bash
bin/cake bake model Users
```

#### Create the default template files for a table (add/edit/view/index)
```bash
bin/cake bake template Users
```

#### Bake add/edit/view/index using one command
```bash
bin/cake bake all Users
```

#### Bake just the index template file
```bash
bin/cake bake template Users index
```

### Ionic
#### Install Ionic
```bash
npm install -g @ionic/cli
```

#### Create a Ionic Project
```bash
ionic start   <my_app_name>  <template> [options]
```

| Template	  | Description                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------|
| tabs	      | A starting project with a simple tabbed interface                                                        |
| blank	      | A blank starter project                                                                                  |
| sidemenu    |	A starting project with a side menu with navigation in the content area                                  |
| super	      | A starting project complete with pre-built pages, providers and best practices for Ionic development.    |
| conference  |	A project that demonstrates a realworld application                                                      |
| tutorial	  | A tutorial based project that goes along with the Ionic documentation                                    |
| aws	        | AWS Mobile Hub Starter                                                                                   |


#### Run Locally in a Web Browser
```bash
ionic serve
```

#### Adding a new page
```bash
ionic g page login
```

#### Routing to another page
```TypeScript
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-gamelevels',
  templateUrl: './gamelevels.page.html',
  styleUrls: ['./gamelevels.page.scss'],
})
export class GamelevelsPage implements OnInit {

  constructor(private router: Router) {}

  ngOnInit() {
  }

  playgame(level:number){
    this.router.navigate(['gameplay', level ]);
  }

}
```

#### Integrating JQuery
```bash
npm install jquery --save
npm install @types/jquery
```

#### Import jquery on your page like this
```TypeScript
import * as $ from "jquery";
```

### Java
coming soon

### Javascript
coming soon

### jQuery
coming soon

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


### PeopleCode
coming soon

### Splunk
coming soon

### SQL
coming soon

### Windows
coming soon

### Wordpress
coming soon
