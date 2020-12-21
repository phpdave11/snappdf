<p align="center">
    <img src="https://raw.githubusercontent.com/beganovich/snappdf/master/cover.png" alt="snappdf logo">
</p>

# snappdf
This is a simple library that lets you convert webpages or HTML into the PDF file using Chromium or Google Chrome.

## Usage:

Here's quick example, how it works:

```php
$snappdf = new \Beganovich\Snappdf\Snappdf();

$pdf = $snappdf
    ->setHtml('<h1>Hello world!</h1>')
    ->generate();

file_put_contents('my-awesome.pdf', $pdf);
```

In case you want to convert web page into the PDF, you can use `setUrl()` instead of `setHtml()`:

```php
$snappdf = new \Beganovich\Snappdf\Snappdf();

$pdf = $snappdf
    ->setUrl('https://github.com')
    ->generate();

file_put_contents('my-awesome.pdf', $pdf);
```

.. if you need specific version of Chrome, or don't want to use locally downloaded Chromium, make use of `setChromiumPath` method.

```php
$snappdf = new \Beganovich\Snappdf\Snappdf();

$pdf = $snappdf
    ->setUrl('https://github.com')
    ->setChromiumPath('/path/to/your/chrome')
    ->generate();
```

If none of previously listed option fits your needs, you can also set path to executable Chromium with environment variable.
```bash
SNAPPDF_EXECUTABLE_PATH=/path/to/your/chrome
```

Note: `setChromiumPath` has highest priority. Second one is environment variable & third local download.
### Possible runtime exceptions:
**Symfony\Component\Process\Exception\ProcessFailedException**
- When generating PDF was unsuccessful.
  
**Beganovich\Snappdf\Exception\BinaryNotFound**:
- When no locally downloaded binary was found & setChromiumPath() isn't called.

**Beganovich\Snappdf\Exception\MissingContent**
- When no `setHtml` nor `setUrl` was called.

## Requirements
- PHP 7.3+

## Supported platforms
Package has been tested & developed for **Linux**.

For Windows or Mac you have to use `setChromiumPath()` to provide executable variable path.

## Installation
Composer is recommended way of installing library:

```bash
composer require beganovich/snappdf
```

### Downloading local Chromium
snappdf can download & use local revision of Chromium. To achieve that, you can use:

```bash
./vendor/bin/snappdf download
```

You can find local downloads/revisions in `%projectRoot%/vendor/beganovich/snappdf/versions`.

Local revision will be used **only** when you don't provide path using `setChromiumPath()`.

**Note:** snappdf will download & use latest build of Chromium. Since Chromium itself doesn't have stable or unstable release, browser itself can be buggy or possibly broken. We don't take any responsibility for that. **If security & stability is your top priority, please install Google Chrome stable version & point package to use that.** 

### Comparison to Browsershot:
In case you need much more complex software to perform operations with headless browser go for [Spatie's Browsershot](https://github.com/spatie/browsershot). It's fantastic package.
Purpose of snappdf is to be really minimal & only focus on making PDFs.

Also, snappdf doesn't need Node installed to operate.
## Credits
- [David Bomba](https://github.com/turbo124)
- [Benjamin Beganović](https://github.com/beganovich)
- [All contributors](https://github.com/beganovich/chromium-pdf/contributors)

## Licence
The MIT License (MIT).
