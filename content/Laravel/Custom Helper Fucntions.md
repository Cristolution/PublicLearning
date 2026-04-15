---
title: Untitled
draft: false
tags:
---

after adding using this command
```powershell
mkdir app/Helpers
```

then add to config.json to be globally visible
```json
    "autoload": {

        "psr-4": {

            "App\\": "app/",

            "Database\\Factories\\": "database/factories/",

            "Database\\Seeders\\": "database/seeders/"

        },

        "files": [

            "app/Helpers/SlugGenerator.php"

        ]

    }
```
and then 
```powershell
composer dump-autoload
```