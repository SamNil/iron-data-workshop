# OpenRefine

Much of this material is modified from [the Data Carpentry lesson on OpenRefine in Ecology](http://www.datacarpentry.org/OpenRefine-ecology-lesson/), which is released under an open license.

---

## Learning Objectives

* Describe OpenRefine’s uses and applications.
* Differentiate data cleaning from data organization.
* Experiment with OpenRefine’s user interface.
* Locate helpful resources to learn more about OpenRefine.


## Overview

Using OpenRefine offers some really nice benefits:
* It's really important that you know what you did. More journals/grants/etc. are also making it important for them to know what you did. You can capture all steps done to your data in OpenRefine to the raw file and share them with your publication as supplemental material.
* All steps are easily reversed in Refine.
* You _must_ save your work to a new file; Refine _does not_ modify your original dataset.
* Data is often very messy - and this tool saves a lot of cleaning headaches.
* Data cleaning steps often need repeating with multiple files. Refine is perfect for speeding up repetitive tasks.
* Some concepts like clustering algorithms are quite complex, but Refine makes it easy to introduce them, use them, and show their power.

## Before we get started

* Check that you have Firefox or Chrome browsers installed. Open Refine runs in your default browser. It will not run correctly in Internet Explorer.
* Download software from [http://openrefine.org](http://openrefine.org) if you have not done this yet.
* Unzip the downloaded file into a directory by double-clicking it (Mac) or right-clicking and selecting "Extract..." on Windows. Name that directory something like Open-Refine.
* Go to your newly created Open-Refine directory.
* Launch Open Refine
  * Windows: Click the google-refine.exe (this will launch a command prompt window, but you can ignore that and wait for the browser to launch)
  * Mac: Drag icon into Applications folder, and Ctrl-click/Open... it. (See [this article](https://support.apple.com/kb/PH21769?locale=en_US) for more information on what you're doing here.)
  * Linux: Type `./refine` into the terminal within the OpenRefine directory
* Note: this is a Java program that runs on your machine (not in the cloud). It runs inside your browser, but no web connection is needed.
* If you are using a different browser, or OpenRefine does not automatically open for you, point your browser at http://127.0.0.1:3333/ or http://localhost:3333 to launch the program.

## Basics of OpenRefine

You can find out a lot more about OpenRefine at [http://openrefine.org]() and check out some great introductory videos. There is a [Google Group](https://groups.google.com/forum/?hl=en#!forum/openrefine) that can answer a lot of beginner questions and problems. There is also an [Open Refine Google Plus community](https://plus.google.com/communities/117280693504889048168) where you can find a lot of help and a lot of folks from the life sciences are members. As with other programs of this type, OpenRefine libraries are available too, where you can find a script you need and copy it into your Refine instance to run it on your dataset.

## Features
* Open source ([source on GitHub](https://github.com/OpenRefine/OpenRefine)).
* A large growing community, from novice to expert, ready to help.
* Works with large-ish datasets (100,000 rows). Does not scale to many millions. (yet).

In this lesson, we're going to talk about:

1. Working with OpenRefine
2. OpenRefine scripts
3. Saving and exporting from OpenRefine


# 1. Working with OpenRefine

## Creating a Project

Start the program. (Double-click on the google-refine.exe file. Java services will start on your machine, and Refine will open in your browser).

Note the file types Open Refine handles: TSV, CSF, *SV, Excel (.xls .xlsx), JSON, XML, RDF as XML, Google Data documents. Support for other formats can be added with Google Refine extensions.

If you haven't already, download the 'iron.csv' data file.


**Once Refine is open, you'll be asked if you want to Create, Open, or Import a Project.**

```
  To create a project,
  - click Create... and it will bring you to "Get data from this computer."
  - Click Browse, find iron.csv
  - Click next to open iron.csv
  - Refine gives you a preview - a chance to show you it understood the file. If, for example, your file was really tab-delimited, the preview might look strange, you would choose the correct separator in the box shown and click "update preview."
  - If all looks well, click _Create Project._
```

## Faceting

*Exploring data by applying multiple filters*

OpenRefine supports faceted browsing as a mechanism for

* seeing a big picture of your data, and
* filtering down to just the subset of rows that you want to change in bulk.

Typically, you create a facet on a particular column. The facet summarizes the cells in that column to give you a big picture on that column, and allows you to filter to some subset of rows for which their cells in that column satisfy some constraint. That's a bit abstract, so let's jump into some examples.

[More on faceting](https://github.com/OpenRefine/OpenRefine/wiki/Faceting)

````
  - Locate the station_name column
  - Click the down arrow and choose > Facet > Text facet
  - In the left margin, you'll see a box containing every unique, distinct value in the station_name column and Refine shows you how many times that value occurs in the column (a count), and allows you to sort (order) your facets by name or count.
  - Try editing. For example, you could change the single 'Glenwod Springs' to 'Glenwood Springs' if you knew it was a typo.
  - Note that at any time, in any cell of the Facet box, or data cell in the Refine window, you have access to "edit" and can fix an error immediately. Refine will even ask you if you'd like to make that same correction to every value it finds like that one (or not).
````

## Clustering

One of the most magical bits of Refine are the several clustering algorithms built in. 
In OpenRefine, clustering refers to the operation of "finding groups of different values that might be alternative representations of the same thing". For example, the two strings "New York" and "new york" are very likely to refer to the same concept and just have capitalization differences. Likewise, "Gödel" and "Godel" probably refer to the same person.

````
  - Start with the Text Facet you created for the 'station_name" column and click the _Cluster_ button.
  - In the resulting pop-up window, you can change the algorithm method, and keying function. Try different combinations to see the difference.
  - For example, with this dataset, the _key collision_ method with the _metaphone3_ keying function does a pretty good job. 
  - Intentional errors in these station names have been introduced to show how errors (typos) in any position can be found with this method. All errors can then be fixed by simply entering the correct value in the box on the right. Often, the algorithm has guessed correctly. 
  - After corrections are made in this window, you can either Merge and Close the Cluster pop-up, or Merge and Re-cluster.
````

[More on clustering](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth)


## Split / Leading - Trailing Whitespace / Undo - Redo

If data in a column needs to be split into multiple columns, and the strings in the cells are separated by a common separator (say a comma, or a space), you can use that separator to divide up the bits into their own columns.

````
  - Go to the drop-down tab at the top of the column that you need to split into multiple columns
  - For example, go to the datetime_utc column > from drop-down choose Edit Column > Split into several columns
  - In the pop-up, for separator, remove the comma, put in a space
  - Remove the check in the box that says "remove column after splitting"
  - You'll get two extra columns called, in this case: datetime_utc 1, datetime_utc 2
  - Try to rename the datetime utc 1 column to 'date'. What happens when you do that?
  - To Undo create columns, look just above the station_name facet in the left side of the screen. Click where it says Undo / Redo. Click back one step (all steps, all changes are saved here). Just go back to the previous step and click. The extra columns will be gone.
  
Note: a very common data typo is extra spaces or tabs, which can be hard for human eyes to see but read differently by a computer. These can be easily removed with another Refine feature in the column drop-down choices. See drop-down: Edit cells > Common transforms > Remove leading and trailing whitespace
  
````


# 2. OpenRefine scripts

## Scripts

* Refine saves every change, every edit you make to the dataset in a file you can save on your machine.
* If you had 20 files to clean, and they all had the same type of errors, and all files had the same columns, you could save the script, open a new file to clean, paste in the script and run it. Voila, clean data.

````
  - In the Undo / Redo section, click Extract, save the bits desired using the check boxes. 
  - Copy the code and paste it into a text editor. Save it as a .txt file. 
````

To run these steps on a new dataset, import the new dataset into Refine, open the Extract / Apply section, paste in the .txt file, click Apply.


# 3. Saving and exporting from OpenRefine

## Saving and Exporting a Project

In OpenRefine you can save or export the project. This means you're saving the data and all the 
information about the cleaning steps you've done. Once you've saved a Project, you can
open it up again and be just where you left off.

### Saving

By default OpenRefine is saving your project. If you close OpenRefine and open it up again,
you'll see a list of your projects. You can click on any one of them to open it up again.

### Exporting

You can also export a project, for instance if you wanted to send it to someone else. 

````
  - Go to the 'Export' button in the top right. Click 'Export project'. This will save a compressed file that you can then open in OpenRefine that contains all the data and steps. 
````

## Exporting Cleaned Data 

Save your work when you are done by exporting it in your desired format. Save your files with meaningful names, no spaces. Refine does not change your original dataset (hooray!).

````
  - Go to 'Export' in the top right. Click on the file type you want to export the data in. 'Tab-separated values' or 'Comma-separated values' would be good choices. 
````

That file will get exported to your default Download directory. That file can then be eaily opened in a spreadsheet program or imported into programs like R or Python.


