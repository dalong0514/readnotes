## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。找一个他的 TED 演讲，有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是在这个专栏的整个地图里，这一章节所在的节点。

### 2. 摘录及评论

## 0000. get started

使用 3.1 版本的，laravel 用 6.0 以及 php 7.1 以上。

### 01. Introduction

Laravel Excel is intended at being Laravel-flavoured PhpSpreadsheet: a simple, but elegant wrapper around PhpSpreadsheet with the goal of simplifying exports and imports. PhpSpreadsheet is a library written in pure PHP and providing a set of classes that allow you to read from and to write to different spreadsheet file formats, like Excel and LibreOffice Calc.

Laravel Excel Features: 1) Easily export collections to Excel. 2) Export queries with automatic chunking for better performance. 3) Queue exports for better performance. 4) Easily export Blade views to Excel. 5) Easily import to collections. 6) Read the Excel file in chunks. 7) Handle the import inserts in batches.

### 02. Installation

Require this package in the composer.json of your Laravel project. This will download the package and PhpSpreadsheet.

    composer require maatwebsite/excel

The Maatwebsite\Excel\ExcelServiceProvider is auto-discovered and registered by default. If you want to register it yourself, add the ServiceProvider in config/app.php:

```php
'providers' => [
    /*
     * Package Service Providers...
     */
    Maatwebsite\Excel\ExcelServiceProvider::class,
]
```

The Excel facade is also auto-discovered. If you want to add it manually, add the Facade in config/app.php:

```php
'aliases' => [
    ...
    'Excel' => Maatwebsite\Excel\Facades\Excel::class,
]
```

To publish the config, run the vendor publish command:

    php artisan vendor:publish --provider="Maatwebsite\Excel\ExcelServiceProvider"

This will create a new config file named config/excel.php.


