# IP Geolocation REST API

![travis-ci](https://travis-ci.org/observabilitystack/geoip-api.svg?branch=master)
![docker-pulls](https://img.shields.io/docker/pulls/observabilitystack/geoip-api)

This project provides a simple web service which returns geolocation information for a given IP address.

The service loads location information from Maxmind's GeoIP2 City (commercial) or
[GeoLite2](https://dev.maxmind.com/geoip/geoip2/geolite2/) database; and ISP information from Maxmind's GeoIP2 ISP
database.

The database files are not included in this project. The location of the files can be specified using environment
variables:

| Variable | Description | Default value |
| -------- | ----------- | ------------- |
| CITY_DB_FILE | The location of the GeoIP2 City or GeoLite2 database file. | `/srv/GeoLite2-City.mmdb` |
| ISP_DB_FILE | The location of the GeoIP2 ISP database file. | (none) |

At least one of the database files must be provided.

## Building the project

Build the Java application by running

    ./mvnw clean verify
    
No create the Docker image:

    docker build -t s24/geoip-api .

## Running the container

    docker run -p 8080:8080 -v /path/to/GeoLite2-City.mmdb:/srv/GeoLite2-City.mmdb s24/geoip-api

## Using the API

When the container is running, you can query it via simple HTTP GET requests:

    curl http://localhost:8080/8.8.8.8
    {
        "country":"US",
        "latitude":"37.751",
        "longitude":"-97.822"
    }



## Contributing

We're looking forward to your comments, issues and pull requests!

## License

This project is licensed under the [Apache License, Version 2](http://www.apache.org/licenses/LICENSE-2.0.html).
