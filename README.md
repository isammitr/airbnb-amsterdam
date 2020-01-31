# Exploring the Airbnb Amsterdam Dataset
## Project Motivation
Amsterdam has always been one of the cities that I want to visit. The houses, the canals, the
tulips, the weather have always attracted me when I see any photos of Amsterdam. While going
through the [Airbnb's Open-Sourced Datasets website](http://insideairbnb.com/get-the-data.html), the first name I across was `Amsterdam`.
Without any further thinking I downloaded the dataset and started to explore it.

## Python Libraries Used:
- [pandas](https://pandas.pydata.org), [numpy](https://numpy.org), [matplotlib](https://matplotlib.org), [seaborn](https://seaborn.pydata.org)
- [sklearn](https://scikit-learn.org/stable/), [statsmodels](http://www.statsmodels.org/stable/index.html) 
- [NLTK's SentimentIntensityAnalyzer](https://www.nltk.org/api/nltk.sentiment.html#module-nltk.sentiment.vader)

## Files Description:
- **airbnb-amsterdam.ipynb**: The jupyter notebook with documented code.
- **airbnb-amsterdam.html**: HTML file that can be downloaded and viewed with any browser.
- I'm not uploading the dataset as there are three data files and they are large. But the data-set is available [here](http://insideairbnb.com/get-the-data.html). The dataset files I which I have used are:
    1. **listings.csv**: Detailed Listings data for Amsterdam
    2. **calendar.csv**: Detailed Calendar Data for listings in Amsterdam
    3. **reviews.csv**: Detailed Review Data for listings in Amsterdam
    - Unfortunately, there is no data dictionary availble for the dataset description, but the column names are easily understood.

## Understanding the Business:
[Airbnb](https://www.airbnb.co.in) is a website where users can host their homes and rent others' homes for stays and vacations. Even though the company does not any homes they receive a brokerage when users rent the places. 

## Understanding the Data:
1. _listings.csv_: This dataset contains the detailed information about the hosts, their properties, property's description, neighbourhoods, cancellation policies, room types, area, the rent prices, etc.
2. _calendar.csv_: This dataset contains the availability of the property for each date from Dec 2019 to Dec 2020, it's prices, and minimum & maximum nights conditions for each listing in the _listings_ dataset
3. _reviews.csv_: This dataset contains the **available** reviews, reviewer name, date of the review for each listing in the _listings_ dataset.

## Preparing the Data:
- The columns in the listings dataset, which contained more than 12% of missing or unknown values (NaNs) were removed from the dataset becuase such a large number of missing values would cause the dataset to misguide the results. Further, rows containing any missing or unknown values were also dropped.
- Most of the columns were dropped on manual inspection of each column and intuition, because I felt that using my knowledge that these columns would not be much helpful for me in any analysis.
- Some columns contained `t` and `f` for true and false, which were converted to boolean type.
- The `price` column was a string column which was converted to float by removing the '$'
sign.
- Dataset was also checked for duplicate rows and unique IDs.

## Data Modeling:
- Multiple Regression model was built to predict the `price` of the property based on several explanatory variables.
- The Mean Absolute Error of the model came to be 52.66 which suggests that:
    - that our predicted price is 52.66 units near to the actual price
    - i.e. (predicted_price-52.66) < actual_price < (predicted_price+52.66)
- Multiple Regression was performed not only with `sklearn` but also using `statsmodels.api`'s Ordinary Least Squares (OLS)', because the output table of `statsmodels.api` is more detailed.
- Also NLTK's Sentiment Intensity Analyser was also used to calculate the sentiment score of the users' reviews.

## Evaluating the Results - Summary:
### Q1. Search the top 5 factors affecting which cause the rise in rent prices:
From the `statsmodels.api` OLS model output table, the columns with positive coefficients and higher values are the factors that affect in the price rise. Thus the top 5 factors due to which the Price increases are:
- latitude & longitude: The Location of the Property
- property_type_Lighthouse: the hosted property is a Lighthouse or in the vicinity of a Lighthouse, the price will be higher.
- property_type_Aparthotel: if the hosted property is an Apartment Hotel i.e. the user gets a homely feel with the facilities of an hotel, the price will be higher.
- bathrooms & bedrooms: the more the number of bathrooms and bedrooms, the price will be higher.
- instant_bookable: if the User is able to book the property instantly, the price will be higher.

### Q2. Find the Peak Season and Off Season for the year 2020
It is evident from the figure that `April to July` is the `peak season` with average price ranging from  `$170` to `$174` and `January to March` are comparatively `lower` with average price ranging from  `$163 to $165`. The [Tulips bloom](https://rove.me/to/amsterdam) during this period from April to June, and further the weather must be pleasant which can be reasons for the peak season. 

### Q3. Find the Top Hosts based on User Reviews and Top Hosts' neighbourhood
The sentiment score was calculated based on the reviews, and the top hosts (only based on user reviews) are: 

| Rank | Host Name | Neighbourhood            | Sentiment Score |
|------|-----------|--------------------------|-----------------|
| 1    | Laila     | Westerpark               | 0.9977          |
| 2    | Karen     | Centrum-Oost             | 0.9972          |
| 3    | Emelie    | De Baarsjes - Oud-West   | 0.9972          |
| 4    | Elif      | IJburg - Zeeburgereiland | 0.9971          |
| 5    | Joren     | De Pijp - Rivierenbuurt  | 0.9970          |

So now you know, when and where to book in Amsterdam! :)

**Disclaimer**: This is not an advertisement of any kind.

## Deploying:
- Download the jupyter notebook and the dataset from the source, store all in the same folder and on your terminal, run: `jupyter notebook`
- You can also download the HTML file and open it with any browser to see the jupyter notebook contents

## Acknowledgements:
I have used some answers from http://stackoverflow.com/ for reference. Other references like the official documentations, have been hyperlinked in the above sections wherever mentioned.
