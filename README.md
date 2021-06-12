# GeoNuclearData

This repository contains a database with information about Nuclear Power Plants worldwide.

### Version

Database version: **0.17.0** (**2020/04/19**)  
Dataset last updated in version: **0.17.9** (**2021/06/12**)

### Changelog

See [CHANGELOG](https://github.com/cristianst85/GeoNuclearData/blob/master/CHANGELOG.md) file for details.

### Data formats

Data is available in multiple formats (MySQL, JSON, and CSV).

### Quick database summary (by reactor status)

|**Status**            |**Count**|
|----------------------|--------:|
|Unknown               |        1|
|Planned               |       92|
|Under Construction    |       57|
|Operational           |      443|
|Shutdown              |      193|
|Suspended Construction|        6|
|Cancelled Construction|        4|
|Never Commissioned    |        2|
|**Total**             |  **798**|

## Tables structure

### countries
- `code` - ISO 3166-1 alpha-2 country code
- `name` - country name in English
 
### nuclear_power_plant_status_type
- `id` - numeric id key
- `type` - nuclear power plant status

### nuclear_reactor_type
- `id` - numeric id key
- `type` - nuclear reactor type acronym
- `description` - nuclear reactor type long form
 
### nuclear_power_plants
- `id` - numeric id key
- `name` - nuclear power plant name
- `latitude` - latitude in decimal format
- `longitude` - longitude in decimal format
- `country_code` - ISO 3166-1 alpha-2 country code
- `status_id` - nuclear power plant status id
- `reactor_type_id` - nuclear reactor type id
- `reactor_model` - nuclear reactor model
- `construction_start_at` - date when nuclear power plant construction was started
- `operational_from` - date when nuclear power plant became operational (also known as commercial operation date)
- `operational_to` - date when nuclear power plant was shutdown (also known as permanent shutdown date)
- `capacity` - nuclear power plant capacity (design net capacity in MWe)
- `source` - source of the information
- `last_updated_at` - date and time when information was last updated
- `iaea_id` - IAEA PRIS reactor id
 
## Notes
Data from `source`, `last_updated_at`, and `iaea_id` columns is for maintenance purposes only and is not recommended to be used.

### Known Inconsistencies (GeoNuclearData vs. WNA vs. IAEA PRIS)

_Operational Reactors_

* There are currently 443 reactors listed as being operational in the GeoNuclearData database, the same number as in the PRIS database. Although the China Experimental Fast Reactor ([CEFR](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1047)) is grid-connected and occasionally producing 20 MWe net, it is omitted from the WNA's operating nuclear power reactors table ([see here](https://www.world-nuclear.org/information-library/country-profiles/countries-a-f/china-nuclear-power.aspx)) because it is considered minor and experimental, but it is included in IAEA figures for operational reactors ([see here](https://pris.iaea.org/PRIS/CountryStatistics/CountryDetails.aspx?current=CN)).

_Reactors Under Construction_

- The number of reactors listed as being under construction in the GeoNuclearData database does not match with either the number of reactors under construction from WNA's database or with the number from the PRIS database:
  - [BALTIC-1](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=968) reactor (Russia) is shown as under construction in PRIS, but it was removed from the WNA's database in November 2000 ([see here](https://www.world-nuclear.org/information-library/country-profiles/countries-o-s/russia-nuclear-power.aspx));
  - [TIANWAN-6](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=976) reactor (China) is shown as under construction in PRIS, but it is listed as operable in WNA's database ([see here](https://www.world-nuclear.org/reactor/default.aspx/TIANWAN-6));
- In addition to the list of reactors under construction from the PRIS database, the GeoNuclearData database also contains the following reactors (as in WNA's database): 
  - CAP1400-1 ([Shidaowan 1](https://www.world-nuclear.org/reactor/default.aspx/SHIDAOWAN-1));
  - CAP1400-1 ([Shidaowan 2](https://www.world-nuclear.org/reactor/default.aspx/SHIDAOWAN-2));
  - Xiapu-2 ([Xiapu 2](https://www.world-nuclear.org/reactor/default.aspx/XIAPU-2));
  - Xudabao-3 ([Xudabao 3](https://www.world-nuclear.org/reactor/default.aspx/XUDABAO-3));
  - Tianwan-7 ([Tianwan 7](https://www.world-nuclear.org/reactor/default.aspx/TIANWAN-7)).

_Naming_

- The GeoNuclearData database usually follows the naming conventions from PRIS for reactors, but in WNA's database some nuclear reactors have completely different names. Some examples are:
  - [BELARUSIAN-1](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1056) and [2](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1061) reactors (Belarus) are named in WNA's database [Ostrovets 1](https://www.world-nuclear.org/reactor/default.aspx/BELARUSIAN-1) and  [2](https://www.world-nuclear.org/reactor/default.aspx/BELARUSIAN-1), respectively;
  - [SANAOCUN-1](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1094) reactor (China) is named in WNA's database [San'oa 1](https://www.world-nuclear.org/reactor/default.aspx/SANOA-1);
  - [CAP1400-1](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1085) and [2](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1086) reactors (China) (they were unlisted from PRIS as of 30 April 2021) are named in WNA's database [Shidaowan 1](https://www.world-nuclear.org/reactor/default.aspx/SHIDAOWAN-1) and [2](https://www.world-nuclear.org/reactor/default.aspx/SHIDAOWAN-2), respectively;
  - [KANUPP-1](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=427), [2](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1067), and [3](https://pris.iaea.org/PRIS/CountryStatistics/ReactorDetails.aspx?current=1068) reactors (Pakistan) are named in WNA's database [Karachi 1](https://www.world-nuclear.org/reactor/default.aspx/KANUPP-1), [2](https://www.world-nuclear.org/reactor/default.aspx/KANUPP-2), and [3](https://www.world-nuclear.org/reactor/default.aspx/KANUPP-3).

_Coordinates_

- the coordinates found in GeoNuclearData database are approximate;
- the original source for the existing coordinates was an old Google Fusion Table dating back to March 2012 (probably sourced from WNA). Since the inception of this database some of the coordinates were manually corrected using Wikipedia/GeoHack and/or satellite imagery from Google Maps;
- the operational [Akademik Lomonosov-1](https://www.world-nuclear.org/reactor/default.aspx/AKADEMIK%20LOMONOSOV-1) and [2](https://www.world-nuclear.org/reactor/default.aspx/AKADEMIK%20LOMONOSOV-2) reactors (Russia) and planned Bohai Shipyard FNPP and Jiaodong Shipyard FNPP (China) reactors are floating nuclear power plants thus the coordinates from this database may not necessarily indicate their current location.

## Usage
    SELECT npp.`id`
        , npp.`name`
        , npp.latitude
        , npp.longitude
        , c.`name` 'country'
        , s.type 'status'
        , r.type 'reactor_type'
        , npp.reactor_model
        , npp.construction_start_at
        , npp.operational_from
        , npp.operational_to
    FROM nuclear_power_plants npp
    INNER JOIN countries AS c ON npp.country_code = c.`code`
    INNER JOIN nuclear_power_plant_status_type AS s ON npp.status_id = s.id
    LEFT OUTER JOIN nuclear_reactor_type AS r ON npp.reactor_type_id = r.id
    ORDER BY npp.`id`

## License
The GeoNuclearData database is made available under the Open Database License whose full text can be found at https://opendatacommons.org/licenses/odbl/1.0/.
 
Any rights in individual contents of the database are licensed under the Database Contents License whose full text can be found at https://opendatacommons.org/licenses/dbcl/1.0/.
 
## Sources
Countries data is taken from [Unicode Common Locale Data Repository](https://github.com/unicode-org/cldr-json/blob/master/cldr-json/cldr-localenames-full/main/en/territories.json).  
Nuclear power plants data is taken from [WNA](http://www.world-nuclear.org/information-library/facts-and-figures/reactor-database.aspx)/[IAEA](https://www.iaea.org/pris/), but some other sources are used, e.g., [Wikipedia](https://en.wikipedia.org/wiki/List_of_nuclear_power_stations).  

WNA data is also taken from the IAEA PRIS reactor database, with more recent information added if available ([see here](https://www.world-nuclear.org/information-library/facts-and-figures/reactor-database-guide.aspx)).

## Showcase
- [uRADMonitor - Global Environmental Monitoring Network](http://www.uradmonitor.com).
