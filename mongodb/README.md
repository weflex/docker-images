MongoDB
=======

To build MongoDB containers for Weflex apps, we use the official [mongo][1] repository as the base image.

## Configuration

> **Note:** When deploying the docker instance, please use the same .env file to set MONGODB_ROOT_USERNAME and MONGODB_ROOT_PASSWORD as the Primary server

1. To setup mongodb instance we use the following [docker-compose.yml][2] file.

2. For production server setup, we create three docker instances on each of our servers.

| Instance        | Address     |
|:----------------|:------------|
| **Primary**     | 192.168.1.3 |
| **Secondary**   | 192.168.1.4 |
| **Arbiter**     | 192.168.1.7 |

3. The above instances are then setup in replication mode with the below priority levels and the replSetName "rs0".

| Instance        | Address     | Priority |
|:----------------|:------------|:--------:|
| **Primary**     | 192.168.1.3 | 1        |
| **Secondary**   | 192.168.1.4 | 0        |
| **Arbiter**     | 192.168.1.7 | 0.5      |

## Usage

- When connecting through the [gateway-v2][3] app, the datasources.json file must include the reference to all the MongoDB instances as specified in MongoDB [docs][4].

[1]: https://hub.docker.com/_/mongo/
[2]: https://github.com/weflex/docker-images/blob/master/mongodb/docker-compose.yml
[3]: https://github.com/weflex/gateway-v2
[4]: https://docs.mongodb.com/manual/reference/connection-string/#standard-connection-string-format
