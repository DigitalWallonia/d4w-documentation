# Request parameters

a \* indicates that this parameter is mandatory so should be present but could be empty. For example `"clientSites": []` is a valid parameter

## ambition-search-template

Returns all `person` _weight 50_, `program` _weight 45_, `post` _weight 35_, `event` _weight 15_, `profile` _weight 10_ and `pressReview` _weight 5_ matching `fields.ambitions.fr.slug.${LANGUAGE}` slug
It will order the documents by `endDate lte now` _weight 30_ and `endDate lte now` _weight 1_

Parameters:
  * \*`query_string`: `<str>` The slug we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`lamguage`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

```json
POST d4w-entries_staging/_search/template
{
  "id": "ambition-search-template",
  "params": {
        "query_string": "My query string"
        },
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

## category-search-template

Returns all `person` _weight 50_, `program` _weight 45_, `post` _weight 35_, `event` _weight 15_, `profile` _weight 10_ and `pressReview` _weight 5_ matching `fields.categories.fr.slug.${LANGUAGE}` slug
It will order the documents by `endDate lte now` _weight 30_ and `endDate lte now` _weight 1_

Parameters:
  * \*`query_string`: `<str>` The slug we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`lamguage`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

```json
POST d4w-entries_staging/_search/template
{
  "id": "category-search-template",
  "params": {
        "query_string": "My query string"
        },
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
  * \*`lamguage`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

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
            "language": "fr"
  }
}
```

## filter-ambition-search-template

Returns all the `ambition` matching a specified slug
It will order the documents by `fields.title.${language} order asc`

Parameters:
  * \*`slugList`: `<list>` The slugs we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`lamguage`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

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
        "language": "fr"
}
```

## filter-category-search-template

Returns all the `category` matching a specified slug
It will order the documents by `fields.title.${language} asc`

Parameters:
  * \*`slugList`: `<list>` The slugs we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`lamguage`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

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
        "language": "fr"
}
```

## filter-category-search-template

Returns all the `actionPlan` matching a specified slug

Parameters:
  * \*`actionPlanSlug`: `<str>` The slugs we want to query
  * \*`clientSites`: `<list>` A list of clientSites
  * \*`lamguage`: `<str>` The language we want to use _at the moment `fr`. `en`, `de`, `nl`_

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
        "language": "fr"
}
```
