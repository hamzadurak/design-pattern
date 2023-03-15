# 1.Adapter Pattern (Adaptör Deseni)

Mevcut bir sınıfın arayüzünü değiştirmeden, başka bir arayüze uyacak şekilde uyarlama yapmak için kullanılan bir tasarım desenidir. Bu sayede farklı arayüzlere sahip nesnelerin birbiriyle etkileşimleri sağlanabilir.

Örneğin, bir uygulama mevcut bir veri kaynağına bağlı olabilir ve bu veri kaynağından veri almak için belirli bir arayüz kullanabilir. Fakat daha sonra bu veri kaynağı değişirse, uygulama uyumluluğu korumak için yeni arayüzü kullanmalıdır. Adapter Pattern, bu senaryoda yeni veri kaynağını eski arayüze uyacak şekilde uyarlama işlemini yapar.

## Kod

```php
// Adaptör arayüzü
interface DatabaseAdapter {
  public function connect($host, $username, $password, $database);
  public function query($query);
}

// Mevcut veri kaynağı sınıfı
class MySQLDatabase {
  public function connectToDatabase($hostname, $username, $password, $databaseName) {
    // bağlantı kodları
  }

  public function runQuery($sql) {
    // sorgu çalıştırma kodları
  }
}

// Adaptör sınıfı
class MySQLAdapter implements DatabaseAdapter {
  private $mysql;

  public function __construct(MySQLDatabase $mysql) {
    $this->mysql = $mysql;
  }

  public function connect($host, $username, $password, $database) {
    $this->mysql->connectToDatabase($host, $username, $password, $database);
  }

  public function query($query) {
    $this->mysql->runQuery($query);
  }
}

// Kullanım
$mysql = new MySQLDatabase();
$adapter = new MySQLAdapter($mysql);
$adapter->connect('localhost', 'root', '', 'my_database');
$adapter->query('SELECT * FROM users');
```

Yukarıdaki örnekte, MySQLDatabase sınıfı mevcut veri kaynağıdır ve DatabaseAdapter arayüzüne uymaz. MySQLAdapter sınıfı ise MySQLDatabase sınıfını adaptör arayüzüne uydurur. Bu sayede uygulama, MySQLDatabase sınıfını kullanmak yerine MySQLAdapter sınıfını kullanarak veri kaynağına erişebilir.
