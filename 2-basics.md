# Open Refine Basics

## Creating a new OpenRefine project

In Windows, you can start the OpenRefine program by double-clicking on the openrefine.exe file. Java services will start automatically on your machine, and OpenRefine will open in your browser. On a Mac, OpenRefine can be launched from your Applications folder. If you are using Linux, you will need to navigate to your OpenRefine directory in the command line and run `./refine`.

OpenRefine can import a variety of file types, including tab separated (`tsv`), comma separated (`csv`), Excel (`xls`, `xlsx`), JSON, XML, RDF as XML, Google Spreadsheets. See the [OpenRefine Importers page](https://github.com/OpenRefine/OpenRefine/wiki/Importers) for more information.

In this first step, we'll browse our computer to the sample data file for this lesson.
In this case, we will be using data obtained from interviews of farmers in two countries in eastern sub-Saharan Africa (Mozambique and Tanzania).
Instructions on downloading the data are available
[here](https://github.com/dressupucla/openrefine/blob/master/setup.md).

Once OpenRefine is launched in your browser, the left margin has options to `Create Project`, `Open Project`, or `Import Project`. Here we will create a new project:

1. Click `Create Project` and select `Get data from` `This Computer`.  
2. Click `Choose Files` and select the file `SAFI_openrefine.csv`. Click `Open` or double-click on the filename.  
3. Click `Next>>` under the browse button to upload the data into OpenRefine.  
4. OpenRefine gives you a preview - a chance to show you it understood the file. If, for example, your file was really tab-delimited, the preview might look strange, you would choose the correct separator in the box shown and click `Update Preview` (bottom left). If this is the wrong file, click `<<Start Over` (upper left).  There are also options to indicate whether the dataset has column headers included and whether OpenRefine should skip a number of rows before reading the data.  

![Parse Options](https://datacarpentry.org/openrefine-socialsci/fig/OR_01_parse_options.png)

5. If all looks well, click `Create Project>>` (upper right).  

Note that at step 1, you could upload data in a standard form from a web address by selecting `Get data from` `Web Addresses (URLs)`. However, this won't work for all URLs.  

## Using Facets

*Exploring data by applying multiple filters*

Facets are one of the most useful features of OpenRefine and can help both get an overview of the data in a project as well as helping you bring more consistency to the data. OpenRefine supports faceted browsing as a mechanism for

* seeing a big picture of your data, and
* filtering down to just the subset of rows that you want to change in bulk.

A 'Facet' groups all the like values that appear in a column, and then allow you to filter the data by these values and edit values across many records at the same time.

One type of Facet is called a 'Text facet'. This groups all the identical text values in a column and lists each value with the number of records it appears in. The facet information always appears in the left hand panel in the OpenRefine interface.

### Exercise 1
Here we will use faceting to look for potential errors in data entry in the `village` column.

1. Scroll over to the `village` column.
2. Click the down arrow and choose `Facet` > `Text facet`.
3. In the left panel, you'll now see a box containing every unique value in the `village` column
along with a number representing how many times that value occurs in the column.
4. Try sorting this facet by name and by count. Do you notice any problems with the data? What are they?
5. Hover the mouse over one of the names in the `Facet` list. You should see that you have an `edit` function available.
6. You could use this to fix an error immediately, and OpenRefine will ask whether you want to make the same correction to every value it finds like that one. But OpenRefine offers even better ways to find and fix these errors, which we'll use instead. We'll learn about these when we talk about clustering.

> ### Solution
> - `Chirdozo` is likely a mis-entry of `Chirodzo`.
> - `Ruca` is likely a mis-entry of `Ruaca`.
> - `Ruaca - Nhamuenda` and `Ruaca-Nhamuenda` refer to the same place (differ only by spaces around the hyphen). You might also wonder if both of these are the same as `Ruaca`. We will see how to correct these misspelled and mistyped entries in a later exercise.
> - The entry `49` is almost certainly an error but you will not be able to fix it by reference to other data. 

### Exercise 2
1. Using faceting, find out how many different `interview_date` values there are in the survey results.
2. Is the column formatted as Text or Date?
3. Use faceting to produce a timeline display for `interview_date`. You will need to use `Edit cells` > `Common transforms` > `To date` to convert this column to dates.
4. During what period were most of the interviews collected?

> ### Solution
> - For the column `interview_date` do `Facet` > `Text facet`. A box will appear in the left panel showing that there are 19 unique entries in this column.   
> - By default, the column `interview_date` is formatted as Text. You can change the format by doing `Edit cells` > `Common transforms` > `To date`. Notice the the values in the column turn green. Doing `Facet` > `Timeline facet` creates a box in the left panel that shows a histogram of the number of entries for each date.  
> - Most of the data was collected in November of 2016.  

## More on Facets
[OpenRefine Wiki: Faceting](https://github.com/OpenRefine/OpenRefine/wiki/Faceting)

As well as 'Text facets' Refine also supports a range of other types of facet. These include:
* Numeric facets
* Timeline facets (for dates)
* Custom facets
* Scatterplot facets

**Numeric and Scatterplot facets** display graphs instead of lists of values. The numeric facet graph includes 'drag and drop' controls you can use to set a start and end range to filter the data displayed. These facets are explored further in [Examining Numbers in OpenRefine](http://www.datacarpentry.org/OpenRefine-ecology-lesson/03-numbers/)

**Custom facets** are a range of different types of facets. Some of the default custom facets are:
* Word facet - this breaks down text into words and counts the number of records each word appears in
* Duplicates facet - this results in a binary facet of 'true' or 'false'. Rows appear in the 'true' facet if the value in the selected column is an exact match for a value in the same column in another row
* Text length facet - creates a numeric facet based on the length (number of characters) of the text in each row for the selected column. This can be useful for spotting incorrect or unusual data in a field where specific lengths are expected (e.g. if the values are expected to be years, any row with a text length more than 4 for that column is likely to be incorrect)
* Facet by blank - a binary facet of 'true' or 'false'. Rows appear in the 'true' facet if they have no data present in that column. This is useful when looking for rows missing key data.

## Using clustering to detect possible typing errors

In OpenRefine, clustering means "finding groups of different values that might be alternative representations of the same thing". For example, the two strings `New York` and `new york` are very likely to refer to the same concept and just have capitalization differences. Likewise, `Gödel` and `Godel` probably refer to the same person. Clustering is a very powerful tool for cleaning datasets which contain misspelled or mistyped entries. OpenRefine has several clustering algorithms built in. Experiment with them, and learn more about these algorithms and how they work.

1. In the `village` Text Facet we created in the step above, click the `Cluster` button.
2. In the resulting pop-up window, you can change the `Method` and the `Keying Function`. Try different combinations to
 see what different mergers of values are suggested.
3. Select the `key collision` method and `metaphone3` keying function. It should identify two clusters.
4. Click the `Merge?` box beside each cluster, then click `Merge Selected and Recluster` to apply the corrections to the dataset.
4. Try selecting different `Methods` and `Keying Functions` again, to see what new merges are suggested. 
5. You should find no more clusters are found. None of the available methods offered to cluster `Ruaca-Nhamuenda` with `Ruaca` or `Chirdozo` with `Chirodzo`.  To merge these values we need to hover over them in the village text facet, select edit, and manually change the names.
6. Change `Chirdozo` to `Chirodzo` and `Ruaca-Nhamuenda` to `Ruaca`. You should now have four clusters: `Chirodzo`, `God`, `Ruaca` and `49`.

Important: If you `Merge` using a different method or keying function, or more times than described in the instructions above,
your solutions for later exercises will not be the same as shown in those exercise solutions.

## Different clustering algorithms

The technical details of how the different clustering algorithm work can be found at the link below.

[More on clustering](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth)
