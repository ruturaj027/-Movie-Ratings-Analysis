# -Movie-Ratings-Analysis
An R-based data analysis project exploring movie ratings from multiple sources to identify trends, visualize patterns, and derive insights using tidyverse and other data science libraries.

install.packages("tidyverse") 
library(tidyverse)
movies <- read_csv("movie_metadata.csv")
ggplot(movies, aes(x = imdb_score)) +
geom_histogram(binwidth = 0.5, fill = "dodgerblue", color = "white") +
labs(title = "Distribution of IMDB Scores",
 subtitle = "Most movies score between 5-8",
 x = "Rating (1-10)",
 y = "Number of Movies") +
 scale_x_continuous(breaks = 1:10) +
 theme_minimal()
movies %>%
 separate_rows(genres, sep = "\\|") %>%
 group_by(genres) %>%
 summarise(avg_rating = mean(imdb_score, na.rm = TRUE)) %>%
 arrange(desc(avg_rating)) %>%
 head(10) %>%
 ggplot(aes(x = reorder(genres, avg_rating), y = avg_rating)) +
 geom_col(fill = "darkblue") +
 coord_flip() +
 labs(title = "Highest Rated Movie Genres",
 x = "",
 y = "Average IMDB Score") +
 geom_text(aes(label = round(avg_rating, 1)),
 hjust = -0.1, size = 3) +
 theme_minimal
