php-upload
==========

Class PHP upload file.

## Installation / Usage
-----------------

1. Download the [`composer.phar`](https://getcomposer.org/composer.phar) executable or use the installer.

    ``` sh
    $ curl -sS https://getcomposer.org/installer | php
    ```
    
2. Create a composer.json defining your dependencies. Note that this example is
a short version for applications that are not meant to be published as packages
themselves. To create libraries/packages please read the
[documentation](http://getcomposer.org/doc/02-libraries.md).

    ``` json
    {
        "repositories": [
     	    {"type": "git", "url": "https://github.com/hashbr-Oficial/php-upload"}
        ], 
        "require": {  
            "hashbr-Oficial/php-upload": "dev-master"
        }
    }
    ```
3. Run Composer: `php composer.phar install`
4. Browse for more packages on [Packagist](https://packagist.org).

## Updating Composer
-----------------

Running `php composer.phar self-update` or equivalent will update a phar
install with the latest version.

## Installation from Source
------------------------

1. Run `git clone https://github.com/offboard/php-upload.git /var/www/your-project/libs/`
3. Include the class in your project file: `include('./Lib/Upload.php');`


## Simple Example
-----------------
```php
include("../autoload.php");

$upload = new Upload('img');
$upload
        ->file_name('uploaded')
        ->upload_to('upload/')
        ->run();

if (!$upload->was_uploaded) {
    die("Error : {$upload->error}");
} else {
    echo 'image sent successfully !';
}
```

## Example random name 
-----------------
```php
include("../autoload.php");

$upload = new Upload('img');
$upload
        ->file_name(true)
        ->upload_to('upload/')
        ->run();

if (!$upload->was_uploaded) {
    die("Error : {$upload->error}");
} else {
    echo 'image sent successfully !';
}
```

## Example maximum allowed size
-----------------
```php
include("../autoload.php");

$upload = new Upload('img');
$upload
        ->file_name('uploaded')
        ->upload_to('upload/')
        ->file_max_size(1000000 * 4) // 1000000 bytes = 1 MB
        ->run();

if (!$upload->was_uploaded) {
    die("Error : {$upload->error}");
} else {
    echo 'image sent successfully !';
}
```

## Example disable mime checker
-----------------
```php
include("../autoload.php");

$upload = new Upload('img');
$upload
        ->file_name('uploaded')
        ->upload_to('upload/')
        ->mime_check(false)
        ->run();

if (!$upload->was_uploaded) {
    die("Error : {$upload->error}");
} else {
    echo 'image sent successfully !';
}
```

## Example resize image
-----------------
```php
include("../autoload.php");

$upload = new Upload('img');
$upload
        ->file_name('resized')
        ->upload_to('upload/')
        ->resize_to(150, 150, 'exact') // resize exact to 150x150 pixels
        ->run();

if (!$upload->was_uploaded) {
    die("Error : {$upload->error}");
} else {
    echo 'image sent successfully !';
}
```

## Example custom mime checker
-----------------
```php
include("../autoload.php");

$upload = new Upload('img');
// only imagens
$upload->MIME_allowed = array(
    "image/jpeg",
    "image/pjpeg",
    "image/bmp",
    "image/gif",
    "image/png",
);
$upload
        ->file_name('resized')
        ->upload_to('upload/')
        ->resize_to(480, 380, "maxwidth") // resize exact to 150x150 pixels
        ->run();

if (!$upload->was_uploaded) {
    die("Error : {$upload->error}");
} else {
    echo 'image sent successfully !';
}
```

## Example multiple upload
-----------------
```php
include("../autoload.php");

$file = $_FILES['img'];
if (empty($file['tmp_name'][0])) {
    die("No images");
}
foreach ($file["tmp_name"] as $k => $v) {
    $upload = new Upload(array(
      'name' => $file['name'][$k],
      'type' => $file['type'][$k],
       'tmp_name' => $file['tmp_name'][$k],
       'error' => $file['error'][$k],
       'size' => $file['size'][$k]
    ), false);
    $upload
            ->file_name(true)
            ->upload_to('document/')
            ->run();
    if (!$upload->was_uploaded) {
       die("Error image {$i} : {$upload->error}");
    } 
    echo "image {$i} sent successfully !";
}
```
