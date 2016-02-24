# resurfaceio-logger-java
&copy; 2016 Resurface Labs LLC, All Rights Reserved

This library makes it easy to log server usage including HTTP request/response details.

## Dependencies

No runtime dependencies to conflict with your app. Requires Java 8.

## Installing with Maven

Add these sections to your pom.xml:

    <dependencies>
        <dependency>
            <groupId>io.resurface</groupId>
            <artifactId>resurfaceio-logger</artifactId>
            <version>1.0.12-SNAPSHOT</version>
        </dependency>
    </dependencies>

    <repositories>
        <repository>
            <id>resurfaceio-mavenrepo</id>
            <url>https://github.com/resurfaceio/resurfaceio-mavenrepo/raw/master</url>
            <releases>
                <enabled>false</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>

## Java API

    import io.resurface.HttpLogger;
    import io.resurface.HttpLoggerFactory;
    
    HttpLogger logger = HttpLoggerFactory.get();     // returns default cached HTTP logger
    logger.logRequest(request);                      // log HTTP request details
    logger.logResponse(response);                    // log HTTP response details
    if (logger.isEnabled()) ...                      // intending to log stuff?
    logger.enable();                                 // enable logging for dev/staging/production
    logger.disable();                                // disable logging for automated tests

## Using with Spark Framework

### Logging requests and responses

    HttpLogger logger = HttpLoggerFactory.get();
    before((req, res) -> logger.logRequest(req.raw()));
    after((req, res) -> logger.logResponse(res.raw()));    

### Logging requests only

    before((req, res) -> HttpLoggerFactory.get().logRequest(req.raw()));

### Logging responses only

    after((req, res) -> HttpLoggerFactory.get().logResponse(res.raw()));    
