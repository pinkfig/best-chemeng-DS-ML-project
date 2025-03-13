# best-chemeng-DS-ML-project
Sherry, Bharti, and Carter's CHEMENG DS/ML Project :)

FUN FACTS ABOUT RANDOM FOREST IMPLEMENTATION IN PYTHON
https://builtin.com/data-science/random-forest-python-deep-dive

REPO WITH ALL THE SCRIPTS BY THE OG AUTHORS
https://github.com/energystatusdata/bat-age-data-scripts

=======================================================================================
PRE-PROCESSING DATA
=======================================================================================

Our program requires extensive pre-processing. The original dataset contains thousands of
csv files. The Zip files containing all of these can be located here:

https://drive.google.com/drive/folders/1yhPxQQflXhciPLblkHfrIW8ydF6nWYnQ?usp=sharing

Because this dataset is so large, we can not upload it directly to github, but
it can be downloaded and unzipped from the shared Google drive link.
For our purposes in predicting end-of-life, we only needed the information from
cell_eocv2.zip. This file contains 228 csv files. It also is too large to upload to github.
For this 
reason, we have uploaded an unzipped folder of eocv2 here: 

https://drive.google.com/drive/folders/1r25kGjtFxS0VYu4mkrVXjF9MHjnRd5gm?usp=drive_link

This is the only folder that is used for our program. For preprocessing, we created
a separate program on Google Colab and individually download each file into the
current Colab python environment using a Google Cloud API. From here, the program
processes data by finding cyclic data samples (there are 144 of them in our dataset),
parsing out unnecesary data, determining state of charge windows, and averaging out
other necessary test statistics. This data is compiled into a singular csv file
that is automatically downloaded to the user's computer after the program finishes.
Because the program must individually download all files via the web, it can take
~20 minutes for the csv file to generate after clicking run.

The instructions for running this program are as follows: 

1.) Open the Summary_CSV_Compiler.ipynb in Google Colab. The script is posted in the
repository, but a link to a version you can use directly is here: 

https://colab.research.google.com/drive/1WHm7P4cXpyX6ZtyLOw_uBmckO7ECjdkx?usp=sharing

2.) Install the required packages: requests, pandas, gdown, google-colab, os, time, re,
and shutil. (os, time, re, and shutil are part of the standard python library,
and google-colab should work by default if running in colab. For this reason, usually
you only need to install by running: 

!pip install --upgrade requests pandas gdown

This is included in the first cell, which you can run separately if you'd like.

3.) Download an extension from chrome webstore. This essentially passes browser cookies
on to Google Drive to ensure you aren't a robot wasting bandwidth downloading
files from the Drive. The link to the extension is here:

https://chromewebstore.google.com/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc?pli=1

Once downloaded, open the extension and click "Export All Cookies." This will
download a cookies.txt cfile to your computer.

4.) Run the #COOKIES cell. It will prompt you to upload a file. Upload the cookies.txt file
that was just downloaded in step 3. This passes the cookies as authentication in the program.

5.) Run the #SUMMARY_CSV_COMPILER cell. 

6.) The program will prompt you: 
"Enter your Google Drive folder shareable link (containing the CSV files):"

Enter this link, which is the link to the EOCV2 dataset folder in google drive: 

https://drive.google.com/drive/folders/1r25kGjtFxS0VYu4mkrVXjF9MHjnRd5gm?usp=drive_link

7.) The program will then prompt you:
"Enter your Google API key (folder must be publicly shared):"

Enter this key:

AIzaSyD0-kbdS3GOuRiKcbqXOzYQzlHEZ580qJI

8.) The program will run by downloading all 228 files and then processing them for necessary
information. Note that this may take a while, often ~20 minutes. After the program is done,
you will have a summary.csv file that you can use to upload to the modelling python script.

=======================================================================================
MACHINE LEARNING MODEL
=======================================================================================

