# How-to-debug-php-in-docker-container
How to debug php in docker container

STEP1 : Create php.ini in same directory with dockerfile
```
[xdebug]
xdebug.mode = debug
xdebug.start_with_request = yes
xdebug.client_host = host.docker.internal
```

STEP2: Install xdebug in docker file and copy php.ini to docker
```
RUN pecl install xdebug-3.1.5
RUN docker-php-ext-enable xdebug
COPY ./php.ini /usr/local/etc/php/
```

STEP3: Install php debug
```
https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug
```

STEP4: Create launch.json in .vscode folder
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}"
            }
        }
    ]
}
```

STEP5: Test xdebug
```
<?php
echo xdebug_info();
?>
```

STEP6: Add break point and start php debug extension
