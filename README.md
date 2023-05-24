# NIKE MONITOR WITH HOMEMADE PROXY ROTATION

This workshop aims to make you create you first monitor on Nike API, that will have a (free)proxy rotation, using proxies and headers if needed.

## MUST HAVE

In order to be able to work on this, you should install a few libraries (if you do not have them), here they are:

- python3
- requests
- json

## STEP 1: PROXIES

### Exercise 1: CATCH THEM ALL

The first step will be to create your own "proxy scraper", you can use any site that provides free (or not) proxies.
For those who doesn't know how to pick a good one, here are some links to good free proxies websites :

- https://geonode.com/free-proxy-list
- https://proxyscrape.com/share/6357i6g
- https://scrapingant.com/free-proxies/

Some of them are just requiering to download a file, copy & paste the ip addresses, others are a little bit tricky to
parse and needs some libraries (like pandas or bs4), you still can use them to parse the others websites to get your proxies
but if you do not feel comfortable with it, just take the easy ones.

### Exercise 2: TESTING PROXIES

The goal now is to test your proxies. I will invite you to make a request, using a proxy (in your list of proxies obviously),
and check if everythings works good.

Try your requests on this website and print the result (it should be a json file but we don't care, we just need the IP in it).
`https://httpbin.org/ip`

### Exercise 3: FILTER PROXIES

Now you should find a way to make two (or more) programs that will run simultaneously.
One will scrap the proxy website (in order to get new proxies everytime), the other will make a loop with sending a request with each proxy,
on the website that you want, and then it will store them in a file.txt or whatever type of file that you want (but if you find an another
way to pass it to different programs it's ok).
By the way, do not forget to refresh your list at every loop tour, so the new proxies will synchronize with the old one by appending them.

**NOTE**
You will not need proxies directly, it will just avoid to making you stop what you are doing during the scraping part.

## STEP 2: SET HEADERS *OPTIONAL*

*Since Nike doesn't needs to recieve a header, you can avoid making your request with a header.*
*But if you really want to make something good and avoid any detection for your monitor, I would tell you to make a header*

### Exercise 1: GET THEM

In order to make requests with headers, we need different headers than ours (if we make a lot of requests in a minute,
we don't want to be flagged by the website), here is a github that provides a lot of user-agents `https://gist.github.com/pzb/b4b6f57144aea7827ae4`.

You can take only one, here we do not need a list, it should be fine.

### Exercise 2: TEST THEM

Now you will do the same as you did for the proxies but for the headers, on this website:
`https://httpbin.org/user-agent`

**NOTE**
A header is a dictionnary in python that you give to the get/post method of the request module.

## STEP 3: REQUESTS WITH PROXIES

**NOTE**
You should maybe take a look at the documentation to understand how `requests` library works.

`https://requests.readthedocs.io/en/latest/`

The page that we will be monitoring today will be : `https://www.nike.com/fr/w/dunk-chaussures-basses-chaussures-7hf8ez90aohzy7ok?q=dunk`

What we want here is to get notified when Nike put a new shoe on the given research.

Before starting the exercises, you will have to find the API call (from the link) in order to catch the informations about all the listed shoes.

### Exercise 1: RETRIEVE YOUR PROXIES

We are getting closer to the biggest part of it, which is, the monitoring (A.K.A. scraping) part.

But first, I will need you to create your own list, parsed, with all your proxies in order to make the rotation between each request.

### Exercise 2: MAKE YOUR REQUEST

First thing first, you will have to make the function that will do your request. *DO NOT MAKE A LOOP FOR NOW IF YOU ARE NOT SURE*

Becareful, Nike maybe needs a header to be sent in order to get a response !
To make sure, print the content of the response if needer.

Put try and except in your code in order to get any error that could occur.

### Exercise 3: INTERPRET REQUEST

Now that you have got the response from the API, you will recieve the content of it.
Generally, API will return a file in JSON format, so we will need to `import json`.

Now, by taking the previous function, in which we get the response of the request, you will have to complete fully your function that scraps.
You will have to load the json that the request sends you, and return the part that will give you the informations that you need.

### Exercise 4: COMPARE

This part is pretty simple, you will just need to make a function, in which you send the part of the JSON that we want, and then check if
the ID is (or not) in the list of IDs. Your list of IDs should be a global variable so you can modify it and access it anywhere.

### Exercise 5: MAKE IT WORK EVERYTIME

This is the easiest part of the project, you will have to manage to make this work on multiple loops for the proxy,
the content of the request and maybe other elements that you would want to care about.

*BONUS STEP*

### STEP 4: GET NOTIFIED ON DISCORD

This is in case that you would really want to make your own monitor, with this project as basis.

To get notified on discord, first you will have to create or use an existing Discord server.
Go on whatever channel you want and create a Webhook, and get the link of it, it will allow you in the cases that you want,
to get a notification if something happens on your monitor.

**Make your Webhook link a global variable**

We will take the function from Exercise 4 and add something to it.

In case that if your ID is not in your list of IDs, you will obviously add it to the list, as the exercise suggested, and then,
you will call a new function, in which you will pass several arguments, such as : the title of the article, the link of it, the price,
a picuture of it (there should be an url), and other stuffs.

Then you will simply make a dictionnary, in which there will be an another dictionnary, this one should be called 'embeds' in order to send
a beautiful notification on discord. Then you fill your fields of the embeds with the parameters that you have given to the function.

After that you can simply make a post request, using the URL of your discord webhook, and send it as json (don't forget to put an header in the request).
You can, if you want, print the status code of the request.