# HDistill

HDistill is a Python CLI tool for exploring and parsing HTML

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install hdistill.

```bash
pip install hdistill
```

## Usage

```python
hdistill 'https://www.imdb.com/chart/top/?ref_=nv_mv_250' "//td[@class='titleColumn']/text() | //td[@class='titleColumn']//a/text() | //td[@class='titleColumn']//a/@title | //td[@class='titleColumn']//span[@class='secondaryInfo']/text()" -t 'Rank,Key People,Title,Year Released' -o 'output'
```

will parse the HTML at the given URL with the given XPath expression, transform the output based on the keys specificed after the -t argument, and then write as JSON to the file specified by the -o argument.

```
[   {   'Key People': 'Frank Darabont (dir.), Tim Robbins, Morgan Freeman',
        'Rank': '1.',
        'Title': 'The Shawshank Redemption',
        'Year Released': '(1994)'},
    {   'Key People': 'Francis Ford Coppola (dir.), Marlon Brando, Al Pacino',
        'Rank': '2.',
        'Title': 'The Godfather',
        'Year Released': '(1972)'},
    {   'Key People': 'Francis Ford Coppola (dir.), Al Pacino, Robert De Niro',
        'Rank': '3.',
        'Title': 'The Godfather: Part II',
        'Year Released': '(1974)'},
    {   'Key People': 'Christopher Nolan (dir.), Christian Bale, Heath Ledger',
        'Rank': '4.',
        'Title': 'The Dark Knight',
        'Year Released': '(2008)'},
    etc...
```

for raw output for more exploratory purposes, simply ommit the -t and -o arguments:

```python
hdistill 'https://www.imdb.com/chart/top/?ref_=nv_mv_250' '//td[@class=\"titleColumn\"]/text() | //td[@class=\"titleColumn\"]//a/text() | //td[@class=\"titleColumn\"]//a/@title | //td[@class=\"titleColumn\"]//span[@class=\"secondaryInfo\"]/text()'
```

which will output to console a raw list of the attributes and elements found by your XPath query:

```
[   '1.',
    'Frank Darabont (dir.), Tim Robbins, Morgan Freeman',
    'The Shawshank Redemption',
    '(1994)',
    '2.',
    'Francis Ford Coppola (dir.), Marlon Brando, Al Pacino',
    'The Godfather',
    '(1972)',
    '3.',
    'Francis Ford Coppola (dir.), Al Pacino, Robert De Niro',
    'The Godfather: Part II',
    '(1974)',
```

Or to get the day's top headlines from google news:

```
hdistill 'https://news.google.com/topstories?hl=en-US&gl=US&ceid=US:en' "//a[@class='DY5T1d RZIKme']/text()"
```

which will output something like:

```
[   "Florida-Based Doctor Arrested in Haiti President's Assassination",
    'Prominent Florida doctor tied to assassination of Haitian president',
    'Police say suspect in killing of Haitiâ\x80\x99s MoÃ¯se planned to assume '
    'presidency',
    'Your Monday Briefing',
    "The US is 'analyzing' the Haitian government's request to send troops "
    'after its president was assassinated',
    'Cubans take to the streets for the biggest anti-government protests in '
    'decades',
    'Video emerges of mass protests against communist dictatorship in Cuba: '
    "'We are not afraid'",
    'Demonstrators in Havana protest shortages, rising prices',
    'Behind Cubaâ\x80\x99s Covid Uprising',
    'Cubans Denounce â\x80\x98Miseryâ\x80\x99 in Biggest Protests in Decades',
    'Trump easily wins CPAC 2024 GOP presidential nomination straw poll',
    'Trump wins the CPAC straw poll as attendees clamor for him to run again',
    "CPAC: Trump Jr says he 'understands addiction' then blasts Hunter Biden",
    "Donald Trump Jr. on his father's Sunday CPAC speech: 'People will be "
    "outraged'",
    'CNN spoke with Trump supporter at CPAC who knows Biden won',
    'Beckwourth Complex fire crosses Hwy. 395, burns structures in Doyle, '
    'California',
    "'Extreme fire behavior': 2 firefighters killed as Western wildfires "
    'intensify during heat wave',
    'US heatwave: Wildfires rage in western states as temperatures soar',
    "California's raging Beckwourth Complex Fire doubles in size, jumps "
    'highway',
    'How bad is this fire season in California really going to be?',
    'Kristi Noem criticizes GOP governors who enacted Covid-19 mandates while '
    'accusing some of rewriting their history',
    "Noem says it was 'tough' to be 'attacked by my friends' in conservative "
    'media over trans-athlete bill',
    'Why Are Republican Governors Sending National Guard to the Border?',
    "Noem, at CPAC, argues country needs to 'fix damage' Biden is doing",
    'South Dakota sends National Guard troops to help with border crisis',
    'Death Valley hits 130 degrees as relentless Western heat wave adds fuel '
    'to wildfires',
    'How the highly unusual Death Valley temperatures just got more '
    'complicated',
    'Relief in sight as extreme heat wave in West breaks more records. For '
    'Death Valley? Cooler temps mean 120-125.',
    'New Heat Wave Blisters the West',
    '10 things you need to know today: July 11, 2021',
    "Yes, Lauren Boebert Tweeted That 'Turning Off CNN' was the 'Easiest Way' "
    'to Make the Delta Variant Go Away',
    'Fact check: Viral meme makes false claim about delta variant',
    "Fauci's 'two Americas' comment on COVID-19 vaccination rates taken out of "
    'context',
    "Haiti's First Lady Martine Moise Was Not Killed In Assassination Attempt",
    "Data showing lower death rate for coronavirus delta variant doesn't mean "
    "it's less dangerous",
    'Food labels and the lies they tell us about grocery store â\x80\x98best '
    'beforeâ\x80\x99 expiration dates',
    'The invisible addiction: is it time to give up caffeine?',
    'A Private-School Sex Educator Defends Her Methods',
    "Nuclear power is clean and safe. Why aren't we using more of it?",
    "When Will China's Economy Beat the US to Become No. 1? Why It May Never "
    'Happen',
    'What America Didnâ\x80\x99t Understand About Its Longest War',
    'A horn-wearing â\x80\x98shaman.â\x80\x99 A cowboy evangelist. For some, '
    'the Capitol attack was a kind of Christian revolt.',
    "Here's Why the Nuclear-Powered 1958 Ford Nucleon Never Entered Production",
    "2021 Child Tax Credit: Here's who will get up to $1,800 per child in cash "
    'â\x80\x94 and who will need to opt out',
    "A Tsunami of Disability Is Coming as a Result of 'Long COVID'",
    'Heat Wave Killed Marine Wildlife en Masse',
    'Executive Order on Promoting Competition in the American Economy',
    'â\x80\x9cCat Personâ\x80\x9d by Kristen Roupenian draws specific details '
    'from my life. - Slate',
    'What Is the Metaverse?',
    'Biden launches assault on monopolies',
    'Samsung Galaxy A32 5G Review: Renaissance Phone',
    'The 36 questions that lead to love (but with your co-founder)',
    'A New Kind of Information-Coding Seen in the Human Brain',
    'The Futuristic Stink of Amazonâ\x80\x99s Science Fiction',
    'A Young Naturalist Inspires With Joy, Not Doom']
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

For development purposes, run
```
python -m hdistill.main
```
from root of the repository to run the application.

## License
[MIT](https://choosealicense.com/licenses/mit/)
