<!--suppress HtmlDeprecatedAttribute -->
<h1 align="center">
  🐘🎯 Arquitectura Hexagonal, DDD & TDD en Symfony
</h1>

![Screenshot](/bg/hexagon.jpg)<br>

<p align="center">
   Ejemplo de <strong>Symfony aplicación uando Domain-Driven Design (DDD) i <br /> 
   Test Driver Development (TDD) principios</strong> manteniendi el código lo más simple posible
  <br />
  <br />
</p>

## 🚀 Environment Setup

This project is made with [Symfony][1] 7.

### 🐳 Needed tools

1. PHP 8.1 or higher;
2. Composer
3. PDO-MySQL PHP extension enabled;
4. and the [usual Symfony application requirements][2].
5. NodeJS v14.*.
6. Clone this project: `git clone git@github.com:david-berruezo/php-symfony-arquitectura-hexagonal.git`
7. Move to the project folder: `cd php-symfony-arquitectura-hexagonal`

### 🛠️ Environment configuration

1. Create a local environment file (`cp .env .env.local`) if you want to modify any parameter

### 🔥 Application execution

1. Install the backend dependencies: `composer install`.
3. Create database & tables with `php bin/console d:d:c` then `php bin/console make:migration`
   and `php bin/console migration:migrate` or force with `php bin/console d:s:u -f`
5. Install the fronted dependencies: `yarn install` or `npm install`.
6. For the development purpose, run `yarn watch` or `npm run watch`. For the production version, run `yarn build`
   or `npm run build`.
7. Start the server with Symfony: `symfony serve`.
   Then access the application in your browser at the given URL ([https://localhost:8000](https://localhost:8000) by
   default).
   If you don't have the Symfony binary installed, run `php -S localhost:8000 -t public/`
   to use the built-in PHP web server or [configure a web server][3] like
   Apache to run the application.

### ✅ Tests execution

1. Install the dependencies if you haven't done it previously: `composer install`
2. Execute PHPUnit tests: `php bin/phpunit --configuration phpunit.xml.dist`

### 🎯 Hexagonal Architecture

This repository follows the Hexagonal Architecture pattern. Also, it's structured using `modules`.
With this, we can see that the current structure of a Bounded Context is:

```scala
$ tree -L 5 src
    
src
├── Application // The application layer of our app
│   └── Post // Inside the application layer all is structured by actions
│       └── Create
│           ├── CreatePostCommand.php
│           └── CreatePostUseCase.php
├── Domain // The domain layer of our app
│   └── Post
│       ├── Post.php // The Aggregate of the Module
│       └── Repository
│           └── PostRepositoryInterface.php // The `Interface` of the repository is inside Domain
├── Infrastructure // The layer infrastructure of our app
│   ├── Controller
│   └── Persistence
│       ├── Doctrine
│       │   └── Post
│       │       ├── PostDoctrineParser.php
│       │       ├── PostDoctrineRepository.php // An implementation of the repository
│       │       └── Post.php
│       ├── InFile
│       │   ├── FilesystemHandler.php
│       │   └── Post
│       │       ├── InFilePostParser.php
│       │       └── InFilePostRepository.php
│       └── InMemory
│           └── Post
│               └── InMemoryPostRepository.php
└── Kernel.php
```