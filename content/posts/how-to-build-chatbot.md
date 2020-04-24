---
title: "How to Build Chatbot"
date: 2020-04-21T21:36:10+02:00
draft: false
tags: 
  - Heroku
  - Python
  - Chatbot
  - Messenger
---

What chatbots are? Chatbots are the future of software and a new way to provide services through a conversational interface like Messenger, WhatsApp, Slack, Telegram etc.

![Hero image](https://miro.medium.com/max/700/1*8ct70K3FbQQ2OOwW030fwA.jpeg)

I will show you how to build your own bot and deploy it on Messenger platform in several simply steps using [Python](https://www.python.org/), [Flask](https://palletsprojects.com/p/flask/) and [Heroku](https://dashboard.heroku.com/).

![chatbot preview](https://miro.medium.com/max/320/1*x7KfD6oNraVwDqbNjrRN8g.gif)

## Setup Facebook Developer Account

Before you start coding have to create a [Facebook developer account(https://developers.facebook.com/apps/)], [Facebook App](https://developers.facebook.com/apps/), [Facebook page](https://www.facebook.com/pages/creation/?ref_type=pages_you_admin), and set it all up.

![Creating new App (My Apps → Create App)](https://miro.medium.com/max/700/1*2qW4tHU6B3B07WhmJOjDYg.png)
Creating new App (My Apps → Create App)

![Creating new Facebook page](https://miro.medium.com/max/540/1*NVeHT9jeWSXOyfXaUh8AAg.gif)
Creating new Facebook page

When yours’ new Facebook Page and App are ready you have to connect them together. To do this, open the App page, use the Set up button under the Messenger box in Dashboard tab. Add your newly created Page and allow App to manage and access conversation in Messenger. After that Edit Page Subscriptipon check **messages, messaging_postback and messagingn_referrals**. Then generate, copy and save secret token which will be necessary later and use button Add to Submission next to pages_messaging — that’s will be enough for now. Let’s move on. We’ll be back here when our Flask application starts working.

![](https://miro.medium.com/max/600/1*5qbq86-oJqVdwVW3nYV3wA.gif)
![Editing page subscriptions](https://miro.medium.com/max/700/1*wxOnnRFE7qCKWwYqQaDATg.png)

## Coding time 🕑👨🏻‍💻

I assume that you know what Flask is and you already have at least basic experience with Python. If not I’ll refer you to the Python and Flask documentation. Best will be use Python 3.7 or newer version. If you still use Python 2.x you have to migrate as soon as possible.

![migration 2.x to 3.x](https://miro.medium.com/max/500/1*pnG0E4PyU43Uyw9wd54zfg.png)

Ok, start with creating an HTTP server:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == "__main__":
    app.run(threaded=True, port=5000)

```

And add your Webhook endpoint — this is the core of your Messenger bot. By using Webhook you will receive, process, and send messages.

```python

import credentials, requests
from flask import Flask, request
app = Flask(__name__)

# Adds support for GET requests to our webhook
@app.route('/webhook',methods=['GET'])
def webhook():
    verify_token = request.args.get("hub.verify_token")
    # Check if sent token is correct
    if verify_token == credentials.WEBHOOK_VERIFY_TOKEN:
        # Responds with the challenge token from the request
        return request.args.get("hub.challenge")
    return 'Unable to authorise.'

if __name__ == "__main__":
    app.run(threaded=True, port=5000)
```

Now you can run your Flask app locally and public URLs using ngrok which
will allow to test the solution until deploy them on Heroku.

To authorize Webhook back to your Facebook Developer App Dashboard. Add Callback URL in Webhook part and provide Verify Token (the same which you set in Flask app).

![Webhook authorization](https://miro.medium.com/max/600/1*KMaLR59JZBIB_7ysrtGKYA.gif)

Voila 👌🏻 your connection between server and Messenger is ready. Now we can take care of messaging ✉️. As there is in [documentation](https://developers.facebook.com/docs/messenger-platform/send-messages)…

''
Messages are sent by submitting a POST request to the Send API with your page access token appended to the URL query string:
https://graph.facebook.com/v5.0/me/messages?access_token=<PAGE_ACCESS_TOKEN>
''

… so add POST support and start receiving messages from users 📩.

```python

# Adds support for POST requests

@app.route("/webhook", methods=['POST'])
def webhook_handle():
    output = request.get_json()
    print(output)
    return 'ok'

```
Now if you send a message to your chatbot in console you can see how the **POST** request looks like:

```python
{'object': 'page', 'entry': [{'id': '105114914362459', 'time': 1579028712412, 'messaging': [{'sender': {'id': 'xxxxxxxx'}, 'recipient': {'id': 'xxxxxx'}, 'timestamp': 1579028712093, 'message': {'mid': 'm_ttOeT7YUN5m65ly2AwPujso38029QHO5Nx8Qvwo-XDWt5gWohDo5z4hmDh8NTiLDgOJ8CRgFV7_7JKQ4eFskTw', 'text': 'Hi'}}]}]}

```

This is a Python dict with several keys like sender id, recipient_id or message[‘text’] that stores the message from the user. If you can know how to catch messages will be good to answer them, right?
Look at the [documentation](https://developers.facebook.com/docs/messenger-platform/send-messages) and everything will be clear 💡


```
Sending Text
To send a basic text message, submit a POST request to the Send API, with message.text set in the request body:
curl -X POST -H "Content-Type: application/json" -d '{
"recipient":{
"id":"<PSID>"
},
"message":{
"text":"hello, world!"
}
}' "https://graph.facebook.com/v5.0/me/messages?access_token=<PAGE_ACCESS_TOKEN>"
```

```python
@app.route("/webhook", methods=['POST'])
def webhook():
    data = request.get_json()
    message = data['entry'][0]['messaging'][0]['message']
    sender_id = data['entry'][0]['messaging'][0]['sender']['id']
    if message['text']:
        request_body = {
                'recipient': {
                    'id': sender_id
                },
                'message': {"text":"hello, world!"}
            }
        response = requests.post('https://graph.facebook.com/v5.0/me/messages?access_token='+credentials.TOKEN,json=request_body).json()
        return response
    return 'ok'
```

![](https://miro.medium.com/max/580/1*9qnW86KgOp-DfeYFUGMplQ.gif)

Of course you can arrange different conditions and answers depending on what the user has written to us (if — else). You can arrange various scenario, query the API of external suppliers and return desired information depending on what you or your business need. I highly recommend you to read the [documentation](https://developers.facebook.com/docs/messenger-platform/introduction) prepared by Facebook. They’ve provided many types of response you can use to do it. It doesn’t have to be plain text. Persistent Menu, Buttons, Quick Replies these are just some of them, and all of them significantly improve the user experience.

## Deploying Flask App to Heroku

At first of course you have to create account on [Heroku](https://dashboard.heroku.com/) if you don’t have yet. Create new project on it, install on your computer [Heroku CLI(https://devcenter.heroku.com/articles/heroku-cli#download-and-install)] & [Git CLI](https://git-scm.com/docs/gitcli) (we use git to upload our code).
Open console inside your project create Profile with code bellow:

```
web: gunicorn app:app
```

The web command tells Heroku to start a web server for app using gunicorn. If your app file name is named app.py, you have to set the app name to be app as well.
If you did it, in the next step in console run…

```
$ pip install gunicorn
$ pip freeze > requirements.txt
$ git init
$ git add .$ git commit -m "First deploy" 
$ heroku login
$ heroku git:remote -a <YOUR-HEROKU-PROJECT-NAME>
$ git push heroku master
```

… your apps should working on Heroku now. Last thing which you have to do it’e edit Callback URL onto Facebook Developer account. Have fun! 🐍
Final code you can finde on my [Github repo](https://github.com/radipawelec/messenger-py-chatbot-sample/blob/master/app.py).

This post originally was published also on Medium. 