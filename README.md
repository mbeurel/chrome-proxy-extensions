# chrome-proxy-extensions
Proxy Extension in chromeDriver for this connected and scrape a website.

## Documentation

### Configuration

Edit file 'proxy/background.js' :

```
  var config = {
    ...
    singleProxy: {
      scheme: "http",
      host: 	"IP",		// Proxy IP or URL: type -> string
      port: 	80		// Proxy port : type -> int
    },
    ...
    authCredentials: {
      username: "username",
      password: "password"
    },
    ...
  }
```

### Generate CRX

Open chrome://extensions/ in Chrome  and enable "Developer mode", click "Pack Extension" and choose your proxy directory.

Chrome generate file.crx and file.pem

### For Use extension in ChromeDriver

Read ChromeDriver documentation -> https://chromedriver.chromium.org/extensions

_/!\ Chrome error if you add --headless in client attribute_

### For PHP library

Use symfony/panther -> https://github.com/symfony/panther

_/!\ Chrome Manager does not accept extension's add, so we must duplicate_

\Symfony\Component\Panther\Client
```php
// use your ChromeManager

public static function createChromeClient(?string $chromeDriverBinary = null, ?array $arguments = null, array $options = [], array $extensions = [], ?string $baseUri = null): self
{
  return new self(new ChromeManager($chromeDriverBinary, $arguments, $options, $extensions), $baseUri);
}
```

\Symfony\Component\Panther\ProcessManager\ChromeManager

```php
<?php

private $extensions;

public function __construct(?string $chromeDriverBinary = null, ?array $arguments = null, array $options = [], array $extensions = [])
{
  //...
  $this->extensions = $extensions;
}
//...
public function start(): WebDriver
{
  //...
  $chromeOptions = new ChromeOptions();
  $chromeOptions->addArguments($this->arguments);
  if($this->extensions)
  {
    $chromeOptions->addExtensions($this->extensions);
  }
  $capabilities->setCapability(ChromeOptions::CAPABILITY, $chromeOptions);
  //...
}
```

Create a new ChromeClient

```php
<?php
 
$client = Client::createChromeClient(null, array('--window-size=1980,1080', '--disable-gpu'), array(), array("_path_/proxy.crx"));
```

## Credits

Created by [Matthieu Beurel](https://www.mbeurel.com). Sponsored by [Nexboard](https://www.nexboard.fr).
