как начать писать проект используя smarty и svelte
Чтобы начать писать проект, используя Smarty и Svelte, можно следовать следующим шагам:

Установка и настройка проекта:

Создайте новый проект и установите необходимые зависимости:

bash
mkdir my-project
cd my-project
composer require smarty/smarty
npx degit sveltejs/template svelte-app
cd svelte-app
npm install
Настройка Smarty:

Создайте папку для шаблонов Smarty (например, templates) и настройте основную конфигурацию:

php
// index.php
require 'vendor/autoload.php';

$smarty = new Smarty();
$smarty->setTemplateDir('templates');
$smarty->setCompileDir('templates_c');
$smarty->setCacheDir('cache');
$smarty->setConfigDir('configs');

// Пример данных для шаблона
$smarty->assign('title', 'Hello Svelte with Smarty');
$smarty->display('index.tpl');
Создание шаблона Smarty:

Создайте файл шаблона index.tpl для отображения данных и включения Svelte компонентов:

smarty
<!DOCTYPE html>
<html>
<head>
    <title>{$title}</title>
    <script defer src="svelte-app/public/build/bundle.js"></script>
</head>
<body>
    <div id="svelte-app"></div>
</body>
</html>
Разработка Svelte компонентов:

Создайте компонент App.svelte в папке svelte-app/src:

svelte
<script>
  import { onMount } from "svelte";

  let message = "Loading...";

  onMount(async () => {
    const response = await fetch("/api/message");
    const data = await response.json();
    message = data.message;
  });
</script>

<main>
  <h1>{message}</h1>
</main>
Создание API для взаимодействия:

Разработайте API на PHP, которое будет возвращать данные для Svelte компонента:

php
// api/message.php
header('Content-Type: application/json');
$data = ['message' => 'Hello from PHP API!'];
echo json_encode($data);
Настройка маршрутизации и сервера:

Настройте ваш сервер для отдачи сгенерированных страниц и обработки запросов к API. Например, используя Apache, настройте .htaccess для переадресации запросов:

plaintext
RewriteEngine On
RewriteRule ^api/(.*)$ api/$1 [QSA,L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php [L]
Теперь у вас есть проект, который использует мощные возможности шаблонизации Smarty на серверной стороне и современные компоненты пользовательского интерфейса на основе Svelte на клиентской стороне. Если у вас возникнут вопросы или нужна помощь с каким-то этапом, дайте знать!

