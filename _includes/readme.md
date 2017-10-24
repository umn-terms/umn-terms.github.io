# At The Sound Of The Tone, The Term Will Be...
## AKA terms.umn.edu

A web service that tells you what term is active today, or any other day that you might care about.

## Terminology

- _Active_: term based on the range of actual start of term (term_begin_dt) and actual end of term (term_end_dt)
- _Latest_: term based on the most recently begun term that ends the day before the actual start of term (term_begin_dt) for the following term

## Usage

### Get Terms Active for Today:
* [All active terms for all institutions and careers](http://terms.umn.edu/active/today)
* [All active terms for UMNTC and all careers](http://terms.umn.edu/umntc/active/today)
* [All active terms for UMNTC and UGRD](http://terms.umn.edu/umntc/ugrd/active/today)

### Get Terms Latest for Today:
* [All latest terms for all institutions and careers](http://terms.umn.edu/latest/today)
* [All latest terms for UMNTC and all careers](http://terms.umn.edu/umntc/latest/today)
* [All latest terms for UMNTC and UGRD](http://terms.umn.edu/umntc/ugrd/latest/today)

### Get Terms by Date: 
_The date 2017-09-15 is used for all examples_
* [All active terms for all institutions and careers by date](http://terms.umn.edu/active/2017-09-15)
* [All latest terms for all institutions and careers by date](http://terms.umn.edu/latest/2017-09-15)
* [All active terms for UMNTC and all careers by date](http://terms.umn.edu/umntc/active/2017-09-15)
* [All latest terms for UMNTC and all careers by date](http://terms.umn.edu/umntc/latest/2017-09-15)
* [All active terms for UMNTC and UGRD by date](http://terms.umn.edu/umntc/ugrd/active/2017-09-15)
* [All latest terms for UMNTC and UGRD by date](http://terms.umn.edu/umntc/ugrd/latest/2017-09-15)


### Get Terms by STRM
_STRM 1179 is used on all examples_
* [All terms for STRM 1179](http://terms.umn.edu/1179)
* [All terms for UMNTC and STRM 1179](http://terms.umn.edu/umntc/1179)
* [The term for UMNTC, career UGRD, and STRM 1179](http://terms.umn.edu/umntc/ugrd/1179)
## Data Returned

You will get a collection of `term` resources back. The data will be like this example:

```json
{
  "id": "6",
  "type": "terms",
  "links": {
    "self": "http://terms.umn.edu/terms/6",
    "prev": "http://terms.umn.edu/terms/5",
    "next": "http://terms.umn.edu/terms/7"
  },
  "attributes": {
  "institution": "UMNCR",
  "strm": "1179",
  "begin-date": "2017-08-22",
  "end-date": "2017-12-14",
  "name": "Fall 2017",
  "career": "UGRD"
  }
}
```

The `prev` link will take you to the previous term for the same Institution & Career. The `next` link will take you to the subsequent term for the same Institution and Career.

## Responses for non-existent terms

- If you request a collection of terms that contains no terms, such as http://terms.umn.edu/active/1700-01-01, you will get an empty collection back

```json
{
  "data": []
}
```

- If you request a collection of non-existent terms, such as http://terms.umn.edu/0000, you will get an empty collection back

```json
{
  "data": []
}
```

- If you request a single, non-existent term, such as http://terms.umn.edu/terms/0, you will get an error object back

```json
{
  "errors": [
    {
      "title": "Record not found",
      "detail": "The record identified by 0 could not be found.",
      "code": "404",
      "status": "404"
    }
  ]
}
```

## Development
- `gem install overcommit`
- `script/setup` 

Local development uses a SQLite database for speed and ease-of-setup. The deployed application uses an Oracle database. In some cases this can introduce bugs, as developers are working against a different database platform that what is used in production. If you'd like to work against an Oracle database, contact Ian Whitney (whit0694) for credentials.

