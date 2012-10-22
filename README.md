Open Companies House
====================

Simple ruby wrapper around Companies House Open API


Usage:
=====

    company = CompaniesHouse.lookup "07495895"
    => #<CompaniesHouse:0x00000100932870 @registration_number="07495895"... >

    company["CompanyName"]
    => "GOCARDLESS LTD"

    company.sic_code # convenience method
    => "62090"

Specs
=====

    rspec spec


Available Data
==============

The following data is currently available on the company object returned by
`CompaniesHouse.lookup`

ToDo: Use some funky metaprogramming to make these available as human-readable
method calls, eg `company.name` or `company.registered_address.line_1`.

For now, you can use it like this:

    company["RegAddress"]["AddressLine1"]
    => "22-25 FINSBURY SQUARE"

All data:

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