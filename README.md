# Assignment-3.4

1. Import the Titanic Dataset from the link Titanic Data Set.
Perform the following:
a. Preprocess the passenger names to come up with a list of titles that represent families
and represent using appropriate visualization graph.

      #creating new dataframe with the separate col for lastname and firstname from titanic df
      install.packages(&quot;tidyr&quot;)
      library(tidyr)
      install.packages(&quot;dplyr&quot;)
      library(dplyr)
      titan_train=separate(titanic_train, Name,c(&quot;lastname&quot;,&quot;firstname&quot;), &quot;, &quot;)
      #to get the df with
      library(sqldf)
      titan_lastname=sqldf(&quot;select lastname, count(PassengerId) from titan_train where parch&gt;0 or sibsp&gt;0
      group by lastname&quot;)
      #convert to df
      titan_lastname_df=as.data.frame(titan_lastname)
      #draw word cloud of list of titles having families
      library(wordcloud)
      library(&quot;tm&quot;)
      set.seed(1234)
      wordcloud(words = titan_lastname_df$lastname, freq = titan_lastname_df$`count(PassengerId)`,
      min.freq = 1, max.words=Inf,scale=c(2,.3), random.order=FALSE, rot.per=0.35, colors=brewer.pal(8,
      &quot;Dark2&quot;))

b. Represent the proportion of people survived from the family size using a graph.

      titan_lastname=sqldf(&quot;select lastname, count(PassengerId), sum(Survived) from titan_train where
      parch&gt;0 or sibsp&gt;0 group by lastname&quot;)

      barplot(table(titan_lastname_df$`sum(Survived)`, titan_lastname_df$`count(PassengerId)`), legend.text
      = TRUE,beside = TRUE )

c. Impute the missing values in Age variable using Mice Library, create two different
graphs showing Age distribution before and after imputation.
