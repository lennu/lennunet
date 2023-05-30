---
title: Web Testing Tutorial Using DalekJS
date: 2015-01-15
redirect_from: /web-testing-tutorial-using-dalekjs/
---

{% image "./dalekjs.png", "DalekJS Logo" %}

Have you ever wondered how to easily test the web pages you were creating? Or just want to test some issues multiple times between development phases? I have tried some testing tools including the widely used Selenium. These tools tend to be quite heavy and hard to start doing the actual testing.

Now there is a new guy in the room which in my opinion offers a quite new experience. Dalek.js provides simple and very fast way to do automated web testing which scales from very small projects to large ones. It supports all the major browsers and can script them, take screenshots and create reports about the tests.

Automated web testing
---------------------

Web testing is something you would do to ensure everything is working correctly in a website. For example if you are developing a new website and you are still doing the development, you may want to make sure everything keeps working while doing changes to the source code. Or maybe you would want to test if your website is cross browser compatible?

All of these can be quite time consuming to do if you start doing them by hand. And even if you would finish them fast there are always a chance that you can make human mistakes during the testing. What if you want to do the same tests later?

For all of these cases there have been made software to help testing the web. One of the latest to enter this area is [DalekJS](http://dalekjs.com/) which comes with a powerful feature of beign very easy to deploy and write and run the tests.

### Dalek.js installation

We need to install node.js and npm in order to install Dalek.js.

#### node.js

If you are using Ubuntu or similar modern Linux you can fetch it with the following command:

```
sudo apt-get install nodejs
sudo apt-get install npm
```

If your Linux can’t find the packages you can compile them yourself by downloading the source from: [http://nodejs.org/download/](http://nodejs.org/download/).

From the same location you can also download the Windows installer.

#### dalek.js

Once we have installed node.js we can fetch dalek.js from npm repository.

```
npm install dalek-cli -g
npm install dalekjs --save-dev
```

Thats it! You can verify that the installation is completed with `dalek -v`. Now we can write our first test.

### Running DalekJS

Lets create a directory and open up a file for our test:

```
mkdir dalekJStest
cd dalekJStest
nano test1.js
```

Here we will write our test code:

```
module.exports = {
	'Hacker News Testing': function (test) {
	test
		.open('https://news.ycombinator.com/news')
		.assert.title().is('Hacker News', 'Hacker News has the correc title!')
		.click('a[href="newest"]')
		.waitForElement('body')
		.assert.title().is('New Links | Hacker News', 'New Links section has the correc title!')
		.done();
	}
};
```

Run the file with the following command:

```
dalek test1.js
```

The test opens Hacker News website and checks if the page title is correct. After that the test opens a link, waits for the site to load and check the title of that page.  
After running the tests if everything went well we should see passed test results.

```
RUNNING TEST - "Page title is correct"
> OPEN https://news.ycombinator.com/news
* TITLE Hacker News has the correc title!
> CLICK a[href="newest"]
> WAITFORELEMENT
* TITLE New Links section has the correc title!
* 2 Assertions run
* TEST - "Page title is correct" SUCCEEDED
 
 2/2 assertions passed. Elapsed Time: 2.26 sec
```

#### Real Browser Automated Testing

If you want to use real browser to run the test just use these commands and a Chrome browser will fireup and run your test as you witnessing everything.

```
npm install dalek-browser-chrome --save-dev
dalek test/my_first_test.js -b chrome
```

### More testing

If you want to learn more, go check DalekJS website and their [documentation](http://dalekjs.com/pages/documentation.html).

As this tutorial shows the setup of testing component is not hard and with DalekJS you can be testing your websites of application withing 10 minutes. I hope you have learned web testing from this tutorial and use DalekJS to do something in the future!