Phewtick Hack
=============

This is a python script to automatically call Phewtick RESTful APIs. 

It does 2 things very well:

1. Automatically 'scan QR code' to earn you money!

2. Send message to _any_ Phewtick user!


What is Phewtick?
------------------

[Phewtick](http://www.techinasia.com/phewtick-mobile-app/) is an app that let you earn money when you meetup with friends! 

To earn, your friend must be nearby, then you scan his/her QR code, and both of you will get a random number of points (which is pegged to real money). On average, you earn a few cents per meetup.. 

You also need to wait 1 hour before you can 'meetup' with the same friend again.

To cash out, you need to accumulate ~$30, which means you need ~1000 meetups before you can get the money.



Why create this hack?
----------------------

The story goes like this..

My colleagues and I all use Phewtick, and is intrigued with this app 'idea' and 'business model'. We are active users of Phewtick, and the first thing we did as we arrive in office is to 'meetup'.

And we meetup almost every hour..

As a [convert hacker](http://linked.in/junda), whose work is in [providing awesome API](http://developer.hoiio.com), I thought I should take a look at Phewtick internals.



What is this hack?
----------------------

Using mitmproxy to sniff it's HTTP traffic, I learnt it's API endpoints and protocols. 

Then I wrote some python codes to help automate the scanning.

Just the scanning. 

We are not really cheating. We are indeed meeting up everyday in the office :)


Usage 1: Auto Scan
------------------

Clone the project and rename the `settings-sample.py` to `settings.py`

	git clone https://github.com/samwize/phewtick-hack.git
	mv phewtick-hack/settings-sample.py phewtick-hack/settings.py

Open `settings.py` and enter your token, and your friends' tokens. To more tokens, the denser your network.

Read the next section on how you can retrieve your token.

Run the script:

	cd phewtick-hack
	python phew.py

The script will automate refreshing of QR code and scanning it for everyone. Then it will sleep for around 1 hour before repeating again.

Cheers (if you manage to cash out..)


Usage 2: Messaging
-------------------

Instead of `python phew.py` as described above, start python interactive shell.

	cd phewtick-hack
	python

Assuming you want to send from the first token which is in the array `tokens[0]` to a Phewtick id `123456`, type

```python
	from phew import *
	message(0, 123456, "Hello!")
```

You can message to _any_ Phewtick id. Yes, that means you can spam anybody.

To find your friends Phewtick id, you can generate with this 

```python
	from phew import *
	generateUsers()
```	

Retrieving tokens
-----------------

It is a bit more tedious to get the token. It involves sniffing the HTPP traffic as you run your Phewtick app. 

You could use any software to sniff the http traffic.

For me, I use [mitmproxy](http://mitmproxy.org/). Here is a guide on [how to use mitmproxy](http://blog.just2us.com/2012/05/sniff-iphone-http-traffic-using-mitmproxy/).

This is how my mitmproxy looks:

![mitmproxy screenshot](https://raw.github.com/samwize/phewtick-hack/master/mitmproxy.png)

What you need here is the `token` (which is purposefully blurred in the screenshot). Copy that and add to `settings.py` `tokens` array.

Tip: You could ask all your friends to connect to your proxy and sniff their tokens.



Deploying to dotcloud
----------------------

You can also deploy to [dotcloud](http://dotcloud.com) so that the python script is run day and night on a remote server. 

The 2 files added are `dotcloud.yml` and `supervisord.conf`, which you do not need to touch. 

Simply sign up with dotcloud, learn to create a python app, then push to it.
