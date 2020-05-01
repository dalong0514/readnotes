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

## 0101. Lifecycle

### 01. Introduction

When using a package in your application, it's good to understand how the package functions behind the scenes. Understanding the behind-the-scenes will make you feel more comfortable and confident using the maximum potential of the tool. The goal of this page is to give you a high-level overview of how Laravel Excel works.

### 02. Exports Lifecycle Overview

This section will try to give you an overview of how the export works behind the scenes.

#### 2.1 Export Object

Everything starts with the Export object. This object encapsulates your entire export logic. It both configures and handles the export logic. A simple example of an export object is:

```php
<?php

namespace App\Exports;

use App\User;
use Maatwebsite\Excel\Concerns\FromCollection;

class UsersExport implements FromCollection
{
    public function collection()
    {
        return User::all();
    }
}
```

If you want to read more about export objects, go to the architecture page of export objects.

#### 2.2 Passing on the Export object

Next the Export object will be passed on to the Laravel Excel package. The main entry point for this is the Maatwebsite/Excel/Excel class. This class can be called in multiple ways.

#### 2.2.1 Facade

The easiest way to work with the Excel class is to use the Maatwebsite\Excel\Facades\Excel facade. If you use auto-discovery, you can use the alias \Excel directly instead of using the fully qualified namespace.

[Package Development - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/packages#package-discovery)

#### 2.2.2 Dependency injection

You can inject the Maatwebsite/Excel/Excel manager class into your class, either via constructor injection or method injection in case of a controller.

```php
<?php
use App\Exports\UsersExport;
use Maatwebsite\Excel\Excel;

class ExportController
{
    private $excel;

    public function __construct(Excel $excel)
    {
        $this->excel = $excel;
    }
    
    public function exportViaConstructorInjection()
    {
        return $this->excel->download(new UsersExport, 'users.xlsx');
    }
    
    public function exportViaMethodInjection(Excel $excel)
    {
        return $excel->download(new UsersExport, 'users.xlsx');
    }
}
```

1『获取 excel 对象的 2 个方式。』

#### 2.2.3 Contract

You can also use the Maatwebsite\Excel\Exporter interface to decouple more from the concrete Excel manager implementation. The contract offers the same methods as the Excel class. It will make it easier to e.g. stub out the Exporter in your unit tests. The Exporter contract can be either injected via the constructor or a method in a controller.

```php
use App\Exports\UsersExport;
use Maatwebsite\Excel\Exporter;

class ExportsController
{
    private $exporter;

    public function __construct(Exporter $exporter)
    {
        $this->exporter = $exporter;
    }
    
    public function export()
    {
        return $this->exporter->download(new UsersExport, 'users.xlsx');
    }
}
```

#### 2.2.4 Container binding

If you want to bind the Maatwebsite\Excel\Excel manager to your own class via a container binding, you can use the excel container binding.

```php
$this->app->bind(YourCustomExporter::class, function() {
    return new YourCustomExporter($this->app['excel']);
});
```

#### 2.2.5 Exportable trait

If you prefer a sprinkle of magic, you can use the Maatwebsite\Excel\Concerns\Exportable trait in your Export object. This trait will expose a couple of methods that will make it possible to directly export an Export object.

```php
namespace App\Exports;

use App\User;
use Maatwebsite\Excel\Concerns\FromCollection;
use Maatwebsite\Excel\Concerns\Exportable;

class UsersExport implements FromCollection
{
    use Exportable;

    public function collection()
    {
        return User::all();
    }
}
```

You can now download the export without the need for the facade or Excel manager.

```php
return (new UsersExport)->download('users.xlsx');
```

Read more about the exportable trait in the exportables docs.

#### 2.3 Handling the Export object

#### 2.3.1 Writer type detection

After using one of the above methods to pass on the Export object to the Excel manager, it will try to figure out what export it needs to be generated to. This will be either based on the extension of the file, the explicitly passed writer type. You can find the extension to writer type mapping in the excel.php config, in the extension\_detector section. In case no writer type can be detected, a Maatwebsite\Excel\Exceptions\NoTypeDetectedException exception is thrown and the export process will be stopped.

#### 2.3.2 Starting the Writing process

The Excel manager will then delegate the handling to the Maatwebsite\Excel\Writer. The first action of the Writer is to register the event listeners that are registered. Next it will create a new PhpOffice\PhpSpreadsheet\Spreadsheet instance that we will use to convert our Export object to.

The first event that is raised, is the BeforeExport event. This is raised just after the Spreadsheet instance is created and allows early access to it.

#### 2.3.3 Multiple sheets

Next the Writer will determine if multiple sheets are configured, by checking for the Maatwebsite\Excel\Concerns\WithMultipleSheets concern. Then it will delegate the further handling of each sheet to the Maatwebsite\Excel\Sheet class.

#### 2.3.4 Processing the sheets

In the Sheet class, the most heavy lifting happens. It first will create a PhpOffice\PhpSpreadsheet\Worksheet\Worksheet instance. Then it will raise the BeforeSheet event which allows you to hook into the moment just before the sheet handling starts.

Then it will determine what kind of export we are dealing with: FromQuery, FromArray, FromCollection or FromView. Based on that it will start the connected export process.

1. FromView will pass on the rendered Blade view to PhpSpreadsheet's Html Reader. That Reader will turn the table html into Excel cells. It also handles some inline styles (color and background color) and col/rowspans.

2. The Query passed with the FromQuery will automatically be chunked and each chunk will be appended to the Sheet. The chunking is done to limit the amount of Eloquent object it needs to keep in memory. It greatly reduces memory usage.

3. The entire array of Collection will directly be appended to the Sheet.

When the Sheet starts appending records, it will first call the map() method if the WithMapping concern is used. This allows the Export object to format the data before it is inserted. Then it will handling column formatting (WithColumnFormatting concern) and cell autosizing (ShouldAutoSize). To close off the Sheet processing, it will raise a AfterSheet event.

#### 2.3 Passing on to PhpSpreadsheet

After the sheets are processed, the writing process will start. The writing process is started by raising the BeforeWriting event; this allow you to hook into the process of writing. Next we will create a new PhpSpreadsheet Writer based on the writer type that was determined. Then it will save it to a temporary file and return that filepath to the Excel manager.

#### 2.4 Creating a Response

The Excel manager basically has 2 types of responses, it either starts the download process or it will store the file to disk.

#### 2.4.1 Download the file

We will take the temporary file that was returned by the Writer and use Laravel's ResponseFactory to create a Symfony\Component\HttpFoundation\BinaryFileResponse. When returning this response in your controller, it will start a download.

#### 2.4.2 Storing the file

The storing of the file will be handled by Laravel's Filesystem. By default the file will be stored on your default disk, but you can also pass a custom disk via the Excel::store() method.

### 03. Imports Lifecycle Overview

This section will try to give you an overview of how the import works behind the scenes.

#### 3.1 Import Object

Everything starts with the Import object. This object encapsulates your entire import logic. It both configures and handles the import logic. A simple example of an import object is:

```
namespace App\Imports;

use App\User;
use Illuminate\Support\Collection;
use Maatwebsite\Excel\Concerns\ToCollection;

class UsersImport implements ToCollection
{
    public function collection(Collection $rows)
    {
        foreach ($rows as $row) 
        {
            User::create([
                'name' => $row[0],
            ]);
        }
    }
}
```

If you want to read more about imports objects, go to the architecture page of imports objects.

#### 3.2 Passing on the Import object

Next the Import object will be passed on to the Laravel Excel package. The main entry point for this is the Maatwebsite/Excel/Excel class. This class can be called in the same way as outlined in the Export lifecycle.

#### 3.2.1 Contract

You can also use the Maatwebsite\Excel\Importer interface to decouple more from the concrete Excel manager implementation. The contract offers the same methods as the Excel class. It will make it easier to e.g. stub out the Importer in your unit tests. The Importer contract can be either injected via the constructor or the method of a controller.

```php
use App\Imports\UsersImport;
use Maatwebsite\Excel\Importer;

class ImportsController
{
    private $importer;

    public function __construct(Importer $importer)
    {
        $this->importer = $importer;
    }
    
    public function export()
    {
        return $this->importer->import(new UsersImport, 'users.xlsx');
    }
}
```

#### 3.2.2 Importable trait

If you prefer a sprinkle of magic, you can use the Maatwebsite\Excel\Concerns\Importable trait in your Import object. This trait will expose a couple of methods that will make it possible to directly import an Import object.

```
namespace App\Imports;

use App\User;
use Maatwebsite\Excel\Concerns\ToCollection;
use Maatwebsite\Excel\Concerns\Importable;

class UsersImport implements ToCollection
{
    use Importable;

    ...
}
```

You can now import without the need for the facade or Excel manager.

```php
(new UsersImport)->import('users.xlsx');
```

Read more about the importable trait in the importables docs.

[Importables | Laravel Excel](https://docs.laravel-excel.com/3.1/imports/importables.html)

#### 3.3 Handling the Import object

#### 3.3.1 Reader type detection

After using one of the above methods to pass on the Import object to the Excel manager, it will try to figure out what reader type it is . This will be either based on the extension of the file or the explicitly passed reader type. You can find the extension to reader type mapping in the excel.php config, in the extension_detector section. In case no reader type can be detected, a Maatwebsite\Excel\Exceptions\NoTypeDetectedException exception is thrown and the import process will be stopped.

#### 3.3.2 Starting the Reading process

The Excel manager will then delegate the handling to the Maatwebsite\Excel\Reader. The first action of the Reader is to register the event listeners that are registered. It will copy the file from Laravel's Filesystem to the local filesystem, so PhpSpreadsheet can read it. Next it will create a PhpSpreadsheet Reader based on the reader type that was given and load the file into a PhpOffice\PhpSpreadsheet\Spreadsheet instance.

Next it will create a new PhpOffice\PhpSpreadsheet\Spreadsheet instance that we will use to read our Import object from. The first event that is raised, is the BeforeImport event. This is raised just after the Spreadsheet instance is loaded and allows early access to it.

#### 3.3.3 Multiple sheets

Next we will determine if we are dealing with multiple sheets. This is done based on the WithMultipleSheets concern.

#### 3.3.4 Processing the sheets

Then each Sheet gets processed. This process gets started off by raising the BeforeSheet event. Then it will either import it to a Collection, an array or handle each row as an Eloquent model.

1. When using ToModel, each returned model will be persisted via Eloquent. When using this in combination with WithBatchInserts, it will defer the persistence till the batch is complete and then insert them as one batch in the database.

2. When using ToCollection or ToArray, the entire dataset will be passed to the Import method and the user can determine itself how to use it.

The sheet handling is ended by raising the AfterSheet event.

## 0102. Import & Export Objects

The entire Laravel Excel philosophy evolves around having Export and/or Import objects.

### 01. Directory structure

The location of these Import and Exports classes could be as follows:

```
.
├── app
│   ├── Exports (Groups all exports in your app)
│   │   ├── UsersExport.php
│   │   ├── ProductsExport.php
│   │   └── Sheets (You can group sheets together)
│   │      ├── InactiveUsersSheet.php
│   │      └── ActiveUsersSheet.php
|   |
│   ├── Imports (Groups all imports in your app)
│   │   ├── UsersImport.php
│   │   ├── ProductsImport.php
│   │   └── Sheets (You can group sheets together)
│   │      ├── OutOfStockProductsSheet.php
│   │      └── ProductsOnSaleSheet.php
│ 
└── composer.json
```

### 02. Encapsulation

These objects encapsulate the entire export or import process. The idea behind it is that you can neatly use these objects in controllers, services, jobs, event listeners or commands. In all of theses cases, the entire logic of how the export/import needs to happen is kept within this object.

### 03. Data transfer object

The import/export objects are in essence simple data transfer objects (DTO). This means they will transfer the information you want to export/import to the Excel writer/reader. This information is not only the actual data you want to export, but also additional information like the styling of the file, the name of the worksheet, the number format of the cell etc.

In most cases, this means that your code doesn't need to have direct exposure to the actual read/write process.

### 04. Plain Old PHP Object

Besides being a DTO, the import/export objects are also just Plain Old PHP Objects (POPO). This means that you can do anything with them that you can do with normal PHP objects.

#### 4.1 Constructor

For instance, you can simply inject data through the constructor of the export object.

```php
class UsersExport implements FromCollection {
    private $year;

    public function __construct(int $year) 
    {
        $this->year = $year;
    }
    
    public function collection()
    {
        return Users::whereYear('created_at', $this->year)->get();
    }
}
Excel::download(new UsersExport(2019), 'users.xlsx');
```

#### 4.2 Setters

Another option is to add setters for data that you want to pass.

```php
class UsersExport implements FromCollection {
    private $year;

    public function setYear(int $year)
    {
        $this->year = $year;
    }
    
    public function collection()
    {
        return Users::whereYear('created_at', $this->year)->get();
    }
}
$export = new UsersExport();
$export->setYear(2019);

Excel::download($export, 'users.xlsx');
```

#### 4.3 Getters

In similar fashion to setters, you can also add getters. This can potentially be useful if you want to keep a state of your export/import. For instance, you can keep a row count in your users import.

```php
namespace App\Imports;

use App\User;
use Maatwebsite\Excel\Concerns\ToModel;

class UsersImport implements ToModel
{
    private $rows = 0;

    public function model(array $row)
    {
        ++$this->rows;
    
        return new User([
            'name' => $row[0],
        ]);
    }
    
    public function getRowCount(): int
    {
        return $this->rows;
    }
}
```

After doing the import, we can request the state with the getter.

```php
$import = new UsersImport;
Excel::import($import, 'users.xlsx');

dd('Row count: ' . $import->getRowCount()); 
```

### 05. Concerns

Most of the export/import configuration is done by using Concerns. Concerns are basically just simple interfaces. Implementing them will make the object adhere to a certain contract. This contract can request specific methods that e.g. data can be passed through. In other cases it might not ask for any methods to be implemented, but merely functions as a pointer interface.

Read more about Concerns in the concerns documentation.

### 06. Hooks

In more complex cases you might want to hook into certain moments of the read/write process. This can be done by using Events. To register these events in your import/export object, you need to implement the Maatwebsite\Excel\Concerns\WithEvents concern.

```php
namespace App\Exports;

use Maatwebsite\Excel\Concerns\WithEvents;
use Maatwebsite\Excel\Events\BeforeExport;

class UsersExport implements WithEvents
{
    /**
     * @return array
     */
    public function registerEvents(): array
    {
        return [
            // Handle by a closure.
            BeforeExport::class => function(BeforeExport $event) {
                // Do something before the export process starts.
            },
        ];
    }
}
```

Alternatively, you can also configure these listeners globally if you want it to happen to any export.

```php
Writer::listen(BeforeExport::class, function () {
    // Do something before any export process starts.
});
```

## 0103. Concerns

Most of the export/import configuration is done by using Concerns.

### 01. Contracts

Concerns are basically just simple interfaces. Implementing them will make the object adhere to a certain contract. This contract can request specific methods that e.g. data can be passed through. For instance, the FromCollection requests the Export object to implement a collection method, that needs to return a Collection instance.

```php
namespace App\Exports;

use App\User;
use Maatwebsite\Excel\Concerns\FromCollection;

class UsersExport implements FromCollection
{
    public function collection()
    {
        return User::all();
    }
}
```

### 02. Pointer interface

In other cases it might not ask for any methods to be implemented, but merely functions as a pointer interface. For instance, the ShouldAutoSize concern doesn't pass on any specific information, but does tell the Export process that the columns need to be automatically sized.

```php
namespace App\Exports;

use App\User;
use Maatwebsite\Excel\Concerns\ShouldAutoSize;

class UsersExport implements ShouldAutoSize
{

}
```

## 0201. quick start

Create an export class in app/Exports. You may do this by using the make:export command.

    php artisan make:export UsersExport --model=User

The file can be found in app/Exports:

```
.
├── app
│   ├── Exports
│   │   ├── UsersExport.php
│ 
└── composer.json
```

If you prefer to create the export manually, you can create the following in app/Exports:

```php
<?php

namespace App\Exports;

use App\User;
use Maatwebsite\Excel\Concerns\FromCollection;

class UsersExport implements FromCollection
{
    public function collection()
    {
        return User::all();
    }
}
```

In your controller you can call this export now:

```php
<?php

namespace App\Http\Controllers;

use App\Exports\UsersExport;
use Maatwebsite\Excel\Facades\Excel;

class UsersController extends Controller 
{
    public function export() 
    {
        return Excel::download(new UsersExport, 'users.xlsx');
    }
}
```

And finally add a route to be able to access the export:

```php
Route::get('users/export/', 'UsersController@export');
```

## 0301. quick start

Create an import class in app/Imports. You may do this by using the make:import command.

    php artisan make:import UsersImport --model=User

The file can be found in app/Imports:

```
.
├── app
│   ├── Imports
│   │   ├── UsersImport.php
│ 
└── composer.json
```

If you prefer to create the import manually, you can create the following in app/Imports:

```php
<?php

namespace App\Imports;

use App\User;
use Illuminate\Support\Facades\Hash;
use Maatwebsite\Excel\Concerns\ToModel;

class UsersImport implements ToModel
{
    /**
     * @param array $row
     *
     * @return User|null
     */
    public function model(array $row)
    {
        return new User([
           'name'     => $row[0],
           'email'    => $row[1], 
           'password' => Hash::make($row[2]),
        ]);
    }
}
```

In your controller you can call this import now:

```php
use App\Imports\UsersImport;
use Maatwebsite\Excel\Facades\Excel;
use App\Http\Controllers\Controller;

class UsersController extends Controller 
{
    public function import() 
    {
        Excel::import(new UsersImport, 'users.xlsx');
        
        return redirect('/')->with('success', 'All good!');
    }
}
```

## 0302. Importing basics

If you have followed the 5 minute quick start, you'll already have a UsersImport class.

```php
<?php

namespace App\Imports;

use App\User;
use Illuminate\Support\Facades\Hash;
use Maatwebsite\Excel\Concerns\ToModel;

class UsersImport implements ToModel
{
    /**
     * @param array $row
     *
     * @return User|null
     */
    public function model(array $row)
    {
        return new User([
           'name'     => $row[0],
           'email'    => $row[1],
           'password' => Hash::make($row[2]),
        ]);
    }
}
```

### 2.1 Importing from default disk

Passing the UsersImport object to the Excel::import() method, will tell the package how to import the file that is passed as second parameter. The file is expected to be located in your default filesystem disk (see config/filesystems.php).

```php
Excel::import(new UsersImport, 'users.xlsx');
```

### 2.2 Importing from another disk

You can specify another disk with the third parameter like your Amazon s3 disk. (see config/filesystems.php)

```php
Excel::import(new UsersImport, 'users.xlsx', 's3');
```

### 2.3 Importing uploaded files

If you let your user upload the document, you can also just pass the uploaded file directly.

```php
Excel::import(new UsersImport, request()->file('your_file'));
```

1『直接读取上传的文件，这个正式自己最想要的，一定要实现。』

### 2. 4 Importing full path

If you want to specifiy the path where your file is, without having to move it to a disk, you can directly pass that file path to the import method.

```php
Excel::import(new UsersImport, storage_path('users.xlsx'));
```

### 2.5 Importing to array or collection

If you want to bypass the ToArray or ToCollection concerns and want to have an array of imported data in your controller (beware of performance!), you can use the ::toArray() or ::toCollection() method.

```php
$array = Excel::toArray(new UsersImport, 'users.xlsx');

$collection = Excel::toCollection(new UsersImport, 'users.xlsx');
```

1『这个知识点感觉可以跟「读取上传文件」结合起来一起用。』

### 2.6 Specifying a reader type

If the reader type is not detectable by the file extension, you can specify a reader type by passing it as fourth parameter.

```php
Excel::import(new UsersImport, 'users.xlsx', 's3', \Maatwebsite\Excel\Excel::XLSX);
```







