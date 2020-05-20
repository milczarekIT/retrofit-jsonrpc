# retrofit-jsonrpc

JSON-RPC with Retrofit.

# Usage

Declare your RPC Service.

```java
interface MultiplicationService {
    @JsonRPC("Arith.Multiply") @POST("/rpc")
    Call<Integer> multiply(@Body MultiplicationArgs args);
}
```

Register the `JsonRPCConverterFactory` while building your `Retrofit` instance.
This must be done before any other converters are applied.

```java
Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("http://localhost:1234")
        .addConverterFactory(JsonRPCConverterFactory.create())
        .addConverterFactory(MoshiConverterFactory.create())
        .build();
```

Use Retrofit to build your service.

```java
MultiplicationService service = retrofit.create(MultiplicationService.class);
```

Use your service.

```java
service.multiply(MultiplicationArgs.create(2, 3)).execute().body(); // -> 6
```

# Add jsonrpc to your project


Maven:
- Add Jitpack repository
```xml
<repositories>
	<repository>
	    <id>jitpack.io</id>
	    <url>https://jitpack.io</url>
	</repository>
</repositories>
```

- Add the dependency
```xml
<dependency>
    <groupId>com.github.milczarekIT.retrofit-jsonrpc</groupId>
    <artifactId>jsonrpc</artifactId>
    <version>1.0.0</version>
</dependency>
```

or Gradle:

- Add Jitpack repository
```groovy
allprojects {
	repositories {
		maven { url 'https://jitpack.io' }
	}
}
```

- Add the dependency
```groovy
dependencies {
    implementation 'com.github.milczarekIT.retrofit-jsonrpc:jsonrpc:1.0.0'
}
```
