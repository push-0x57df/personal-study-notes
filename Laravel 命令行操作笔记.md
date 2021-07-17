# Laravel 命令行操作笔记

## 控制器

- 生成控制器

  ``` powershell
  php artisan make:controller System\LoginController
  ```

  生成一个控制器，生成的控制器位于 app\Http\Controllers

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

  

