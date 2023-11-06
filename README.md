# D-Lab Python Web Scraping Workshop

[![Datahub](https://img.shields.io/badge/launch-datahub-blue)](https://dlab.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2Fdlab-berkeley%2FPython-Web-Scraping&urlpath=lab%2Ftree%2FPython-Web-Scraping%2F&branch=main)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dlab-berkeley/Python-Web-Scraping/HEAD)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)


This repository contains the materials for D-Lab’s Python Web Scraping Workshop.
We recommend attending Python Fundamentals and Python Data Wrangling prior to
this workshop. We additionally recommend a basic understanding of HTML and CSS.

Check D-Lab's [Learning Pathways](https://dlab-berkeley.github.io/dlab-workshops/python_path.html) to figure out which of our workshops to take!


## Workshop Goals

In this workshop, we cover how to scrape data from the web using Python. Web
scraping involves downloading a webpage's source code and sifting through the
material to extract desired data.

Web scraping is typically only done when Web APIs are not available. Platforms
like Twitter, Reddit, or The New York Times offer APIs to retrieve data. If you
want to learn how to use web APIs in Python, see D-Lab's [Python Web
APIs](https://github.com/dlab-berkeley/Python-Web-APIs) workshop.

## Installation Instructions

Anaconda is a useful package management software that allows you to run Python
and Jupyter notebooks easily. Installing Anaconda is the easiest way to make
sure you have all the necessary software to run the materials for this workshop.
If you would like to run Python on your own computer, complete the following
steps prior to the workshop:

1. [Download and install Anaconda (Python 3.9
   distribution)](https://www.anaconda.com/products/individual). Click the
   "Download" button.

2. Download the Python Web Scraping [workshop
   materials](https://github.com/dlab-berkeley/Python-Web-Scraping):

   -   Click the green "Code" button in the top right of the repository
        information.
   -   Click "Download Zip".
   -   Extract this file to a folder on your computer where you can easily
        access it (we recommend Desktop).

3. Optional: if you're familiar with `git`, you can instead clone this
   repository by opening a terminal and entering the command `git clone
   git@github.com:dlab-berkeley/Python-Web-Scraping.git`.


## Is Python Not Working on Your Computer?

If you do not have Anaconda installed and the materials loaded on your workshop
by the time it starts, we *strongly* recommend using the UC Berkeley Datahub to
run the materials for these lessons. You can access the DataHub by clicking this
button: 

[![Datahub](https://img.shields.io/badge/launch-datahub-blue)](https://dlab.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2Fdlab-berkeley%2FPython-Web-Scraping&urlpath=lab%2Ftree%2FPython-Web-Scraping%2F&branch=main)

The DataHub downloads this repository, along with any necessary packages, and
allows you to run the materials in a Jupyter notebook that is stored on UC
Berkeley's servers. No installation is necessary from your end - you only need
an internet browser and a CalNet ID to log in. By using the DataHub, you can
save your work and come back to it at any time. When you want to return to your
saved work, just go straight to [DataHub](https://datahub.berkeley.edu), sign
in, and you click on the `Python-Web-Scraping` folder.

If you don't have a Berkeley CalNet ID, you can still run these lessons in the
cloud, by clicking this button:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dlab-berkeley/Python-Web-Scraping/HEAD)

By using this button, however, you cannot save your work.

## Run the code

1. Open the Anaconda Navigator application. You should see the green snake logo
   appear on your screen. Note that this can take a few minutes to load up the
   first time. 

2. Click the "Launch" button under "Jupyter Notebooks" and navigate through your
   file system to the `Python-Web-Scraping` folder you downloaded above.  Note
   that, if you download the materials from GitHub, the folder name may instead
   be `Python-Text-Analysis-main`.

3. Open the `lessons` folder, and click `01_introduction.md` to begin.

4. Press Shift + Enter (or Ctrl + Enter) to run a cell.

5. By default, the necessary packages for this workshop should already be
   installed. You can install them within the Jupyter notebook by running the
   following line in its own cell:

> ```%pip install -r requirements.txt```

Note that all of the above steps can be run from the terminal, if you're
familiar with how to interact with Anaconda in that fashion. However, using
Anaconda Navigator is the easiest way to get started if this is your first time
working with Anaconda.

# About the UC Berkeley D-Lab

D-Lab works with Berkeley faculty, research staff, and students to advance
data-intensive social science and humanities research. Our goal at D-Lab is to
provide practical training, staff support, resources, and space to enable you to
use R for your own research applications. Our services cater to all skill levels
and no programming, statistical, or computer science backgrounds are necessary.
We offer these services in the form of workshops, one-to-one consulting, and
working groups that cover a variety of research topics, digital tools, and
programming languages.  

Visit the [D-Lab homepage](https://dlab.berkeley.edu/) to learn more about us.
You can view our [calendar](https://dlab.berkeley.edu/events/calendar) for
upcoming events, learn about how to utilize our
[consulting](https://dlab.berkeley.edu/consulting) and [data
services](https://dlab.berkeley.edu/data), and check out upcoming
[workshops](https://dlab.berkeley.edu/events/workshops). Subscribe to our
[newsletter](https://dlab.berkeley.edu/news/weekly-newsletter) to stay up to
date on D-Lab events, services, and opportunities.

# Other D-Lab Python Workshops

D-Lab offers a variety of Python workshops, catered toward different levels of
expertise.

## Introductory Workshops

-  [Python Fundamentals](https://github.com/dlab-berkeley/Python-Fundamentals)
-  [Python Data Wrangling](https://github.com/dlab-berkeley/Python-Data-Wrangling)
-  [Python Data Visualization](https://github.com/dlab-berkeley/Python-Data-Visualization)

## Intermediate and Advanced Workshops

-  [Python Geospatial Fundamentals](https://github.com/dlab-berkeley/Geospatial-Data-and-Mapping-in-Python)
-  [Python Web Scraping and APIs](https://github.com/dlab-berkeley/Python-Web-Scraping)
-  [Python Machine Learning](https://github.com/dlab-berkeley/Python-Machine-Learning)
-  [Python Text Analysis](https://github.com/dlab-berkeley/Python-Text-Analysis)
-  [Python Deep Learning](https://github.com/dlab-berkeley/Python-Deep-Learning)

# Contributors

* [Rochelle Terman](https://github.com/rochelleterman)
* [George McIntire](https://github.com/GeorgeMcIntire)
* [Pratik Sachdeva](https://github.com/pssachdeva)
* [Tom van Nuenen](https://github.com/tomvannuenen)
