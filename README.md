
# CFPB Twitter Analysis

The project examines all tweets from February 3, 2011 to October 8, 2020 from the following Twitter page:

 - **[CFPB](https://twitter.com/CFPB?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)**

**Data Sources**

This project analyzes the Consumer Financial Protection Bureau's (CFPB) Twitter data. The CFPB Twitter data was collected and acquired from the [Social Feed Manager](https://library.gwu.edu/scholarly-technology-group/social-feed-manager).


## Analysis and Visualization

### Tweet type

![](https://github.com/dz777/twitter-analysis/tree/main/Images/1tweet_type_ratio.png)

https://github.com/dz777/twitter-analysis/tree/main/Images

<img src="images/1tweet_type_ratio.png">

Based on the pie chart above, we can see that roughly two-thirds of the tweets from the @CFPB page were original tweets. Almost one-third were replies to others, only a very small percentage (2.81%) were retweets, and 0.28% were quotes. 

### Hashtags


```python
# Counting the total number of tweets by hashtag
hashtag_totals = twitter['hashtags'].value_counts()
# Checking first 5
hashtag_totals.head()
```




    KnowBeforeYouOwe     150
    MoneyAsYouGrow       133
    StudentDebtStress    112
    MoneyTalk             92
    AskCFPB               89
    Name: hashtags, dtype: int64


```python
# import WordCloud package
from wordcloud import WordCloud
# create word cloud of hashtags, edit specifications
wc_ = WordCloud(width=800, height=400, 
                 background_color ='white', max_words=120).generate_from_frequencies(wc)
# adjust size, improve visualization, show graph
plt.figure(figsize=(8, 5))
plt.imshow(wc_, interpolation='bilinear')
plt.axis('off')
plt.tight_layout()
# saving image
plt.savefig('2hashtag_wc.png')
```


![png](output_24_0.png)


The word cloud visually shows the frequency of the used hashtags from the Twitter dataset. #KnowBeforeYouOwe, #MoneyAsYouGrow, and #StudentDebtStress were most frequently used and likely point toward their focus as an organization, such as about thinking before borrowing, regarding student debt, and saving up money. They were closely trailed by #MoneyTalk, #AskCFPB, and #CFPW2020.



### Days of week


```python
# creating column day_of_week and fill it with parsed date tweet was created
twitter['day_of_week'] = twitter.parsed_created_at.dt.day_name()
# creating list of the names of the day of the week
day_names = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
# groups and counts by day of week, reset index
out = twitter.groupby('day_of_week').count().reindex(day_names).reset_index()
# checking output
out
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>day_of_week</th>
      <th>id</th>
      <th>tweet_url</th>
      <th>created_at</th>
      <th>parsed_created_at</th>
      <th>text</th>
      <th>tweet_type</th>
      <th>hashtags</th>
      <th>media</th>
      <th>urls</th>
      <th>...</th>
      <th>in_reply_to_user_id</th>
      <th>retweet_count</th>
      <th>retweet_or_quote_id</th>
      <th>retweet_or_quote_screen_name</th>
      <th>retweet_or_quote_user_id</th>
      <th>source</th>
      <th>user_favourites_count</th>
      <th>user_followers_count</th>
      <th>user_listed_count</th>
      <th>user_statuses_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Monday</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
      <td>673</td>
      <td>538</td>
      <td>1452</td>
      <td>...</td>
      <td>570</td>
      <td>1766</td>
      <td>37</td>
      <td>37</td>
      <td>37</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
      <td>1766</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tuesday</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
      <td>820</td>
      <td>628</td>
      <td>1669</td>
      <td>...</td>
      <td>618</td>
      <td>2105</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
      <td>2105</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wednesday</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
      <td>839</td>
      <td>638</td>
      <td>1831</td>
      <td>...</td>
      <td>555</td>
      <td>2174</td>
      <td>93</td>
      <td>93</td>
      <td>93</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
      <td>2174</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thursday</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
      <td>835</td>
      <td>693</td>
      <td>1745</td>
      <td>...</td>
      <td>457</td>
      <td>2079</td>
      <td>85</td>
      <td>85</td>
      <td>85</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
      <td>2079</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Friday</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
      <td>600</td>
      <td>607</td>
      <td>1563</td>
      <td>...</td>
      <td>512</td>
      <td>1850</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
      <td>1850</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Saturday</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
      <td>332</td>
      <td>437</td>
      <td>726</td>
      <td>...</td>
      <td>35</td>
      <td>747</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
      <td>747</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Sunday</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
      <td>165</td>
      <td>282</td>
      <td>418</td>
      <td>...</td>
      <td>32</td>
      <td>434</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
      <td>434</td>
    </tr>
  </tbody>
</table>
<p>7 rows × 23 columns</p>
</div>




```python
# names of columns from variable out
out.columns
```




    Index(['day_of_week', 'id', 'tweet_url', 'created_at', 'parsed_created_at',
           'text', 'tweet_type', 'hashtags', 'media', 'urls', 'favorite_count',
           'in_reply_to_screen_name', 'in_reply_to_status_id',
           'in_reply_to_user_id', 'retweet_count', 'retweet_or_quote_id',
           'retweet_or_quote_screen_name', 'retweet_or_quote_user_id', 'source',
           'user_favourites_count', 'user_followers_count', 'user_listed_count',
           'user_statuses_count'],
          dtype='object')




```python
# creating subplots of metrics per day of the week, removing extra
fig, axs = plt.subplots(nrows=4, ncols=2, figsize=(15,12))
axs = axs.flatten()
axs[-1].remove()

# columns
labels = ['id', 'hashtags', 'media','in_reply_to_screen_name', 'in_reply_to_status_id',
       'in_reply_to_user_id', 'retweet_or_quote_id']
# saving selected columns into dat for bar graphs
dat = out[labels]
# tightening up, setting colors, labels, title, ticks in bar graphs
fig.tight_layout()
colors =  ['#129845','#271254', '#FA4411', '#098765', '#000009', '#FA4568', '#123456']
for col, ax, c in zip(labels, axs, colors):
    dat[col].plot.bar(ax=ax, color=c)
    ax.set_title(col)
    ax.set_xticklabels(out.day_of_week.values, rotation=0)
#adjusting, setting title and spacing    
fig.subplots_adjust(top=0.92)
fig.suptitle("Per Days of the Week", fontweight='bold')
fig.subplots_adjust(hspace=0.3)

# saving image
plt.savefig('3days_of_week.png')
```


![png](output_30_0.png)


The bar graphs give an overview of the activity based on the days of the week. The weekend was clearly not as active when compared to Tuesday-Thursday. Furthermore, the retweet and quote id were the least active, overall, particularly on Sunday.


```python
# finding percentage/ratio of hashtags
# creating variable favs of the sorted order of the sum of favorite_count, grouped by hashtag
favs = twitter.groupby('hashtags').favorite_count.sum().sort_values(ascending=False)

# MOST USED HASHTAGS
# most_hashtag = twitter['hashtags'].value_counts().reset_index(name='count')
# most_hashtag.head

# calculating the percentage
favs = favs/favs.sum()*100
# checking
favs
```




    hashtags
    MoneyAsYouGrow                                      4.010417
    mortgages knowbeforeyouowe                          3.553241
    KnowBeforeYouOwe                                    2.129630
    4Years4You                                          2.048611
    mortgage                                            1.950231
    ConsumersCount                                      1.921296
    prepaid                                             1.892361
    EndDebtTraps                                        1.527778
    ShopMortgage                                        1.452546
    StudentDebtStress                                   1.412037
    Harvey                                              1.278935
    debtcollection                                      1.192130
    studentloan                                         1.180556
    autoloan                                            1.070602
    arbitration                                         1.030093
    CFPW2020                                            0.873843
    Equifax                                             0.862269
    debt                                                0.839120
    AutoLoan                                            0.815972
    FindYourPlace                                       0.769676
    studentloans                                        0.752315
    OwningAHome                                         0.729167
    creditcard                                          0.711806
    MoneyTalk                                           0.648148
    SocialSecurity                                      0.648148
    creditreport                                        0.613426
    studentdebt                                         0.601852
    KidsTalkMoney                                       0.555556
    Fraud                                               0.520833
    FinancialLiteracyMonth                              0.468750
                                                          ...   
    CFPW2020 HMDA                                       0.000000
    COVID19                                             0.000000
    COVID19 coronavirus                                 0.000000
    COVIDreliefIRS IRS                                  0.000000
    CallForPapers                                       0.000000
    milchat DebtCollection                              0.000000
    CharityFraudOut                                     0.000000
    medicaldebt                                         0.000000
    hurricane HurricaneFlorence                         0.000000
    Coronavirus                                         0.000000
    hogar familia                                       0.000000
    followfriday                                        0.000000
    CreditMistakes                                      0.000000
    CreditReporting FinancialCapabilityMonth AskCFPB    0.000000
    FCCLive                                             0.000000
    elderly                                             0.000000
    elderfinancialfraud BCFPtownhall                    0.000000
    creditscores CreditReport                           0.000000
    creditfreezes                                       0.000000
    credit healthcare                                   0.000000
    caregiving                                          0.000000
    DebtCollector                                       0.000000
    IRS COVID19                                         0.000000
    DisasterPrepardness                                 0.000000
    DominoEffect NCPW                                   0.000000
    USCMWinter                                          0.000000
    TheWarRoom                                          0.000000
    ElderFraud                                          0.000000
    StudentLoan StudentDebtStress Thunderclap           0.000000
    2020Resolution                                      0.000000
    Name: favorite_count, Length: 858, dtype: float64




```python
#favs = favs[favs>1]
#favs.loc['others'] = 100 - favs.sum()

# selecting top 10 favorite hashtags
favs = favs[:10]
# checking
favs
```




    hashtags
    MoneyAsYouGrow                4.010417
    mortgages knowbeforeyouowe    3.553241
    KnowBeforeYouOwe              2.129630
    4Years4You                    2.048611
    mortgage                      1.950231
    ConsumersCount                1.921296
    prepaid                       1.892361
    EndDebtTraps                  1.527778
    ShopMortgage                  1.452546
    StudentDebtStress             1.412037
    Name: favorite_count, dtype: float64




```python
# creating variable other, which is the percentage of other than the top 10 hashtags 
others = 100 - favs.sum()  
# checking
others
```




    78.10185185185185




```python
# plotting ratio of top hashtags overall and ratio of top hashtags among themselves
figs, axes = plt.subplots(1,2, figsize=(12,7))
# creates a barplot from dataframe favs, turns off the grid parameter
favs.plot(ax=axes[0], kind='bar', grid=False)
# on axis 1, creates a pie chart of favs, labels are favs index, autopct is a function 
# that changes the input values to a percentage string for display 
axes[1].pie(favs, autopct=lambda x: f'{x:.2f}%', startangle=0, labels=favs.index) 

# setting title and labels
axes[0].set_title("Ratio of top 10 hashtags overall", fontweight='bold')
axes[1].set_title("Distribution/ratio of top 10 hashtags among themselves", fontweight='bold')
axes[0].set_ylabel("Percentage")
axes[0].set_xlabel("Top 10 hashtags")

plt.show()

# saving image
plt.savefig('4hashtag_pct.png')
```


![png](output_35_0.png)



    <Figure size 432x288 with 0 Axes>


Overall, the top 10 hashtags account for around 22% of the total hashtags. The hashtags in the "others" (those below the top 10) account for around 78% of the hashtags. 

Among these top 10 hashtags only, #MoneyAsYouGrow accounts for around 18%, the hashtags #knowbeforeyouowe with regards to #mortgages accounts for around 16%, and #KnowBeforeYouOwe for around 10%. 


```python
# finding mentions of Experian, Transunion, Equifax, JPMorgan, and Capital One
twitter['Experian'] = twitter['text'].str.lower().str.contains('experian') 
twitter['Transunion'] = twitter['text'].str.lower().str.contains('transunion') 
twitter['Equifax'] = twitter['text'].str.lower().str.contains('equifax') 
twitter['JPMorgan'] = twitter['text'].str.lower().str.contains('jpmorgan')
twitter['Capital One'] = twitter['text'].str.lower().str.contains('capital one') 

# counting each mention of experian, transunion, equifax, jpmorgan, and capital one
credit_bureaus_count = twitter[['Experian', 'Transunion', 'Equifax', 'JPMorgan','Capital One']].sum(axis=0).reset_index(name='Count')
credit_bureaus_count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Experian</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Transunion</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Equifax</td>
      <td>32</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JPMorgan</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capital One</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# creating circle/donut plot break down of the selected credit_bureaus
# (https://medium.com/@kvnamipara/a-better-visualisation-of-pie-charts-by-matplotlib-935b7667d77f)
credit_bureaus_count.Count.plot.pie(autopct=lambda x: f'{x:.2f}%', figsize=(9,9), labels =credit_bureaus_count["index"] )
# plot, configure, and draw a white circle over the center of the plot
circle = plt.Circle((0,0),0.70,fc='white') 
fig = plt.gcf() 
fig.gca().add_artist(circle)
plt.ylabel("")
plt.title("Ratio of mentions of five companies", fontweight='bold')
plt.savefig('5hashtag_pct.png')
```


![png](output_38_0.png)


Consumers often have complaints about the credit bureaus or large banks. In fact, companies such as Equifax have gone through very public issues like the 2017 data breach, which may have been reflected in this dataset. After checking to see how often there were mentions of "Equifax," "JPMorgan," "Experian," "Transunion," and "Capital One," it was not surprising to see that Equifax was holding the number one spot among these companies, representing around 56% of the mentions among these. Another credit agency called Experian was in second, followed by JPMorgan with around 14%. This is followed by another credit agency called Transunion with almost 9%, and then Capital One with around 7%.   

### Loading for text analysis


```python
twitter_df = pd.read_csv('Twitter_Data.csv')
```


```python
# (https://github.com/lisanka93/text_analysis_python_101/blob/master/Dummy%20movie%20dataset.ipynb)
# importing relevant packages
import re
from nltk.stem import WordNetLemmatizer, PorterStemmer, SnowballStemmer
from nltk.corpus import stopwords

# setting stop words
stop_words = set(stopwords.words('english'))

def preprocess(raw_text):
    
    # regular expression removing links
    no_links_text = re.sub("((https|http|www)[\S]*)", " ", raw_text)
    
    # regular expression keeping only letters 
    letters_only_text = re.sub("[^a-zA-Z]", " ", no_links_text)

    # convert to lower case and split into words 
    # convert string into list 
    words = letters_only_text.lower().split()

    cleaned_words = []
    lemmatizer = PorterStemmer()
    
    # remove stopwords
    for word in words:
        if word not in stop_words:
            cleaned_words.append(word)
    
    # stemm/lemmatize
    stemmed_words = []
    for word in cleaned_words:
        word = lemmatizer.stem(word)
        stemmed_words.append(word)
    
    # converting list back to string
    return " ".join(stemmed_words)
```


```python
# cleaning text
# making a new column 'prep', taking all twitter_df text, apply preprocess function
# removing stop words, stemming words, lemmatizing words and returning as string
twitter_df['prep'] = twitter_df['text'].apply(preprocess)
twitter_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>tweet_url</th>
      <th>created_at</th>
      <th>parsed_created_at</th>
      <th>user_screen_name</th>
      <th>text</th>
      <th>tweet_type</th>
      <th>coordinates</th>
      <th>hashtags</th>
      <th>media</th>
      <th>...</th>
      <th>user_followers_count</th>
      <th>user_friends_count</th>
      <th>user_listed_count</th>
      <th>user_location</th>
      <th>user_name</th>
      <th>user_statuses_count</th>
      <th>user_time_zone</th>
      <th>user_urls</th>
      <th>user_verified</th>
      <th>prep</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>822149266269470720</td>
      <td>https://twitter.com/CFPB/status/82214926626947...</td>
      <td>Thu Jan 19 18:30:34 +0000 2017</td>
      <td>2017-01-19 18:30:34+00:00</td>
      <td>CFPB</td>
      <td>Check out these 6 steps to avoid overdraft fee...</td>
      <td>original</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
      <td>check step avoid overdraft fee</td>
    </tr>
    <tr>
      <th>1</th>
      <td>822142084480045056</td>
      <td>https://twitter.com/CFPB/status/82214208448004...</td>
      <td>Thu Jan 19 18:02:02 +0000 2017</td>
      <td>2017-01-19 18:02:02+00:00</td>
      <td>CFPB</td>
      <td>If you’re thinking about buying a home, RT and...</td>
      <td>original</td>
      <td>NaN</td>
      <td>ShopMortgage</td>
      <td>NaN</td>
      <td>...</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
      <td>think buy home rt read blog learn shopmortgag</td>
    </tr>
    <tr>
      <th>2</th>
      <td>822097194266271750</td>
      <td>https://twitter.com/CFPB/status/82209719426627...</td>
      <td>Thu Jan 19 15:03:39 +0000 2017</td>
      <td>2017-01-19 15:03:39+00:00</td>
      <td>CFPB</td>
      <td>Have you been wrongfully billed for Medicare c...</td>
      <td>original</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://pbs.twimg.com/media/C2itCZgXAAAzsvz.jpg</td>
      <td>...</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
      <td>wrong bill medicar cost learn</td>
    </tr>
    <tr>
      <th>3</th>
      <td>822085279116890112</td>
      <td>https://twitter.com/CFPB/status/82208527911689...</td>
      <td>Thu Jan 19 14:16:18 +0000 2017</td>
      <td>2017-01-19 14:16:18+00:00</td>
      <td>CFPB</td>
      <td>@JustinKramm_SF If you would like to submit a ...</td>
      <td>original</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
      <td>justinkramm sf would like submit credit card c...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>822085060824367104</td>
      <td>https://twitter.com/CFPB/status/82208506082436...</td>
      <td>Thu Jan 19 14:15:26 +0000 2017</td>
      <td>2017-01-19 14:15:26+00:00</td>
      <td>CFPB</td>
      <td>@JustinKramm_SF Thank you for your question. Y...</td>
      <td>reply</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
      <td>justinkramm sf thank question learn unauthor c...</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 38 columns</p>
</div>




```python
# most common words
from collections import Counter
Counter(' '.join(twitter_df['prep']).split()).most_common(10)
```




    [('us', 2907),
     ('help', 2211),
     ('financi', 2068),
     ('thank', 1967),
     ('complaint', 1503),
     ('share', 1370),
     ('learn', 1232),
     ('submit', 1199),
     ('cfpb', 1137),
     ('resourc', 1134)]




```python
# WorldCloud
#from wordcloud import WordCloud

all_words = '' 

# looping through incidents, join them to one text, extract most common words
for arg in twitter_df["prep"]: 

    tokens = arg.split()  
      
    all_words += " ".join(tokens)+" "

wordcloud = WordCloud(width = 700, height = 700, 
                background_color ='black', 
                min_font_size = 10).generate(all_words) 
  
# plotting worldcloud                      
plt.figure(figsize = (8, 10), facecolor = None) 
plt.imshow(wordcloud) 
plt.axis("off") 
plt.tight_layout(pad = 0) 
  

plt.savefig('6cleaned_wc.png')

plt.show()
```


![png](output_45_0.png)


Cleaning and preparing the data such as through the use of stop words allows us to get a more accurate understanding of the data and text itself. Not surprisinly, the most common text appears to be about submitting complaints which is expected since the CFPB has a very large complaints database that is regularly updated and consulted. What is interesting is that phrases such as "thank," "reach," "contact," "share," and "submit" are engaging and clear calls to actions, signaling that the CFPB appear to be trying to engage with their audience. 

### Number of tweets


```python
# overall number of tweets per year
pd.to_datetime(twitter_df['parsed_created_at']).dt.year.value_counts()
```




    2018    2171
    2019    1765
    2016    1612
    2017    1344
    2015    1240
    2020    1127
    2013     582
    2012     482
    2011     480
    2014     352
    Name: parsed_created_at, dtype: int64




```python
# total favorited tweets by year
twitter_df['parsed_created_at'] = twitter_df['parsed_created_at'].astype('datetime64')
twitter_df.groupby([twitter_df['parsed_created_at'].dt.year])['favorite_count'].sum()
```




    parsed_created_at
    2011      350
    2012      750
    2013     1146
    2014     1342
    2015     5844
    2016    10646
    2017     6649
    2018     3469
    2019     3411
    2020     3003
    Name: favorite_count, dtype: int64




```python
# saving total tweet count
tweet_count = pd.to_datetime(twitter_df['parsed_created_at']).dt.year.value_counts()
tweet_count = tweet_count.sort_index()
tweet_count
```




    2011     480
    2012     482
    2013     582
    2014     352
    2015    1240
    2016    1612
    2017    1344
    2018    2171
    2019    1765
    2020    1127
    Name: parsed_created_at, dtype: int64




```python
# graphing tweets

# converting 
twitter_df['parsed_created_at'] = twitter_df['parsed_created_at'].astype('datetime64')

# total favorites and retweet count by year
favorites_by_year = twitter_df.groupby([twitter_df['parsed_created_at'].dt.year])["favorite_count"].sum()
retweet_count = twitter_df.groupby([twitter_df['parsed_created_at'].dt.year])["retweet_count"].sum()

# Creating plot, configuring the plot specifications inside the variables fig and ax
fig, ax = plt.subplots(figsize=(14,5))

# Plotting daily variable as a a line plot, set x,y, linewidth, and specifying ax, setting legend
favorite_line = favorites_by_year.plot(kind='line', x='year', y='favorites', linewidth=2, ax=ax, legend=True, label='Favorited tweets')
tweet_count_line = tweet_count.plot(kind='line', x='year', y='favorites', linewidth=2, ax=ax, legend=True, label='Total tweets')
retweet_count_line = retweet_count.plot(kind='line', x='year', y='favorites', linewidth=2, ax=ax, legend=True, label='Retweets')

# Setting x,y label and size
ax.set_xlabel('Year', fontsize=14, fontweight = 'bold')
ax.set_ylabel('Number of', fontsize=14, fontweight = 'bold')

# title and subtitle
ax.text(2011, 16000, "Number of favorited, retweets, and total tweets per year", fontsize=20, fontweight="bold")
ax.text(2011, 15000, "2016 had the highest visibility and engagement", fontsize=15, fontweight="bold", alpha=0.85)

plt.savefig('7tweets_compar.png')
```


![png](output_51_0.png)


The year 2018 had the most number of tweets, overall. Also, the year 2020 had the lowest number of tweets when comparing from 2015 to today. In terms of favorited tweets, 2016 overwhelmingly had the most when compared to the whole time period between 2011 to 2020. In contrast, the year 2011 had the lowest number of favored tweets and this value has never been as low as that after, but rather, in general, has only increased. The year 2014 to 2016 saw a very sharp and significant hike in the number of favorited tweets. With regards to the retweets, it is the most unstable metric, having reached its lowest point in 2011, its highest in 2016, and shifting in between. 

### Retweets


```python
# creating table of retweets & tweet count
# (https://towardsdatascience.com/visualization-of-information-from-raw-twitter-data-part-1-99181ad19c)
# sorting the values of retweet 
retweets_sorted = twitter_df.sort_values(by=['retweet_count'], ascending=False)

# taking the @RT tweets from string and replacing, grouping by aggregate sum and count
# and sorting by descending order, displaying first 10
table = retweets_sorted[['retweet_count','text']].copy()
table.text = table.text.str.extract('(?:RT )(@[\d\w]*:)')
table.text = table.text.str.replace(":", "")
table = table.groupby("text").aggregate(["sum", "count"]).sort_values([("retweet_count", "sum")], ascending=False).head(10)
# creating and finding average retweet per tweet, rounding
table["retweets per tweet"] = table[("retweet_count", "sum")]/table[("retweet_count", "count")]
table.columns = ["Retweets", "Tweet Count", "Retweets per Tweet"]
round(table, 2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Retweets</th>
      <th>Tweet Count</th>
      <th>Retweets per Tweet</th>
    </tr>
    <tr>
      <th>text</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>@fema</th>
      <td>1991</td>
      <td>1</td>
      <td>1991.00</td>
    </tr>
    <tr>
      <th>@FTC</th>
      <td>912</td>
      <td>33</td>
      <td>27.64</td>
    </tr>
    <tr>
      <th>@SBAgov</th>
      <td>885</td>
      <td>7</td>
      <td>126.43</td>
    </tr>
    <tr>
      <th>@Readygov</th>
      <td>783</td>
      <td>6</td>
      <td>130.50</td>
    </tr>
    <tr>
      <th>@IRSnews</th>
      <td>603</td>
      <td>16</td>
      <td>37.69</td>
    </tr>
    <tr>
      <th>@CFPBDirector</th>
      <td>557</td>
      <td>5</td>
      <td>111.40</td>
    </tr>
    <tr>
      <th>@WhiteHouse</th>
      <td>282</td>
      <td>2</td>
      <td>141.00</td>
    </tr>
    <tr>
      <th>@CFPBMilitary</th>
      <td>280</td>
      <td>25</td>
      <td>11.20</td>
    </tr>
    <tr>
      <th>@usedgov</th>
      <td>219</td>
      <td>3</td>
      <td>73.00</td>
    </tr>
    <tr>
      <th>@CNNMoney</th>
      <td>200</td>
      <td>2</td>
      <td>100.00</td>
    </tr>
  </tbody>
</table>
</div>



The table shows some interesting information about the different retweets metrics. For example, the @fema retweet seems to have been the best-performing one. There was one RT (tweet count) of @fema which garnered 1,991 retweets, the highest value, giving it a very impressive performance and competitive average over the others. 


```python
# creating scatterplot of top tweet count and retweets of twitter handles
table.plot.scatter("Tweet Count", "Retweets", figsize=(8,6))
# setting text, esp @CNNMoney so it is legible
for x,y,s in zip(table["Tweet Count"], table["Retweets"], table.index):
    if s == "@CNNMoney":
        plt.text(x-1,y-60,s)
    else:
        plt.text(x+.3,y+10,s)
# title
plt.title("Top 10 Retweeted Twitter Handles: Tweet Count vs. Retweets", fontweight='bold')

plt.savefig('9retweeted.png')
```


![png](output_56_0.png)


The scatterplot depicts the relation between the number of times a specific Twitter handle tweeted, and the number of retweets. As noted above, @fema did very well, having a very low tweet count but a high number of retweets. @CFPBMilitary performed pretty poorly since it had a relatively high tweet count despite a fairly low retweet count in comparison. 


```python
# Printing out 10 highest performing tweets sorted by retweet count
for i in range(10):
    print(retweets_sorted.iloc[i]['text'])
    print()
```

    RT @fema: We have created a rumor control page for Hurricane #Florence that will be updated regularly. During disasters, it’s critical to a…
    
    RT @CFPBDirector: Busy day at the @CFPB. Digging into the details. https://t.co/yfs0gmh28F
    
    RT @Readygov: Prepare your home before a hurricane arrives:  🚗 Fill your car up with gas. ⛱ Bring outdoor furniture in and secure items out…
    
    RT @SBAgov: REMINDER: The deadline for SBA to approve #PaycheckProtectionProgram loan applications is TOMORROW.   👇 Find a lender and apply…
    
    When it comes to #mortgages, take your time, ask questions and #knowbeforeyouowe. https://t.co/UUaGyWDbzk
    
    When it comes to #mortgages, take your time, ask questions and #knowbeforeyouowe. https://t.co/UUaGyWDbzk
    
    If you have been affected by Hurricane #Harvey, we have resources to help you protect and rebuild your finances. https://t.co/Bdhnes6FWD https://t.co/SJ1qjf9Tvc
    
    RT @FTC: FTC warns hurricane victims about flood insurance robocall scam: https://t.co/mLNaukeu2O #Harvey #HurricaneHarvey #ScamAlert https…
    
    RT @SBAgov: REMINDER: The deadline for SBA to approve #PaycheckProtectionProgram loan applications is TOMORROW.   👇 Find a lender and apply…
    
    RT @SBAgov: #ICYMI: This morning, the #PaycheckProtectionProgram began accepting new loan applications in response to the Paycheck Protecti…
    


## Conclusion

The @CFPB Twitter page includes all tweets from early February 2011 to October 2020. The page's tweet breakdown is around 75% original tweets, followed in second by replies. The use of hashtags such as #KnowBeforeYouOwe, #MoneyAsYouGrow, and #StudentDebtStress signal to us that knowing more about money, saving up, and handling student stress due to debt are topics that are brought up more often in their posts. The account also appears to be more busy during the week, particularly around Tuesday-Thursday and has very low activity on the weekends, particularly Sunday.

The most common words in the twitter dataset were calls to action (action-oriented) and include words such as "help," "thank," "complaint", "share," "learn," and "submit." Regarding the different types of tweets, favorite, retweet, and tweet, the years 2014 to 2016 were the best years overall, with 2016 breaking records and reaching its peak in terms of the number of favorited tweets and retweets. The frequency of tweets that are retweets appear to be the most "volatile" with more sudden changes and not a very clear trend. In 2020, however, the retweets and favorited tweets have been slighlty declining and look like they could continue along that trend. 

Overall, the twitter page could do better, particularly with regard to its own twitter activity since the metrics that have done the best are those that are retweets of others rather than those done by the CFPB themselves. The best performing one was a retweet from @FEMA regarding hurricane Florence. In fact, among the top 10 best performing retweet types, four of them mentioned hurricanes. The paycheck protection program (often mentioned along with @SBAgov) comes in second place, which is expected given the pandemic. 
