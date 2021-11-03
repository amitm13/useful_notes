
# Add Gitlab to Laravel to report errors as gitlab issue

how to add gitlab php package to handle error reporting in gitlab issue.


## Acknowledgements

 - [Github PHP Package URL](https://github.com/GrahamCampbell/Laravel-GitLab)

## Installation

Follow below steps to install this package and configure with laravel

```bash
  composer require "graham-campbell/gitlab:^5.4" "guzzlehttp/guzzle:^7.2" "http-interop/http-factory-guzzle:^1.0"
```

```bash
  php artisan vendor:publish
```
    
Now you will have gitlab.php file in config folder.

config/gitlab.php

add below key after *'default' => 'main',* in config file

**'project_id'=>env('GITLAB_PROJECT_ID’),**

update token variable in “connections” -> “main”

**'token'   => env('GITLAB_TOKEN'),**

Now we need to update `App\Exceptions\Handler.php` file

add below line 

`use GrahamCampbell\GitLab\Facades\GitLab;`

In register function -> reportable -> add below code

`$errorMessage = '<strong>Error:</strong>' . $e->getMessage();`

`$errorMessage .= '<br/><strong>File:</strong>' . $e->getFile();`

`$errorMessage .= '<br/><strong>Line No:</strong>' . $e->getLine();`

`$projectIsuses = collect(\GrahamCampbell\GitLab\Facades\GitLab::Projects()->issues(config('gitlab.project_id'),['state'=>'opened']))->pluck('description')->toArray();`

`if (!in_array($errorMessage, $projectIsuses)) {
   GitLab::issues()->create(config('gitlab.project_id'), ['description' => $errorMessage, 'title' => 'Runtime Error', 'labels' => 'Issues']);
 }`
## Environment Variables

add this two Environment Variables in you .env file

`GITLAB_PROJECT_ID`

`GITLAB_TOKEN`


## Contributing

Contributions are always welcome!

if you have suggestion create PR on this repo.


## Authors

- [@amit_m13](https://twitter.com/amit_m13)
