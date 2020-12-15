
# CFPB Twitter Analysis

The project examines all tweets from February 3, 2011 to October 8, 2020 from the following Twitter page:

 - **[CFPB](https://twitter.com/CFPB?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)**

**Data Sources**

This project analyzes the Consumer Financial Protection Bureau's (CFPB) Twitter data. The CFPB Twitter data was collected and acquired from the [Social Feed Manager](https://library.gwu.edu/scholarly-technology-group/social-feed-manager).



## Data: importing and pre-processing

### Import packages


```python
## Importing packages

# Importing packages for data manipulation and cleaning
import pandas as pd
import numpy as np

# Filter warning
import warnings
warnings.filterwarnings('ignore')

# Importing packages for visualization
import seaborn as sns

import matplotlib.pyplot as plt

# Telling matplotlib to use 538 style for graphs
plt.style.use('fivethirtyeight')
## 2nd option plt.style.use('seaborn-whitegrid')

# Telling matplotlib to use 'retina' display when ouputting graphs to make it sharper
%config InlineBackend.figure_format = 'retina'

# Making plot outputs appear
%matplotlib inline
```

## Load data 


```python
# Load the twitter data
twitter = pd.read_csv('Twitter_Data.csv')

# Show the first 5 rows
twitter.head()
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
      <th>user_favourites_count</th>
      <th>user_followers_count</th>
      <th>user_friends_count</th>
      <th>user_listed_count</th>
      <th>user_location</th>
      <th>user_name</th>
      <th>user_statuses_count</th>
      <th>user_time_zone</th>
      <th>user_urls</th>
      <th>user_verified</th>
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
      <td>182</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
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
      <td>182</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
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
      <td>182</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
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
      <td>182</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
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
      <td>182</td>
      <td>65075</td>
      <td>17</td>
      <td>1823</td>
      <td>Washington, DC</td>
      <td>consumerfinance.gov</td>
      <td>2409</td>
      <td>Eastern Time (US &amp; Canada)</td>
      <td>http://www.consumerfinance.gov</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 37 columns</p>
</div>




```python
# Checking number of rows (11,155) and columns (37)
twitter.shape
```




    (11155, 37)



## Pre-processing


```python
# Changing the parsed_created_at column to datetime to use all the date features Pandas offers
twitter['parsed_created_at'] = pd.to_datetime(twitter['parsed_created_at'])
```


```python
# Checking the different types of data, confirming that parsed_created_at is now datetime64
twitter.dtypes
```




    id                                            int64
    tweet_url                                    object
    created_at                                   object
    parsed_created_at               datetime64[ns, UTC]
    user_screen_name                             object
    text                                         object
    tweet_type                                   object
    coordinates                                 float64
    hashtags                                     object
    media                                        object
    urls                                         object
    favorite_count                                int64
    in_reply_to_screen_name                      object
    in_reply_to_status_id                       float64
    in_reply_to_user_id                         float64
    lang                                         object
    place                                       float64
    possibly_sensitive                           object
    retweet_count                                 int64
    retweet_or_quote_id                         float64
    retweet_or_quote_screen_name                 object
    retweet_or_quote_user_id                    float64
    source                                       object
    user_id                                       int64
    user_created_at                              object
    user_default_profile_image                     bool
    user_description                             object
    user_favourites_count                         int64
    user_followers_count                          int64
    user_friends_count                            int64
    user_listed_count                             int64
    user_location                                object
    user_name                                    object
    user_statuses_count                           int64
    user_time_zone                               object
    user_urls                                    object
    user_verified                                  bool
    dtype: object




```python
# Finding the number of unique values for each column
twitter.nunique()
```




    id                              7852
    tweet_url                       7852
    created_at                      7232
    parsed_created_at               7232
    user_screen_name                   1
    text                            7573
    tweet_type                         4
    coordinates                        0
    hashtags                         858
    media                           2793
    urls                            3135
    favorite_count                    42
    in_reply_to_screen_name         1899
    in_reply_to_status_id           2294
    in_reply_to_user_id             1896
    lang                               4
    place                              0
    possibly_sensitive                 1
    retweet_count                     82
    retweet_or_quote_id              231
    retweet_or_quote_screen_name      80
    retweet_or_quote_user_id          80
    source                            12
    user_id                            1
    user_created_at                    1
    user_default_profile_image         1
    user_description                   2
    user_favourites_count             10
    user_followers_count            1073
    user_friends_count                 2
    user_listed_count                280
    user_location                      1
    user_name                          1
    user_statuses_count             1068
    user_time_zone                     1
    user_urls                          1
    user_verified                      1
    dtype: int64




```python
# selecting unecessary columns, those with only 1 or 2 unique values
cols = twitter.nunique()[twitter.nunique()<3].index
# display index of column names to delete
cols
```




    Index(['user_screen_name', 'coordinates', 'place', 'possibly_sensitive',
           'user_id', 'user_created_at', 'user_default_profile_image',
           'user_description', 'user_friends_count', 'user_location', 'user_name',
           'user_time_zone', 'user_urls', 'user_verified'],
          dtype='object')




```python
# perform deletion of columns saved in variable cols, specifying columns, inplace to avoid reassigning
twitter.drop(cols, 1, inplace=True)
# checking to see that columns with only 1 or 2 unique values were dropped
twitter.nunique()
```




    id                              7852
    tweet_url                       7852
    created_at                      7232
    parsed_created_at               7232
    text                            7573
    tweet_type                         4
    hashtags                         858
    media                           2793
    urls                            3135
    favorite_count                    42
    in_reply_to_screen_name         1899
    in_reply_to_status_id           2294
    in_reply_to_user_id             1896
    lang                               4
    retweet_count                     82
    retweet_or_quote_id              231
    retweet_or_quote_screen_name      80
    retweet_or_quote_user_id          80
    source                            12
    user_favourites_count             10
    user_followers_count            1073
    user_listed_count                280
    user_statuses_count             1068
    dtype: int64




```python
# dropping "lang" column, specifying column, inplace to avoid reassigning
twitter.drop("lang", 1, inplace=True)

# selecting unecessary columns, those with less than 5 unique values
cols = twitter.nunique()[twitter.nunique()<5].index
cols
```




    Index(['tweet_type'], dtype='object')



# Analysis and Visualizations

### Tweet type


```python
# Creating pie plot, configuring specifications
# (https://stackoverflow.com/questions/30059862/pandas-pie-chart-plot-remove-the-label-text-on-the-wedge)
fig, ax = plt.subplots(figsize=(11,5))
explode = (0.1, 0.1, 0.1, 0.1) 
patches, text, _ = ax.pie(twitter["tweet_type"].value_counts(), autopct='%.2f', explode=explode, startangle=0, 
                          pctdistance=0.7, labels=twitter["tweet_type"].value_counts().index)
## ax.legend(patches, labels=twitter["tweet_type"].value_counts().index, loc='best')

# Take out matplotlib message, adjust placement
plt.tight_layout()
plt.subplots_adjust(top=0.88)

# Putting title and subtitle in specific x,y coordinates
# customizing font size, weight, and transparency
ax.text(-1.5,1.3, "Types of tweets", fontsize=20, fontweight="bold")
ax.text(-1.5,1.15, "Roughly two-thirds were original tweets", fontsize=15, fontweight="bold", alpha=0.85)

# saving image
plt.savefig('1tweet_type_ratio.png')
```


![png](output_18_0.png)


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
# checking length
len(hashtag_totals)
```




    858




```python
# Creating wc as a dictionary of the hashtag value counts
wc = pd.DataFrame(twitter.hashtags.value_counts()).to_dict()['hashtags']
wc
```




    {'KnowBeforeYouOwe': 150,
     'MoneyAsYouGrow': 133,
     'StudentDebtStress': 112,
     'MoneyTalk': 92,
     'AskCFPB': 89,
     'CFPW2020': 82,
     'mortgage': 70,
     'NCPW': 60,
     'ShopMortgage': 57,
     'prepaid': 57,
     'autoloan': 48,
     'CFPB': 46,
     'studentdebt': 44,
     'studentloan': 41,
     'debtcollection': 40,
     'AskFAFSA': 36,
     'SeniorMoney': 36,
     'NewCar': 35,
     '4Years4You': 34,
     'ConsumersCount': 34,
     'YouSavedForThis': 33,
     'midinero': 32,
     'AutoLoan': 32,
     'DebtCollection': 28,
     'debt': 28,
     'BankingonCampus': 28,
     'StartSmallSaveUp': 27,
     'CARDAct': 26,
     'SocialSecurity': 26,
     'OwningAHome': 26,
     'GovFinChat': 24,
     'NewCar AutoLoan': 23,
     'aske2i': 22,
     'studentloans': 20,
     'StudentDebt': 20,
     'Fraud': 20,
     'FindYourPlace': 20,
     'FinancialPlanningMonth': 20,
     'creditcard': 20,
     'CreditReport': 20,
     'TodaysTip FinancialPlanningMonth': 19,
     'retirement': 19,
     'NaturalDisaster EmergencyPreparedness DisasterRecovery': 19,
     'KidsTalkMoney': 18,
     'coronavirus': 17,
     'CreditReports': 16,
     'CreditReporting': 16,
     'MoneyTips': 15,
     'FinancialLiteracyMonth': 15,
     'fraud': 15,
     'FinancialLiteracyMonth FinLit': 15,
     'Homebuying': 15,
     'MoneyThoughtsWithKids': 14,
     'CoronavirusScams': 14,
     'ASW19': 14,
     'RushCard': 14,
     'studentloanhelp': 14,
     'FinancialCapabilityMonth AskCFPB': 14,
     'Banking': 13,
     'identitytheft': 13,
     'studentloans studentdebt': 13,
     'creditreport': 13,
     'Sandy': 12,
     'Scams': 12,
     'paydayloans': 12,
     'studentloan StudentDebtStress': 12,
     'CreditCard': 12,
     'EndDebtTraps': 12,
     'DebtCollectionStory': 12,
     'springcleaning': 11,
     'StudentLoans': 11,
     'NaturalDisaster': 11,
     'autoloan NewCar': 11,
     'CorruptCollectorChat': 11,
     'ASW17': 11,
     'IRS': 10,
     'PayingForCollege': 10,
     'arbitration': 10,
     'college': 10,
     'mortgage OwningAHome': 10,
     'MortgageClosingScams': 10,
     'CFPBEnforcement': 10,
     'NCEAnow': 10,
     'FinancialAid': 10,
     'ASW18': 10,
     'FinancialLiteracyMonth finlit': 10,
     'home OwningAHome': 10,
     'hurricanematthew': 10,
     'AutoLoan NewCar': 9,
     'homebuying': 9,
     'EmergencySavings StartSmallSaveUp': 9,
     'LifeSkills K12 FinancialLiteracy FinancialEducation': 9,
     'DYK': 9,
     'OECDPISA FinLit': 9,
     'MoneyTip': 9,
     'CertifyYourService': 8,
     'FinLit': 8,
     'ReverseMortgage': 8,
     'creditscore': 8,
     'NaturalDisaster DisasterRecovery HurricaneSeason': 8,
     'financialrecords': 8,
     'protectseniors': 8,
     'TaxTime': 8,
     'Equifax': 8,
     'knowbeforeyouowe': 8,
     'SaveLikeMike': 8,
     'debtcollector': 8,
     'StudentLoan': 8,
     'FinancialWellnessMonth': 8,
     'AskCFPB prepaid': 8,
     'OwningAHome NoPlaceLikeHome': 8,
     'mortgage KnowBeforeYouOwe': 8,
     'MoneyLessons': 7,
     'downpayment': 7,
     'IDtheft': 7,
     'VeteransDay': 7,
     'creditreports': 7,
     'scams': 7,
     'elderabuse': 7,
     'SavingsTip': 7,
     'finedu': 6,
     'mortgagecalculator': 6,
     'MoneyTip CreditScore': 6,
     'TaxRefund': 6,
     'mySocialSecurity': 6,
     'AskFAFSA StudentDebtStress': 6,
     'HolidayShopping': 6,
     'MiDinero': 6,
     'Mortgage': 6,
     'CFPBtech': 6,
     'ForeclosureHelpIsFree': 6,
     'creditcards': 6,
     'CFPBdata': 6,
     'seniorcitizens': 6,
     'WEAAD': 6,
     'MoneyTip StartSmallSaveUp': 6,
     'elderfraud': 6,
     'OAM17': 6,
     'HondaFinancial': 6,
     'ProtectSeniors': 6,
     'afinlitfuture': 6,
     'NCPW2018 ConsumerProtection': 6,
     'scam': 6,
     'ProjectCatalyst': 6,
     'creditscores': 5,
     'SocialSecurity scams': 5,
     'TaxTimeTip': 5,
     'elderfinancialexploitation': 5,
     'HurricaneDorian': 5,
     'IdentityTheft': 5,
     'NCPW2018': 5,
     'HolidayShoppingTip': 5,
     'overdraft': 5,
     'HomeownershipMonth FindYourPlace': 5,
     'BCFPtownhall': 5,
     'databreach': 5,
     'servicemembers': 5,
     'CreditScore': 5,
     'YourMoneyYourGoals': 5,
     'PaycheckProtectionProgram': 5,
     'Florence': 5,
     'ImposterScams': 5,
     'credit': 5,
     'DownPayment': 5,
     'bitcoin': 4,
     'BudgetTips SpringCleaning': 4,
     'socialsecurity': 4,
     'BudgetingTips Saving': 4,
     'DYK ShopMortgage': 4,
     'studentdebt dreamsnotdebt': 4,
     'AiA16': 4,
     'FinCon19': 4,
     'Autoloans': 4,
     'veterans': 4,
     'prepaid RushCard': 4,
     'CallForPapers': 4,
     'SeguroSocial': 4,
     'Thunderclap StudentDebtStress': 4,
     'opendata': 4,
     'KnowBeforeYouOwe NARLegislative': 4,
     'NaturalDisaster Sally Laura HurricaneSeason': 4,
     'TodaysTip': 4,
     'credit mortgage': 4,
     'Savings StartSmallSaveUp': 4,
     'CreditReport FinLitMonth': 4,
     'moneytalk': 4,
     'mortgages': 4,
     'MortgageCalculator': 4,
     'RealEstate': 4,
     'StudentLoan PayingForCollege': 4,
     'Retirement': 4,
     'ApplicationAbyss': 4,
     'PersonalFinance SpringCleaning': 4,
     'credit CreditReport': 4,
     'downpayment ShopMortgage': 4,
     'StudentDebtStress StudentLoan': 4,
     'CARESAct': 4,
     'Language': 4,
     'KnowBeforeYouOwe mortgage': 4,
     'Harvey': 4,
     'hogar familia': 4,
     'StudentLoan StudentDebtStress': 4,
     'financial 4Years4You': 4,
     'backtoschool': 4,
     'interestrates': 4,
     'ChildrensBookWeek': 4,
     'StudentLoan RepaymentRoadblocks': 4,
     'finlit': 4,
     'nextfront': 4,
     'AskCFPB ProtectyourID': 4,
     'Home OwningAHome': 4,
     'taxseason': 4,
     'ReentryWeek': 4,
     'savings ASW2015': 4,
     'smallbiz': 4,
     'CreditScores': 4,
     'StudentDebtStress studentloans': 4,
     'SocialSecurityScams': 4,
     'OlderAmericansMonth OAM2020': 4,
     'BudgetTips MoneyTips': 4,
     'MedicalDebt': 4,
     'MoneyTip creditscore': 4,
     'SocialSecurityScam': 4,
     'carpayment': 4,
     'CFPW2020 MilitaryConsumerMonth': 4,
     'studentloandebt': 4,
     'eClosing': 4,
     'GrandparentScam': 4,
     'home KnowBeforeYouOwe': 4,
     'ProTips SpringCleaning': 4,
     '4thofJuly': 4,
     'budget': 4,
     'FAFSA': 4,
     'CitizensBank': 4,
     'WHCOA': 4,
     'NARLegislative': 4,
     'paydayloans EndDebtTraps': 4,
     'CARESAct MortgageRelief': 4,
     'prepaid KnowBeforeYouOwe': 4,
     'PayingforCollege studentloans': 4,
     'SocialMediaDay': 4,
     'RegulationZ': 4,
     'COVID19': 3,
     'HMDA CFPW2020': 3,
     'Earthquake Anchorage': 3,
     'HurricaneSeason DisasterRecovery EmergencyPreparedness': 3,
     'HomeownershipMonth': 3,
     'HomeSweetHome Mortgage': 3,
     'FinancialWellness': 3,
     'Equifax DataBreach': 3,
     'NaturalDisaster DisasterRecovery': 3,
     'Savings': 3,
     'FinLitMonth': 3,
     'interestrate': 3,
     'MidwestFlooding DisasterRecovery Flood2019': 3,
     'Budgeting': 3,
     'finances': 3,
     'TaxTimeTip tax': 3,
     'military': 3,
     'ElderAbuse': 3,
     'taxscams': 3,
     'SpringCleaning': 3,
     'HurricaneFlorence': 3,
     'FinancialEducation FinancialLiteracy': 3,
     'financialwellness': 3,
     'Argosy ArgosyUniversity': 3,
     'NaturalDisasters HurricaneSeason TropicalStorms': 3,
     'resolutions': 3,
     'ConsumerProtection NCPW2018': 3,
     'TaxSeason': 3,
     'MoneyTip StartSmallSAveUp': 3,
     'Savings StartSmallSaveUp FinCon19': 3,
     'Credit': 3,
     'scams ElderAbuse': 3,
     'fraud scams': 3,
     'BudgetTip': 3,
     'Irene': 2,
     'financial reversemortgage': 2,
     'moneyandkids': 2,
     'MortgageTips': 2,
     'downpayment home': 2,
     'reversemortgage': 2,
     'VirtualCurrency BitCoin FinLitMonth': 2,
     'credit healthcare': 2,
     'CollegeAcceptance studentloans': 2,
     'studentloans AskFAFSA': 2,
     'consumerculture': 2,
     'campus bankaccount': 2,
     'ForeclosureHelpisFree': 2,
     'taxscam': 2,
     'credit healthcarecosts': 2,
     'payday FinLitMonth': 2,
     'opengov gov20': 2,
     'financially': 2,
     'ESL Language': 2,
     'NationalSocialSecurityMonth': 2,
     'PaydayLoan': 2,
     'ReverseMortgages': 2,
     'retirement SocialSecurity PlanningforRetirement': 2,
     'saving': 2,
     'paydayloan complaint': 2,
     'insurance CreditReport': 2,
     'Thanksgiving finances': 2,
     'creditcard 4Years4You': 2,
     'debt 4Years4You': 2,
     'mortgage HomeSweetHome Homebuying': 2,
     'Wildfire TropicalStorm HurricaneSeason Sally Laura': 2,
     'Buyingahome': 2,
     'campus': 2,
     'debtstress': 2,
     'ASW2015 financialgoals': 2,
     'complaint': 2,
     'spendingmoney': 2,
     'CheckYourStatement mySocialSecurity': 2,
     'selfcontrol': 2,
     'paydayloans EndDebtTraps 4Years4You': 2,
     'Fed': 2,
     'financialdecisions 4Years4You': 2,
     'homebuyers mortgage KnowBeforeYouOwe': 2,
     'AmericaSaves NCPW': 2,
     'CreditScore FinancialCapabilityMonth AskCFPB': 2,
     'studentloan studentdebtstress': 2,
     'studentloan PayingForCollege 4Years4You': 2,
     'StudentLoans Thunderclap': 2,
     'Teachers CertifyYourService': 2,
     'StudentLoans StudentDebtStress': 2,
     'moneytransfers': 2,
     'NCLR CFPB NCLR16': 2,
     'OwningAHome mortgage GovFinChat': 2,
     'COVIDreliefIRS IRS': 2,
     'moneylesson kidsandmoney': 2,
     'HomeDepot': 2,
     'fraud FinLitMonth': 2,
     'great': 2,
     'StudentDebt PayingForCollege': 2,
     'seniorcitizens eldercare': 2,
     'notanaprilfoolsjoke': 2,
     'OwningAHome homeownership KnowBeforeYouOwe': 2,
     'moneylessons': 2,
     'CreditScore FinLitMonth': 2,
     'protectyourID': 2,
     'IRS tax SCAM': 2,
     'UX': 2,
     'OwningAHome CFPB': 2,
     'PrepareNow NaturalDisasters HurricaneSeason': 2,
     'GiftCard holidays': 2,
     'studentdebt ConsumerProtection NCPW17': 2,
     'StudentDebtStress Thunderclap': 2,
     'doctor credit medicalexpenses': 2,
     'FinancialEducation educators': 2,
     '529day': 2,
     'FinancialAid FAFSA PayingForCollege': 2,
     'robocall debtcollection': 2,
     'fraud CreditReport': 2,
     'DidYouKnow': 2,
     'EndDebtTraps paydayloans': 2,
     'IdentityTheft IDTheft': 2,
     'loan mortgage OwningAHome': 2,
     'BCFPtownhall elderfraud': 2,
     'Homebuying HomeSweetHome Mortgages': 2,
     'college PayingForCollege': 2,
     'FinancialStress': 2,
     'YourMoney': 2,
     'PeaceCorps CertifyYourService': 2,
     'creditscore NewYear': 2,
     'PublicServiceLoanForgiveness militaryservice AmeriCorps': 2,
     'AskFAFSA AskFAFSA': 2,
     'DidYouKnow CertifyYourService': 2,
     'FIF2015': 2,
     'mortgage OwningaHome': 2,
     'OSCON cfpbtech': 2,
     'gov20 opengov nerdalert': 2,
     'mySocialSecurity Someday': 2,
     'ads Superbowl adfree': 2,
     'UX PayingForCollege': 2,
     'CreditHistory mortgage': 2,
     'creditfreezes': 2,
     'ElderFinancialFraud NewMedicareCards': 2,
     'nbcusa2013': 2,
     'bankaccounts': 2,
     'retirement PlanningforRetirement': 2,
     'RepaymentRoadblocks StudentLoanDebt': 2,
     'UnemploymentBenefits': 2,
     'studentloan studentdebt': 2,
     'CFPB DoddFrank': 2,
     'PayingForCollege CollegeSigningDay ReachHigher': 2,
     'FF': 2,
     'FF GovFinChat': 2,
     'FalseAdvertising CreditCards': 2,
     'Corinthian students': 2,
     'savings BudgetTips': 2,
     'financial lovedone': 2,
     'ADA25': 2,
     'MilChat DebtCollection Military': 2,
     'DebtRelief': 2,
     'mortgage NCPW17': 2,
     'HowToSave': 2,
     'BlackFriday CyberMonday': 2,
     'debtcollectors': 2,
     'Connecticut': 2,
     'parents ASW2015': 2,
     'NMAM': 2,
     'studentloans ConsumersCount': 2,
     'languages': 2,
     'creditreport creditscores': 2,
     'HappyFathersDay': 2,
     'medicaldebt': 2,
     'eldercare': 2,
     'KnowBeforeYouOwe mortgagedisclosures realestate': 2,
     'YouHaveTheRight 4Years4You': 2,
     'TheWarRoom': 2,
     'Studentdebtstress': 2,
     'TaxRefund Taxes': 2,
     'CBCFALC13 ItStartsWithYou': 2,
     'buyingahome refinancing': 2,
     'KnowBeforeYouOwe NCPW': 2,
     'SuperBowlAds': 2,
     'FCClabels': 2,
     'MobileBanking': 2,
     'Section8Housing': 2,
     'PayingForCollege studentloan 4Years4You': 2,
     'JustEconomy': 2,
     'instantgratification selfcontrol': 2,
     'MCPD': 2,
     'MortgageClosingScam': 2,
     'HMDA CFPBData': 2,
     'studentloan Twitterchat AskFAFSA': 2,
     'FCCLive': 2,
     'financialwellbeing': 2,
     'OpCorruptCollector': 2,
     'MoneyManagement': 2,
     'creditcard debt': 2,
     'mortgageloan KnowBeforeYouOwe': 2,
     'NewYear CreditReport': 2,
     'BCFPtownhall elderfraud BatonRouge': 2,
     'servicemembers veterans MilitaryAppreciatioMonth MilFam': 2,
     'Servicemembers CertifyYourService': 2,
     'NCPW17': 2,
     'designers developers UX': 2,
     'TaxSecurity': 2,
     'forprofitcollege': 2,
     'SmallBusinesses': 2,
     'retirement pension': 2,
     'mortgage ShopMortgage': 2,
     'paydayloans loans EndDebtTraps': 2,
     'mortgages GovFinChat': 2,
     'TaxPreparer': 2,
     'ASW2015 imsavingfor': 2,
     'OwningAHome homeownership': 2,
     'realestate KnowBeforeYouOwe': 2,
     'mortgage buyingahome owningahome': 2,
     'NBMBAA': 2,
     'loan debt': 2,
     'BiketoWorkDay': 2,
     'MemorialDay2016': 2,
     'MoneyProTip': 2,
     'fintech': 2,
     'financial PayingForCollege': 2,
     'FinancialLiteracyMonth AskCFPB': 2,
     'studentloans retirement': 2,
     'FoodForThought Thanksgiving': 2,
     'financialeducation': 2,
     'medical creditcards': 2,
     'RepayStudentDebt PayingForCollege AskFAFSA': 2,
     'homebuyers': 2,
     'CreditReport 4Years4You': 2,
     'FTC NCPW': 2,
     'DYK ChildrensBookWeek': 2,
     'USHCCSummit2014 latism': 2,
     'home mortgages': 2,
     'credit NewYear': 2,
     'veterans WoundedWarrior': 2,
     'home OwningaHome': 2,
     'enddebttraps': 2,
     'CyberMonday': 2,
     'opengov transparency': 2,
     'GiftCard holiday shopping': 2,
     'paydayloan complaint EndDebtTraps': 2,
     'pension ASW17': 2,
     'money college studentloan': 2,
     'DidYouKnow overdraft': 2,
     'home mortgage': 2,
     'money2020': 2,
     'buyingahome OwningAHome': 2,
     'Katrina': 2,
     'MedicalDebt debt': 2,
     'consumer': 2,
     'DidYouKnow studentloan': 2,
     'consumerscount': 2,
     'StudentDebtStress StudentLoans 4Years4You': 2,
     'yourstory': 2,
     'servicemembers MilitaryAppreciation': 2,
     'debtrelief Corinthian students': 2,
     'StudentLoan StudentDebtStress Thunderclap': 2,
     'StudentLoans PayingForCollege': 2,
     'StudentLoans KnowBeforeYouOwe': 2,
     'kidsandmoney': 2,
     'DebtTraps': 2,
     'NationalSunglassesDay': 2,
     'bank college finances': 2,
     'mortgagedisclosure': 2,
     'whichformshouldItake': 2,
     'DYK moneyandkids': 2,
     'GlobalMoneyWeek': 2,
     'Mortgages': 2,
     'scams fraud FinLitMonth': 2,
     'FreeCreditScore': 2,
     'PlanningForRetirement SocialSecurity': 2,
     'CreditReports FinancialCapabilityMonth AskCFPB': 2,
     'opensource gov20': 2,
     'mortgages knowbeforeyouowe': 2,
     'DidYouKnow CreditCard': 2,
     'Springcleaning': 2,
     'FinancialEducation': 2,
     'financialgoals ASW2015': 2,
     'HowTo IdentityTheft FinLitMonth': 2,
     'BackToTheFutureDay savings': 2,
     'MoneySmartWeek': 2,
     'DebtCollection 4Years4You': 2,
     'credit EndDebtTraps': 2,
     'bills budgets FinEdu': 2,
     'BackToSchool': 2,
     'HowTo home': 2,
     'eldercare family': 2,
     'MilitaryAppreciation': 2,
     'loan 4Years4You': 2,
     'studentdebtstress': 2,
     'equity': 2,
     '4years4You': 2,
     'EmergencyPreparedness HurricanePrep NaturalDisaster': 2,
     'foreclosure GovFinChat': 2,
     'RegresoAClases': 2,
     'SmallBusinesses rulemaking': 2,
     'TaxTime taxes': 2,
     'DidYouKnow YouHaveTheRight': 2,
     'resolution ShopMortgage': 2,
     'KnowBeforeYouOwe TheWarRoom': 2,
     'Call4311': 2,
     'studentloans StudentDebtStress': 2,
     'GiftCard HolidayShopping': 2,
     'FirstDayofSummer': 2,
     'Debt YourMoney': 2,
     'KnowBeforeYouOwe OwningAHome NARLegislative': 2,
     'AnchorageEarthquake DisasterRecovery Earthquake': 2,
     'ncpw': 2,
     'BuyingAHouse': 2,
     'frauds': 2,
     'financialhealth': 2,
     'MSW2017': 2,
     'milchat DebtCollection': 2,
     'financial FinLitMonth': 2,
     'DidYouKnow StudentLoans': 2,
     'PayingforCollege': 2,
     'WEADD': 2,
     'thunderclap StudentDebtStress': 2,
     'FamilyFinance': 2,
     'DominoEffect NCPW': 2,
     'bankruptcy creditreport': 2,
     'Prepaid': 2,
     'homebuying OwningAHome': 2,
     'student PayingForCollege': 2,
     'HMDA mortgagemarket': 2,
     'SocialSecurity retirement': 2,
     'opengov': 2,
     'cfpb': 2,
     'mortgage buyingahome': 2,
     'money ASW2015': 2,
     'StudentDebt StudentDebtStress': 2,
     'NMAM Military': 2,
     'HonortheOath': 2,
     'NationalRES': 2,
     'startingcollege PayingforCollege': 2,
     'financial wellbeing': 2,
     'homebuying GovFinChat': 2,
     '4Years4You mortgage KnowBeforeYouOwe': 2,
     'BeMoneySmart': 2,
     'mortgage housing NARLegislative': 2,
     'NaturalDisasters Prepare': 2,
     'HurricaneMaria': 2,
     'DebtRelief StudentLoans': 2,
     'pension': 2,
     'PaydayLoans EndDebtTraps': 2,
     'Peerpressure': 2,
     'Autoloan': 2,
     'RealEstate KnowBeforeYouOwe': 2,
     'DidYouKnow debtcollectors': 2,
     'money MoneyTalk kids parenting FinLitMonth': 2,
     'CollegeFreshman money': 2,
     'bills CreditScore FinLitMonth': 2,
     'StudentDebtStress StudentLoans': 2,
     'reversemortgages': 2,
     'creditreporting': 2,
     'destinohogar': 2,
     'FinancialFuture TellYourStory 4Years4You': 2,
     'scams fraudprevention': 2,
     'newhome OwningAHome': 2,
     'KnowBeforeYouOwe eclosing': 2,
     'creditreport 4Years4You': 2,
     'StudentLoan DebtRelief Corinthian': 2,
     'CollegeDecisionDay studentloans': 2,
     'college FAFSA': 2,
     'FinancialTech': 2,
     'studentloan debt': 2,
     'OwningAHome GovFinChat': 2,
     'VeteransDay ThankYou': 2,
     'milfams': 2,
     'phishing': 2,
     'TakeOurDaughtersandSonstoWorkDay': 2,
     'Language ESL': 2,
     'financial Savings': 2,
     'followfriday': 2,
     'ADA ADA25': 2,
     'CFPB NCPW': 2,
     'hogar': 2,
     'consumers': 2,
     'scams FraudPrevention': 2,
     'mortgage OwningAHome 4Years4You': 2,
     'MemorialDay': 2,
     'USCMWinter': 2,
     'FirstResponders CertifyYourService': 2,
     'financial YourStory 4Years4You': 2,
     'studentdebt cfpb': 2,
     'RepaymentRoadblocks StudentLoans': 2,
     '4years4you': 2,
     'mortgage 4Years4You': 2,
     'pension retirement': 2,
     'interestrates FindYourPlace': 2,
     'KnowBeforeYouOwe alliteration': 2,
     'financial NewYear': 2,
     'studentdebt NewYearsResolution': 2,
     'financial': 2,
     'CFPB OwningAHome': 2,
     'SecDef': 2,
     'DataSharing': 2,
     'imposter scams': 2,
     'TakeOurDaughtersAndSonsToWork moneyskills': 2,
     'Georgia': 2,
     'bankruptcy': 2,
     'EquifaxDataBreach': 2,
     'CARESAct Retirement': 1,
     'HurricaneSeason PrepareNow EmergencyPreparedness': 1,
     'FinancialLiteracy FinancialEducation K12 LifeSkills': 1,
     'ElderFraud': 1,
     'HurricaneDorian FloodSmart HurricanePrep HurricaneSeason': 1,
     'ICYMI PaycheckProtectionProgram': 1,
     'TaxTime ASW18': 1,
     'homesweethome mortgage findyourplace interestrates': 1,
     'servicemembers MilFam': 1,
     'CharityFraudOut': 1,
     'NewMedicareCards ElderFinancialFraud': 1,
     'BatonRouge BCFPTownHall elderfraud': 1,
     'badcredit ShopMortgage': 1,
     'HurricaneLaura': 1,
     'fraud WEAAD2020': 1,
     'MilFam': 1,
     'SocialSecurity Retirement': 1,
     'ConsumerProtection': 1,
     '529Day': 1,
     'OnlineBanking': 1,
     'taxes': 1,
     'Earthquake DisasterRecovery': 1,
     'mortgage scam': 1,
     'DYK creditreport': 1,
     'DisasterPreparedness': 1,
     'bank CreditReport': 1,
     'directdeposit ASW17': 1,
     'FreeCreditScore FinancialCapabilityMonth AskCFPB': 1,
     'FloodSmart EmergencyPreparedness NaturalDisaster': 1,
     'BlackFriday': 1,
     'CFPW2020 MilConsumer2020': 1,
     'emailcourse debt': 1,
     'DisasterRecovery Earthquake Anchorage': 1,
     'FinancialLiteracyMonth mortgage': 1,
     'HolidaySpendingPlan': 1,
     '2020Resolution': 1,
     'CreditReport FinancialCapabilityMonth AskCFPB': 1,
     'checking': 1,
     'resolve': 1,
     'HurricaneSeason DisasterRecovery PrepareNow': 1,
     'ASW2019': 1,
     'SocialSecurityScam ScamAlert ElderFraud': 1,
     'TaxIDTheft': 1,
     'MSW19 ASW19': 1,
     'collegesavings': 1,
     'servicemember': 1,
     'scam fraudprevention elderfinancialfraud': 1,
     'COVID19 coronavirus': 1,
     'hurricane': 1,
     'FreeCreditReport ConsumerProtection': 1,
     'MoneyHabits': 1,
     'CreditMistakes': 1,
     'FraudPrevention ElderAbuse': 1,
     'SchoolsOut MoneyHabits': 1,
     'NaturalDisaster EmergencyPreparedness DisasterRecovery HurricaneMichael': 1,
     'hurricane HurricaneFlorence': 1,
     'PublicService CertifyYourService': 1,
     'NewYearsResolution': 1,
     'Taxes': 1,
     'moneylesson': 1,
     'emailcourse': 1,
     'WEAAD2020': 1,
     'PrepareNow BeReady HurricaneSeason': 1,
     'ageinplace': 1,
     'HurricaneFlorence FloodSmart HurricanePrep': 1,
     'CreditScores CreditScore': 1,
     'Earthquake': 1,
     'FCCtips': 1,
     'StaySafeOnline BeCyberSmart': 1,
     'bankaccount CreditReport': 1,
     'credit Mortgage': 1,
     'Servicemembers equifaxbreach': 1,
     'homebuying CreditReport': 1,
     'YourMoney debt': 1,
     'scam ValentinesDay': 1,
     'elderfraud BCFPtownhall': 1,
     'mortgage homebuying': 1,
     'mortgage creditscore': 1,
     'NaturalDisaster DisasterRecovery Earthquake': 1,
     'BookLoversDay bookclub': 1,
     'WEAAD WEAAD2020': 1,
     'IRS COVID19': 1,
     'elderfinancialexploitation BCFPtownhall': 1,
     'Harvey Irma': 1,
     'Medicare': 1,
     'RainyDayFund': 1,
     'FinancialCapabilityMonth FinancialFuture2018': 1,
     'HurricaneDorian HurricaneSeason': 1,
     'PrepareNow HurricanePrep NatlPrep': 1,
     'OlderAmericans': 1,
     'Senior Fraud': 1,
     'NaturalDisaster DisasterPreparedness': 1,
     'CreditTips': 1,
     'OpCorruptCollector CorruptCollectorChat': 1,
     'CreditReporting FinancialCapabilityMonth AskCFPB': 1,
     'scams SocialSecurity': 1,
     'CreditReport AskCFPB': 1,
     'NCPW2018 Homebuying': 1,
     'ICYMI': 1,
     'Homebuying HomeSweetHome': 1,
     'AskCFPB FinancialCapabilityMonth': 1,
     'CreditScores AskCFPB FinancialLiteracy': 1,
     'HurricaneFlorence PrepareNow EmergencyPreparedness NaturalDisaster': 1,
     'HurricaneDorian FloodSmart HurricaneRecovery HurricaneSeason': 1,
     'retirement socialsecurity': 1,
     'taxrefund ASW18': 1,
     'mortgage ShopMortgage CreditScore': 1,
     'DidYouKnow elderabuse NCEAnow': 1,
     'CreditScore Mortgage': 1,
     'Homebuying NCPW2018': 1,
     'FinancialCapabilityMonth': 1,
     'MoneyTip YouSavedForThis': 1,
     'BookLoversDay': 1,
     'servicemembers MilFam veterans': 1,
     'SocialSecurity Retirement NRPW': 1,
     'tax': 1,
     'MilitarySaves': 1,
     'TaxDay Taxes': 1,
     'giftcards prepaid': 1,
     'BudgetTips': 1,
     'FinancialCapabilityMonth credit AskCFPB FinLit': 1,
     'HurricaneSeason EmergencyPreparedness FloodSmart': 1,
     'Retirement NRPW': 1,
     'HurricaneMichael NaturalDisaster EmergencyPreparedness': 1,
     'Harvey HurricaneHarvey ScamAlert': 1,
     'HDMA CFPW2020': 1,
     'NCEAnow NCEAnow': 1,
     'IRS tax': 1,
     'scams Equifax': 1,
     'MidwestFlooding': 1,
     'txla18': 1,
     'elderly': 1,
     'holidayseason': 1,
     'HurricaneFlorence NaturalDisaster EmergencyPreparedness': 1,
     'BankAccount': 1,
     'HurricaneFlorence EmergencyPreparedness HurricanePrep': 1,
     'OlderAmericans BCFPtownhall': 1,
     'mortgage studentloans': 1,
     'veterans studentloans': 1,
     'Mortgage Homebuying': 1,
     'scams fraud financialexploitation NCEAnow': 1,
     'NaturalDisasters HurricaneSeason': 1,
     'DisasterPrepardness': 1,
     'unemployment': 1,
     'CreditFreeze': 1,
     'MedicareIDFraud elderfinancialfraud': 1,
     'caregiving': 1,
     'CreditCards': 1,
     'moneyresolutions': 1,
     'Florence FloodSmart HurricanePrep HurricaneSeason': 1,
     'MortgageRelief COVID19': 1,
     'Scam': 1,
     'DYK creditfreeze': 1,
     'HurricaneSeason Laura HurricaneLaura': 1,
     'FreeCreditScore AskCFPB FinancialLiteracyMonth': 1,
     'mortgage Homebuying HomeSweetHome': 1,
     'newcar': 1,
     'retirement NRSW17': 1,
     'family': 1,
     'ClosingOnAHome': 1,
     'MedicalInsurance CreditReport': 1,
     'IRSTaxTip': 1,
     'pension NRPW': 1,
     'FinancialCapabilityMonth AskCFPB FinLit': 1,
     'creditscores CreditReport': 1,
     'pension ASW18': 1,
     'bills debt': 1,
     'savings ASW18': 1,
     'FinancialWellBeing': 1,
     'prepaidcards': 1,
     'SocialSecurity NRPW': 1,
     'MoneyAsYouGrow moneyandkids': 1,
     'NMAM MilFam': 1,
     'AmeriCorps CertifyYourService': 1,
     'HomeSweetHome InterestRates': 1,
     'StimulusCheck': 1,
     'scams fraud': 1,
     'servicemembers identitytheft': 1,
     'MedicalCreditCard': 1,
     'homeowners reversemortgage': 1,
     'ShopMortgage Homebuying': 1,
     'inclusion': 1,
     'fraudprevention scams': 1,
     'CreditReports mortgage': 1,
     'RetirementPlanning': 1,
     'AskCFPB FinancialLiteracy': 1,
     'bankaccount': 1,
     'SeniorFraudAwareness': 1,
     'Mortgage HomeSweetHome': 1,
     'retirement NRPW': 1,
     'EmergencyPreparedness HurricanePrep FloodSmart': 1,
     'HomeSweetHome Homebuying Mortgages': 1,
     'InterestRate HomeSweetHome': 1,
     'HurricaneSeason NaturalDisaster': 1,
     'DebtCollector': 1,
     'NaturalDisaster DisasterRecovery Alaska': 1,
     'PersonalFinances': 1,
     'TaxRefund TaxReturn': 1,
     'MoneySmart Senior Fraud': 1,
     'scams BCFPTownHall': 1,
     'MilitaryKids financial money': 1,
     'budget springcleaning': 1,
     'HurricanePrep PrepareNow NaturalDisaster': 1,
     'elderfinancialfraud BCFPtownhall': 1,
     'FinancialFuture2018 FinancialCapabilityMonth': 1,
     'socialsecurity reversemortgage': 1,
     'financialaid': 1,
     'NaturalDisaster EmergencyPreparedness HurricanePrep': 1,
     'CFPW2020 HMDA': 1,
     'creditscores mortgage': 1,
     'autoloans': 1,
     'NaturalDisaster Wildfire TropicalStorm HurricaneLaura Laura HurricaneSeason': 1,
     'Coronavirus': 1,
     'mortgage studentloans creditcards': 1,
     'AskCFPB FinLit': 1,
     'FinlPrep ASW19': 1,
     'financialexploitation NCEAnow': 1,
     'NaturalDisaster BeReady DisasterPreparedness': 1,
     'summerjob': 1}




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
