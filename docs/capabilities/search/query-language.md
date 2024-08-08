# Search API Schema

Our Search API takes advantage of our custom Query Langauge to enable powerful searches against our dataset.

Our query language is designed to be simple to use but powerful, comprising a set of `filters` with `comparators`



## Basic Schema Layout

A blank schema looks like the following:

```json
{
    "query": {
        "filters": []
    }
}
```

This structure is a blank query. It is the basis of every query made to the Search API.

## Building a query

### Filters

To start to filter the data, we add Filter Objects to the `query.filters` array. The array, then combines to create the guidelines for Search API to go and search our dataset with.

The Filter Object looks like the following:

```json
{
    "field": "hpdb.signal.cowrie.eventid",
    "comparator": "eq",
    "value": "cowrie.session.connect"
}
```

#### `field`

`field` describes the place in our logs where you want to search. These take the form of a dot (`.`) delimited path, from the root of the document to the key you want to search on. 

In the example we want to filter on the field `hpdb.signal.cowrie.eventid`. The Search API will interpret that and search for a log with the following structure:

```json
{
    "hpdb": {
        "signal": {
            "cowrie": {
                "eventid": "cowrie.session.connect"
                ...
            },
            ...
        },
        ...
    },
    ...
}
```

Please, check our dedicated Signal Schemas to identify all the fields availiable to search on.

#### `value`

`value` is the information which represents what you are looking for in the signals. How this value is applied is controlled by the `comparator` key.

#### `comparator`

This field tells the Search API how to apply the `value` to the `field` when searching logs.

| Supported Value | Effect                                                                                                                                         |
| :-------------: | ---------------------------------------------------------------------------------------------------------------------------------------------- |
|      `eq`       | Will look for an exact match with the given `value`.                                                                                           |
|      `neq`      | Will look for anything other than the given `value`.                                                                                           |
|   `includes`    | Will perform a full-text search to look for the partial `value`.                                                                               |
|   `excludes`    | Will perform a full-text search to look for values not included `value`.                                                                       |
|     `cidr`      | Indicates that the `value` is a IP address or IP Address range. Will try to match exactly, or return for IPs which are within the given range. |

## Filters - Advanced

Sometimes, we need to do more advanced searches with our filters. By default any Filter Objects put in the `query.filters` array will only return Signals which match ALL of the filter objects. To do this, we have included two additional blocks.


### AND

```json
{
    "and": []
}
```

The AND block is put in the `query.filters` array, and contains one key: `and`. The `and` key is an array of ONLY Filter Objects. This block ensures that all filters put in the array match for a Signal to be returned.


__You CANNOT nest this block.__


### OR

```json
{
    "or": []
}
```

The OR block is put in the `query.filters` array, and contains one key: `or`. The `or` key is an array of ONLY Filter Objects. This block ensures that at least one of the filters put in the array match for a Signal to be returned.


__You CANNOT nest this block.__


## The Datetime Window

Sometimes, we only care about Signals in a specific time window. To do this, we can use the `query.datetime` object.

```json
{
    "query": {
        "datetime": {
            "gte": "2024-06-20T14:17:13.260570+00:00",
            "lt": "2024-06-21T14:17:13.260570+00:00"
        },
        "filters": []
    }
}
```

The `query.datetime` is a JSON object which describes a datetime range in which to match logs. It contains exactly 1 of `gt` or `gte` to serve as the lower bound of the range, and exactly one of `lt` or `lte` to serve as the upper bound in the range.

|  Key  | Description                                                           |
| :---: | --------------------------------------------------------------------- |
| `gt`  | Any matching Signals must have originated AFTER this datetime.        |
| `gte` | Any matching Signals must have originated AT or AFTER this datetime.  |
| `lt`  | Any matching Signals must have originated BEFORE this datetime.       |
| `lte` | Any matching Signals must have originated AT or BEFORE this datetime. |

This object can be left blank or ommitted entirely. Search API will search ALL availiable data in that instance.

## Non-Functional Keys

There is one non-functional key in this schema. That is the `name` key, which exists at the same level as the `query` key. This allows a developer to describe their query for internal documentation. Search API ignores this key.

__Non-Functional keys may recieve functionality during the HPDB BETA period. Please check the update Blog Posts to be notified of any non-functional key receiving functionality.__ 