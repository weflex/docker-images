Elasticsearch
======

At Weflex, we use Elasticsearch to monitor and visualize the logs and also for full text search functionality to our apps.

The [Dockerfile][1] is used to create the weflex/elasticsearch image which is then commit and pushed to our private [docker-hub][2] registry.

### Version
We are using elasticsearch version **6.2.4**

[1]: https://github.com/weflex/docker-images/blob/master/elasticsearch/Dockerfile.yml
[2]: https://docker-v2.theweflex.com
