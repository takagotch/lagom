### lagom
---
https://github.com/lagom/lagom

https://www.lightbend.com/lagom-framework

```scala
// persistence-jdbc/core/src/test/scala/com/lightbend/lagom/internal/persistence/jdbc/SlickDbTestProvider.scala

object SlickDoTestProvider {

  private val JNDIName = "DefaultDS"
  private val JNDIDBName = "DefaultDB"
  
  private val AsyncExecConfig: AsyncExecutorConfig = new AsyncExecutorConfig {
    override val numThreads: Int = 20
    override val minConnections: Int = 20
    override val maxConnections: Int = 20
    override val queueSize: Int = 100
    override def registerMbeans: Boolean = false
  }
  
  def buildAndBindSlickDb(baseName: String, lifecycle: ApplicationLifecycle): Unit = {
    val dbName = s"${baseName}_${Random.alphanumeric.take(8).mkString}"
    val db = Databases.inMemory(dbName, config = Map("jndiName" -> JNDIName))
    lifecycle.addStopHook(() => Future.successful(db.shutdown()))
    
    SlickDbProvider.buildAndBindSlickDatabase(db, AsyncExecConfig, JNDIDBName, lifecycle)
  }
}
```

```java

```

```sh


```
