# google-hotels-scraper
This project was created as a prerequisite to another machine learning project, in order to gather hotels data and their reviews, to train a machine learning model that can classify a review as either positive, negative or neutral.

It's basically a python 3 scraper that scraps a few Marakesh and Tangier hotels' names, price, image links and ratings with a label of -1 meaning negative, 0 meaning neutral and 1 meaning it's a positive rating/comment.

# Warning
This project is not maintained so it may not work in the future, however it still serves as good learning material on web scraping.

# Files and Directories
[scraper](https://github.com/techguyseli/google-hotels-scraper/tree/main/scraper) : This directory contains the actual python scripts, the firefox driver that the scripts use, the downloaded html pages and the cleaned csv data.

[requirements.txt](https://github.com/techguyseli/google-hotels-scraper/blob/main/requirements.txt) : This file contains the dependencies needed for the python scripts to run.

# Usage
Open a terminal from this directory (the root of this git repository), move to the [scraper](https://github.com/techguyseli/google-hotels-scraper/tree/main/scraper) directory:
```bash
cd scraper

```

Download the dependencies in [requirements.txt](https://github.com/techguyseli/google-hotels-scraper/blob/main/requirements.txt) either globaly or using a python virtual environment (this project was writen in python 3.10.8):
```bash
pip install -r requirements.txt
```

Then run these scripts (if needed) in this exact order :

This script downloads 2 html pages that contain all the basic data of a few Marakesh and Tangier hotels, it takes a couple of minutes to run :
```bash
python page_downloader.py 
```

This script scraps basic hotel data (such as the hotel link that will later be used to scrape each hotel's ratings, the name, price, a few images' links, etc) from the 2 downloaded html pages and then produces 2 unclean csv files, one contains hotel data, and one contains hotel images : 
```bash
python hotel_basic_data_scraper.py
```

For each hotel in the hotels csv file that the previous script created, this script takes the hotel's link, opens it in the firefox driver, selects the reviews page and then scrolls for 1 minute to load as much reviews as possible, then downloads that reviews' page as an html page, so you end up with as much html files as there are hotels.
This script takes a lot of time to finish (it took me 5 hours), but of course you can stop it at any time by pressing CTRL + c in the terminal :
```bash
python ratings_downloader.py
```

This next script goes through each hotel's ratings html page that was downloaded by the previous script, then scrapes the rating's comment, and adds a label depending on the actual rating number (e.g. 4/5 becomes 1, meaning it's a positive review, 1/5 becomes -1, meaning it's a negative review, etc) :
```bash
python ratings_scraper.py
```

This next script creates the final cleaned data files that are ready for use : 
- [cleaned_hotels.csv](https://github.com/techguyseli/google-hotels-scraper/blob/main/scraper/data/csv_data/cleaned_hotels.csv)
- [cleaned_images.csv](https://github.com/techguyseli/google-hotels-scraper/blob/main/scraper/data/csv_data/cleaned_images.csv)
- [cleaned_ratings.csv](https://github.com/techguyseli/google-hotels-scraper/blob/main/scraper/data/csv_data/cleaned_ratings.csv)
```bash
python clean_data.py
```


