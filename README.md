<!-- Basic Coding Standard -->

基本編碼規範
=====================

本章節在於訂定標準編碼元件以確保共享PHP code之間高等技術的互用性

"MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" 
這些關鍵字在這份文件的意思等同於 [RFC 2119][] 裡的描述.

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md


1. 概要
-----------

- 檔案 MUST 使用 `<?php` 和 `<?=` 標籤.

- PHP 檔案 MUST 只能使用 UTF-8 without BOM.

- 檔案 SHOULD *either* 聲明符號 (classes, functions, constants, etc.) *or* 產生副作用
  (e.g. generate output, change .ini settings, etc.) but SHOULD NOT do both  

- 命名空間 和 類別 MUST 遵循 [PSR-0][].

- 類別名稱 MUST 宣告 `StudlyCaps`.

- 類別常量 MUST 宣告為全大寫並用底線區分

- 方法名稱 MUST 宣告 `camelCase`.


2. 檔案
--------

### 2.1. PHP 標籤

PHP code MUST 使用 long `<?php ?>` 標籤或是 short-echo `<?= ?>` 標籤
MUST NOT 使用其他標籤變化.

### 2.2. 字元編碼

PHP code MUST 只能使用 UTF-8 without BOM.

### 2.3. 副作用

一個檔案 SHOULD 宣告新符號 (classes, functions, constants, etc.)
並不會引起其他副作用, 或者 SHOULD 執行副作用的邏輯, 但
SHOULD NOT 同時做.

副作用(side effects) 意指執行無直接關係的宣告類別, 函式, 
常數等, *僅僅是從包含的文件*.

副作用包含但不限於: 產生輸出, 清楚的使用 `require` or `include`, 連結外部服務, 
修改ini設定, 發出碩物或異常, 修改全局或靜態變量, 讀取或寫入檔案, 以此類推.


下面是同時宣告和副作用應該避免的範例

```php
<?php
// 副作用: 改變 ini 設定
ini_set('error_reporting', E_ALL);

// 副作用: 載入檔案
include "file.php";

// 副作用: 產生輸出
echo "<html>\n";

// 宣告
function foo()
{
    // function body
}
```

下面是應當效仿的沒有副作用的宣告檔案範例

```php
<?php
// 宣告
function foo()
{
    // function body
}

// 條件式宣告 *not* 副作用
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. 命名空間和類別名稱
----------------------------

命名空間和類別名稱 MUST 遵循 [PSR-0][].

意思是每個類別本身在一個檔案中, 並且是在一個命名空間裡, 至少在一個層面
是一個頂級供應者名稱.

類別名稱 MUST 宣告 `StudlyCaps`.

PHP 5.3 之後的代碼編寫 MUST 使用正規式命名空間

For example:

```php
<?php
// PHP 5.3 之後:
namespace Vendor\Model;

class Foo
{
}
```

5.2.x 之前的代碼編寫 SHOULD 使用 pseudo-namespacing convention 在類別名稱加上
前綴字 `Vendor_`.

```php
<?php
// PHP 5.2.x 之前:
class Vendor_Model_Foo
{
}
```

4. 類別 常量, 屬性, 方法
-------------------------------------------

類別是指所有的類別, 接口, 特性.

### 4.1. 常量

類別 常量 MUST 宣告為全大寫並用底線區分.

For example:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. 屬性

本指南有意避免任何關於使用 `$StudlyCaps`, `$camelCase`, 或 `$under_score` 屬性名稱的建議.

無論怎樣的命名協定 SHOULD 使用在合理的範圍, 該範圍可能是 供應商級, 封裝級, 類別級, 
方法級.

### 4.3. 方法

方法名稱 MUST 宣告 `camelCase()`.
