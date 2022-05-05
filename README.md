# sampling_data

#!/bin/bash

download the weather excel file

`wget https://github.com/labusiam/dataset/raw/main/weather_data.xlsx` 

convert every sheet into their own csv files

`in2csv weather_data.xlsx --sheet "weather_2014" > weather_2014.csv` 
`in2csv weather_data.xlsx --sheet "weather_2015" > weather_2015.csv`

merge both of the newly generated csv files

`csvstack weather_2014.csv <(tail +1 weather_2015.csv) > weather.csv`

remove the weather excel file

`rm weather_data.xlsx`

sampling of the file 'weather.csv' with 0.3 rate, removing the comma in the year, removing '| ', replacing the excess spaces with one space, and replacing the single space to comma, so that the file will be recognized properly 

`csvlook weather.csv | sample -r 0.3 | sed 's/,//g' | sed 's/| //g' | sed 's/|//g' | sed 's/  */ /g' | sed 's/ /,/g' > weather_sample.csv`


