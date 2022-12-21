# google-hotels-scrapper
This project was created as a prerequisite to another machine learning project, in order to gather hotels data and their reviews, to train a machine learning model that can classify a review as either positive, negative or neutral.

# Files and workflow
This project is made up of multiple scripts, each does a job to produce a file that will be needed as the next script's input, It's this way because there were phases that took somewhat of a long time so I had to do multiple programs so that I could complete the phases of data collection one by one, and not all at once, because I'm busy haha.

I know this may seem a bit vague but hopefully this file listing clears everything :

## ./scrapper/page_downloader.py
This script basically opens these 2 websites in firefox using selenium and the firefox driver :
- https://www.google.com/travel/hotels/Tangier
- https://www.google.com/travel/hotels/Marrakesh

These 2 webpages hold the hotels that exist in Tangier and Marrakesh, then for each webpage does the following :
- Click the sort by number of reviews button.
- Scroll down for 1 minute to load more hotels.
- Get the div tag that holds inside it the necessary html that contains each hotel's data (e.g. name, link...).
- Download put that div in an html file for later scrapping.

Then by the end of the script you end up with **./scrapper/data/html_source/marakesh.html** and **./scrapper/data/html_source/tangier.html**.

## ./scrapper/hotel_basic_data_scrapper.py
This script takes the 2 previously generated files **./scrapper/data/html_source/marakesh.html** and **./scrapper/data/html_source/tangier.html**
, then for each hotel in each file it gets the basic data then generates 2 csv files **./data/csv_data/images.csv** and **./data/csv_data/hotels.csv**, and of course as the name suggests, one files holds the images for each hotel, and the other holds basic information such as name, price, link (for later use and serves as a primary/foreign key reference for now) and city.

## ./scrapper/ratings_downloader.py
This script reads each hotel's link from **./scrapper/csv_data/hotels.csv** and then opens the page with selenium just like earlier with **./scrapper/page_downloader.py**, clicks the reviews button to show the reviews and then scrolls down for 1 minute then downloads each hotels ratings' page in this format : **./scrapper/data/html_source/i.html** -> where **i** is a number that starts from 1 and increments for each file (e.g. 1.html, 2.html...300.html...), for me it produced arround 300 files because I scrapped arround 300 hotels.

## Other files will be added later 
