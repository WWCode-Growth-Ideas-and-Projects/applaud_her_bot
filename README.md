# Applaud Her Bot

#### Purpose: 

This bot fetches the latest Applaud her Posts from Women Who Code Website section and displays it on slack 

#### Image-Sample:

![Image-Sample](https://github.com/varchanaiyer/applaud_her_bot/blob/master/figs/bot-look.png)



#### Website Reference https://www.womenwhocode.com/applaudher

#### Packages Used: 

- [Slack API](https://api.slack.com/start): To post messages on slack

- [Beautiful Soup](https://realpython.com/beautiful-soup-web-scraper-python/): For Scraping the website
- [Request HTML](https://requests.readthedocs.io/projects/requests-html/en/latest/): To render content from a dynamic page

#### Procedure

This bot is very easy to implement. It barely takes 10-15 lines of code! 

1. **Step 1: Scrape the website**

   You can use selenium, beautiful soup or scrappy to scrape the [website]( https://www.womenwhocode.com/applaudher). Since it is a dynamic website, you will have to use request html, which will get content from a dynamic page. 

   ```python
   from requests_html import HTMLSession
   
   from bs4 import BeautifulSoup
   
   URL = 'https://www.womenwhocode.com/applaudher'
   
   session = HTMLSession()
   
   r = session.get(URL)
   
   r.html.render(wait=1, sleep=1, keep_page=True)
   
   soup = BeautifulSoup(r.html.html, 'html.parser')
   
   
   ```

2.  **Step 2: Creating a Slack App**

   After doing the scraping you will now to have build the bot for Slack. To do so follow the steps below

   1) Create an app by going through this [link](https://api.slack.com/start/overview#creating)

   2) Select a development work space

   3) After this you will arrive at this page, you can choose to add features or move on.

   ![add-features](https://github.com/varchanaiyer/applaud_her_bot/blob/master/figs/basic-functionality.png)

   

3. **Step 3: The Slack API**

   After this you just need to integrate with slack api. For this, you need to check the 

   It is very easy to integrate and you can find the code directly under *Basic Usage of the Web Client* segment of the README file

   You will find the following the code:

   ```python
   import os
   from slack import WebClient
   from slack.errors import SlackApiError
   
   client = WebClient(token=os.environ['SLACK_API_TOKEN'])
   
   try:
       response = client.chat_postMessage(
           channel='#random',
           text="Hello world!")
       assert response["message"]["text"] == "Hello world!"
   except SlackApiError as e:
       # You will get a SlackApiError if "ok" is False
       assert e.response["ok"] is False
       assert e.response["error"]  # str like 'invalid_auth', 'channel_not_found'
       print(f"Got an error: {e.response['error']}"
   ```

   

   You will use the same code with a little modification on the way you recieve the "message" and "text".

   In this step you need to access your Slack API Token, to do so follow the steps below on your slack app:

   - Click on Oauth and Permissions
   - Under Tokens for Your Workspace copy the **Bot User OAuth Access Token**

   You can use this in your code now 

   ```python
   import os
   from slack import WebClient
   from slack.errors import SlackApiError
   client = WebClient(token='Your **Bot User OAuth Access Token here')
   try:
       response = client.chat_postMessage(
           channel='your channel here',
           text=info)
       assert response["message"]["text"]==info
   except SlackApiError as e:
       # You will get a SlackApiError if "ok" is False
       assert e.response["ok"] is False
       assert e.response["error"]  # str like 'invalid_auth', 'channel_not_found'
       print(f"Got an error: {e.response['error']}")
   ```

   

---

And you are done! You are bot is ready to be deployed. 

The next step is deployment



### Deployment of the Bot

