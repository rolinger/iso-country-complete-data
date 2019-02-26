A painstakingly collected data set for country info validation. I got quite tired of independent lists that needed reformatting and that did not have all the necessary info per data set.  This is the most comprehensive object json I am aware of.  I am going to be writing PHP/JS code for loading and quick data extraction but essentially all you need to do is download the JSON file (CountryData_minify.json) and load it in your scripts and your ready to go.

This data set merges 7 different independent datasets to create a single master country json object that can be used for HTML/Code validation when dealing with country specific information.

        // Two files:
        CountryData_minify.json (233k)
        CountryData_pretty.json (531k)

I now use this object to auto-build Country `<select>` menus which then preformat and provide validation for all other input/select fields related to that country (IE: state lists, postal/zip code, phone numbers (country code and local number formats))

This object can be used to cross reference any country specific information for:
            
        // Object Data Includes:
        Alpha2 code
        Alpha3 code
        short name (ie: United States)
        long name (ie: United States of America)
        isoNumber code
        ioc code (olympic committee)
        currency
            currency code 
            currency name
            currency symbol
        Languages
        Phone:
            country code (ie: +1 (US))
            mobile_begin_with prefix codes
            Phone format lengths (ie: XXXYYYZZZZ (10))
        Postal:
            Postal code formats
            Permitted non-postal characters
            Included postal validation regex
            Postal lengths
            character sets (for keyboard types: number or text (varchar))
        Country States & State Codes (ie: "Alaska" : "AK" )
      
Sample JS calls:

      //javascript:
      var obj = { dataset } ;
      console.log(obj.country["BEL"]) ;

The above format uses lookup by the 3 character country code (IE: USA) and returns all info about that country.  But you can also do quick reverse lookups to get the the 3 character code if you only have country name or country 2 digit code:
  
    //Javascript
    var obj = { dataset } ;
    
    // extract country info with only 2 digit code
    console.log(obj.country[obj.alpha2_to_alpha3["BE"]]) ;  
    
    // extract country info with only country name
    console.log(obj.country[obj.name_to_alpha3["Belguium"]] ;  

Please help keep this data accurate or make contributions to it to expand the datasets.  Things that could be added are known zip/postal codes PER country STATE as well as local phone prefix numbers. 

NOTE: Not all countries have postal info avaialble.  Either the information was incomplete or it simply does not exist for that country.  There are maybe a dozen that postal or so that don't have it.  Always test for `obj.country["XXX"].postal`

Sample Break Out of country-data object:

    //console.log(obj.country["BEL"]) ;
    {
        "country_formats": {
            "name_to_alpha3": {
                "United States": "USA",
                "Aruba": "ABW",
                "Afghanistan": "AFG",
                "Belgium" : "BEL",
            ...
            },
            "alpha2_to_alpha3": {
                "US": "USA",
                "AW": "ABW",
                "AF": "AFG",
                "BE": "BEL",
             ...
             }
        },
        "country" : {
            "BEL": {
                "currency": {
                    "currencyCode": [
                        "EUR"
                    ],
                    "currencyName": "Euro",
                    "currencySymbol": null
                },
                "info": {
                    "shortName": "Belgium",
                    "longName": "Belgium",
                    "alpha2": "BE",
                    "alpha3": "BEL",
                    "isoNumericCode": "56",
                    "ioc": "BEL",
                    "capitalCity": "Bruxelles [Brussel]",
                    "tld": ".be"
                },
                "languages": [
                    "nld",
                    "fra",
                    "deu"
                ],
                "phone": {
                    "countryCode": "32",
                    "mobile_begin_with": [
                        "4"
                    ],
                    "phone_number_lengths": [
                        9
                    ]
                },
                "postal": {
                    "Description": "4-Digits - NNNN",
                    "RedundantCharacters": " -",
                    "ValidationRegex": "^[0-9]{4}$",
                    "charSet": "number",
                    "postalLengths": [
                        "4"
                    ],
                    "postalFormats": [
                        "NNNN"
                    ]
                },
                "states": {
                    "Bruxelles-Capitale": "BRU",
                    "Rgion Flamande": "VLG",
                    "Rgion Walloni": "WAL"
                }
            }
