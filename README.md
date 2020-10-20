# netflix_data
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
data = pd.read_csv("datasets/netflix_titles.csv")
data.head()
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
0	81145628	Movie	Norm of the North: King Sized Adventure	Richard Finn, Tim Maltby	Alan Marriott, Andrew Toth, Brian Dobson, Cole...	United States, India, South Korea, China	September 9, 2019	2019	TV-PG	90 min	Children & Family Movies, Comedies	Before planning an awesome wedding for his gra...
1	80117401	Movie	Jandino: Whatever it Takes	NaN	Jandino Asporaat	United Kingdom	September 9, 2016	2016	TV-MA	94 min	Stand-Up Comedy	Jandino Asporaat riffs on the challenges of ra...
2	70234439	TV Show	Transformers Prime	NaN	Peter Cullen, Sumalee Montano, Frank Welker, J...	United States	September 8, 2018	2013	TV-Y7-FV	1 Season	Kids' TV	With the help of three human allies, the Autob...
3	80058654	TV Show	Transformers: Robots in Disguise	NaN	Will Friedle, Darren Criss, Constance Zimmer, ...	United States	September 8, 2018	2016	TV-Y7	1 Season	Kids' TV	When a prison ship crash unleashes hundreds of...
4	80125979	Movie	#realityhigh	Fernando Lebrija	Nesta Cooper, Kate Walsh, John Michael Higgins...	United States	September 8, 2017	2017	TV-14	99 min	Comedies	When nerdy high schooler Dani finally attracts...
data.shape
(6234, 12)
data.describe()  #summary
show_id	release_year
count	6.234000e+03	6234.00000
mean	7.670368e+07	2013.35932
std	1.094296e+07	8.81162
min	2.477470e+05	1925.00000
25%	8.003580e+07	2013.00000
50%	8.016337e+07	2016.00000
75%	8.024489e+07	2018.00000
max	8.123573e+07	2020.00000
data.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 6234 entries, 0 to 6233
Data columns (total 12 columns):
show_id         6234 non-null int64
type            6234 non-null object
title           6234 non-null object
director        4265 non-null object
cast            5664 non-null object
country         5758 non-null object
date_added      6223 non-null object
release_year    6234 non-null int64
rating          6224 non-null object
duration        6234 non-null object
listed_in       6234 non-null object
description     6234 non-null object
dtypes: int64(2), object(10)
memory usage: 584.6+ KB
data.dropna(axis=0,how="all",inplace=True)
data.dropna(axis=1,how="all",inplace=True)
plt.figure(figsize = (15,20))
plt.plot(data['listed_in'].value_counts(),'*--')
plt.xticks(color="red",rotation=90)
plt.yticks(color="red")
plt.show()

data['listed_in'].value_counts()
Documentaries                                         299
Stand-Up Comedy                                       273
Dramas, International Movies                          248
Dramas, Independent Movies, International Movies      186
Comedies, Dramas, International Movies                174
                                                     ... 
Action & Adventure, Anime Features, Classic Movies      1
Anime Features, Music & Musicals, Sci-Fi & Fantasy      1
Docuseries, Reality TV, Teen TV Shows                   1
International Movies, Sports Movies                     1
Kids' TV, TV Dramas, Teen TV Shows                      1
Name: listed_in, Length: 461, dtype: int64
plt.rcParams['figure.figsize'] = (11,5)
plt.rcParams['axes.labelcolor'] = "red"
plt.rcParams['axes.labelsize'] = 20
plt.rcParams['xtick.color'] = "#123456"
plt.rcParams['ytick.color'] = "coral"
plt.rcParams['ytick.labelsize'] = 15
data['country'].value_counts()[:10]
United States     2032
India              777
United Kingdom     348
Japan              176
Canada             141
South Korea        136
Spain              117
France              90
Mexico              83
Turkey              79
Name: country, dtype: int64
Top countries producing netflix series/movies
data['country'].value_counts()[:20].plot(kind="bar")
<matplotlib.axes._subplots.AxesSubplot at 0x21d0c3c1c88>

data['type'].value_counts()
Movie      4265
TV Show    1969
Name: type, dtype: int64
data['rating'].value_counts()
TV-MA       2027
TV-14       1698
TV-PG        701
R            508
PG-13        286
NR           218
PG           184
TV-Y7        169
TV-G         149
TV-Y         143
TV-Y7-FV      95
G             37
UR             7
NC-17          2
Name: rating, dtype: int64
2. How many movies are with rating TV-MA and how many Tv shows with rating TV-MA
data.head()
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
0	81145628	Movie	Norm of the North: King Sized Adventure	Richard Finn, Tim Maltby	Alan Marriott, Andrew Toth, Brian Dobson, Cole...	United States, India, South Korea, China	September 9, 2019	2019	TV-PG	90 min	Children & Family Movies, Comedies	Before planning an awesome wedding for his gra...
1	80117401	Movie	Jandino: Whatever it Takes	NaN	Jandino Asporaat	United Kingdom	September 9, 2016	2016	TV-MA	94 min	Stand-Up Comedy	Jandino Asporaat riffs on the challenges of ra...
2	70234439	TV Show	Transformers Prime	NaN	Peter Cullen, Sumalee Montano, Frank Welker, J...	United States	September 8, 2018	2013	TV-Y7-FV	1 Season	Kids' TV	With the help of three human allies, the Autob...
3	80058654	TV Show	Transformers: Robots in Disguise	NaN	Will Friedle, Darren Criss, Constance Zimmer, ...	United States	September 8, 2018	2016	TV-Y7	1 Season	Kids' TV	When a prison ship crash unleashes hundreds of...
4	80125979	Movie	#realityhigh	Fernando Lebrija	Nesta Cooper, Kate Walsh, John Michael Higgins...	United States	September 8, 2017	2017	TV-14	99 min	Comedies	When nerdy high schooler Dani finally attracts...
len(data[(data['type'] == "Movie") & (data['rating'] == "TV-MA")])
1348
len(data[(data['type'] == "TV Show") & (data['rating'] == "TV-MA")])
679
data['release_year'].dtype
dtype('int64')
3. Check The number of movies and tv shows released in that year and check the number of movies released maximum in which year
release_year = int(input("\n Enter the release year : "))
data[data['release_year'] == release_year].count()
 Enter the release year : 2020
show_id         25
type            25
title           25
director         8
cast            23
country         18
date_added      25
release_year    25
rating          25
duration        25
listed_in       25
description     25
dtype: int64
release_year = int(input("\n Enter the release year : "))
type_ = input("\n Which type of data you want(movie/tvshows) : ").lower()
if type_ == "movie":    
    d = (data[(data['release_year'] == release_year) & (data['type'] == "Movie")][['title','rating']][:10].values)
    for i in d:
        print(f"TITLE ---> {i[0]}".center(80))
        print(f"RATING ---> {i[1]}".center(80))
        print("_"*80)
elif type_ == "tvshows":
    d = (data[(data['release_year'] == release_year) & (data['type'] == "TV Show")][['title','rating']][:10].values)
 Enter the release year : 2018

 Which type of data you want(movie/tvshows) : movie
                             TITLE ---> City of Joy                             
                               RATING ---> TV-MA                                
________________________________________________________________________________
                              TITLE ---> Next Gen                               
                               RATING ---> TV-PG                                
________________________________________________________________________________
                      TITLE ---> Sierra Burgess Is A Loser                      
                               RATING ---> PG-13                                
________________________________________________________________________________
              TITLE ---> The Most Assassinated Woman in the World               
                               RATING ---> TV-MA                                
________________________________________________________________________________
                        TITLE ---> Care of Kancharapalem                        
                               RATING ---> TV-14                                
________________________________________________________________________________
                        TITLE ---> Ee Nagaraniki Emaindi                        
                               RATING ---> TV-14                                
________________________________________________________________________________
                            TITLE ---> Black Panther                            
                               RATING ---> PG-13                                
________________________________________________________________________________
                         TITLE ---> The Debt Collector                          
                               RATING ---> TV-MA                                
________________________________________________________________________________
                            TITLE ---> Paradise Lost                            
                               RATING ---> TV-MA                                
________________________________________________________________________________
                            TITLE ---> Animal World                             
                               RATING ---> TV-MA                                
________________________________________________________________________________
fig = plt.figure(facecolor="black")
ax = fig.add_axes([0,0,1,1],facecolor="black")
data['release_year'].value_counts()[:30].plot(kind="bar",ax=ax,color="grey")
ax.tick_params(axis="x",labelcolor="coral",labelsize=18)
plt.text(13,700,"YEAR WISE",color="white",fontsize=20)
plt.legend(["YEAR"])
plt.show()

### now i want to check the highest date of 2020 year
data.head()
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
0	81145628	Movie	Norm of the North: King Sized Adventure	Richard Finn, Tim Maltby	Alan Marriott, Andrew Toth, Brian Dobson, Cole...	United States, India, South Korea, China	September 9, 2019	2019	TV-PG	90 min	Children & Family Movies, Comedies	Before planning an awesome wedding for his gra...
1	80117401	Movie	Jandino: Whatever it Takes	NaN	Jandino Asporaat	United Kingdom	September 9, 2016	2016	TV-MA	94 min	Stand-Up Comedy	Jandino Asporaat riffs on the challenges of ra...
2	70234439	TV Show	Transformers Prime	NaN	Peter Cullen, Sumalee Montano, Frank Welker, J...	United States	September 8, 2018	2013	TV-Y7-FV	1 Season	Kids' TV	With the help of three human allies, the Autob...
3	80058654	TV Show	Transformers: Robots in Disguise	NaN	Will Friedle, Darren Criss, Constance Zimmer, ...	United States	September 8, 2018	2016	TV-Y7	1 Season	Kids' TV	When a prison ship crash unleashes hundreds of...
4	80125979	Movie	#realityhigh	Fernando Lebrija	Nesta Cooper, Kate Walsh, John Michael Higgins...	United States	September 8, 2017	2017	TV-14	99 min	Comedies	When nerdy high schooler Dani finally attracts...
data['cast'].dtype
dtype('O')
data['cast'].dropna()
0       Alan Marriott, Andrew Toth, Brian Dobson, Cole...
1                                        Jandino Asporaat
2       Peter Cullen, Sumalee Montano, Frank Welker, J...
3       Will Friedle, Darren Criss, Constance Zimmer, ...
4       Nesta Cooper, Kate Walsh, John Michael Higgins...
                              ...                        
6228                                        Igor Dmitriev
6229    Burnie Burns, Jason Saldaña, Gustavo Sorola, G...
6230    Marc Maron, Judd Hirsch, Josh Brener, Nora Zeh...
6232    Daniel Radcliffe, Jon Hamm, Adam Godley, Chris...
6233    Jennifer Aniston, Courteney Cox, Lisa Kudrow, ...
Name: cast, Length: 5664, dtype: object
data['cast'].fillna("")
0       Alan Marriott, Andrew Toth, Brian Dobson, Cole...
1                                        Jandino Asporaat
2       Peter Cullen, Sumalee Montano, Frank Welker, J...
3       Will Friedle, Darren Criss, Constance Zimmer, ...
4       Nesta Cooper, Kate Walsh, John Michael Higgins...
                              ...                        
6229    Burnie Burns, Jason Saldaña, Gustavo Sorola, G...
6230    Marc Maron, Judd Hirsch, Josh Brener, Nora Zeh...
6231                                                     
6232    Daniel Radcliffe, Jon Hamm, Adam Godley, Chris...
6233    Jennifer Aniston, Courteney Cox, Lisa Kudrow, ...
Name: cast, Length: 6234, dtype: object
data[data['release_year'] == 2020]
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
1315	81034946	TV Show	Maradona in Mexico	NaN	Diego Armando Maradona	Argentina, United States, Mexico	November 13, 2019	2020	TV-MA	1 Season	Docuseries, Spanish-Language TV Shows	In this docuseries, soccer great Diego Maradon...
3180	81214114	Movie	Bulletproof 2	Don Michael Paul	Faizon Love, Kirk Fox, Tony Todd, Pearl Thusi,...	United States	January 9, 2020	2020	TV-MA	97 min	Action & Adventure, Comedies	A special agent abruptly reunites with a crimi...
3189	81039393	TV Show	Cheer	NaN	NaN	United States	January 8, 2020	2020	TV-MA	1 Season	Docuseries, Reality TV, Teen TV Shows	This gripping docuseries follows the ups and d...
3195	80233408	Movie	Live Twice, Love Once	Maria Ripoll	Oscar Martínez, Inma Cuesta, Mafalda Carbonell...	Spain	January 7, 2020	2020	TV-MA	102 min	Comedies, Dramas, International Movies	When Emilio (Oscar Martínez) is diagnosed with...
3220	80997687	TV Show	Dracula	NaN	Claes Bang, Dolly Wells, John Heffernan	United Kingdom	January 4, 2020	2020	TV-14	1 Season	British TV Shows, International TV Shows, TV D...	The Count Dracula legend transforms with new t...
3221	80237347	TV Show	Go! Go! Cory Carson	NaN	Alan C. Lim, Paul Killam, Maisie Benson, Kerry...	United States	January 4, 2020	2020	TV-Y	1 Season	Kids' TV	Beep, beep – go, go! Buckle up for fun and adv...
3249	81006825	Movie	All the Freckles in the World	Yibrán Asuad	Hánssel Casillas, Loreto Peralta, Andrea Sutto...	Mexico	January 3, 2020	2020	TV-14	90 min	Comedies, International Movies, Romantic Movies	Thirteen-year-old José Miguel is immune to 199...
3325	81160763	TV Show	Sex, Explained	NaN	Janelle Monáe	United States	January 2, 2020	2020	TV-MA	1 Season	Docuseries, Science & Nature TV	From the biology of attraction to the history ...
3352	81127902	Movie	A Fall from Grace	Tyler Perry	Crystal Fox, Phylicia Rashad, Cicely Tyson, Br...	NaN	January 17, 2020	2020	TV-MA	121 min	Dramas, Thrillers	When gentle, law-abiding Grace confesses to ki...
3353	80995039	TV Show	Ares	NaN	Jade Olieberg, Tobias Kersloot, Lisa Smit, Fri...	NaN	January 17, 2020	2020	TV-MA	1 Season	International TV Shows, TV Dramas, TV Horror	Aiming to become part of Amsterdam's elite, an...
3354	81062580	TV Show	Nailed It! Germany	NaN	Angelina Kirsch, Bernd Siefert	NaN	January 17, 2020	2020	TV-14	1 Season	International TV Shows, Reality TV	Home cooks try – and inevitably fail – to re-c...
3363	80996973	TV Show	Handsome Siblings	NaN	Hu Yitian, Chen Zheyuan, Liang Jie, Vicky Lian...	China	January 16, 2020	2020	TV-14	1 Season	International TV Shows, TV Dramas, TV Sci-Fi &...	Clashing martial arts twins face relentless vi...
3379	81062828	TV Show	Killer Inside: The Mind of Aaron Hernandez	NaN	Aaron Hernandez	United States	January 15, 2020	2020	TV-MA	1 Season	Crime TV Shows, Docuseries	Via interviews with friends, players and insid...
3426	80221553	TV Show	Kipo and the Age of Wonderbeasts	NaN	Karen Fukuhara, Sydney Mikayla, Deon Cole, Coy...	United States	January 14, 2020	2020	TV-Y7-FV	1 Season	Kids' TV, TV Comedies	Making her way through a world of mutant anima...
3427	81060049	Movie	Leslie Jones: Time Machine	David Benioff, D.B. Weiss	Leslie Jones	United States	January 14, 2020	2020	TV-MA	66 min	Stand-Up Comedy	From trying to seduce Prince to battling sleep...
3436	80239306	TV Show	The Healing Powers of Dude	NaN	Jace Chapman, Larisa Oleynik, Tom Everett Scot...	NaN	January 13, 2020	2020	TV-G	1 Season	Kids' TV, TV Comedies, TV Dramas	When an 11-year-old boy with social anxiety di...
3464	80237329	TV Show	AJ and the Queen	NaN	RuPaul Charles, Izzy G., Michael-Leon Wooley, ...	United States	January 10, 2020	2020	TV-14	1 Season	TV Comedies, TV Dramas	While traveling across the country in a run-do...
3466	81183491	TV Show	Jamtara - Sabka Number Ayega	Soumendra Padhi	Amit Sial, Dibyendu Bhattacharya, Aksha Pardha...	India	January 10, 2020	2020	TV-MA	1 Season	Crime TV Shows, International TV Shows, TV Dramas	A group of small-town young men run a lucrativ...
3467	81011449	TV Show	Medical Police	NaN	Erinn Hayes, Rob Huebel, Malin Akerman, Rob Co...	United States	January 10, 2020	2020	TV-MA	1 Season	Crime TV Shows, TV Action & Adventure, TV Come...	Doctors Owen Maestro and Lola Spratt leave Chi...
3472	81074060	TV Show	Until Dawn	NaN	Ahmed Sylla, Alban Ivanov, Ornella Fleury, Nat...	France	January 10, 2020	2020	TV-MA	1 Season	International TV Shows, Reality TV, TV Comedies	France’s funniest comics carry out ghastly tas...
3518	81088083	Movie	Ghost Stories	Anurag Kashyap, Dibakar Banerjee, Karan Johar,...	Janhvi Kapoor, Sobhita Dhulipala, Sukant Goel,...	India	January 1, 2020	2020	TV-MA	145 min	Horror Movies, International Movies, Thrillers	The directors of Emmy-nominated "Lust Stories"...
3541	80117557	TV Show	Messiah	NaN	Michelle Monaghan, Mehdi Dehbi, John Ortiz, To...	United States	January 1, 2020	2020	TV-MA	1 Season	TV Dramas, TV Thrillers	A wary CIA officer investigates a charismatic ...
3546	80197991	TV Show	Nisman: The Prosecutor, the President, and the...	Justin Webster	NaN	NaN	January 1, 2020	2020	TV-MA	1 Season	Crime TV Shows, Docuseries, International TV S...	This docuseries details the suspicious death o...
3562	80201590	TV Show	Spinning Out	NaN	Kaya Scodelario, January Jones, Will Kemp, Wil...	NaN	January 1, 2020	2020	TV-MA	1 Season	TV Dramas	A figure skating Olympic hopeful struggles to ...
3573	81044551	TV Show	The Circle	NaN	Michelle Buteau	NaN	January 1, 2020	2020	TV-MA	1 Season	Reality TV	Status and strategy collide in this social exp...
Last release of year 2019
pd.to_datetime(data['date_added'])
0      2019-09-09
1      2016-09-09
2      2018-09-08
3      2018-09-08
4      2017-09-08
          ...    
6229          NaT
6230          NaT
6231          NaT
6232          NaT
6233          NaT
Name: date_added, Length: 6234, dtype: datetime64[ns]
data.tail()
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
6229	80000063	TV Show	Red vs. Blue	NaN	Burnie Burns, Jason Saldaña, Gustavo Sorola, G...	United States	NaN	2015	NR	13 Seasons	TV Action & Adventure, TV Comedies, TV Sci-Fi ...	This parody of first-person shooter games, mil...
6230	70286564	TV Show	Maron	NaN	Marc Maron, Judd Hirsch, Josh Brener, Nora Zeh...	United States	NaN	2016	TV-MA	4 Seasons	TV Comedies	Marc Maron stars as Marc Maron, who interviews...
6231	80116008	Movie	Little Baby Bum: Nursery Rhyme Friends	NaN	NaN	NaN	NaN	2016	NaN	60 min	Movies	Nursery rhymes and original music for children...
6232	70281022	TV Show	A Young Doctor's Notebook and Other Stories	NaN	Daniel Radcliffe, Jon Hamm, Adam Godley, Chris...	United Kingdom	NaN	2013	TV-MA	2 Seasons	British TV Shows, TV Comedies, TV Dramas	Set during the Russian Revolution, this comic ...
6233	70153404	TV Show	Friends	NaN	Jennifer Aniston, Courteney Cox, Lisa Kudrow, ...	United States	NaN	2003	TV-14	10 Seasons	Classic & Cult TV, TV Comedies	This hit sitcom follows the merry misadventure...
data_2 = data.copy()
data_2['date_added'] = pd.to_datetime(data_2['date_added'])
data_2['date_added']
0      2019-09-09
1      2016-09-09
2      2018-09-08
3      2018-09-08
4      2017-09-08
          ...    
6229          NaT
6230          NaT
6231          NaT
6232          NaT
6233          NaT
Name: date_added, Length: 6234, dtype: datetime64[ns]
d = data_2['date_added'].dropna()
d
0      2019-09-09
1      2016-09-09
2      2018-09-08
3      2018-09-08
4      2017-09-08
          ...    
6218   2019-04-10
6219   2019-04-01
6220   2016-04-01
6221   2016-04-01
6222   2014-04-01
Name: date_added, Length: 6223, dtype: datetime64[ns]
d = pd.DataFrame(d)
d
date_added
0	2019-09-09
1	2016-09-09
2	2018-09-08
3	2018-09-08
4	2017-09-08
...	...
6218	2019-04-10
6219	2019-04-01
6220	2016-04-01
6221	2016-04-01
6222	2014-04-01
6223 rows × 1 columns

pd.concat([d,data_2],axis=1,ignore_index=True)
0	1	2	3	4	5	6	7	8	9	10	11
0	2019-09-09	81145628	Movie	Norm of the North: King Sized Adventure	Richard Finn, Tim Maltby	Alan Marriott, Andrew Toth, Brian Dobson, Cole...	United States, India, South Korea, China	2019	TV-PG	90 min	Children & Family Movies, Comedies	Before planning an awesome wedding for his gra...
1	2016-09-09	80117401	Movie	Jandino: Whatever it Takes	NaN	Jandino Asporaat	United Kingdom	2016	TV-MA	94 min	Stand-Up Comedy	Jandino Asporaat riffs on the challenges of ra...
2	2018-09-08	70234439	TV Show	Transformers Prime	NaN	Peter Cullen, Sumalee Montano, Frank Welker, J...	United States	2013	TV-Y7-FV	1 Season	Kids' TV	With the help of three human allies, the Autob...
3	2018-09-08	80058654	TV Show	Transformers: Robots in Disguise	NaN	Will Friedle, Darren Criss, Constance Zimmer, ...	United States	2016	TV-Y7	1 Season	Kids' TV	When a prison ship crash unleashes hundreds of...
4	2017-09-08	80125979	Movie	#realityhigh	Fernando Lebrija	Nesta Cooper, Kate Walsh, John Michael Higgins...	United States	2017	TV-14	99 min	Comedies	When nerdy high schooler Dani finally attracts...
...	...	...	...	...	...	...	...	...	...	...	...	...
6229	NaT	80000063	TV Show	Red vs. Blue	NaN	Burnie Burns, Jason Saldaña, Gustavo Sorola, G...	United States	2015	NR	13 Seasons	TV Action & Adventure, TV Comedies, TV Sci-Fi ...	This parody of first-person shooter games, mil...
6230	NaT	70286564	TV Show	Maron	NaN	Marc Maron, Judd Hirsch, Josh Brener, Nora Zeh...	United States	2016	TV-MA	4 Seasons	TV Comedies	Marc Maron stars as Marc Maron, who interviews...
6231	NaT	80116008	Movie	Little Baby Bum: Nursery Rhyme Friends	NaN	NaN	NaN	2016	NaN	60 min	Movies	Nursery rhymes and original music for children...
6232	NaT	70281022	TV Show	A Young Doctor's Notebook and Other Stories	NaN	Daniel Radcliffe, Jon Hamm, Adam Godley, Chris...	United Kingdom	2013	TV-MA	2 Seasons	British TV Shows, TV Comedies, TV Dramas	Set during the Russian Revolution, this comic ...
6233	NaT	70153404	TV Show	Friends	NaN	Jennifer Aniston, Courteney Cox, Lisa Kudrow, ...	United States	2003	TV-14	10 Seasons	Classic & Cult TV, TV Comedies	This hit sitcom follows the merry misadventure...
6234 rows × 12 columns

d['date_added']
0      2019-09-09
1      2016-09-09
2      2018-09-08
3      2018-09-08
4      2017-09-08
          ...    
6218   2019-04-10
6219   2019-04-01
6220   2016-04-01
6221   2016-04-01
6222   2014-04-01
Name: date_added, Length: 6223, dtype: datetime64[ns]
data_2['date_added']
0      2019-09-09
1      2016-09-09
2      2018-09-08
3      2018-09-08
4      2017-09-08
          ...    
6229          NaT
6230          NaT
6231          NaT
6232          NaT
6233          NaT
Name: date_added, Length: 6234, dtype: datetime64[ns]
df1 = pd.merge(d,data_2,on="date_added")
df1.set_index("date_added",inplace=True)
df1.resample("BM").count()
show_id	type	title	director	cast	country	release_year	rating	duration	listed_in	description
date_added											
2008-01-31	1	1	1	1	1	1	1	1	1	1	1
2008-02-29	1	1	1	0	0	1	1	1	1	1	1
2008-03-31	0	0	0	0	0	0	0	0	0	0	0
2008-04-30	0	0	0	0	0	0	0	0	0	0	0
2008-05-30	0	0	0	0	0	0	0	0	0	0	0
...	...	...	...	...	...	...	...	...	...	...	...
2019-09-30	2607	2607	2607	1740	2431	2408	2607	2607	2607	2607	2607
2019-10-31	7040	7040	7040	5205	6609	6777	7040	7040	7040	7040	7040
2019-11-29	13633	13633	13633	10602	13171	12150	13633	13633	13633	13633	13633
2019-12-31	8519	8519	8519	7237	8297	7452	8519	8519	8519	8519	8519
2020-01-31	16242	16242	16242	14347	15987	14464	16242	16242	16242	16242	16242
145 rows × 11 columns

def check(x):
    if type(x) == str:
        if "31, 2019" in x:
            #if "December" in x:
            return True
            #else:
                #return False
        else:
            return False
    return False
data['date_added']
0       September 9, 2019
1       September 9, 2016
2       September 8, 2018
3       September 8, 2018
4       September 8, 2017
              ...        
6229                  NaN
6230                  NaN
6231                  NaN
6232                  NaN
6233                  NaN
Name: date_added, Length: 6234, dtype: object
data[data['date_added'].apply(check)]
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
465	81084225	Movie	Grego Rossello: Disculpe las molestias	Juani Libonatti	Grego Rossello	Argentina	October 31, 2019	2019	TV-MA	65 min	Stand-Up Comedy	Argentine comedian Grego Rossello takes the st...
466	80203920	TV Show	Nowhere Man	DJ Chen	Alyssa Chia, Mavis Fan, Joseph Chang, Wang Po-...	Taiwan	October 31, 2019	2019	TV-MA	1 Season	Crime TV Shows, International TV Shows, TV Act...	Two nefarious schemes taking place 10 years ap...
467	80242051	TV Show	Sleepless Society: Bedtime Wishes	NaN	Shahkrit Yamnarm, Savika Chaiyadej, Supoj Chan...	NaN	October 31, 2019	2019	TV-MA	1 Season	Crime TV Shows, International TV Shows, TV Dramas	During a holiday stay at a hotel resort, a fli...
1601	80202874	Movie	Always Be My Maybe	Nahnatchka Khan	Ali Wong, Randall Park, James Saito, Michelle ...	United States	May 31, 2019	2019	PG-13	102 min	Comedies, Romantic Movies	Reunited after 15 years, famous chef Sasha and...
1602	70109249	Movie	C Kkompany	Sachin Yardi	Mahesh Bhatt, Mithun Chakraborty, G.K. Desai, ...	India	May 31, 2019	2008	TV-14	127 min	Action & Adventure, Comedies, International Mo...	To blow off some steam, friends Akshay, Joshi ...
...	...	...	...	...	...	...	...	...	...	...	...	...
5781	80221787	TV Show	Bad Blood	NaN	Anthony LaPaglia, Kim Coates, Enrico Colantoni...	Canada	May 31, 2019	2019	TV-MA	2 Seasons	Crime TV Shows, TV Dramas	This sprawling crime drama follows the true st...
5782	80209096	TV Show	My Next Guest Needs No Introduction With David...	NaN	President Barack Obama, George Clooney, Malala...	United States	May 31, 2019	2019	TV-MA	2 Seasons	Stand-Up Comedy & Talk Shows	TV legend David Letterman teams up with fascin...
5933	80198635	TV Show	The Letdown	NaN	Alison Bell, Duncan Fellows, Noni Hazlehurst, ...	Australia	July 31, 2019	2019	TV-MA	2 Seasons	International TV Shows, TV Comedies, TV Dramas	Audrey, mother of a 2-month-old, joins a new-p...
6073	81224868	TV Show	Robot Trains	NaN	Bill Rogers, Carrie Savage, Ken Spassione, Ang...	South Korea	December 31, 2019	2018	TV-Y7	2 Seasons	Kids' TV, Korean TV Shows	Keeping peace and safety in Train World is no ...
6074	80092654	TV Show	Occupied	NaN	Henrik Mestad, Ane Dahl Torp, Ingeborga Dapkun...	Norway, Sweden	December 31, 2019	2017	TV-MA	2 Seasons	International TV Shows, TV Dramas, TV Thrillers	In the near future, Russia initiates a "silk g...
115 rows × 12 columns

Check the top 10 directors of country mentioned by user
country = input("\n Enter country : ")
data[data['country'] == country]['director'].value_counts()[:10].plot(kind="bar")
plt.tick_params(axis="x",labelsize=25)
plt.show()
 Enter country : India

data['release_year'].value_counts().plot()
plt.grid()
plt.show()

Top movies of which genre
d = {}
for i in data['listed_in'].apply(lambda x : x.split(",")):
    for j in i:
        j = j.strip()
        if d.get(j):
            d[j] += 1
        else:
            d[j] = 1
d
{'Children & Family Movies': 378,
 'Comedies': 1113,
 'Stand-Up Comedy': 281,
 "Kids' TV": 328,
 'Crime TV Shows': 363,
 'International TV Shows': 1001,
 'Spanish-Language TV Shows': 117,
 'International Movies': 1927,
 'Sci-Fi & Fantasy': 193,
 'Thrillers': 392,
 'Docuseries': 279,
 'Science & Nature TV': 67,
 'Action & Adventure': 597,
 'Dramas': 1623,
 'Cult Movies': 55,
 'Independent Movies': 552,
 'Romantic Movies': 376,
 'Documentaries': 668,
 'Horror Movies': 262,
 'Romantic TV Shows': 278,
 'TV Comedies': 436,
 'TV Dramas': 599,
 'TV Thrillers': 44,
 'TV Mysteries': 69,
 'British TV Shows': 210,
 'Music & Musicals': 243,
 'Reality TV': 153,
 'TV Action & Adventure': 126,
 'Anime Features': 45,
 'Teen TV Shows': 44,
 'Faith & Spirituality': 47,
 'Korean TV Shows': 132,
 'Anime Series': 117,
 'LGBTQ Movies': 60,
 'TV Horror': 54,
 'Movies': 56,
 'Stand-Up Comedy & Talk Shows': 42,
 'TV Sci-Fi & Fantasy': 68,
 'Classic Movies': 84,
 'Sports Movies': 157,
 'TV Shows': 10,
 'Classic & Cult TV': 24}
from random import choice
def getcolor():
    c = "#"
    ch = ['a','b','c','d','e','f','1','2','3','4','5','6']
    for i in range(6):
        c += choice(ch)
    return c
%%writefile get_color.py


from random import choice
def getcolor():
    c = "#"
    ch = ['a','b','c','d','e','f','1','2','3','4','5','6']
    for i in range(6):
        c += choice(ch)
    return c
Writing get_color.py
fig = plt.figure(facecolor="black")
ax = fig.add_axes([0,0,1,1],facecolor="black")
ax.bar(d.keys(),d.values(),color=[getcolor() for i in range(len(d.keys()))])
ax.tick_params(axis="x",labelcolor="coral",labelsize=18,rotation=90)
plt.show()

print(dir(ax))
['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setstate__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_add_text', '_adjustable', '_agg_filter', '_alpha', '_anchor', '_animated', '_aspect', '_autoscaleXon', '_autoscaleYon', '_autotitlepos', '_axes', '_axes_locator', '_axisbelow', '_clipon', '_clippath', '_connected', '_contains', '_convert_dx', '_current_image', '_facecolor', '_frameon', '_gci', '_gen_axes_patch', '_gen_axes_spines', '_get_axis_list', '_get_clipping_extent_bbox', '_get_lines', '_get_patches_for_fill', '_get_view', '_gid', '_gridOn', '_in_layout', '_init_axis', '_label', '_layoutbox', '_left_title', '_make_twin_axes', '_mouseover', '_mouseover_set', '_navigate', '_navigate_mode', '_oid', '_on_units_changed', '_originalPosition', '_parse_scatter_color_args', '_path_effects', '_pcolorargs', '_picker', '_position', '_poslayoutbox', '_process_unit_info', '_prop_order', '_propobservers', '_quiver_units', '_rasterization_zorder', '_rasterized', '_remove_legend', '_remove_method', '_right_title', '_sci', '_set_artist_props', '_set_gc_clip', '_set_lim_and_transforms', '_set_position', '_set_title_offset_trans', '_set_view', '_set_view_from_bbox', '_shared_x_axes', '_shared_y_axes', '_sharex', '_sharey', '_sketch', '_snap', '_stale', '_sticky_edges', '_tight', '_transform', '_transformSet', '_twinned_axes', '_update_image_limits', '_update_line_limits', '_update_patch_limits', '_update_title_position', '_update_transScale', '_url', '_use_sticky_edges', '_validate_converted_limits', '_visible', '_xaxis_transform', '_xcid', '_xmargin', '_yaxis_transform', '_ycid', '_ymargin', 'acorr', 'add_artist', 'add_callback', 'add_child_axes', 'add_collection', 'add_container', 'add_image', 'add_line', 'add_patch', 'add_table', 'aname', 'angle_spectrum', 'annotate', 'apply_aspect', 'arrow', 'artists', 'autoscale', 'autoscale_view', 'axes', 'axhline', 'axhspan', 'axis', 'axison', 'axvline', 'axvspan', 'bar', 'barbs', 'barh', 'bbox', 'boxplot', 'broken_barh', 'bxp', 'callbacks', 'can_pan', 'can_zoom', 'child_axes', 'cla', 'clabel', 'clear', 'clipbox', 'cohere', 'collections', 'containers', 'contains', 'contains_point', 'contour', 'contourf', 'convert_xunits', 'convert_yunits', 'csd', 'dataLim', 'drag_pan', 'draw', 'draw_artist', 'end_pan', 'errorbar', 'eventplot', 'eventson', 'figure', 'fill', 'fill_between', 'fill_betweenx', 'findobj', 'fmt_xdata', 'fmt_ydata', 'format_coord', 'format_cursor_data', 'format_xdata', 'format_ydata', 'get_adjustable', 'get_agg_filter', 'get_alpha', 'get_anchor', 'get_animated', 'get_aspect', 'get_autoscale_on', 'get_autoscalex_on', 'get_autoscaley_on', 'get_axes_locator', 'get_axisbelow', 'get_children', 'get_clip_box', 'get_clip_on', 'get_clip_path', 'get_contains', 'get_cursor_data', 'get_data_ratio', 'get_data_ratio_log', 'get_default_bbox_extra_artists', 'get_facecolor', 'get_fc', 'get_figure', 'get_frame_on', 'get_gid', 'get_images', 'get_in_layout', 'get_label', 'get_legend', 'get_legend_handles_labels', 'get_lines', 'get_navigate', 'get_navigate_mode', 'get_path_effects', 'get_picker', 'get_position', 'get_rasterization_zorder', 'get_rasterized', 'get_renderer_cache', 'get_shared_x_axes', 'get_shared_y_axes', 'get_sketch_params', 'get_snap', 'get_tightbbox', 'get_title', 'get_transform', 'get_transformed_clip_path_and_affine', 'get_url', 'get_visible', 'get_window_extent', 'get_xaxis', 'get_xaxis_text1_transform', 'get_xaxis_text2_transform', 'get_xaxis_transform', 'get_xbound', 'get_xgridlines', 'get_xlabel', 'get_xlim', 'get_xmajorticklabels', 'get_xminorticklabels', 'get_xscale', 'get_xticklabels', 'get_xticklines', 'get_xticks', 'get_yaxis', 'get_yaxis_text1_transform', 'get_yaxis_text2_transform', 'get_yaxis_transform', 'get_ybound', 'get_ygridlines', 'get_ylabel', 'get_ylim', 'get_ymajorticklabels', 'get_yminorticklabels', 'get_yscale', 'get_yticklabels', 'get_yticklines', 'get_yticks', 'get_zorder', 'grid', 'has_data', 'have_units', 'hexbin', 'hist', 'hist2d', 'hlines', 'ignore_existing_data_limits', 'images', 'imshow', 'in_axes', 'indicate_inset', 'indicate_inset_zoom', 'inset_axes', 'invert_xaxis', 'invert_yaxis', 'is_transform_set', 'legend', 'legend_', 'lines', 'locator_params', 'loglog', 'magnitude_spectrum', 'margins', 'matshow', 'minorticks_off', 'minorticks_on', 'mouseover', 'mouseover_set', 'name', 'patch', 'patches', 'pchanged', 'pcolor', 'pcolorfast', 'pcolormesh', 'phase_spectrum', 'pick', 'pickable', 'pie', 'plot', 'plot_date', 'properties', 'psd', 'quiver', 'quiverkey', 'redraw_in_frame', 'relim', 'remove', 'remove_callback', 'reset_position', 'scatter', 'secondary_xaxis', 'secondary_yaxis', 'semilogx', 'semilogy', 'set', 'set_adjustable', 'set_agg_filter', 'set_alpha', 'set_anchor', 'set_animated', 'set_aspect', 'set_autoscale_on', 'set_autoscalex_on', 'set_autoscaley_on', 'set_axes_locator', 'set_axis_off', 'set_axis_on', 'set_axisbelow', 'set_clip_box', 'set_clip_on', 'set_clip_path', 'set_contains', 'set_facecolor', 'set_fc', 'set_figure', 'set_frame_on', 'set_gid', 'set_in_layout', 'set_label', 'set_navigate', 'set_navigate_mode', 'set_path_effects', 'set_picker', 'set_position', 'set_prop_cycle', 'set_rasterization_zorder', 'set_rasterized', 'set_sketch_params', 'set_snap', 'set_title', 'set_transform', 'set_url', 'set_visible', 'set_xbound', 'set_xlabel', 'set_xlim', 'set_xmargin', 'set_xscale', 'set_xticklabels', 'set_xticks', 'set_ybound', 'set_ylabel', 'set_ylim', 'set_ymargin', 'set_yscale', 'set_yticklabels', 'set_yticks', 'set_zorder', 'specgram', 'spines', 'spy', 'stackplot', 'stale', 'stale_callback', 'start_pan', 'stem', 'step', 'sticky_edges', 'streamplot', 'table', 'tables', 'text', 'texts', 'tick_params', 'ticklabel_format', 'title', 'titleOffsetTrans', 'transAxes', 'transData', 'transLimits', 'transScale', 'tricontour', 'tricontourf', 'tripcolor', 'triplot', 'twinx', 'twiny', 'update', 'update_datalim', 'update_datalim_bounds', 'update_from', 'use_sticky_edges', 'viewLim', 'violin', 'violinplot', 'vlines', 'xaxis', 'xaxis_date', 'xaxis_inverted', 'xcorr', 'yaxis', 'yaxis_date', 'yaxis_inverted', 'zorder']
ax.get_xticklabels()
<a list of 42 Text xticklabel objects>
