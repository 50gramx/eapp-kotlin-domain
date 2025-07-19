# EAPP Kotlin Domain ☕

[![Kotlin Version](https://img.shields.io/badge/kotlin-1.8+-purple.svg)](https://kotlinlang.org/)
[![Java Version](https://img.shields.io/badge/java-11+-orange.svg)](https://adoptium.net/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Build Status](https://img.shields.io/github/actions/workflow/status/50gramx/eapp-kotlin-domain/protobuf-distribution.yml)](https://github.com/50gramx/eapp-kotlin-domain/actions)
[![Maven Central](https://img.shields.io/maven-central/v/com.ethosverse/eapp-kotlin-domain.svg)](https://search.maven.org/artifact/com.ethosverse/eapp-kotlin-domain)

> **Kotlin/Java client library for EAPP (Ethos Apps Platform)** - Auto-generated protobuf client code for seamless Kotlin and Java integration with EAPP services.

## 📋 Table of Contents

- [Overview](#-overview)
- [🚀 Quick Start](#-quick-start)
- [📦 Installation](#-installation)
- [🔧 Usage](#-usage)
- [📚 API Reference](#-api-reference)
- [🔄 Auto-Generation](#-auto-generation)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

## 🌟 Overview

EAPP Kotlin Domain provides **auto-generated Kotlin/Java client code** for all EAPP system contracts. This package is automatically generated from Protocol Buffer definitions and provides type-safe, efficient access to EAPP services from Kotlin and Java applications.

### 🎯 Key Features

- **🔄 Auto-Generated** - Built from protobuf definitions in [eapp-system-contracts](https://github.com/50gramx/eapp-system-contracts)
- **📦 Type-Safe** - Full Kotlin type safety with null safety
- **⚡ High Performance** - Optimized protobuf serialization
- **🔄 Coroutines Support** - Modern Kotlin coroutines for async operations
- **🔒 Production Ready** - Used in production EAPP services
- **📚 Comprehensive** - Covers all EAPP service contracts
- **☕ Java Compatible** - Full Java interoperability

### 🏗️ Service Coverage

| Service Category | Description | Available |
|------------------|-------------|-----------|
| **🔐 Identity** | User authentication & authorization | ✅ |
| **💬 Communication** | Messaging & notifications | ✅ |
| **🧠 Cognitive** | AI & knowledge management | ✅ |
| **🛍️ Commerce** | Transactions & payments | ✅ |
| **🌌 Multiverse** | Space & universe management | ✅ |

## 🚀 Quick Start

### 1. Installation

#### Gradle (Kotlin DSL)
```kotlin
// build.gradle.kts
dependencies {
    implementation("com.ethosverse:eapp-kotlin-domain:0.1.0")
    implementation("io.grpc:grpc-kotlin-stub:1.3.0")
    implementation("io.grpc:grpc-protobuf:1.53.0")
}
```

#### Gradle (Groovy)
```groovy
// build.gradle
dependencies {
    implementation 'com.ethosverse:eapp-kotlin-domain:0.1.0'
    implementation 'io.grpc:grpc-kotlin-stub:1.3.0'
    implementation 'io.grpc:grpc-protobuf:1.53.0'
}
```

#### Maven
```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.ethosverse</groupId>
    <artifactId>eapp-kotlin-domain</artifactId>
    <version>0.1.0</version>
</dependency>
```

### 2. Basic Usage

```kotlin
import com.ethosverse.eapp.domain.User
import com.ethosverse.eapp.domain.Account
import com.ethosverse.eapp.domain.UserStatus
import com.ethosverse.eapp.domain.AccountStatus

fun main() {
    // Create a user
    val user = User.newBuilder()
        .setId("user123")
        .setName("John Doe")
        .setEmail("john@example.com")
        .setStatus(UserStatus.ACTIVE)
        .build()

    // Create an account
    val account = Account.newBuilder()
        .setId("acc123")
        .setUserId(user.id)
        .setStatus(AccountStatus.ACTIVE)
        .build()

    println("User: ${user.name} (${user.email})")
    println("Account: ${account.id} - Status: ${account.status}")
}
```

### 3. Service Integration

```kotlin
import io.grpc.ManagedChannelBuilder
import com.ethosverse.eapp.domain.AccountServiceGrpcKt
import com.ethosverse.eapp.domain.CreateAccountRequest

suspend fun createAccount() {
    val channel = ManagedChannelBuilder
        .forAddress("localhost", 50051)
        .usePlaintext()
        .build()

    val stub = AccountServiceGrpcKt.AccountServiceCoroutineStub(channel)

    val request = CreateAccountRequest.newBuilder()
        .setUserId("user123")
        .setAccountType(AccountType.PERSONAL)
        .build()

    try {
        val response = stub.createAccount(request)
        println("Created account: ${response.account.id}")
    } catch (e: Exception) {
        println("Error: $e")
    } finally {
        channel.shutdown()
    }
}
```

## 📦 Installation

### Requirements

- **Kotlin**: 1.8.0+
- **Java**: 11+
- **Dependencies**: 
  - `protobuf-java: ^3.21.12`
  - `grpc-kotlin-stub: ^1.3.0`
  - `grpc-protobuf: ^1.53.0`

### Installation Methods

#### 1. Maven Central (Recommended)
```kotlin
// build.gradle.kts
repositories {
    mavenCentral()
}

dependencies {
    implementation("com.ethosverse:eapp-kotlin-domain:0.1.0")
}
```

#### 2. From GitHub Releases
```kotlin
// build.gradle.kts
repositories {
    maven {
        url = uri("https://github.com/50gramx/eapp-kotlin-domain/releases/download/v0.1.0/")
    }
}

dependencies {
    implementation("com.ethosverse:eapp-kotlin-domain:0.1.0")
}
```

#### 3. Local Development
```bash
git clone https://github.com/50gramx/eapp-kotlin-domain.git
cd eapp-kotlin-domain
./gradlew build
```

## 🔧 Usage

### Importing Classes

```kotlin
// Core entities
import com.ethosverse.eapp.domain.User
import com.ethosverse.eapp.domain.Account
import com.ethosverse.eapp.domain.Space

// Service stubs
import com.ethosverse.eapp.domain.AccountServiceGrpcKt
import com.ethosverse.eapp.domain.UserServiceGrpcKt
import com.ethosverse.eapp.domain.SpaceServiceGrpcKt
```

### Working with Messages

```kotlin
import com.ethosverse.eapp.domain.User
import com.ethosverse.eapp.domain.UserStatus

// Create messages
val user = User.newBuilder()
    .setId("user123")
    .setName("John Doe")
    .setEmail("john@example.com")
    .setStatus(UserStatus.ACTIVE)
    .build()

// Serialize to bytes
val userBytes = user.toByteArray()

// Deserialize from bytes
val userFromBytes = User.parseFrom(userBytes)

// Convert to/from JSON
val userJson = JsonFormat.printer().print(user)
val userFromJson = User.newBuilder().also { 
    JsonFormat.parser().merge(userJson, it) 
}.build()
```

### gRPC Service Calls

```kotlin
import io.grpc.ManagedChannelBuilder
import com.ethosverse.eapp.domain.AccountServiceGrpcKt
import com.ethosverse.eapp.domain.GetUserAccountsRequest

suspend fun getUserAccounts(userId: String): List<Account> {
    val channel = ManagedChannelBuilder
        .forAddress("localhost", 50051)
        .usePlaintext()
        .build()

    val stub = AccountServiceGrpcKt.AccountServiceCoroutineStub(channel)

    return try {
        val request = GetUserAccountsRequest.newBuilder()
            .setUserId(userId)
            .build()
        
        val response = stub.getUserAccounts(request)
        response.accountsList
    } finally {
        channel.shutdown()
    }
}
```

### Spring Boot Integration

```kotlin
import org.springframework.stereotype.Service
import org.springframework.web.bind.annotation.*
import io.grpc.ManagedChannelBuilder
import com.ethosverse.eapp.domain.*

@Service
class UserService {
    private val channel = ManagedChannelBuilder
        .forAddress("localhost", 50051)
        .usePlaintext()
        .build()
    
    private val userStub = UserServiceGrpcKt.UserServiceCoroutineStub(channel)

    suspend fun createUser(request: CreateUserRequest): User {
        return userStub.createUser(request)
    }

    suspend fun getUser(id: String): User {
        val request = GetUserRequest.newBuilder()
            .setId(id)
            .build()
        return userStub.getUser(request)
    }
}

@RestController
@RequestMapping("/users")
class UserController(private val userService: UserService) {
    
    @PostMapping
    suspend fun createUser(@RequestBody request: CreateUserRequest): User {
        return userService.createUser(request)
    }

    @GetMapping("/{id}")
    suspend fun getUser(@PathVariable id: String): User {
        return userService.getUser(id)
    }
}
```

### Java Interoperability

```java
import com.ethosverse.eapp.domain.User;
import com.ethosverse.eapp.domain.UserStatus;

public class UserService {
    public User createUser(String name, String email) {
        return User.newBuilder()
            .setId(generateId())
            .setName(name)
            .setEmail(email)
            .setStatus(UserStatus.ACTIVE)
            .build();
    }
}
```

## 📚 API Reference

### Core Entities

#### User
```kotlin
val user = User.newBuilder()
    .setId("string")           // Unique user identifier
    .setName("string")         // Display name
    .setEmail("string")        // Email address
    .setStatus(UserStatus.ACTIVE)  // User status
    .setCreatedAt(timestamp)   // Creation timestamp
    .setUpdatedAt(timestamp)   // Last update timestamp
    .build()
```

#### Account
```kotlin
val account = Account.newBuilder()
    .setId("string")           // Unique account identifier
    .setUserId("string")       // Associated user ID
    .setType(AccountType.PERSONAL)  // Account type
    .setStatus(AccountStatus.ACTIVE) // Account status
    .setCreatedAt(timestamp)   // Creation timestamp
    .build()
```

#### Space
```kotlin
val space = Space.newBuilder()
    .setId("string")           // Unique space identifier
    .setName("string")         // Space name
    .setDescription("string")  // Space description
    .setOwnerId("string")      // Owner user ID
    .setType(SpaceType.PUBLIC) // Space type
    .setCreatedAt(timestamp)   // Creation timestamp
    .build()
```

### Service Stubs

#### AccountServiceCoroutineStub
```kotlin
val stub = AccountServiceGrpcKt.AccountServiceCoroutineStub(channel)

// Available methods:
// - createAccount(request)
// - getAccount(request)
// - updateAccount(request)
// - deleteAccount(request)
// - getUserAccounts(request)
```

#### UserServiceCoroutineStub
```kotlin
val stub = UserServiceGrpcKt.UserServiceCoroutineStub(channel)

// Available methods:
// - createUser(request)
// - getUser(request)
// - updateUser(request)
// - deleteUser(request)
// - listUsers(request)
```

## 🔄 Auto-Generation

This package is **automatically generated** from protobuf definitions in the [eapp-system-contracts](https://github.com/50gramx/eapp-system-contracts) repository.

### Generation Process

1. **Protobuf Changes** - Updates to `.proto` files in system-contracts
2. **CI/CD Trigger** - GitHub Actions workflow automatically triggers
3. **Code Generation** - `protoc` generates Java code from `.proto` files
4. **Package Building** - Creates JAR package with generated code
5. **Release Creation** - Creates GitHub release with new version
6. **Index Update** - Updates package index with new release

### Versioning

- **Auto-generated versions** - Based on timestamp: `0.1.0.{timestamp}`
- **Release frequency** - On every protobuf change
- **Backward compatibility** - Maintained within major versions

## 🤝 Contributing

### For Kotlin-Specific Changes

1. **Fork** the repository
2. **Create** a feature branch
3. **Make** your changes
4. **Test** thoroughly
5. **Submit** a pull request

### For Protobuf Changes

1. **Update** protobuf definitions in [eapp-system-contracts](https://github.com/50gramx/eapp-system-contracts)
2. **Push** to trigger auto-generation
3. **Review** generated Kotlin/Java code
4. **Test** with your changes

### Development Setup

```bash
# Clone repository
git clone https://github.com/50gramx/eapp-kotlin-domain.git
cd eapp-kotlin-domain

# Build project
./gradlew build

# Run tests
./gradlew test

# Run linting
./gradlew ktlintCheck
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🔗 Quick Links

- **📦 Maven Central**: [eapp-kotlin-domain](https://search.maven.org/artifact/com.ethosverse/eapp-kotlin-domain)
- **🏗️ System Contracts**: [eapp-system-contracts](https://github.com/50gramx/eapp-system-contracts)
- **🐛 Issues**: [GitHub Issues](https://github.com/50gramx/eapp-kotlin-domain/issues)
- **📖 Documentation**: [API Docs](https://github.com/50gramx/eapp-kotlin-domain/wiki)
- **💬 Discussions**: [GitHub Discussions](https://github.com/50gramx/eapp-kotlin-domain/discussions)

---

<div align="center">
  <p><strong>Auto-generated Kotlin/Java client for EAPP System Contracts</strong></p>
  <p><em>Built with ❤️ by the EAPP Team</em></p>
</div>
