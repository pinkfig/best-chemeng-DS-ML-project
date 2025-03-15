# best-chemeng-DS-ML-project
Sherry, Bharti, and Carter's CHEMENG DS/ML Project :)

FUN FACTS ABOUT RANDOM FOREST IMPLEMENTATION IN PYTHON
https://builtin.com/data-science/random-forest-python-deep-dive

REPO WITH ALL THE SCRIPTS BY THE OG AUTHORS
https://github.com/energystatusdata/bat-age-data-scripts

PRE-PROCESSING DATA
=======================================================================================

Our program requires extensive pre-processing. The original dataset contains thousands of
csv files. The Zip files containing all of these can be located here:

https://drive.google.com/drive/folders/1yhPxQQflXhciPLblkHfrIW8ydF6nWYnQ?usp=sharing

Because this dataset is so large, we cannot upload it directly to GitHub, but
it can be downloaded and unzipped from the shared Google Drive link.
For our purposes in predicting end-of-life (EoL), we only needed the information from
cell_eocv2.zip. This file, containing 228 .csv files, is also is too large to upload to GitHub.
For this reason, we have uploaded an unzipped folder of eocv2 here: 

https://drive.google.com/drive/folders/1r25kGjtFxS0VYu4mkrVXjF9MHjnRd5gm?usp=drive_link

This is the only folder that is used for our program. For preprocessing, we created
a separate program on Google Colab and individually downloaded each file into the
current Colab Python environment using a Google Cloud API. From here, the program
processes data by finding cyclic data samples (there are 144 of them in our dataset),
parsing out unnecesary data, determining state-of-charge (SoC) windows, and averaging out
other necessary test statistics. This data is compiled into a singular .csv file
that is automatically downloaded to the user's computer after the program finishes.
Because the program must individually download all files via the web, it can take
~20 minutes for the .csv file to generate after clicking run.

The instructions for running this program are as follows: 

1.) Open the Summary_CSV_Compiler.ipynb in Google Colab. The script is posted in the
repository, but a link to a version you can use directly is here: 

https://colab.research.google.com/drive/1WHm7P4cXpyX6ZtyLOw_uBmckO7ECjdkx?usp=sharing

2.) Install the required packages: requests, pandas, gdown, google-colab, os, time, re,
and shutil. (os, time, re, and shutil are part of the standard Python library,
and google-colab should work by default if running in Colab. For this reason, usually
you only need to install by running: 

!pip install --upgrade requests pandas gdown

This is included in the first cell, which you can run separately if you'd like.

3.) Download the following extension from Chrome webstore. This essentially passes browser cookies
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

Enter this link, which is the link to the EOCV2 dataset folder in Google Drive: 

https://drive.google.com/drive/folders/1r25kGjtFxS0VYu4mkrVXjF9MHjnRd5gm?usp=drive_link

7.) The program will then prompt you:
"Enter your Google API key (folder must be publicly shared):"

Enter this key:

AIzaSyD0-kbdS3GOuRiKcbqXOzYQzlHEZ580qJI

8.) The program will run by downloading all 228 files and then processing them for necessary
information. Note that this may take a while, often ~20 minutes. After the program is done,
you will have a summary.csv file that you can use to upload to the modelling Python script.

For users to customize this program to their own dataset, they simply need to upload their
own dataset to Google Drive in a publically shared folder, create a Google Cloud
API Key, and upload the respective file link and API Key when prompted by the program.
Column header names will need to match those used in the program to work, and cyclic
aging must be represented by the value of 2.

=======================================================================================
MACHINE LEARNING MODEL
=======================================================================================

The machine learning model we have developed is a random forest regressor model.
This model was also made in Google Colab. Required packages are pandas,
numpy, and scikit-learn. These can be installed with: 

!pip install pandas numpy scikit-learn

or by running the #INSTALLS cell in the Google Colab program.

Because we have already pre-processed the data using Summary_CSV_Compiler,
we can easily run the model with a single CSV file as an input. As such, we have uploaded 
the summary.csv script, as generated by Summary_CSV_Compiler, to this GitHub repository as 
summary (1).csv. Here are the instructions to run this program:

1.) Open the RandomForestRegression.ipynb file in Google Colab. Alternatively, you can
directly access the model through this Google Colab link:

https://colab.research.google.com/drive/1voesVUG3kEq3PaopruzwQGWlQFYdSBQY?usp=sharing

2.) Run all cells (minus the first one if you already have all packages).

3.) You will be prompted:

"Paste the raw GitHub URL for summary.csv:"

To do this, open the summary.csv in this GitHub repository. Click "Raw."
Copy the link URL. Paste the link and click enter. To do this with your own CSV,
or another CSV generated from the Summary_CSV_Compiler, simply upload your CSV to 
GitHub and copy the new Raw URL. Note that this link expires periodically - if you
are seeing a 404 error, go back to GitHub and generate a new Raw.

4.) After hitting enter, wait for some processing to occur. This may take a minute or two.

5.) Eventually, you will be prompted to enter the input values. Please note:
    - Aging temperature is generally in the range of -20 to 80 degrees C.
    - Charge/discharge C-rate is generally in the range of 0.1 to 3.
    - SoC window should be either "type 1", "type 2", or "type 3" (corresponding SoC window
      is listed in the prompt).

6.) The model will output the predicted number of cycles until EOL, the RMSE, and tell 
    you how far off your predicted EOL could be based on the RMSE.

