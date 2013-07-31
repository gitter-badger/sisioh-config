sisioh-config
=============

sisioh-config is scala wrapper for typesafe [config](https://github.com/typesafehub/config).

## usage

### read raw value

conf/application.conf

``` 
foo.bar1 = value1
foo.bar2 = value2
foo.bar3 = 1
```

```scala
val config = Configuration.load(new File("conf"))
val Some(bar1) = config.getStringValue("foo.bar1") // value1
val Some(bar2) = config.getStringValue("foo.bar2") // value2
val Some(bar3) = config.getIntValue("foo.bar3") // 1
```

### read ConfigurationValue

conf/application.conf

``` 
foo.bar1 = value1
foo.bar2 = value2
foo.bar3 = 1
```

```scala
val config = Configuration.load(new File("conf"))
val Some(bar1ConfigValue) = config.getConfigurationValue("foo.bar1")
val Some(bar1) = bar1ConfigValue.valueAsString // value1
// ...
```

### read Configuration

conf/application.conf

```
foo.bar1 = value1
foo.bar2 = value2
foo.bar3 = 1
```

```scala
val config = Configuration.load(new File("conf"))
val Some(foo) = config.getConfiguration("foo")
val Some(bar1) = foo.getStringValue("bar1") // value1
val Some(bar2) = foo.getStringValue("bar2") // value2
val Some(bar3) = foo.getIntValue("bar3") // 1
```

### read ConfigurationObject

conf/application.conf

```
db = { driverClassName: com.mysql.jdbc.Driver, url: jdbc:mysql://localhost/test }
```

```scala
val config = Configuration.load(new File("conf"))
val Some(dbConfigObject) = config.getConfigurationObject("db")
val Some(driverClassName) = dbConfigObject.get("driverClassName") // com.mysql.jdbc.Driver
val Some(url) = dbConfigObject.get("url") // jdbc:mysql://localhost/test
```

