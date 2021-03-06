Open Companies House
====================

Simple ruby wrapper around [Companies House Open API](http://www.companieshouse.gov.uk/about/miscellaneous/URI.shtml)

Installation
============

In your Gemfile

```ruby
gem "open-companies-house", "~> 0.2.0", require: 'companies_house'
```

Usage
=====

```ruby
company = CompaniesHouse.lookup "07495895"
=> #<CompaniesHouse:0x00000100932870 @registration_number="07495895"... >

company["CompanyName"]
=> "GOCARDLESS LTD"

company.sic_code # convenience method
=> "62090"
```

Caching
=======

If you'd like to cache your requests, you can configure the gem:

```ruby
# file config/initializers/companies_house.rb

# swap in your own cache here
CompaniesHouse.cache = Rails.cache

# Optional
CompaniesHouse.cache_args = { expires_in: 10.minutes }
```

Specs
=====

    rspec spec


Available Data
==============

The following data is currently available on the `company` object returned by
`CompaniesHouse.lookup`


You can access the data in one of two ways:

1) Directly from the hash:

```ruby
company["RegAddress"]["AddressLine1"]
=> "22-25 FINSBURY SQUARE"
```

2) As a human-readable method:

```ruby
company.reg_address.address_line1
=> "22-25 FINSBURY SQUARE"
```

Note that for more complicated keys, you may have to check the precise 
translation between the camelcase hash key and the human readable method.


All data:

```json
{
  "CompanyName" : "GOCARDLESS LTD",
  "CompanyNumber" : "07495895",
  "RegAddress" : {
     "AddressLine1" : "22-25 FINSBURY SQUARE",
     "PostTown" : "LONDON",
     "Country" : "UNITED KINGDOM",
     "Postcode" : "EC2A 1DX"
  },
  "CompanyCategory" : "Private Limited Company",
  "CompanyStatus" : "Active",
  "CountryOfOrigin" : "United Kingdom",
  "IncorporationDate" : "17/01/2011",
  "PreviousNames" : [
     {
        "CONDate" : "25/08/2011",
        "CompanyName" : "GROUPAY LIMITED"
     }
  ],
  "Accounts" : {
     "AccountRefDay" : "31",
     "AccountRefMonth" : "01",
     "NextDueDate" : "31/10/2013",
     "LastMadeUpDate" : "31/01/2012",
     "AccountCategory" : "TOTAL EXEMPTION SMALL"
  },
  "Returns" : {
     "NextDueDate" : "14/02/2013",
     "LastMadeUpDate" : "17/01/2012"
  },
  "Mortgages" : {
     "NumMortCharges" : "1",
     "NumMortOutstanding" : "1",
     "NumMortPartSatisfied" : "0",
     "NumMortSatisfied" : "0"
  },
  "SICCodes" : {
     "SicText" : [
        "62090 - Other information technology service activities"
     ]
  }
}
```
