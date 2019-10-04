# chrome-proxy-extensions
Proxy Extension in chromeDriver for this connected  and scrape a website.

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

Open chrome://extensions/ in Chrome  and enable "Developer mode", click "Pack Extension" and choose the proxy directory.

Chrome generate file.crx and file.pem

### For Use extension in ChromeDriver

Read ChromeDriver documentation -> https://chromedriver.chromium.org/extensions

### For PHP librairy

Use symfony/panther -> https://github.com/symfony/panther

/!\ ChromeManager does not accepted add extension, so we must duplicate

\Symfony\Component\Panther\Client
```php
public static function createChromeClient(?string $chromeDriverBinary = null, ?array $arguments = null, array $options = [], ?string $baseUri = null): self
{
  // use your ChromeManager
  return new self(new ChromeManager($chromeDriverBinary, $arguments, $options), $baseUri);
}
```

\Symfony\Component\Panther\ProcessManager\ChromeManager

```php
<?php 
// ChromeManager before l.56 add
$chromeOptions->addExtensions(array(
  "_path_/proxy.crx",
));
```

## Credits

Created by [Matthieu Beurel](https://www.mbeurel.com). Sponsored by [Nexboard](https://www.nexboard.fr).