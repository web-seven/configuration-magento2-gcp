# configuration-magento2-gcp
Crossplane Configuration for deploy and manage Magento 2 Architecture on Google Cloud Platform.
# Architecture
Configuration is based on generic recommended setup for Adobe Commerce and Magento Open Source instances.
According to (official documentation)[https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/reference-architecture.html?lang=en]
The Commerce Reference Architecture diagram represents the best practice approach to set up a scalable Commerce site.

The color of each element in the diagram indicates whether the element is part of Magento Open Source or Adobe Commerce and if it is required.

- Orange elements are required for Magento Open Source
- Grey elements are optional for Magento Open Source
- Blue elements are optional for Adobe Commerce

![Commerce reference architecture diagram](https://github.com/web-seven/configuration-magento2-gcp/blob/main/design/ref-architecture-2.3.png?raw=true)

The following sections provide recommendations and considerations for each section of the Commerce Reference Architecture diagram.

## Varnish
- A Varnish cluster can scale to the traffic of a site
- Tune the instance size based on the number of cache pages needed
- On a high-traffic site, use a Varnish Master to ensure on-cache flush one request (at most) per web tier
## Web
- Enable scale of nodes for traffic and redundancy
- One node is master and runs cron
- Alternatively, use a dedicated Admin and worker nodes
## Cache
- Consider implementing a separate Redis instance for sessions
- You can have a Redis instance per cache
- Size your instance to contain the largest expected cache size
## Database and queues
- High-traffic sites can tune DB performance with slave DBs and split DBs for orders/carts (in Adobe Commerce)
- Consider using a slave DB to enable quick recovery and for data backups
- Low-traffic sites can store images in the DB
## Search
- Tune the number of instances based on search traffic
## Storage
- Consider using GFS or GlusterFS for pub/media storage
- Alternatively, use DB storage for low-traffic sites
