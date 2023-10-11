Group 3 Data Cleaning and Analysis
================
Anum, Blagoja, Hannah, Nolan
Final Report Due Monday, March 13, 2023

- <a href="#introduction" id="toc-introduction">Introduction</a>
  - <a href="#information-about-each-datasets-from-the-project"
    id="toc-information-about-each-datasets-from-the-project">Information
    about each datasets from the project</a>
  - <a href="#target-variables-of-data-science-project"
    id="toc-target-variables-of-data-science-project">Target variables of
    Data Science Project</a>
  - <a href="#data-visualization" id="toc-data-visualization">Data
    Visualization</a>

# Introduction

Project Proposal:
<https://docs.google.com/document/d/12Ly0ewjRK-uhTVQvT38E0vjMvc8uvwr67GpmBKwA2ak/edit?usp=sharing>

In this project, we are going to be using the two datasets that we found
on Kaggle: “Highest Holywood Grossing Movies.csv” and
“imdb_top_1000.csv”. We would be renaming them as
‘Highest_Holywood_Grossing_Movies’ and ‘imdb_top_1000’ dataframes to
work with in our project.

## Information about each datasets from the project

### Highest Holywood Grossing Movies.csv dataset

Data frame Highest_Holywood_Grossing_Movies:  
Rows: 918.  
Columns: 11.  
Variables (Column Names): Title, Movie Info, Distributor, Release Date,
Domestic Sales, International Sales, World Sales, Genre, Movie Runtime,
and License.

### imdb_top_1000.csv dataset

Data frame imdb_top_1000:  
Columns: 16  
Rows: 1,000  
Variables (Column Names): Poster_Link, Series_Title, Released_Year,
Certificate, Runtime, Genre, IMDB_Rating, Overview, Meta_score,
Director, Star1, Star2, Star3, Star4, No_of_votes, and Gross.

## Target variables of Data Science Project

The variables that we are going to work with from the two datasets are
Title, Release Year, Runtime, Genre, Domestic Gross, World Gross,
Distributor, and perhaps others.

In terms of variables we will create, we are interested in perhaps
trying to create a new categorical variable of the gender of different
lead actors, separating the different genres movies are classified in,
and other depending on which questions we choose to focus on.

### Call to the original two datasets:

    ## New names:
    ## Rows: 918 Columns: 11
    ## ── Column specification
    ## ──────────────────────────────────────────────────────── Delimiter: "," chr
    ## (7): Title, Movie Info, Distributor, Release Date, Genre, Movie Runtime,... dbl
    ## (4): ...1, Domestic Sales (in $), International Sales (in $), World Sale...
    ## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    ## Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 1000 Columns: 16
    ## ── Column specification
    ## ──────────────────────────────────────────────────────── Delimiter: "," chr
    ## (12): Poster_Link, Series_Title, Released_Year, Certificate, Runtime, Ge... dbl
    ## (3): IMDB_Rating, Meta_score, No_of_Votes num (1): Gross
    ## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    ## Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## • `` -> `...1`

    ## Rows: 918
    ## Columns: 11
    ## $ ...1                         <dbl> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12,…
    ## $ Title                        <chr> "Star Wars: Episode VII - The Force Awake…
    ## $ `Movie Info`                 <chr> "As a new threat to the galaxy rises, Rey…
    ## $ Distributor                  <chr> "Walt Disney Studios Motion Pictures", "W…
    ## $ `Release Date`               <chr> "December 16, 2015", "April 24, 2019", "D…
    ## $ `Domestic Sales (in $)`      <dbl> 936662225, 858373000, 760507625, 70042656…
    ## $ `International Sales (in $)` <dbl> 1132859475, 1939128328, 2086738578, 64717…
    ## $ `World Sales (in $)`         <dbl> 2069521700, 2797501328, 2847246203, 13475…
    ## $ Genre                        <chr> "['Action', 'Adventure', 'Sci-Fi']", "['A…
    ## $ `Movie Runtime`              <chr> "2 hr 18 min", "3 hr 1 min", "2 hr 42 min…
    ## $ License                      <chr> "PG-13", "PG-13", "PG-13", NA, NA, NA, "P…

    ## Rows: 1,000
    ## Columns: 16
    ## $ Poster_Link   <chr> "https://m.media-amazon.com/images/M/MV5BMDFkYTc0MGEtZmN…
    ## $ Series_Title  <chr> "The Shawshank Redemption", "The Godfather", "The Dark K…
    ## $ Released_Year <chr> "1994", "1972", "2008", "1974", "1957", "2003", "1994", …
    ## $ Certificate   <chr> "A", "A", "UA", "A", "U", "U", "A", "A", "UA", "A", "U",…
    ## $ Runtime       <chr> "142 min", "175 min", "152 min", "202 min", "96 min", "2…
    ## $ Genre         <chr> "Drama", "Crime, Drama", "Action, Crime, Drama", "Crime,…
    ## $ IMDB_Rating   <dbl> 9.3, 9.2, 9.0, 9.0, 9.0, 8.9, 8.9, 8.9, 8.8, 8.8, 8.8, 8…
    ## $ Overview      <chr> "Two imprisoned men bond over a number of years, finding…
    ## $ Meta_score    <dbl> 80, 100, 84, 90, 96, 94, 94, 94, 74, 66, 92, 82, 90, 87,…
    ## $ Director      <chr> "Frank Darabont", "Francis Ford Coppola", "Christopher N…
    ## $ Star1         <chr> "Tim Robbins", "Marlon Brando", "Christian Bale", "Al Pa…
    ## $ Star2         <chr> "Morgan Freeman", "Al Pacino", "Heath Ledger", "Robert D…
    ## $ Star3         <chr> "Bob Gunton", "James Caan", "Aaron Eckhart", "Robert Duv…
    ## $ Star4         <chr> "William Sadler", "Diane Keaton", "Michael Caine", "Dian…
    ## $ No_of_Votes   <dbl> 2343110, 1620367, 2303232, 1129952, 689845, 1642758, 182…
    ## $ Gross         <dbl> 28341469, 134966411, 534858444, 57300000, 4360000, 37784…

### Tidying of the IMDB dataset:

    ## Rows: 1,000
    ## Columns: 15
    ## $ title         <chr> "The Shawshank Redemption", "The Godfather", "The Dark K…
    ## $ released_year <chr> "1994", "1972", "2008", "1974", "1957", "2003", "1994", …
    ## $ certificate   <chr> "A", "A", "UA", "A", "U", "U", "A", "A", "UA", "A", "U",…
    ## $ runtime       <chr> "142 min", "175 min", "152 min", "202 min", "96 min", "2…
    ## $ genre         <chr> "Drama", "Crime, Drama", "Action, Crime, Drama", "Crime,…
    ## $ imdb_rating   <dbl> 9.3, 9.2, 9.0, 9.0, 9.0, 8.9, 8.9, 8.9, 8.8, 8.8, 8.8, 8…
    ## $ overview      <chr> "Two imprisoned men bond over a number of years, finding…
    ## $ meta_score    <dbl> 80, 100, 84, 90, 96, 94, 94, 94, 74, 66, 92, 82, 90, 87,…
    ## $ director      <chr> "Frank Darabont", "Francis Ford Coppola", "Christopher N…
    ## $ star1         <chr> "Tim Robbins", "Marlon Brando", "Christian Bale", "Al Pa…
    ## $ star2         <chr> "Morgan Freeman", "Al Pacino", "Heath Ledger", "Robert D…
    ## $ star3         <chr> "Bob Gunton", "James Caan", "Aaron Eckhart", "Robert Duv…
    ## $ star4         <chr> "William Sadler", "Diane Keaton", "Michael Caine", "Dian…
    ## $ no_of_votes   <dbl> 2343110, 1620367, 2303232, 1129952, 689845, 1642758, 182…
    ## $ gross         <dbl> 28341469, 134966411, 534858444, 57300000, 4360000, 37784…

### Tidying of the Top Grossing Movies dataset:

    ## Rows: 918
    ## Columns: 14
    ## $ title                  <chr> "Star Wars: Episode VII - The Force Awakens", "…
    ## $ movie_info             <chr> "As a new threat to the galaxy rises, Rey, a de…
    ## $ distributor            <chr> "Walt Disney Studios Motion Pictures", "Walt Di…
    ## $ release_date           <chr> "December 16, 2015", "April 24, 2019", "Decembe…
    ## $ domestic_sales_in      <dbl> 936662225, 858373000, 760507625, 700426566, 678…
    ## $ international_sales_in <dbl> 1132859475, 1939128328, 2086738578, 647171407, …
    ## $ world_sales_in         <dbl> 2069521700, 2797501328, 2847246203, 1347597973,…
    ## $ genre                  <chr> "['Action', 'Adventure', 'Sci-Fi']", "['Action'…
    ## $ license                <chr> "PG-13", "PG-13", "PG-13", NA, NA, NA, "PG-13",…
    ## $ runtime                <dbl> 138, 181, 162, 134, 149, 148, 194, 124, 143, 15…
    ## $ action                 <chr> "Y", "Y", "Y", "Y", "Y", "Y", "N", "Y", "Y", "Y…
    ## $ comedy                 <chr> "N", "N", "N", "N", "N", "N", "N", "N", "N", "N…
    ## $ drama                  <chr> "N", "Y", "N", "N", "N", "N", "Y", "N", "N", "N…
    ## $ combo                  <chr> "Action only", "Drama and Action", "Action only…

### Creation of merge dataset:

    ## Rows: 186
    ## Columns: 16
    ## $ title         <chr> "Star Wars: Episode VII - The Force Awakens", "Avengers:…
    ## $ movie_info    <chr> "As a new threat to the galaxy rises, Rey, a desert scav…
    ## $ distributor   <chr> "Walt Disney Studios Motion Pictures", "Walt Disney Stud…
    ## $ release_date  <date> 2015-12-16, 2019-04-24, 2009-12-16, NA, 1997-12-19, 201…
    ## $ release_year  <chr> "2015", "2019", "2009", "2018", "1997", "2012", "2018", …
    ## $ dom_sales     <dbl> 936662225, 858373000, 760507625, 678815482, 659363944, 6…
    ## $ world_sales   <dbl> 2069521700, 2797501328, 2847246203, 2048359754, 22016472…
    ## $ license       <chr> "PG-13", "PG-13", "PG-13", NA, "PG-13", "PG-13", NA, "PG…
    ## $ runtime       <dbl> 138, 181, 162, 149, 194, 143, 118, 118, 152, 129, 164, 1…
    ## $ combo         <chr> "Action only", "Drama and Action", "Action only", "Actio…
    ## $ imdb_rating   <dbl> 7.9, 8.4, 7.8, 8.4, 7.8, 8.0, 7.6, 8.5, 9.0, 8.0, 8.4, 7…
    ## $ meta_score    <dbl> 80, 78, 83, 68, 75, 69, 80, 88, 84, 95, 78, 91, 84, 88, …
    ## $ director      <chr> "J.J. Abrams", "Anthony Russo", "James Cameron", "Anthon…
    ## $ star1         <chr> "Daisy Ridley", "Joe Russo", "Sam Worthington", "Joe Rus…
    ## $ imdb_no_votes <dbl> 860823, 809955, 1118998, 834477, 1046089, 1260806, 25005…
    ## $ month         <fct> 12, 04, 12, NA, 12, 04, NA, 07, 07, 03, 07, 06, 06, 06, …

## Data Visualization

### Rating:

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](project_report_files/figure-gfm/rating_an-1.png)<!-- -->

    ## # A tibble: 3 × 4
    ##   title         meta_score imdb_rating director            
    ##   <chr>              <dbl>       <dbl> <chr>               
    ## 1 The Godfather        100         9.2 Francis Ford Coppola
    ## 2 Gravity               96         7.7 Alfonso Cuarón      
    ## 3 Ratatouille           96         8   Brad Bird

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 6 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 6 rows containing missing values (`geom_point()`).

![](project_report_files/figure-gfm/rating_an-2.png)<!-- -->![](project_report_files/figure-gfm/rating_an-3.png)<!-- -->

    ## # A tibble: 2 × 2
    ##   title           imdb_rating
    ##   <chr>                 <dbl>
    ## 1 The Dark Knight         9  
    ## 2 The Godfather           9.2

### Sales:

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](project_report_files/figure-gfm/sales_an-1.png)<!-- -->

    ## # A tibble: 5 × 4
    ##   title                                      dom_sales world_sales release_year
    ##   <chr>                                          <dbl>       <dbl> <chr>       
    ## 1 Avatar                                     760507625  2847246203 2009        
    ## 2 Avengers: Endgame                          858373000  2797501328 2019        
    ## 3 Titanic                                    659363944  2201647264 1997        
    ## 4 Star Wars: Episode VII - The Force Awakens 936662225  2069521700 2015        
    ## 5 Avengers: Infinity War                     678815482  2048359754 2018

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](project_report_files/figure-gfm/sales_an-2.png)<!-- -->

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](project_report_files/figure-gfm/sales_an-3.png)<!-- -->

### Distributor:

    ## # A tibble: 19 × 1
    ##    distributor                        
    ##    <chr>                              
    ##  1 Columbia Pictures                  
    ##  2 DreamWorks                         
    ##  3 DreamWorks Distribution            
    ##  4 Focus Features                     
    ##  5 Fox Searchlight Pictures           
    ##  6 Lionsgate                          
    ##  7 Metro-Goldwyn-Mayer (MGM)          
    ##  8 Miramax                            
    ##  9 New Line Cinema                    
    ## 10 Orion Pictures                     
    ## 11 Paramount Pictures                 
    ## 12 Revolution Studios                 
    ## 13 Sony Pictures Entertainment (SPE)  
    ## 14 The Weinstein Company              
    ## 15 TriStar Pictures                   
    ## 16 Twentieth Century Fox              
    ## 17 Universal Pictures                 
    ## 18 Walt Disney Studios Motion Pictures
    ## 19 Warner Bros.

![](project_report_files/figure-gfm/distributor_an-1.png)<!-- -->

    ## # A tibble: 10 × 3
    ## # Groups:   distributor [4]
    ##    title                                      distributor                dom_s…¹
    ##    <chr>                                      <chr>                        <dbl>
    ##  1 Star Wars: Episode VII - The Force Awakens Walt Disney Studios Motio…  9.37e8
    ##  2 Avengers: Endgame                          Walt Disney Studios Motio…  8.58e8
    ##  3 Avatar                                     Twentieth Century Fox       7.61e8
    ##  4 Avengers: Infinity War                     Walt Disney Studios Motio…  6.79e8
    ##  5 Titanic                                    Paramount Pictures          6.59e8
    ##  6 The Avengers                               Walt Disney Studios Motio…  6.23e8
    ##  7 Incredibles 2                              Walt Disney Studios Motio…  6.09e8
    ##  8 The Lion King                              Walt Disney Studios Motio…  5.44e8
    ##  9 The Dark Knight                            Warner Bros.                5.35e8
    ## 10 Beauty and the Beast                       Walt Disney Studios Motio…  5.04e8
    ## # … with abbreviated variable name ¹​dom_sales

    ## # A tibble: 10 × 2
    ##    distributor                             n
    ##    <chr>                               <int>
    ##  1 Walt Disney Studios Motion Pictures    38
    ##  2 Warner Bros.                           38
    ##  3 Twentieth Century Fox                  27
    ##  4 Universal Pictures                     19
    ##  5 Paramount Pictures                     16
    ##  6 Sony Pictures Entertainment (SPE)      11
    ##  7 DreamWorks Distribution                 6
    ##  8 New Line Cinema                         5
    ##  9 The Weinstein Company                   5
    ## 10 Lionsgate                               3

![](project_report_files/figure-gfm/distributor_an-2.png)<!-- -->

### Starring actor and director:

![](project_report_files/figure-gfm/director_and_star_an-1.png)<!-- -->

    ## # A tibble: 10 × 2
    ##    star1                 n
    ##    <chr>             <int>
    ##  1 Tom Hanks             9
    ##  2 Leonardo DiCaprio     7
    ##  3 Daniel Radcliffe      6
    ##  4 Tom Cruise            5
    ##  5 Daniel Craig          4
    ##  6 Joe Russo             4
    ##  7 Matt Damon            4
    ##  8 Christian Bale        3
    ##  9 Denzel Washington     3
    ## 10 Elijah Wood           3

![](project_report_files/figure-gfm/director_and_star_an-2.png)<!-- -->![](project_report_files/figure-gfm/director_and_star_an-3.png)<!-- -->

    ## # A tibble: 10 × 2
    ##    director              n
    ##    <chr>             <int>
    ##  1 Steven Spielberg      8
    ##  2 Christopher Nolan     6
    ##  3 David Fincher         5
    ##  4 Peter Jackson         5
    ##  5 Ridley Scott          5
    ##  6 Robert Zemeckis       5
    ##  7 Anthony Russo         4
    ##  8 Clint Eastwood        4
    ##  9 James Cameron         4
    ## 10 Sam Mendes            4

![](project_report_files/figure-gfm/director_and_star_an-4.png)<!-- -->

    ## Warning: Removed 1 rows containing non-finite values (`stat_boxplot()`).

![](project_report_files/figure-gfm/director_and_star_an-5.png)<!-- -->

### Release month:

![](project_report_files/figure-gfm/month_an-1.png)<!-- -->![](project_report_files/figure-gfm/month_an-2.png)<!-- -->![](project_report_files/figure-gfm/month_an-3.png)<!-- -->

### Runtime:

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 6 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 6 rows containing missing values (`geom_point()`).

![](project_report_files/figure-gfm/runtime_an-1.png)<!-- -->

### Release year:

![](project_report_files/figure-gfm/year_an-1.png)<!-- -->![](project_report_files/figure-gfm/year_an-2.png)<!-- -->

### Genre:

![](project_report_files/figure-gfm/genre_an-1.png)<!-- -->![](project_report_files/figure-gfm/genre_an-2.png)<!-- -->

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 6 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 6 rows containing missing values (`geom_point()`).

![](project_report_files/figure-gfm/genre_an-3.png)<!-- -->
