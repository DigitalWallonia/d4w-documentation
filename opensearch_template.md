# Request parameters

a \* indicates that this parameter is mandatory so should be present but could be empty. For example `"clientSites": []` is a valid parameter

## ambition-search-template

Returns all `person` _weight 50_, `program` _weight 45_, `post` _weight 35_, `event` _weight 15_, `profile` _weight 10_ and `pressReview` _weight 5_ matching `fields.ambitions.fr.slug.${LANGUAGE}` slug
It will order the documents by `endDate lte now` _weight 30_ and `endDate lte now` _weight 1_

Parameters:
  * \*`query_string`: `<str>` The slug we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "ambition-search-template",
    "params": {
        "query_string": "My query string",
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "size": 12,
        "from": 0
    }
}
```

## category-search-template

Returns all `person` _weight 50_, `program` _weight 45_, `post` _weight 35_, `event` _weight 15_, `profile` _weight 10_ and `pressReview` _weight 5_ matching `fields.categories.fr.slug.${LANGUAGE}` slug
It will order the documents by `endDate lte now` _weight 30_ and `endDate lte now` _weight 1_

Parameters:
  * \*`query_string`: `<str>` The slug we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "category-search-template",
    "params": {
        "query_string": "My query string",
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "size": 12,
        "from": 0
    }
}
```

## filter-actionplan-search-template

Returns all `actionPlan`:
* Must match one or more `fields.programs.fr.slug.${LANGUAGE}`
* Should match one or more `fields.type.fr`
* Should match one or more `fields.status.fr`
It will order the documents by default by `startDate asc`

Parameters:
  * \*`programsSlugList`: `<list>` The program's slug we want to query
  * \*`typeList`: `<list>` The type of the actionPlan
  * \*`statusList`: `<list>` The status of the actionPlan
  * `sort`: `<array>` The sorting we wish to use, not mandatory
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-actionplan-search-template",
    "params": {
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "dw-4-circular"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "construction-of-the-future/"
                }
            }
        ],
        "typeList": [
            {
                "term": {
                    "fields.type.fr": "Call for projects"
                }
            }
        ],
        "statusList": [
            {
                "match": {
                    "fields.status.fr": "Finished"
                }
            }
        ],
        "sort": {
            "fields.endDate.fr": {
                "order": "asc"
            }
        },
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.{{language}}": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "size": 12,
        "from": 0
    }
}
```

## filter-ambition-search-template

Returns all the `ambition` matching a specified slug
It will order the documents by `fields.title.${language} order asc`

Parameters:
  * \*`slugList`: `<list>` The slugs we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
  "id": "filter-ambition-search-template",
  "params": {
        "slugList": [
                {
                    "term": {
                        "fields.slug.en": "digital-sector"
                    }
                }
            ]
        },
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "size": 12,
        "from": 0
}
```

## filter-category-search-template

Returns all the `category` matching a specified slug
It will order the documents by `fields.title.${language} asc`

Parameters:
  * \*`slugList`: `<list>` The slugs we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
  "id": "filter-category-search-template",
  "params": {
        "slugList": [
                {
                    "term": {
                        "fields.slug.en": "digital-sector"
                    }
                }
            ]
        },
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "size": 12,
        "from": 0
    }
}
```

## filter-get-actionplan-search-template

Returns all the `actionPlan` matching a specified slug

Parameters:
  * \*`actionPlanSlug`: `<str>` The slugs we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

```json
POST d4w-entries_staging/_search/template
{
  "id": "filter-get-actionplan-search-template",
  "params": {
        "actionPlanSlug": "actionPlanSlugExample",
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr"
    }
}
```

## filter-next-actionplan-search-template

Returns all `event` matching:
* Must `fields.categories.fr.slug.${language}`
* Must `fields.programs.fr.slug.${language}`
* Should `fields.type.fr`
* Should filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`
* Must `fields.endDate.fr gte now`
* Must `fields.endPublicationDate.fr gte now`

Parameters:
  * \*`categoriesSlugList`: `<list>` A list of categories' slug we wish to match
  * \*`programssluglist`: `<list>` a list of programs' slug we wish to match
  * \*`eventTypeList`: `<list>` a list of event's types we wish to match
  * \*`regionsList`: `<list>` a list of regions we wish to search in
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-next-actionplan-search-template",
    "params": {
        "categoriesSlugList": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "eventTypeList": [
            {
                "term": {
                    "fields.type.fr": "International mission"
                }
            },
            {
                "term": {
                    "fields.type.fr": "Expo & program"
                }
            }
        ],
         "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "regionsList": [
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "size": 12,
        "from": 0
    }
}
```

## filter-next-event-search-template

Returns all `event` matching:
* Must `fields.categories.fr.slug.${language}`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Should `fields.type.fr`
* Should `fields.hosts.fr.slug.en`
* Should filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`
* Must `fields.endDate.fr gte now`
* Must `fields.endPublicationDate.fr gte now`

Parameters:
  * \*`categoriesSlugList`: `<list>` A list of categories' slug we wish to match
  * \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
  * \*`eventTypeList`: `<list>` a list of event's types we wish to match
  * \*`profileLinkList`: `<list>` a list of event's hosts we wish to match
  * \*`regionsList`: `<list>` a list of regions we wish to search in
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-next-event-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "categoriesSlugList": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "eventTypeList": [
            {
                "term": {
                    "fields.type.fr": "International mission"
                }
            },
            {
                "term": {
                    "fields.type.fr": "Expo & program"
                }
            }
        ],
        "regionsList": [
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "profileLinkList": [
            {
                "term": {
                    "fields.hosts.fr.slug.en": "service-public-de-wallonie"
                }
            },
            {
                "term": {
                    "fields.partners.fr.slug.en": "service-public-de-wallonie"
                }
            },
            {
                "term": {
                    "fields.organizers.fr.slug.en": "service-public-de-wallonie"
                }
            }
        ]
    }
}
```

## filter-person-search-template

Returns all `person` matching:
* Must exist `fields.internalName.fr`
* Must exist `fields.slug.${language}`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.categories.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Should filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`

Parameters:
  * \*`categoriesSlugList`: `<list>` A list of categories' slug we wish to match
  * \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
  * \*`profileLinkList`: `<list>` a list of event's hosts we wish to match
  * \*`regionsList`: `<list>` a list of regions we wish to search in
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-person-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "categoriesSlugList": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "regionsList": [
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.location.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ]
    }
}
```

## filter-post-search-template

Returns all `post` matching:
* Must exist `fields.title.${language}`
* must exist `fields.slug.${language}`
* must exist `fields.introduction.${language}`
* must exist `fields.content.${language}`
* must exist `fields.publishedDate.fr`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.categories.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Should `fields.type.fr`

Parameters:
  * \*`categoriesSlugList`: `<list>` A list of categories' slug we wish to match
  * \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
  * \*`postTypeList`: `<list>` a list of post's types we wish to match
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-post-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "categoriesSlugList": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "language": "en",
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "postTypeList": [
            {
                "term": {
                    "fields.type.fr": "Feature article"
                }
            }
        ]
    }
}
```

## filter-pressreview-search-template

Returns all `pressReview` matching:
* Must exist `fields.title.${language}`
* must exist `fields.shortDescription.${language}`
* must exist `fields.source.${language}`
* must exist `fields.publishedDate.fr`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.categories.fr.slug.${language}`
* Must `fields.quotedProfiles.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Should `fields.quotedPersons.fr.internalName.${language}.keyword`

Parameters:
  * \*`categoriesSlugList`: `<list>` A list of categories' slug we wish to match
  * \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
  * \*`quotedProfilesSlugList`: `<list>` a list of profiles' slug we wish to match
  * \*`quotedPersonsInternalNameList`: `<list>` a list of quoted persons' internal name types we wish to match
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-pressreview-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "language": "en",
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "categoriesSlugList": [
            {
                "term": {
                    "fields.categories.fr.slug.fr": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.fr": "slug"
                }
            }
        ],
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.fr": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.fr": "slug"
                }
            }
        ],
        "quotedProfilesSlugList": [
            {
                "term": {
                    "fields.quotedProfiles.fr.slug.fr": "lasea"
                }
            }
        ],
        "quotedPersonsInternalNameList": [
            {
                "term": {
                    "fields.quotedPersons.fr.internalName.fr.keyword": "Axel Kupisiewicz - Lasea"
                }
            }
        ]
    }
}
```

## filter-profile-geo-bounding-box-search-template

Returns all `profile` matching:
* Must exist `fields.title.${language}`
* must exist `fields.slug.${language}`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.categories.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Must filter by boundingbox coordonates (`top_right` and `bottom_left`)
* Must filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`
* Must_not filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`

Parameters:
* \*`categoriesSlugList0`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList1`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList2`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList3`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList4`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList5`: `<list>` A list of categories' slug we wish to match
* \*`regionsList`: `<list>` a list of regions we wish to search in
* \*`regionsList`: `<list>` a list of regions we wish to search in
* \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
* \*`clientSites`: `<list>` A list of clientSites
* \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
* \*`top_right`: `<int>`: The top right's coordinate format can be in [Elasticsearch geo_bounding_box format](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-geo-bounding-box-query.html#query-dsl-geo-bounding-box-query-accepted-formats)
  * [GeoJSON](https://geojson.org/) format `[lon, lat]` as in the example bellow
  * [geohash](https://en.wikipedia.org/wiki/Geohash) format `dr5r9ydj2y73` for example
* \*`bottom_left`: `<int>`: The bottom left's coordinate can be
  * [GeoJSON](https://geojson.org/) format `[lon, lat]` as in the example bellow
  * [geohash](https://en.wikipedia.org/wiki/Geohash) format `drj7teegpus6` for example
* `sort`: `<list>` The way we want to sort things, by default by `fields.title.${language}` ascending order
* \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
* \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)
* `displaySource`: `<bool>` If true display the whole document sources, by default false

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-profile-geo-bounding-box-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "language": "en",
        "displaySource": true,
	    "bottom_left": [
            3.2302446062151406,
            48.632898441446876
        ],
        "top_right": [
            7.668721168715142,
            51.45057419097133
        ],
        "categoriesSlugList0": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList1": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList2": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
         "categoriesSlugList3": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList4": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "regionsList": [
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "notInRegionList": [
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "sort": [
            {
                "sys.updatedAt": {
                    "order": "asc"
                }
            }
        ]
    }
}
```

## filter-profile-geo-bounding-aggregation-search-template

Returns all `profile` with an aggregation geo bounding box matching:
* Must exist `fields.title.${language}`
* must exist `fields.slug.${language}`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.categories.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Must filter by boundingbox coordonates (`top_right` and `bottom_left`)
* Must filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`
* Must_not filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`

Parameters:
* \*`categoriesSlugList0`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList1`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList2`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList3`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList4`: `<list>` A list of categories' slug we wish to match
* \*`categoriesSlugList5`: `<list>` A list of categories' slug we wish to match
* \*`regionsList`: `<list>` a list of regions we wish to search in
* \*`regionsList`: `<list>` a list of regions we wish to search in
* \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
* \*`clientSites`: `<list>` A list of clientSites
* \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
* \*`top_right`: `<int>`: The top right's coordinate format can be in [Elasticsearch geo_bounding_box format](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-geo-bounding-box-query.html#query-dsl-geo-bounding-box-query-accepted-formats)
  * [GeoJSON](https://geojson.org/) format `[lon, lat]` as in the example bellow
  * [geohash](https://en.wikipedia.org/wiki/Geohash) format `dr5r9ydj2y73` for example
* \*`bottom_left`: `<int>`: The bottom left's coordinate can be
  * [GeoJSON](https://geojson.org/) format `[lon, lat]` as in the example bellow
  * [geohash](https://en.wikipedia.org/wiki/Geohash) format `drj7teegpus6` for example
* `aggregationPrecision`: `<int>` The precision we wish to use for the aggregation, defaults to 12
* `sort`: `<list>` The way we want to sort things, by default by `fields.title.${language}` ascending order
* \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
* \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-profile-geo-bounding-aggregation-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "language": "en",
        "aggregationPrecision": 12,
	    "bottom_left": [
            3.2302446062151406,
            48.632898441446876
        ],
        "top_right": [
            7.668721168715142,
            51.45057419097133
        ],
        "categoriesSlugList0": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList1": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList2": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
         "categoriesSlugList3": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList4": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "regionsList": [
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "notInRegionList": [
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "sort": [
            {
                "sys.updatedAt": {
                    "order": "asc"
                }
            }
        ]
    }
}
```

## filter-profile-search-template

Returns all `profile` matching:
* Must exist `fields.title.${language}`
* must exist `fields.slug.${language}`
* Must `fields.programs.fr.slug.${language}`
* Must `fields.categories.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`
* Must filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`
* Must_not filter by regions, possible regions are:
  * `brabantWallon`
  * `liege`
  * `namur`
  * `luxembourg`
  * `hainaut`

Parameters:
  * \*`categoriesSlugList0`: `<list>` A list of categories' slug we wish to match
  * \*`categoriesSlugList1`: `<list>` A list of categories' slug we wish to match
  * \*`categoriesSlugList2`: `<list>` A list of categories' slug we wish to match
  * \*`categoriesSlugList3`: `<list>` A list of categories' slug we wish to match
  * \*`categoriesSlugList4`: `<list>` A list of categories' slug we wish to match
  * \*`categoriesSlugList5`: `<list>` A list of categories' slug we wish to match
  * \*`regionsList`: `<list>` a list of regions we wish to search in
  * \*`regionsList`: `<list>` a list of regions we wish to search in
  * \*`programsSlugList`: `<list>` a list of programs' slug we wish to match
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * `sort`: `<list>` The way we want to sort things, by default by `fields.title.${language}` ascending order
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-profile-search-template",
    "params": {
        "size": 12,
        "from": 0,
        "language": "en",
        "categoriesSlugList0": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList1": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList2": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
         "categoriesSlugList3": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "categoriesSlugList4": [
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.categories.fr.slug.en": "slug"
                }
            }
        ],
        "programsSlugList": [
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            },
            {
                "term": {
                    "fields.programs.fr.slug.en": "slug"
                }
            }
        ],
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "regionsList": [
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "notInRegionList": [
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "brabantWallon",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "liege",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "namur",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "luxembourg",
                            "path": "location"
                        }
                    }
                }
            },
            {
                "geo_shape": {
                    "fields.addresses.fr.Geometry.coordinates": {
                        "indexed_shape": {
                            "index": "shapes",
                            "id": "hainaut",
                            "path": "location"
                        }
                    }
                }
            }
        ],
        "sort": [
            {
                "sys.updatedAt": {
                    "order": "asc"
                }
            }
        ]
    }
}
```

## filter-program-by-ambition-template

Returns all `profile` in most recent `updatedDate` order matching:
* Must `fields.ambitions.fr.slug.${language}`
* Must `fields.clientSites.fr.name.fr`

Parameters:
  * \*`ambitionsSlugList`: `<list>` a list of ambition' slug we wish to match
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "filter-program-by-ambition-template",
    "params": {
        "size": 12,
        "from": 0,
        "language": "en",
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "ambitionsSlugList": [
            {
                "term": {
                    "fields.ambitions.fr.slug.en": "ambition-slug"
                }
            },
            {
                "term": {
                    "fields.ambitions.fr.slug.en": "ambition-slug"
                }
            }
        ],
        "from": 0,
        "size": 9
    }
}
```
## fulltext-search-template
🔈 The following fields will be highlighted 🔈
* `fields.shortDescription.${language}`
* `fields.introduction.${language}`
* `fields.additionalDescription.${language}`
* `fields.authors.fr.internalName.fr`
* `fields.content.${language}`
* `fields.contentSummary.${language}`
* `fields.contactPersons.fr.internalName.fr`
* `fields.featuredPersons.fr.internalName.fr`
* `fields.partners.fr.title.${language}`
* `fields.founders.fr.title.${language}`
* `fields.categories.fr.title.${language}`
* `fields.programs.fr.title.${language}`

Returns all `contentType` with `fields.endDate.fr` descending (if exists) matching:
* Must exist `fields.title.${language}` or/and `fields.programs.fr.slug.${language}`
* Must `query_string` _[expression from elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html)_
* Should `sys.contentType.sys.id` with the following [weights](https://www.elastic.co/guide/en/app-search/current/relevance-tuning-guide.html)
  * `person`: 50
  * `program`: 45
  * `post`: 35
  * `event`: 15
  * `profile`: 10
  * `pressReview`: 5
* Must `fields.clientSites.fr.name.fr`
* Should `fields.title.${language}`
* Should `fields.shortTitle.${language}`
* Should `fields.internalName.fr`
* Should `fields.categories.fr.title.${language}`

Parameters:
  * \*`query_string`: `<str>` The string we wish to search for
  * \*`contentType`: `<list>` A list of contenttypes we wish to match
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`language`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_
  * \*`size`: `<int>` The size of the result we wish to retrieve (2 result will return the 2 first entries matching)
  * \*`from`: `<int>` Where the search should start (2 would mean returning result from the 2 match)

```json
POST d4w-entries_staging/_search/template
{
    "id": "fulltext-search-template",
    "params": {
        "size": 12,
        "from": 0
        "query_string": "My query string"
        "clientSites": [
            {
                "term": {
                        "fields.clientSites.fr.name.fr": "Digital Wallonia"
                    }
            }
        ],
        "language": "fr",
        "contentType": [
            {
                "term": {
                        "sys.contentType.sys.id": "profile"
                    }
            },
            {
                "term": {
                        "sys.contentType.sys.id": "post"
                }
            },
            {
                "term": {
                        "sys.contentType.sys.id": "pressReview"
                }
            },
            {
                "term": {
                        "sys.contentType.sys.id": "person"
                }
            },
            {
                "term": {
                        "sys.contentType.sys.id": "event"
                }
            },
            {
                "term": {
                        "sys.contentType.sys.id": "program"
                }
            }
        ]
    }
}
```
