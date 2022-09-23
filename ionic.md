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