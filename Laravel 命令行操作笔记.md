# Laravel 命令行操作笔记

## 控制器

- 生成控制器

  ``` powershell
  php artisan make:controller System\LoginController
  ```

  生成一个控制器，生成的控制器位于 app\Http\Controllers

## 创建中间件

- 生成中间件

  ``` powershell
  php artisan make:middleware LoginMiddleware
  ```

- 注册中间件

  中间件在文件 app\Http\Kernel.php 里进行注册

  - 全局中间件

    注册在全局有效

    ``` php
    protected $middleware = [
    		//全局有效的中间件
    	];
    ```

  - 分配到路由的中间件

    ``` php
    protected $routeMiddleware = [
            //路由中间件
        ];
    ```

  - 成组分配的中间件组

    为一组中间件分配一个 key 再通过 key 调用

    ``` php
    protected $middlewareGroups = [
            'web' => [
                //分配到web组
            ],
            'api' => [
                //分配到api组
            ],
        ];
    ```

## 数据库

- 生成数据库模型的同时生成迁移文件

  ``` powershell
  php artisan make:model User -m
  ```

  生成 model 加 -m 标记，同时生成数据库迁移文件

- 执行数据库迁移

  ``` powershell
  php artisan migrate
  ```


## 清除缓存

1. 清除应用程序缓存

   ``` powershell
   php artisan cache:clear
   ```

2. 清除路由缓存

   ``` powershell
   php artisan route:cache
   ```

3. 清除配置缓存

   ``` powershell
   php artisan config:cache
   ```

4. 清除视图文件缓存

   ``` powershell
   php artisan view:clear
   ```

