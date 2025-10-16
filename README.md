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
