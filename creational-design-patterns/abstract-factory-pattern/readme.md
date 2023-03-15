# 1.Abstract Factory Pattern (Soyut Fabrika Deseni)

Nesne yaratımı (object creation) için kullanılan bir tasarım desenidir. Bu desen, bir nesne ailesi (object family) içindeki nesnelerin oluşturulmasını kolaylaştırmak için kullanılır. Bu nesneler, belirli bir arayüzü (interface) uygular ve aynı soydan (inheritance) gelir.

Abstract Factory Pattern, uygulamanın somut nesnelerle bağlantısını azaltır ve nesnelerin oluşturulması için soyut bir fabrika sınıfı (abstract factory class) sağlar. Bu soyut fabrika sınıfı, farklı somut nesne aileleri için farklı alt sınıflara (subclasses) sahip olabilir. Uygulama, hangi somut fabrikanın kullanılacağına karar verir ve bu fabrika üzerinden nesneleri oluşturur.

Örneğin, bir mobilya üreticisi için, farklı stillerde sandalye, masa ve dolap üretebilen soyut bir fabrika sınıfı oluşturulabilir. Bu soyut fabrika sınıfından türetilen alt sınıflar, İskandinav, Modern ve Klasik mobilyaları temsil edebilir.

PHP'de Abstract Factory Pattern kullanımına örnek olarak, bir web uygulamasında farklı veritabanlarına (MySQL, PostgreSQL, MongoDB) bağlanmak için soyut bir veritabanı fabrikası sınıfı oluşturabiliriz. Bu sınıftan türetilen alt sınıflar, belirli veritabanı türleri için özelleştirilebilir. Aşağıdaki kod örneği, PHP'de bir Abstract Factory Pattern kullanarak farklı veritabanlarına bağlanmak için soyut bir fabrika sınıfı göstermektedir:

## Kod

```php
interface DatabaseFactory {
  public function createConnection();
  public function createQuery();
}

class MySQLFactory implements DatabaseFactory {
  public function createConnection() {
    return new MySQLConnection();
  }

  public function createQuery() {
    return new MySQLQuery();
  }
}

class PostgreSQLFactory implements DatabaseFactory {
  public function createConnection() {
    return new PostgreSQLConnection();
  }

  public function createQuery() {
    return new PostgreSQLQuery();
  }
}

interface Connection {
  public function connect();
}

class MySQLConnection implements Connection {
  public function connect() {
    echo "MySQL connection established.";
  }
}

class PostgreSQLConnection implements Connection {
  public function connect() {
    echo "PostgreSQL connection established.";
  }
}

interface Query {
  public function execute();
}

class MySQLQuery implements Query {
  public function execute() {
    echo "MySQL query executed.";
  }
}

class PostgreSQLQuery implements Query {
  public function execute() {
    echo "PostgreSQL query executed.";
  }
}

// Usage
$factory = new MySQLFactory();
$connection = $factory->createConnection();
$connection->connect();
$query = $factory->createQuery();
$query->execute();
```

Bu kod örneğinde, DatabaseFactory arayüzü, soyut fabrika sınıfını temsil eder ve createConnection ve createQuery yöntemlerini içerir. MySQLFactory ve `PostgreSQLFactory` sınıfları, bu arayüzü uygular ve MySQL ve PostgreSQL veritabanlarını kullanmak için özelleştirilmişConnectionveQuery` sınıflarını oluşturur.

Connection arayüzü, connect yöntemini içerir ve bu yöntemi uygulayan MySQLConnection ve PostgreSQLConnection sınıfları, ilgili veritabanına bağlanmak için kullanılır.

Query arayüzü, execute yöntemini içerir ve bu yöntemi uygulayan MySQLQuery ve PostgreSQLQuery sınıfları, ilgili veritabanında sorguları çalıştırmak için kullanılır.

Son olarak, MySQLFactory sınıfı örneğinde kullanıldığı gibi, bir somut fabrika nesnesi oluşturulabilir ve bu nesne üzerinden ilgili veritabanına bağlanmak için Connection ve Query nesneleri oluşturulabilir.

Bu şekilde, uygulama farklı veritabanı türleri arasında geçiş yaparken, sadece farklı bir fabrika sınıfı kullanarak nesneleri özelleştirebilir ve uygulamanın geri kalan kısmı için değişiklik yapmaya gerek kalmaz.
