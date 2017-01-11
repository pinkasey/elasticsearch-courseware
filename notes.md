
## Elastic Search Nature ##
* new release every few months
* backward compatibility - sometimes breaks!
* Never seen it going down

## Cost ##
* Enterprise Support 5,000$ per node, minimum for production is 3 nodes - 15,000$ per year

## Plugins / Products
- X-PACK (Marvel) - monitors and shows health of system
- bigdesk - might be better than X-PACK
- There is a plugin that cleans up old indexes (Inquisitor or something)
- DataDog - for monitoring
- Loggly.io
- Curator - for data retention


## Installation
* automate it using pupet, ansible, shell, Terraform
* Clustering across multiple data centers - not supported. Use aws high availability regions
* install using Kitematic - UI for docker. Looks like fun.
* autoscale with docker, mesos or coreos. read about it. mayber others will do too.

## Mappings - usefull settings
* Multi field
* not-parsed

## Query
* analyzer is in charge of scoring result
* Filter - reduce results
* boost keyword - give higher score to certain result

## Performance
* queries with wildcards or regexes - cost performance. Other than that - no known expensive pattern.
* use filters as much as possible
* If you don't need scoring - don't use query at all
* specify fields you want in response
* linux's nmon to monitor CPU, network, etc, in real time.
* disable memory swap
* more replicas - faster reads. But slower writes.
* learn performance from Loggly.com - they use elastic search with very big volumes.

## Pit falls
* new data is **not available right away** - it is indexed in a different process, only then available
* serial-number field should not be 'text' - should be data-type 'keyword'
* mapping response cannot be used to insert mapping - 2 first levels of json should be dropped, and url should include index+type
* CPU usage - use filters to reduce the result-set, then the query applies and calculates score for each result that match both query and filter
* Pagination - scoring is done each time - order might change! You might get the same record twice, or skip records.
* Kibana - chrome extention that dumps data only dumps what is shown on the screen
* Number of replicas - when your cluster has more nodes than replicas, **it forbids new documents from being added**
* **use aliases instead of indices**. This way you can do reindex an index, and when you're done - just update the alias. 

##Extra
* https://www.shodan.io/search?query=elasticsearch+%27You+Know%2C+for+Search%27
* http://nmap.org
