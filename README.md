---
title: "AI idea: Book recommendator"
subtitle: Building AI course
author: Markus Murto 
date: \today
lang: en-GB
block-headings: true
papersize: a4
header-includes: |
    \usepackage{hyperref}
    \hypersetup{colorlinks, urlcolor=blue}
...

# Book recommendator

My AI idea for the [Building AI course](https://buildingai.elementsofai.com/).

## Summary

The book recommendator AI recommends book titles based user ratings on similar
titles which in turn are determined by Topical Terms defined in the of
[MARC 21](https://www.loc.gov/marc/bibliographic/) compliant data store. User
ratings are gathered from the user and the Topical Terms are fetched from an
internal library information system. The application would be accessible
only internally for librarians.

## Background

Book worms might consider the existing solutions, for example from
[Goodreads](https://www.goodreads.com/), to be inadequate or not accurate
enough. The idea is to use the internal data used in library catalogue systems,
which can contain more useful and comprehensive keywords to determine
appropriate books for recommendations. 

The list of keywords used in library system is also more reliable and regulated
compared to amateur user generated keywords. In Finnish libraries
[YKL](https://finto.fi/ykl/fi/) (Yleisten kirjastojen luokitusjärjestelmä)
regulates which keywords are used, so there should not be overlapping or
inconsistent keywords in the data set.

## Data sources and AI methods

The main data used to distinguish different kind of titles from each other
would be the 650 Topical Term field in an internal library MARC 21 compliant
cataloguing system. Regular expressions should be a sufficient method of parsing
the field.

The 650 field often contains between 5 and 15 different standardised terms, so
the field can be an accurate way to categorically classify different kind of
books. The different books could be classified using a unsupervised clustering
algorithm. This could be for example K-means clustering algorithm.

Each user can give ratings from 1 to 5 (5 star rating scale) which is then used
to classify for each user which kind of books they like. As different book
types are clustered in advance, a linear regression model could be powerful
enough to find suitable book clusters for a user using the number of books
read in each cluster and the rating given to each read book by the user.

## How it is used

Ideally the application would be deployed in the library internal network, to
enable access to the MARC 21 compatible cataloguing system used in the library,
which is likely fire-walled to be only accessible from the internal network.

The application would present a web interface to users, in which the user can
insert which books they have read and rating on 1 to 5 scale to each book. The
application would present a selection of books the user have not read which the
model has determined to be suitable recommendations; which books the user
likely would give a high rating.

Additionally the application could include user defined filter, if a user
wants to categorically exclude certain types of books. For example a user might
want to avoid books about war.

## Challenges

Especially the clustering algorithm, which classifies the books in the library,
would need to be refitted regularly as the library catalogue, and the topical
terms used in it, is constantly changing.

Books with no defined topical terms creates a challenge for the application as
they would have to be dropped out of the model until they have been given at
least one topical term. Preferably the books would have more than few topical
terms defined.

## What next

The idea would need to be tested with real world data to find which algorithms
are actually workable with this kind of data. The K-means and linear regression
are virtually just guesstimates which could maybe work. Also the whole idea
of using two different algorithms should be reconsidered, if it would be more
appropriate to use one complex algorithm instead.

In the deployment environment there would be need for dedicated personnel to
fill in gaps in the data: books which currently have no topical terms defined.

## Acknowledgements

I would like thank my librarian friend nicknamed Nalice for verbose information
on library catalogue system.

