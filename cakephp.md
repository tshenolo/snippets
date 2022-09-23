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