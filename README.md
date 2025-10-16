# Linkedin Scraper

Scrapes Linkedin User Data

## Installation

```bash
pip3 install --user linkedin_scraper
```

Version **2.0.0** and before is called `linkedin_user_scraper` and can be installed via `pip3 install --user linkedin_user_scraper`

## Setup
First, you must set your chromedriver location by

```bash
export CHROMEDRIVER=~/chromedriver
```

## Sponsor
Message me if you'd like to sponsor me

## Usage
To use it, just create the class.

### Sample Usage
```python
from linkedin_scraper import Person, actions
from selenium import webdriver
driver = webdriver.Chrome()

email = "some-email@email.address"
password = "password123"
actions.login(driver, email, password) # if email and password isnt given, it'll prompt in terminal
person = Person("https://www.linkedin.com/in/joey-sham-aa2a50122", driver=driver)
```

**NOTE**: The account used to log-in should have it's language set English to make sure everything works as expected.

### User Scraping
```python
from linkedin_scraper import Person
person = Person("https://www.linkedin.com/in/andre-iguodala-65b48ab5")
```

### Company Scraping
```python
from linkedin_scraper import Company
company = Company("https://ca.linkedin.com/company/google")
```

### Job Scraping
```python
from linkedin_scraper import Job, actions
from selenium import webdriver

driver = webdriver.Chrome()
email = "some-email@email.address"
password = "password123"
actions.login(driver, email, password) # if email and password isnt given, it'll prompt in terminal
input("Press Enter")
job = Job("https://www.linkedin.com/jobs/collections/recommended/?currentJobId=3456898261", driver=driver, close_on_complete=False)
```

### Job Search Scraping
```python
from linkedin_scraper import JobSearch, actions
from selenium import webdriver

driver = webdriver.Chrome()
email = "some-email@email.address"
password = "password123"
actions.login(driver, email, password) # if email and password isnt given, it'll prompt in terminal
input("Press Enter")
job_search = JobSearch(driver=driver, close_on_complete=False, scrape=False)
# job_search contains jobs from your logged in front page:
# - job_search.recommended_jobs
# - job_search.still_hiring
# - job_search.more_jobs

job_listings = job_search.search("Machine Learning Engineer") # returns the list of `Job` from the first page
```

### Scraping sites where login is required first
1. Run `ipython` or `python`
2. In `ipython`/`python`, run the following code (you can modify it if you need to specify your driver)
3. 
```python
from linkedin_scraper import Person
from selenium import webdriver
driver = webdriver.Chrome()
person = Person("https://www.linkedin.com/in/andre-iguodala-65b48ab5", driver = driver, scrape=False)
```
4. Login to Linkedin
5. [OPTIONAL] Logout of Linkedin
6. In the same `ipython`/`python` code, run
```python
person.scrape()
```

The reason is that LinkedIn has recently blocked people from viewing certain profiles without having previously signed in. So by setting `scrape=False`, it doesn't automatically scrape the profile, but Chrome will open the linkedin page anyways. You can login and logout, and the cookie will stay in the browser and it won't affect your profile views. Then when you run `person.scrape()`, it'll scrape and close the browser. If you want to keep the browser on so you can scrape others, run it as 

**NOTE**: For version >= `2.1.0`, scraping can also occur while logged in. Beware that users will be able to see that you viewed their profile.

```python
person.scrape(close_on_complete=False)
``` 
so it doesn't close.

### Scraping sites and login automatically
From verison **2.4.0** on, `actions` is a part of the library that allows signing into Linkedin first. The email and password can be provided as a variable into the function. If not provided, both will be prompted in terminal.

```python
from linkedin_scraper import Person, actions
from selenium import webdriver
driver = webdriver.Chrome()
email = "some-email@email.address"
password = "password123"
actions.login(driver, email, password) # if email and password isnt given, it'll prompt in terminal
person = Person("https://www.linkedin.com/in/andre-iguodala-65b48ab5", driver=driver)
```
using the same driver.
