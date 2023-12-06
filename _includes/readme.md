# At The Sound Of The Tone, The Term Will Be...
## AKA terms.umn.edu

A web service that tells you what term is active today, or any other day that you might care about.

## Terminology

- _Active_: A term that has begun but has not ended.
- _Latest_: The term that began most recently. This term may be over.
- _Soonest_: The active term, or if there is no active term, the next term. Another way of thinking about this is the term that ends the soonest. This term may not have started yet.

If you look for Active terms, you may sometimes get no terms back. If you look for latest or soonest terms, you should always get a term back.

### Examples

If today is 2017-08-18 and you check for Undergraduate UMNTC terms

- The _Active_ term is Summer, 2017. It began on 2017-05-22 and ends on 2017-08-18, and today's date falls within that span.
- The _Latest_ term is also Summer, 2017. It is the UMNTC Undergraduate term with the most recent start date.
- The _Soonest_ term is also Summer, 2017. Summer, 2017 is not complete (so it is the UMNTC Undergraduate term with the soonest end date).

If you check one day later, on 2017-08-19 then you will see:

- There is *no active term*. Summer, 2017 has completed, and the next term has not yet begun.
- The _Latest_ term is still Summer, 2017. It is the UMNTC Undergraduate term with the most recent start date.
- The _Soonest_ term is Fall, 2017. Summer, 2017 has completed and Fall, 2017 is the next term (so it is the UMNTC Undergraduate term with the soonest end date).

## Usage

### Get Terms Active for Today:
* [All active terms for all institutions and careers](https://terms.umn.edu/active/today)
* [All active terms for UMNTC and all careers](https://terms.umn.edu/umntc/active/today)
* [All active terms for UMNTC and UGRD](https://terms.umn.edu/umntc/ugrd/active/today)

### Get Terms Latest for Today:
* [All latest terms for all institutions and careers](https://terms.umn.edu/latest/today)
* [All latest terms for UMNTC and all careers](https://terms.umn.edu/umntc/latest/today)
* [All latest terms for UMNTC and UGRD](https://terms.umn.edu/umntc/ugrd/latest/today)

### Get Terms Soonest for Today:
* [All soonest terms for all institutions and careers](https://terms.umn.edu/soonest/today)
* [All soonest terms for UMNTC and all careers](https://terms.umn.edu/umntc/soonest/today)
* [All soonest terms for UMNTC and UGRD](https://terms.umn.edu/umntc/ugrd/soonest/today)

### Get Terms by Date: 
_The date 2017-09-15 is used for all examples_
* [All active terms for all institutions and careers by date](https://terms.umn.edu/active/2017-09-15)
* [All latest terms for all institutions and careers by date](https://terms.umn.edu/latest/2017-09-15)
* [All soonest terms for all institutions and careers by date](https://terms.umn.edu/soonest/2017-09-15)
* [All active terms for UMNTC and all careers by date](https://terms.umn.edu/umntc/active/2017-09-15)
* [All latest terms for UMNTC and all careers by date](https://terms.umn.edu/umntc/latest/2017-09-15)
* [All soonest terms for UMNTC and all careers by date](https://terms.umn.edu/umntc/soonest/2017-09-15)
* [All active terms for UMNTC and UGRD by date](https://terms.umn.edu/umntc/ugrd/active/2017-09-15)
* [All latest terms for UMNTC and UGRD by date](https://terms.umn.edu/umntc/ugrd/latest/2017-09-15)
* [All soonest terms for UMNTC and UGRD by date](https://terms.umn.edu/umntc/ugrd/soonest/2017-09-15)


### Get Terms by STRM
_STRM 1179 is used on all examples_
* [All terms for STRM 1179](https://terms.umn.edu/1179)
* [All terms for UMNTC and STRM 1179](https://terms.umn.edu/umntc/1179)
* [The term for UMNTC, career UGRD, and STRM 1179](https://terms.umn.edu/umntc/ugrd/1179)
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

- If you request a collection of terms that contains no terms, such as https://terms.umn.edu/active/1700-01-01, you will get an empty collection back

```json
{
  "data": []
}
```

- If you request a collection of non-existent terms, such as https://terms.umn.edu/0000, you will get an empty collection back

```json
{
  "data": []
}
```

- If you request a single, non-existent term, such as https://terms.umn.edu/terms/0, you will get an error object back

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

Local development uses the `asr_dev_user_<username>` space. A connection to the
U's VPN is required to access the development and test databases.

### Setup

- `gem install overcommit`
- `script/setup`

### Testing

Except for one request spec, these tests are all written as [Cucumber feature tests](https://cucumber.io/). You can find the scenarios in `./features`.

- `script/test` or `script/test path/to/test.feature`

The single request spec can't be run individually using `script/test`. To run it use: `bin/rspec spec/request/cors_spec.rb`. It will also run on `script/test`.

To see a test coverage report:

1. `COVERAGE=1 ./script/test`
1. `open coverage/index.html` to view the report

### Deploying

Be sure your Docker containers are running locally by running `script/server`.

- `script/deploy [environment]`

This will deploy from the master branch and update the `terms.umn.edu` Jekyll site using the contents of the README.

**Note:** You must be a member of the umn-terms organization to publish to the Jekyll site. To skip that step run `bundle exec cap staging deploy`.

### URLs

- Staging: https://terms-staging.umn.edu/active/today
- Production: https://terms.umn.edu/active/today
- Documentation site: https://umn-terms.github.io/

### Owners

Who is responsible for the web application after initial development?
 * [See this spreadsheet](https://docs.google.com/spreadsheets/d/1JOCG2MZnzsQ_ja8B-pEBqARSXyvoR0TwDb_APO3cdL4/edit?usp=sharing).
