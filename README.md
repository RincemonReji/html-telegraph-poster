[![Build Status](https://travis-ci.org/mercuree/html-telegraph-poster.svg?branch=master)](https://travis-ci.org/mercuree/html-telegraph-poster)

# Python html to telegra.ph poster

Simple python function to post plain html text to https://telegra.ph/.
Telegra.ph allows `<a>, <blockquote>, <br>, <em>, <figure>, <h3>, <h4>, <img>, <p>, <strong>, ` elements.
It also supports embedded youtube and vimeo iframe tags.

About telegram telegra.ph service https://telegram.org/blog/instant-view

## Requirements
* lxml
* requests
* requests_toolbelt

## Installation
```Shell
pip install html-telegraph-poster
```

## Usage
```python
>>> from html_telegraph_poster import TelegraphPoster
>>> t = TelegraphPoster(use_api=True)
>>> t.create_api_token('Elon Musk', 'Elon', 'https://www.spacex.com/') # second and third params are optional
{'access_token': '9f3bab568f*************', 'auth_url': 'https://edit.telegra.ph/auth/HFYo***********', 'author_name': 'Elon', 'short_name': 'Elon Musk', 'author_url': 'https://www.spacex.com/'}
>>> t.post(title='Just another funny joke', author='by me', text='<blockquote>Really hard way</blockquote>')
{'path': 'Just-another-funny-joke-06-05-4', 'url': 'http://telegra.ph/Just-another-funny-joke-06-05-4'}

# We can modify this article later
>>> t.edit(text=t.text + '<p>some text at the end</p>')
{'path': 'Just-another-funny-joke-06-05-4', 'url': 'http://telegra.ph/Just-another-funny-joke-06-05-4'}

# Modify page created earlier
>>> t.edit(text="<p>new text</p>", path='/Another-one-page-06-05')
{'path': 'Another-one-page-06-05', 'url': 'http://telegra.ph/Another-one-page-06-05'}
```
## Generate persistent access token
Actually it's a good idea to generate access token and put it inside environment variables.
This command will generate .env file or append  TELEGRAPH_ACCESS_TOKEN at the end of it.
Note: script will not set environment variable. You can use [python-dotenv](https://github.com/theskumar/python-dotenv),
set it manually or hardcode it when call `TelegraphPoster(access_token='access_token_string')`
```Shell
python -m html_telegraph_poster.create_account "Elon Musk" "Elon" "https://www.spacex.com/"
```

## Uploading images
```python

from html_telegraph_poster.upload_images import upload_image

# upload file
upload_image("file_path.jpg")

#upload url
upload_image("http://example.com/img.png")

```
