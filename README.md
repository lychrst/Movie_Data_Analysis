# A Movie Data Analysis for Microsoft

Author: Chris Lyons, June 2022

![in-the_movies](/images/You_are_in_the_%20movies.jpg?raw=true)
## Badges  
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)  


### Repo Contents
- [A Movie Data Analysis Jupyter Notebook](https://github.com/lychrst/Movie_Data_Analysis/blob/main/A%20movie%20data%20analysis%20for%20Microsoft.ipynb)
- [Exploratory Notebook](https://github.com/lychrst/Movie_Data_Analysis/blob/main/exploratory.ipynb)



### Table of Contents  
- [Introduction](#introduction)
- [Business Opportunity](#business-opportunity)
- [The Data Sources](#the-data-sources)
- [Data Understanding and Preparation](#data-understanding-and-preparation)
- [Merging IMDb and The Numbers Databases and Feature Engineering](#merging-IMDb-and-the-numbers-databases-and-feature-engineering)
- [Analysis](#analysis)    
     -  [Genres](#genres)
     -  [Directors](#directors)
     -  [Writers](#writers)
- [Conclusions](#conclusions)
- [Next Steps](#next-steps)



## Introduction 

This was a class assignment designed to test student's ability to use descriptive statistics, python, and pandas. We were given 5 data sets and were instructed to create a business proposal for [Microsoft](https://www.microsoft.com/en-us/?ql=4) to enter into the movie industry. We were assessed by the following criteria: Presentation Content, Slide Style, Presentation Delivery, Business Understanding, Data Understanding, Data Preparation, Data Communication, Authoring Jupyter Notebooks, and Data Manipulation and Analysis with Pandas. Beyond these guidelines, the project was open-ended.  A full git history is unavailable due to my unfamiliarity with git prior to the project but it will be available in subsequent projects.

Descriptive analysis of movie genres, directors, and writers provides insight into which genres outperform others and who the top-performing talent are.   The primary metric used is profit but other metrics are included as they can provide insight into other factors such as prominence. Should it desire to enter the movie industry, Microsoft can use this analysis to decide which type of movies to invest in and who to hire.

## Business Opportunity 

![Activision Blizzard](/images/Rachat_d'Activision_et_Blizzard.webp.png?raw=true)

Since 2005 when [Microsoft sold its stake in NBC to Comcast](https://www.reuters.com/article/us-msnbc-microsoft-idUSBRE86F04W20120716), it has not had a presence in the movie or cable industry.  Instead, it’s [acquisitions](https://acquiredby.co/what-companies-does-microsoft-own/) have focused on software companies (ex. Intrinsa, Github), social networking sites (ex.  LinkedIN), telecommunications (ex. Skype), speech recognition (ex. Tellme Network, Nuance Communications), advertising (ex. aQuantive, Xandr), music (ex. Musiwave), cloud computing (ex. Adallom), machine learning (ex. Equivio), and gaming (ex. Mojang, ZeniMax Media).  Its 2022 acquisition of [Activision Blizzard for $68.7 billion](https://theorg.com/insights/what-companies-does-microsoft-own) continued its expansion into the gaming industry.   While not necessarily its primary purpose, the Activision acquisition gives Microsoft rights to popular video game titles including [Overwatch, Diablo, World of Warcraft, Candy Crush, StarCraft, and Call of Duty]( https://news.microsoft.com/2022/01/18/microsoft-to-acquire-activision-blizzard-to-bring-the-joy-and-community-of-gaming-to-everyone-across-every-device/).  It also expands Microsoft’s CGI talent pool.  The presence of in-house CGI talent and the rights to popular video game titles puts Microsoft in a position to expand into the movie industry should it choose to do so.  Income from movies can help recoup some of the money Microsoft spent on the acquisition of Activision.

## The Data Sources

The two sources of data used in this analysis are [IMDb](https://www.imdb.com/search/) and [The Numbers]( https://www.the-numbers.com/movies/#tab=year).   IMDb is an online searchable database that contains information about a film such as genre, actors, directors, writers, ratings, and “Ways to Watch”.   The Numbers, on the other hand, includes information about worldwide gross, domestic gross, and budget.   These two sites are complimentary as they each have information the other site doesn’t have.  This analysis will merge these two datasets to provide a more complete overview of the movie industry.  IMDb is  owned by Amazon and The Numbers is run by the company [Nash Information Services](https://www.nashinfoservices.com/).

## Data Understanding and Preparation

![IMDb](/images/300px-IMDb_logo.svg.png?raw=true)

IMDb is an SQL database comprised of multiple datasets. The ones used in this analysis are movie basics, persons, writers, and directors as these four datasets provide information on movie titles, genres, directors, and writers which are the four main categorical criteria used in this analysis.  Runtime minutes, birth year, and death year are stored as floats.  Start year is stored as an integer.  The rest of the column values are stored as objects.

IMDb’s movie basics dataframe has all of the IMBD data necessary for an analysis on genres.  In order to create dataframes that contain the IMBD data necessary for an analysis on directors and writers, the directors and writers dataframes need to be joined with the movie basics and persons dataframes.

The genres column has multiple values stored in the same row (Comedy and Drama, for example).  While technically feature engineering, the movie basics dataframe needs to be prepared early on as the explode function utilized will not work once the dataframe is joined with The Numbers dataframe. The genres column also has several movies that don’t have genres listed.  These rows were dropped. 

Both the writers and the directors dataframes have duplicates. This is likely due to other variables included in the database. For example, a director may be listed multiple times due to the fact that there are multiple writers working with him or her.  These duplicates were also dropped.

![The_Numbers](/images/The_Numbers.jpg?raw=true)

The Numbers is a CSV file that contains information about release date, movie title, production budget, domestic gross, and worldwide gross.  The values of the aforementioned columns are all stored as objects.

The Numbers data were stored as objects.  These were converted into floats in order to do numerical analysis.  They were also divided by 1,000,000 so that the numbers represent millions of dollars.  

There were some movies that had zero dollars of world wide gross.  While it is possible for a movie to have zero domestic gross if it is only released internationally, one would expect movies to have at least some world wide gross if it had been released. Inclusion of these values would throw off the data analysis.  Thus, they were dropped.

## Merging IMDb and The Numbers Databases and Feature Engineering

Both the IMDb and The Numbers databases had movies with titles that were duplicated.  Most of these are likely remakes.  For example, The Numbers database includes both the 2019 version of *Aladdin* as well as the 1992 version.  In order to avoid having the wrong data being attached to the wrong movie, two columns were used to merge the IMBD and The Numbers databases, namely the title and the year a movie was released.     

In the case of the IMDb database, start_year was already stored as an integer and thus didn’t need to be converted.  In the case of The Numbers database, it was necessary to convert the release date into an integer. 

A successful merge results in the 2019 data from the Numbers database being joined with the 2019 movie data from the IMBD database.  These same merges are done for the directors and writers dataframes.

Profit can be calculated by subtracting the world wide gross by the production budget.  Domestic gross is included in world wide gross and thus does not factor into this calculation.  Return on investemnt (ROI) can be calculated by dividing the profit by the production budget.

## Analysis

### Genres

According to the data included in the IMDb and The Numbers databases, Animation is the most profitable genre, followed by Musical, Sci-Fi, Adventure, Action, Fantasy, and Family.  The Musical genre data needs to be approached with caution as there are only 8 movies in it and there are 50 movies in the Music category which, if included, would significantly bring down the average.   The other top categories are represented by significant numbers of movies (98 for Animation, 127 for Sci-Fi, 343 for Adventure, 422 for Action, 119 for Fantasy, and 88 for Family).  

Profit is correlated with worldwide and domestic gross (.99).  Hence, more profitable movies also tend to be the movies with the most domestic and global prominence.  For this reason, profit will be used as the primary metric moving forward as it determines net revenue and approximates domestic and global appeal.  The genres with the highest profit also tend to have the highest production costs which shouldn’t be an issue for well-capitalized companies but could prove problematic for ones with stricter budgetary constraints. 

In general, movies have a mean profit of 111 million, a median of 64 million, and a standard deviation of 89 million dollars.   The fact that the median is significantly lower than the mean indicates that several highly profitable movies are bringing up the average of the various genres.   This trend is seen in the top 7 genres mentioned earlier as they all have means higher than the medians.  High standard deviations for the top 7 genres (ranging from 435 million for Musical to 222 million for Family) are indicative of high variability of profit for movies within these genres.

![Genres](/images/genres.png?raw=true)

### Directors

Directors who produced three or more movies were selected in order to filter out one-hit wonders.  The two directors with the highest average profit, Joe and Anthony Russo, are brothers who direct their movies together and thus were combined onto a single row. They averaged over 1 billion dollars.  David Yates was the lowest of the top ten directors.  He averaged over 400 million dollars in profit.

Four of the top ten directors produced movies based off of Marvel Comics and 2 produced movies based off of DC Comics.  Of these six directors, several have produced other well-known big-budget films (ex. James Wan - *Furious 7*, Christopher Nolan – *Dunkirk*, and Bryan Singer - *Bohemian Rhapsody*).   All of the movies based off of comics fell into the Action category. Most fell into the Adventure category, the Batman movie *The Dark Night Rises* being the sole exception.   All but *The Dark Night Rises* and *Aquaman* fell into the Sci-Fi genre.

Two of the directors produced movies based off of popular books - Peter Jackson (*The Hobbit* series) and David Yates (*Fantastic Beasts*).  *The Hobbit* and *Fantastic Beasts* fell into Adventure and Fantasy genres and often into the Family genre.

The remaining two directors produced Animated movies.  Chris Renaud	and Pierre Coffin both produced at least two *Despicable Me* movies.  Coffin also produced *Minions* and Renaud also produced The *Secret Life of Pets*.

The average profit of the bottom ten directors with three or more movies ranged from a high of 18 million (Danny Boyle) to a low of -2.0 million (Jeff Nichols). As it is possible that a director could be in the bottom ten due to having a smaller budget and not due to ineffectiveness, a search that took budget into consideration was done to examine this possibility. All of Leslie Small’s movies were profitable and he had an average budget of less than 10 million dollars. The rest of the directors in the bottom ten had average budgets greater than 10 million.

![Genres](/images/directors.png?raw=true)

### Writers

Writers accredited with three or more movies were selected in order to filter out one-hit wonders.  Writers who are deceased were filtered out as they can no longer write movies.  Don Heck, Joe Simon, and J.R.R. Tolkien had been in the top ten without the filter.  Jim Starlin has the highest profit, with an average movie grossing well over 1 billion dollars.  Stephen McFeely has the lowest of the top ten, with an average profit of 603 million.  

4 of the top writers are either comic book writers or have made screenplays based off of comic books.   3 more have written animated films (Cinco Paul, Ken Daurio, Linda Woolverton).  The remaining 3 have written big budget action films (ex. *Jurassic World*, *Furious 7*, *The Hunger Games*).  

The average profit of the bottom ten writers ranged from a high of 18 million (Stephen Susco) to a low of -14 million (David Dobkin).  A search that took budget into consideration was used to examine the bottom ten.  Kevin Smith and Nicole Holofcener both had average budgets less than 10 million.  None of Kevin Smith’s movies were profitable.  On the other hand, all of Nicole Holofcener’s movies were.

![Writers](/images/writers.png?raw=true)

## Conclusions

- **Resist the temptation to make a movie based off of *Call of Duty***  
    In general, war movies do not do well. The genres that are best suited for Microsoft are Animation, Sci-Fi, Fantasy, Action, Adventure, and Family. These genres have higher production costs which means smaller companies are less likely to take risks on them due to fear of becoming insolvent.  Hence, the only likely competition is with other industry giants.  Unless done as an Animated Family film like *Beauty and the Beast*, it is probably best to avoid the Musical genre.  There aren't enough movies in the dataset to support the genre's inclusion in the top tier and Musicals don't take advantage of the two main strengths Microsoft has – high market capitalization and in-house CGI talent. *Diablo*, *Overwatch*, *World of Warcraft* and *StarCraft* are Activision titles that have the potential to be turned into movies due to their Sci-Fi, Fantasy, Action, and Adventure elements.  [*World of Warcraft*](https://www.imdb.com/video/vi4072453145/?playlistId=tt0803096&ref_=tt_pr_ov_vi)  has been produced before (profitably) and a sequel or remake may be a good entry point into the movie space.  It would be difficult to pull off, but *Candy Crush* could be turned into an Animated Family movie.
   
   
-	**Hire top directing talent for that genre**  
    For films in the Sci FI / Action / Adventure / Fantasy categories, the Russo brothers, Bryan Singer, Christopher Nolan, David Yates, James Wan,  Michael Bay, Peter Jackson, and Ryan Coogler are all top-notch talent.  For the Animated / Family categories, Chris Renaud and Pierre Coffin are better choices.
    
    
-	**Hire top writing talent for that genre**  
    For films in the Sci FI / Action / Adventure / Fantasy categories, Jim Starlin, Gary Scott Thompson, Joss Whedon, Derek Connolly, Suzanne Collins and Stephen McFeely are all top-notch talent.  Larry Lieber might be able to be hired as a consultant, but the fact he is in his 90s probably precludes him from being the primary writer.  For films in the Animated / Family categories, Cinco Paul, Ken Daurio, and Linda Woolverton are better candidates.


## Next Steps 

- **Investigate the interest level of a *Warcraft* sequel or remake.**  
    With a profit of 265 million, the revenue generated by the original movie were average. By comparison, *The Hobbit* films had an average ROI of 724 million despite having similar stylistic elements. Consider bringing in better writing and directing talent as those are possible reasons for its lackluster performance.  If it becomes a huge success, it could be turned into a series of moives much like *Jurassic Park* or *Iron Man*.
    
    
- **Investigate *Overwatch*.**  
    There was an abortive attempt to make *Overwatch* into a Netflix movie or series.  Microsoft now owns the rights.  Consider using them.


- **Consider creating a movie studio.**  
    Microsoft’s in-house CGI talent puts it in a prime position to make Animated films which is the highest grossing genre.  CGI is also used in the highly profitable Action, Sci-Fi, Adventure, and Fantasy genres.  What Microsoft lacks is access to writing and directing talent.  A studio with talent scouts and recruiters from the movie industry could help with that.  It would also be helpful with rebranding and marketing.  "A movie brought to you by Activision Studios" probably sounds better to most people than "A movie brought to you by Microsoft."

## License  

[MIT](https://choosealicense.com/licenses/mit/)
