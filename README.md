# embedded-postgresql-maven-plugin
[![Build status](https://travis-ci.org/slavaz/embedded-postgresql-maven-plugin.svg?branch=master)](https://travis-ci.org/slavaz/embedded-postgresql-maven-plugin/)

## Description

Embedded PostgreSQL Maven Plugin provides a platform neutral way for running postgres server in integration tests.
This plugin  is based on [Embedded PostgreSQL Server library](https://github.com/yandex-qatools/postgresql-embedded)

## Configuration

### pgServerVersion

The plugin currently supports next PostgreSQL versions: 9.3.15, 9.4.10, 9.5.5, 9.6.1

You also may use aliases:
* 9.3 -> 9.3.15
* 9.4 -> 9.4.10
* 9.5 -> 9.5.5
* 9.6 -> 9.6.1
* latest -> 9.6

### pgDatabaseDir

Where server files will be plased. Default {project.build.directory}/pgdata

### pgPort

Port for listening incoming connections.

### pgLocale

Locale for embedded PostgreSQL server. Leave empty for running the server with system locale.
Specify "no" to skip locale & charset definition.

### pgCharset

Charset for embedded PostgreSQL server. Leave empty for running the server with system charset.
Specify "no" to skip locale & charset definition.

### dbName

Database name. Will be created

### userName

User name. Will be created

### password

User password for newly created user

## Usage example

Starts PostgreSQL server, creates a database and a user with specified password

    ...
    <build>
        ..
        <plugins>
          <plugin>
            <groupId>com.github.slavaz</groupId>
            <artifactId>embedded-postgresql-maven-plugin</artifactId>
            <configuration>
              <pgServerVersion>9.5</pgServerVersion>
              <pgServerPort>15432</pgServerPort>
              <dbName>testdb</dbName>
              <userName>testuser</userName>
              <password>userpass</password>
            </configuration>
            <executions>
              <execution>
                <id>start-pgsql</id>
                <phase>pre-integration-test</phase>
                <goals>
                  <goal>start</goal>
                </goals>
              </execution>
              <execution>
                <id>stop-pgsql</id>
                <phase>post-integration-test</phase>
                <goals>
                  <goal>stop</goal>
                </goals>
              </execution>
            </executions>
          </plugin>
        </plugins>
    </build>

## Goals
                  
1. `start` -- start the server
2. `stop` -- stop the server
