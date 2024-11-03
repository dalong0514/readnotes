## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

### 0601. 行动卡——

行动卡是能够指导自己的行动的卡。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是在这个专栏的整个地图里，这一章节所在的节点。

### 2. 摘录及评论

## 0000Getting-Started.md

### 03. Installation

Use composer to install PhpSpreadsheet into your project:

```
composer require phpoffice/phpspreadsheet
```

Or also download the documentation and samples if you plan to use them:

```
composer require phpoffice/phpspreadsheet --prefer-source
```

### 04. Hello World

This would be the simplest way to write a spreadsheet:

```
<?php

require 'vendor/autoload.php';

use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;

$spreadsheet = new Spreadsheet();
$sheet = $spreadsheet->getActiveSheet();
$sheet->setCellValue('A1', 'Hello World !');

$writer = new Xlsx($spreadsheet);
$writer->save('hello world.xlsx');
```

1『

laravel 的入口文件（public/index.php）里设置自动加载。

```
/*
|--------------------------------------------------------------------------
| Register The Auto Loader
|--------------------------------------------------------------------------
|
| Composer provides a convenient, automatically generated class loader for
| our application. We just need to utilize it! We'll simply require it
| into the script here so that we don't have to worry about manual
| loading any of our classes later on. It feels great to relax.
|
*/

require __DIR__.'/../vendor/autoload.php';
```

接着直接在控制器里写：

```php
    public function test()
    {
        $spreadsheet = new Spreadsheet();
        $sheet = $spreadsheet->getActiveSheet();
        $sheet->setCellValue('A1', 'Hello World !');
        
        $writer = new Xlsx($spreadsheet);
        dd($writer);
        $writer->save('hello.xlsx');
    }
```

public 文件夹下会自动生成 hello.xlsx 文件。

』



