# A Movie Data Analysis for Microsoft

This is a class project designed to test student's ability to use descriptive statistics, python, and pandas.  We were given 5 data sets and were instructed to create a business proposal for Microsoft to enter into the movie industry.  We were assessed by the following criteria: Presentation Content, Slide Style, Presentation Delivery, Business Understanding, Data Understanding, Data Preparation, Data Communication, Authoring Jupyter Notebooks, and Data Manipulation and Analysis with Pandas.  Beyond these guidelines, the project was open-ended.  In an effort to provide full transparency, this repository includes the exploratory notebook I used as as a rough draft as well as the notebook I submitted to be graded. A full git history is unavailable due to my unfamiliarity with git prior to the project but it will be available in subsequent projects.

## Project Overview

The data sources given to the class were as follows:
* [Box Office Mojo](https://www.boxofficemojo.com/)
* [IMDB](https://www.imdb.com/)
* [Rotten Tomatoes](https://www.rottentomatoes.com/)
* [TheMovieDB](https://www.themoviedb.org/)
* [The Numbers](https://www.the-numbers.com/)

The IMDB and the 



For this project, you will use exploratory data analysis to generate insights for a business stakeholder.

### Business Problem

Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. You are charged with exploring what types of films are currently doing the best at the box office. You must then translate those findings into actionable insights that the head of Microsoft's new movie studio can use to help decide what type of films to create.

### The Data

In the folder `zippedData` are movie datasets from:


Because it was collected from various locations, the different files have different formats. Some are compressed CSV (comma-separated values) or TSV (tab-separated values) files that can be opened using spreadsheet software or `pd.read_csv`, while the data from IMDB is located in a SQLite database.

![movie data erd](https://raw.githubusercontent.com/learn-co-curriculum/da-phase2-project-enterprise/master/movie_data_erd.jpeg)

Note that the above diagram shows ONLY the IMDB data. You will need to look carefully at the features to figure out how the IMDB data relates to the other provided data files.

It is up to you to decide what data from this to use and how to use it. If you want to make this more challenging, you can scrape websites or make API calls to get additional data. If you are feeling overwhelmed or behind, we recommend you use only the following data files:

* `im.db.zip`
  * Zipped SQLite database (you will need to unzip then query using SQLite)
  * `movie_basics` and `movie_ratings` tables are most relevant
* `bom.movie_gross.csv.gz`
  * Compressed CSV file (you can open without expanding the file using `pd.read_csv`)

### Key Points

* **Your analysis should yield three concrete business recommendations.** The ultimate purpose of exploratory analysis is not just to learn about the data, but to help an organization perform better. Explicitly relate your findings to business needs by recommending actions that you think the business (Microsoft) should take.

* **Communicating about your work well is extremely important.** Your ability to provide value to an organization - or to land a job there - is directly reliant on your ability to communicate with them about what you have done and why it is valuable. Create a storyline your audience (the head of Microsoft's new movie studio) can follow by walking them through the steps of your process, highlighting the most important points and skipping over the rest.

* **Use plenty of visualizations.** Visualizations are invaluable for exploring your data and making your findings accessible to a non-technical audience. Spotlight visuals in your presentation, but only ones that relate directly to your recommendations. Simple visuals are usually best (e.g. bar charts and line graphs), and don't forget to format them well (e.g. labels, titles).

## Deliverables

There are two deliverabl
## Grading

This project has a combination of Complete/Incomplete rubric items and rubric items graded on a scale from "Exceeds Objective" down to "Does Not Meet Objective".

### Complete/Incomplete Rubric Items

These items will be graded as Complete/Incomplete:

1. Presentation Content
2. Slide Style
3. Presentation Delivery
4. Business Understanding
5. Data Understanding
6. Data Preparation


