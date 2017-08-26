Mumbai, India

https://www.openstreetmap.org/node/16173235
https://mapzen.com/data/metro-extracts/metro/mumbai_india/
Mumbai is of my hometown, so I’m more interested to see what database querying reveals, and I’d like an opportunity to contribute to its improvement on OpenStreetMap.org.

Problems Encountered in the Map

After running the audit script from lesson 6 against my chosen area I realized that I should change the regular expression to find the first word of the street name, and not the last. That’s because the language in this map area is Portuguese. After that it was possible to list all sorts of unusual streets. Looking at the names and street types I discovered that there are some abbreviated names. So I modified the shape_element function to correct these abbreviations. Basically all instances were corrected from “Av” or “Av.” to “Avenida”, which is the Portuguese for “Avenue” and also “R.” to “Rua”, which means “Street”.
Inconsistent postal codes (“NC28226”, “28226­0783”, “28226”)

“Incorrect” postal codes 

After listing all map postcodes using the script print_postcodes.py I have found that almost all of them follow the postal code format 00000-000 but some of them were in the wrong format as you can see in the sample below:

...
90030-010
93216-120
93510-310 ÔÇÄ
90230091
92500-000
92410350
92020-970
...
So using regular expressions I manage to correct these postal codes to the correct format by replacing the original value by the first 5 digits followed by “-” and the others 3 digit. After that the osm.json file was generated and imported into a MongoDB collection using the following command:

> mongoimport -d poa -c poa --file porto-alegre_brazil.osm.json
I also noticed that the osm data extracted with the mapzen metro extracts tool contains other cities besides the chosen one. In fact that’s because this tool extracts all the data within a box. So it was found nodes and ways of other cities around Porto Alegre while executing the MongoDB queries.