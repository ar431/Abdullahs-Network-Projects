# Abdullahs-Network-Projects

Hi All!
My name is Abdullah and I'm a Network Automation Engineer. This repository contains some of the projects I've worked on.

## Table of Contents
1. Network Health Data Collection and Reporting
2. Web Scraping Bot for Automated Logins
3. Port Scanner
------------------------------------------------------------------------------------------------------------------------
## Project 1: Network Health Data Collection and Reporting
This project involves a cron job that runs a REST API query against Cisco DNA Center to poll for full inventory health data. 
The key metrics from this data are then uploaded to a SharePoint site. The name of the file corresponds to the date it was 
generated, providing a clear and organized history of network health metrics.

### Problem Statement
Maintaining an up-to-date inventory of network health data is crucial for efficient network management and troubleshooting. 
However, manual data collection can be time-consuming and prone to errors.

### Solution
To automate this process, I created a cron job that regularly queries Cisco DNA Center for full inventory health data using
REST API. The key metrics from this data are extracted and uploaded to a SharePoint site for easy access and review.
Each file is named with the date of generation, allowing for easy tracking of network health over time.

### Technologies Used
- Cisco DNA Center
- REST API
- Task Scheduler
- SharePoint

### Code Snippets
------------------------------------------------------------------------------------------------------------------------
```python
def NetworkHealth():
    offset = 1
    while offset < 1000:
        koffset = str(offset)
    # Runs multiple API calls to DNAC as DNAC  API limits each call to 500 network devices
        offset += 499
        url = 'https://<DNAC_IP_ADDRESS>/dna/intent/api/v1/network-device?family=Switches_and_Hubs&offset=' + koffset
        f = open('<PATH_TO_CREDENTIALS_FILE>', 'r')
        i = 0
        for line in f:
            if i == 0:
                uname = line.strip('\n')
            if i == 1:
                passwd = line.strip('\n')
            i += 1
        f.close()
        token = DNAC_token(uname, passwd)
        headers = {
            "Content-Type": "application/json",
            "x-auth-token": token,
        }
        response = requests.get(url, headers=headers, auth=HTTPBasicAuth(uname, passwd), verify=False)
        switches = json.loads(response.text)
    # Saves switch data to a sharedrive with todays date
        current_date = str(datetime.now().strftime('%d%m%Y'))
        filePath = '<PATH_TO_SHAREPOINT_DIRECTORY>' + current_date+'.txt'
        with open(filePath, 'a') as f:
            for switch in switches['response']:
                f.write(switch['hostname'] + '\n')
                f.write(switch['reachabilityStatus'] + '\n')
                f.write('Uptime in seconds: ' + str(switch['uptimeSeconds']) + '\n\n')
```
------------------------------------------------------------------------------------------------------------------------
## Project 2: Web Scraping Bot for Automated Logins

This project involves a web scraping bot that automates the process of logging into websites. It was created to automate 
logins to slow-loading websites, saving time and improving efficiency. The purpose of this project is to show knowledge 
of technologies that can be used to interact with tools programmatically that do not have an API.

### Problem Statement
Logging into multiple websites, especially slow ones, can be a time-consuming task that needs to be done frequently.

### Solution
To automate this process, I created a web scraping bot using Selenium. The bot navigates to the login page, enters the 
username and password, and submits the form. It handles different login forms and waits for pages to load, ensuring 
successful logins even on slow websites.

### Technologies Used
- Python
- Selenium WebDriver

### Code Snippets
------------------------------------------------------------------------------------------------------------------------
```python
from selenium import webdriver
import time
from selenium.webdriver.common.by import By

def login():
    global passwd
    driver = webdriver.Edge()
    url2 = 'https://<WEBSITE_URL>/'
    driver.get(url2)
        try:
        button = driver.find_element(By.XPATH, "//a[@href='/']")
        button.click()
    except:
        # continue with the rest of your code
        pass
    time.sleep(2)
    username = driver.find_element(By.ID, 'username')
    passwordbox = driver.find_element(By.ID, 'password')
    f = open('<PATH_TO_CREDENTIALS_FILE>', 'r')
    i = 0
    for line in f:
        if i == 2:
            passwd = line.strip('\n')
        i += 1
    f.close()
    # Continues with code to handle different login forms and submits them
```
------------------------------------------------------------------------------------------------------------------------
## Project 3: Port Scanner

This project involves a simple port scanner that checks if a specific port is open on a given IP address or hostname.

### Problem Statement
When managing networks, it's often necessary to check if specific ports are open. Doing this manually can be time-consuming
and inefficient.

### Solution
To automate this process, I created a Python script that uses the socket module to check if a specific port is open on a 
given IP address or hostname. The script prompts the user for the IP address or hostname and the port number, then checks
if the port is open and prints the result.

### Technologies Used
- Python
- Socket module

### Code Snippets
------------------------------------------------------------------------------------------------------------------------
```python
import socket

def is_port_open(ip, port):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(5)
    result = sock.connect_ex((ip, port))
    sock.close()
    return result == 0

print('*' * 90 + "\n" + "*" * 25 + "Welcome to the PortScannerAPP!" + "*" * 25)
ip = str(input("Please Enter an ip or hostname: "))
port = int(input("Please enter the port number: "))
if is_port_open(ip, port):
    print(f'Port {port} is open on {ip}')
else:
    print(f'Port {port} is closed on {ip}')
```
------------------------------------------------------------------------------------------------------------------------

### Contact Me
You can reach me at 
LinkedIn: https://linkedin.com/in/abdullah-raja

------------------------------------------------------------------------------------------------------------------------
