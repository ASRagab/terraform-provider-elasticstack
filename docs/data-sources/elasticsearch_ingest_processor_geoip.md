---
subcategory: "Ingest"
layout: ""
page_title: "Elasticstack: elasticstack_elasticsearch_ingest_processor_geoip Data Source"
description: |-
  Helper data source to create a processor which adds information about the geographical location of an IPv4 or IPv6 address.
---

# Data Source: elasticstack_elasticsearch_ingest_processor_geoip

The geoip processor adds information about the geographical location of an IPv4 or IPv6 address.

By default, the processor uses the GeoLite2 City, GeoLite2 Country, and GeoLite2 ASN GeoIP2 databases from MaxMind, shared under the CC BY-SA 4.0 license. Elasticsearch automatically downloads updates for these databases from the Elastic GeoIP endpoint: https://geoip.elastic.co/v1/database. To get download statistics for these updates, use the GeoIP stats API.

If your cluster can’t connect to the Elastic GeoIP endpoint or you want to manage your own updates, [see Manage your own GeoIP2 database updates](https://www.elastic.co/guide/en/elasticsearch/reference/current/geoip-processor.html#manage-geoip-database-updates).

If Elasticsearch can’t connect to the endpoint for 30 days all updated databases will become invalid. Elasticsearch will stop enriching documents with geoip data and will add tags: ["_geoip_expired_database"] field instead.


See: https://www.elastic.co/guide/en/elasticsearch/reference/current/geoip-processor.html


## Example Usage

```terraform
provider "elasticstack" {
  elasticsearch {}
}

data "elasticstack_elasticsearch_ingest_processor_geoip" "geoip" {
  field = "ip"
}

resource "elasticstack_elasticsearch_ingest_pipeline" "my_ingest_pipeline" {
  name = "geoip-ingest"

  processors = [
    data.elasticstack_elasticsearch_ingest_processor_geoip.geoip.json
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **field** (String) The field to get the ip address from for the geographical lookup.

### Optional

- **database_file** (String) The database filename referring to a database the module ships with (GeoLite2-City.mmdb, GeoLite2-Country.mmdb, or GeoLite2-ASN.mmdb) or a custom database in the `ingest-geoip` config directory.
- **first_only** (Boolean) If `true` only first found geoip data will be returned, even if field contains array.
- **ignore_missing** (Boolean) If `true` and `field` does not exist, the processor quietly exits without modifying the document.
- **properties** (Set of String) Controls what properties are added to the `target_field` based on the geoip lookup.
- **target_field** (String) The field that will hold the geographical information looked up from the MaxMind database.

### Read-Only

- **id** (String) Internal identifier of the resource
- **json** (String) JSON representation of this data source.