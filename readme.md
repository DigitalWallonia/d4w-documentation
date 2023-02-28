# Clarification
* `data4wallonia`: backoffice solution at the time being contentful
* `opensearch`: search engine and data source for data4wallonia
* `graphql`: data query API for data4wallonia
* `index`: this is the equivalent to a table in RDB _relational database_

🛎️ opensearch and graphql possesses the same data (graphql uses opensearch as backend) 🛎️

# Access
In order to access the data stored in data4wallonia we provide 2 means of access:
* **opensearch** _(the same as elasticsearch despite beeing stated otherwise on ES documentation)_
  * Fulltext search _see templates for more details_
  * Access to data4wallonia
* **graphql**
  * Access to data4wallonia

If for any reasons this two means do not suit your needs please come back to us with your problematic and we will try to help you solve the issue.

## Opensearch
### Access
The access to opensearch is subjected to fair use and can be rate limited at any moment in cases of abuse.

💡 only the production opensearch is rate limited 💡

The access URL will be provided to you when an access will be created. It is following the format `search.${ENVIRONEMT}.${CLIENT_SITE_NORMALIZED}.d4w.be`

### Indexation
The data between data4wallonia's backoffice and opensearch/graphql are near real time synchronized _between 3s and 15s, depending on the load_


### General use
Opensearch contains all the entry  contained in the data4wallonia backoffice. The opensearch index is `d4w-entries_${D4W_BRANCH}`. 
For example if our branch is named `staging` the index we should use will be `d4w-entries_staging`.

At the moment 2 indices are used:
* `d4w-entries_staging` for the staging environment
* `d4w-entries_master` for the production environment

🗿 If you need another branch not mentioned above we could set up one in staging 🗿

## GraphQL
Work in progress
# Modifications
In order to keep the most actual content we could provide you with a webhook that will be triggered each time a document or a linked document will be updated.

The webhook's message will have the following format:
```json
{
    "sys": {
        "id": "66aP6YnSaFf9uydDM1EJxU"
    }
}
```

The format supported at the moment are:
* Email
* HTTP Call
* AWS SQS
* AWS SNS
* IP over Avian Carriers as implemented in RFC 2549

🩵 we are open to any suggestions regarding any format of webhook #NoDiscrimination 🩵 

# Document structure
In comparison to contentful which will provide a document without resolving the links correctly, we resolve all the links taking the following keys if they exist:
* `title`
* `slug`
* `name` 
* `url`
* `file` 
* `fileName`
* `contentType`
* `internalName`
* `logoAssetImage`
* `primaryColor`
* `secondaryColor`
* `id`
* `quotedProfiles`
* `role`

For example the following _some parts of the full document were omitted_
```json
"clientSites": {
  "fr": [
    {
      "sys": {
        "type": "Link",
        "linkType": "Entry",
        "id": "16hlZMpDwjFBCFxHC7hqcI"
      }
    }
  ]
}
```

Will become the following

```json
"clientSites": {
  "fr": [
    {
      "name": {
        "fr": "STEAM"
      },
      "url": {
        "fr": "https://steam.bydw.be/"
      },
      "id": "16hlZMpDwjFBCFxHC7hqcI"
    }
  ]
}
```
Any entry that will be resolved will have an ID present. The ID is a unique identifier of any entry and can be used to retrieve an entry.


🌴 Please note that a `fr` is present although this field is not localized. This is due to our backoffice software _(contentful)_ which needs a default localisation even if the field is not localized. We apologize for the inconvenience 🌴
## HTML conversion
The _rich text_ is not easily parsable we  provide an HTML version of the following fields:
* `fields.contentHTML`
* `fields.additionalDescriptionHTML`

Each of the following classes will be present if the type is:
* `paragraph`
  * **css class**: `d4wentry-paragraph`
```html
<p class='d4wentry-paragraph'>A small paragraph</p>
```
* `unordered-list`
  * **css class**: `d4entry-unordered-list` 
```html
<ul class='d4entry-unordered-list'>an unordered list item</ul>
```
* `ordered-list`
  * **css class**: `d4entry-ordered-list` 
```html
<ul class='d4entry-unordered-list'>an unordered list item</ul>
```
* `hr`
  * **css class**: `d4entry-h4` 
```html
<hr class="d4entry-h4">
```
* `blockquote`
  * **css class**: `d4entry-blockquote` 
```html
<blockquote class="d4entry-blockquote">To start a day you have to wake up</blockquote>
```
* `embedded-asset-block`
  * for an image: **css class**: `d4wentry-${entry_id}`, `d4entry-${entry_type}` and `d4entry-asset-block`:
```html
<div class="d4wentry-16hlZMpDwjFBCFxHC7hqcI d4entry-post d4entry-asset-block">'
    <img class="d4wentry-id-3sUQG6cbrvPtra8UoeDqCp d4entry-type-asset"
    src="https://assets.somecdn.com/image.png" alt="an example asset image"
    width="200"
    height="200" />
</div>
```
  * for a pdf: **css class**: `d4wentry-${entry_id}`, `d4entry-${entry_type}` and `d4entry-asset-block`:
```html
<div class="d4wentry-16hlZMpDwjFBCFxHC7hqcI d4entry-post d4entry-asset-block">'
    <a class="d4wentry-id-3sUQG6cbrvPtra8UoeDqCp d4entry-type-asset"
    src="https://assets.somecdn.com/document.pdf">
        An example PDF document
    </a>
</div>
</div>
```
* `embedded-entry-block`
  * no classes for `img`, 
```html
<img
  src="https://assets.somecdn.com/image.png" alt="an example asset image" 
  width="200"
  height="200"/>
```
  * for `externalLink` **css classes**: `d4wentry-${entry_id}`, `d4entry-type-${entry_type}`, `d4entry-embedded-content-title` and `d4entry-embedded-content`, 
```html
<div class="d4wentry-id-16hlZMpDwjFBCFxHC7hqcI d4entry-type-external-link d4entry-embedded-content"><p class="d4entry-embedded-content-title">title of the entry</p>a short description of the entry</div>
```
  * for a link to an entry **css class**: `d4wentry-id-${ID}`, `d4entry-type-${CONTENT_TYPE}` and `d4entry-entry-block` 
```html
<div class="d4wentry-id-16hlZMpDwjFBCFxHC7hqcI d4entry-type-post d4entry-entry-block">'
  <a href="/post/les-castors-lapons-sont-ils">
  {entry_title}
  </a>/* if a logo is present, the img will be inputed here */
</div>

<img 
  src="https://assets.somecdn.com/image.png" alt="an example asset image"
  width="200"
  height="200"
/>

```
* `embedded-entry-inline`
  *  **css classes**: `d4wentry-id-${ID}`, `d4entry-type-${CONTENT_TYPE}`, `d4entry-entry-inline` and `d4entry-entry-inline-title`
```html
a class="d4wentry-id-16hlZMpDwjFBCFxHC7hqcI d4entry-type-profile d4entry-entry-inline d4entry-entry-inline-title" href="/profiles/prince-du-livre-lu">
    Prince du Livre lu
</a>
```
* `entry-hyperlink`
  * **css classes**: `d4wentry-id-${entry_id}`, `d4entry-type-${entry_type}`, `d4entry-entry-inline` and `d4entry-entry-inline-title`
```html
<a class='d4wentry-id-7sFDkxgTdOyKuOZtuVXYV5 d4entry-type-event d4entry-entry-inline d4entry-entry-inline-title' href='/event/la-fete-du-castor-lapin'>La fete du castor lapin</a>
```
* `text`
  * if `bold` **css class**: `d4wentry-font-bold`
```html
<strong class='d4wentry-font-bold'>some bold text</strong>
```
  * if `italic` **css class**: `d4wentry-font-italic`
```html
<em class='d44entry-italic'>some text in emphasis</em>
```
* `asset-hyperlink`
  * **css class**: `d4wentry-id-{entry_id}`, `d4entry-type-{entry_type}` and `d4entry-asset-hyperlink`
```html
<a class='d4wentry-id-5y1eZo5IwObiitHOZxwO8B d4entry-type-post d4entry-asset-hyperkink' href='https://assets.cdn.com/some-url/'>Nice la capital du gendarme de Saint Tropez</a>
```
* `hyperlink`
  * **css classes**: `d4wentry-hyperlink`
```html
<a class='d4wentry-hyperlink' href='https://testing.example.com'>testing example website</a>
```
* `list-item`
  * **css classes**: `d4entry-list-item`
```html
<li class='d4entry-list-item'></ul>a list item</ul></li>
```
* `table`
  * **css classes**: `d4entry-table`
```html
<table class='d4entry-table'>
  <tr class='d4entry-table-row'>
    <th class='d4entry-table-header-cell'>
      <p class='d4wentry-paragraph'>COL Ref</p>
    </th>
    <th class='d4entry-table-header-cell'>
      <p class='d4wentry-paragraph'>data 1</p>
    </th>
    <th class='d4entry-table-header-cell'>
      <p class='d4wentry-paragraph'>data 2</p>
    </th>
    <th class='d4entry-table-header-cell'>
      <p class='d4wentry-paragraph'>data 3</p>
    </th>
  </tr>
  <tr class='d4entry-table-row'>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>ref L1</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>data 1 L1</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>Data 2 L1</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>data 3 L1</p>
    </td>
  </tr>
  <tr class='d4entry-table-row'>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>Ref L2</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>data 1 L2</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>Data 2 L2</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>data 3 L2</p>
    </td>
  </tr>
  <tr class='d4entry-table-row'>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>Ref L3</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>data 1 L3</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>Data 2 L3</p>
    </td>
    <td class='d4entry-table-cell'>
      <p class='d4wentry-paragraph'>data 3 L3</p>
    </td>
  </tr>
</table>
```
* `table-row`
  * **css classes**: `d4entry-table-row`
```html
<tr class='d4entry-table-row'>
  <td class='d4entry-table-cell'>
    <p class='d4wentry-paragraph'>Ref L3</p>
  </td>
  <td class='d4entry-table-cell'>
    <p class='d4wentry-paragraph'>data 1 L3</p>
  </td>
  <td class='d4entry-table-cell'>
    <p class='d4wentry-paragraph'>Data 2 L3</p>
  </td>
  <td class='d4entry-table-cell'>
    <p class='d4wentry-paragraph'>data 3 L3</p>
  </td>
</tr>
```
* `table-cell`
  * **css classes**: `d4entry-table-cell`
```html
<td class='d4entry-table-cell'>
  <p class='d4wentry-paragraph'>Ref L3</p>
</td>
```
* `table-header-cell`
  * **css classes**: `d4entry-table-header-cell`
```html
<th class='d4entry-table-header-cell'>
  <p class='d4wentry-paragraph'>COL Ref</p>
</th>
```

## Plain text conversion
we  provide a plain text version of the following fields as well:
* `fields.content`
* `fields.additionalDescription`

Please note that both of those fields are mapped _refer to mapping in elasticsearch_ and therefore are fulltext searchable.


## Opensearch templates

You can find all the opensearch templates in `/template-opensearch`

For more details about each templates check [the deeper look documentation](opensearch_template.md) 

# Small Help Guide
* templates
* query guide
