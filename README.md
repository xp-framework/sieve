Sieve protocol support for the XP Framework
========================================================================

Usage example ([)listing all available scripts):

```php
use peer\sieve\SieveClient;
use util\cmd\Command;

$s= new SieveClient('imap.example.com');
$s->connect();

$s->authenticate(SIEVE_SASL_PLAIN, 'user', 'password');
Console::writeLine($s->getScripts());

$s->close();
```

Usage example (uploading a script from a local file);

```php
use peer\sieve\SieveClient;
use peer\sieve\SieveScript;
use io\File;
use io\FileUtil;

$s= new SieveClient('imap.example.com');
$s->connect();
$s->authenticate(SIEVE_SASL_PLAIN, 'user', 'password');

with ($script= new SieveScript('myscript')); {
  $script->setCode(FileUtil::getContents(new File('myscript.txt')));
  $s->putScript($script);
}

$s->close();
```
