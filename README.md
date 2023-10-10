# Wikipedia Pageviews API Data Analysis

## Background

Wikipedia has an API called Pageviews, which provides access to traffic data to Wikipedia. By connecting to an API endpoint, users can extract different kinds of information, such as the number of views of an article per month or per day.

## Goal

The goal for this project is to perform an exploratory data analysis using the Pageviews API data. We construct a dataset through repeated API calls, then load the dataset to perform exploratory data analysis. After doing several analysis tasks, the dataset will get published in a repository and include supporting documentation (including this very README file) to guide others on reproducing my results. This is a project not only on data analysis of the Pageviews API, but also an exercise in reproducibility.

## Licenses

According to MediaWiki REST API, articles from the English Wikipedia may be used under the Creative Commons Attribution Share-Alike license. For more information, you can read about their terms of use [here](https://www.mediawiki.org/wiki/API:REST_API#Terms_and_conditions)

## Relevant Input Files

To generate the the JSON files within the notebook, I used several API calls from the [Pageviews API](https://wikimedia.org/api/rest_v1/#/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end). For more information, the API's documentation can be found [here](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews).
The API calls were specifically used for Academy award-winning movies, which are listed in the following [CSV file](thank_the_academy.AUG.2023.csv), located in this very repository.

## Relevant Output Files

When generating the dataset, three separate JSON output files are created:

1. <academy_monthly_mobile_201507-202310.json> is a JSON file that contains monthly mobile pageviews for each article depicting an Academy Award-winning movie, from July 2015 through September 2023.
2. <academy_monthly_desktop_201507-202310.json> is a JSON file that contains monthly desktop pageviews for each article depicting an Academy Award-winning movie.
3. <academy_monthly_cumulative_201507-202310> is a JSON file that contains monthly cumulative pageviews for each article depicting an Academy Award-winning movie. That is, it is the sum of desktop and mobile views.

Each JSON file contains nested data pertaining to each movie. Each tag represents a movie, and for each movie, there are months of pageview counts for that particular movie article. Each of these individual months are structured in the same way, as a set of distinct tags. They include:
- project: This represents the particular domain of the Wikimedia Project we used for our API call. In this case, we used 'en.wikipedia.org'
- article: This is a URI encoded string that represents the title of the Wikipedia article
- granularity: This represents the frequency of the view counts. In this case, we chose "monthly" to get monthly view counts
- timestamp: This represents the particular month that the view count information was recorded for
- agent: This represents the method in which this webpage was retrieved, either through user input or automated input. We are only concerned with user input in this case
- views: This is the raw count of page views for that article in that particular month

My analysis from this data outputs three image files in this repository as well:
1. <MinMaxAvgViewership.png> is a PNG file of a plot produced using Matplotlib. The plot shows a time series for the articles with the highest average mobile traffic, highest average desktop traffic, lowest average mobile traffic, and lowest average desktop traffic.
2. <PeakViewership.png> is another PNG file of a plot produced using Matplotlib. The plot shows a time series for the top 10 articles with the highest peak monthly page views, for both mobile and desktop access.
2. <MostRecentWinners.png> is a PNG created through Matplotlib, and it shows a time series of the 10 articles with the fewest months of available data, for both mobile and desktop access.

## Special Considerations
My Jupyter notebook version is 6.5.2, and it utilizes Python version 3.9.16. Make sure to check the version that you are running under to make sure that the functions are compatible.
Finally, when generating the JSON files, be wary of the time it takes to generate them. Since we are utilizing over 1300 API calls to generate each JSON file, it will take around 10 minutes to run each to their entirety.