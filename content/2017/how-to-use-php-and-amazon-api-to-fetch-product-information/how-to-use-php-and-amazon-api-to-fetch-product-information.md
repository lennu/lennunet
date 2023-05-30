---
title: How to use PHP and Amazon API to fetch product information
date: 2017-03-31
redirect_from: /how-to-use-php-and-amazon-api-to-fetch-product-information/
---
So you have a list of ASINs for which you’d like to get more information? That can be easily done with Amazon API. It’s a great tool to use when you already know which ASINs (products) you want to work with. In this post I assume you want to fetch product information for multiple items and have the list of ASINs ready in a text file, separated by a new line.

The problem
-----------

Many people want to fetch Amazon product information for their websites. They have review sites, comparison sites, blogs about certain subject where Amazon products are displayed (with affiliate links, of course). Often basic information like name and image are enough, but sometimes you want more detailed data. Scraping all product data off Amazon website might’ve occurred to you. But web scraping is rather unreliable and not approved by Amazon. In fact, you are risking your Amazon Associates account if you are publishing scraped content. So, how to retrieve that valuable information for Amazon products if not with web scraping?

The solution
------------

Use Amazon API! After you have a list of ASINs at your disposal the API is a very handy tool. You can retrieve a lot of information with it, including:

*   Price
*   Discount amount and percentage
*   Availability
*   Images
*   UPC

Cool, isn’t it? So let’s see what you need…

Requirements
------------

*   Web server with PHP enabled
*   ASIN list (text file, one ASIN per line)
*   Amazon Associates account ([get it here](http://affiliate-program.amazon.com/gp/associates/apply/main.html))
*   Amazon Product Advertising API enabled ([enable it here](https://affiliate-program.amazon.com/gp/flex/advertising/api/sign-in.html))
*   Amazon API PHP class ([get it from here](http://www.codediesel.com/downloads/amazonapi) thanks to [Sameer Borate](http://www.codediesel.com/))

Opening up Amazon Associates account should be easy and fast. Just go here and follow the instructions. It could take a few days to get you approved – but in my experience, most people are accepted. Just remember to have some kind of a website ready with original content. And preferably give accurate information because they’re going to send you check / deposit money to your bank account after you start generating money (which is, by the way, not so hard with Amazon Associates program). Anyway, in the process you’ll also make a Tracking ID which is used to track the visitors you send to Amazon. Keep that at hand, you’ll need it later.

Once you have enabled Amazon API on your account, you must create Access Key ID and Secret Access Key. They are the keys that the Amazon API PHP script will use to authenticate with Amazon API servers. You can get the keys here. Just click on Access Keys -> Create New Access Key. You’ll be presented with a box saying an access key has been successfully created for you. Click Download Key File and save it on your computer. This is important because once you close the pop-up, you can’t retrieve the secret access key again from your Amazon API account settings.

Next, upload [the two files](http://www.codediesel.com/downloads/amazonapi) (amazon\_api\_class.php and aws\_signed\_request.php) to your web server’s public\_html or its subdirectory. You don’t have to modify the latter, but slight modifications have to be made for the class file itself. So open up amazon\_api\_class.php and find lines 42, 49 and 57 and do as follows:

*   On line 42, put your Access Key ID inside the double quotes. Remember, you downloaded the keys to your computer above.
*   On line 49, put your Secret Access Key inside the double quotes.
*   On line 57, put your Tracking ID inside the double quotes. You can see it [here](https://affiliate-program.amazon.com/gp/associates/network/main.html) on upper right corner (Store) after logging in.

Great, now you have the PHP class ready. It’s time to look at the actual source code of the file that will fetch detailed product information for every ASIN in your list. Put the following code to the same directory you put the amazon\_api\_class.php and aws\_signed\_request.php to and run the code.

PHP Code:

```
<?php
        
        // Open the list of ASINs for reading
        $handle = fopen("asins.txt", "r");
        
        // Include the Amazon API PHP class
        include("amazon_api_class.php");
 
        // Create a new Amazon API object
        $obj = new AmazonProductAPI();
        
        // Start looping through the ASIN file, line by line
        while (($asin = fgets($handle)) !== false) {
        
            // Remove the new line from ASIN
            $asin = str_replace("\n","",$asin);
 
            // Try to fetch product information with the object
            try {
                $result = $obj->getItemByAsin($asin);
            }
            // If unsuccesful, catch the exception...
            catch(Exception $e)
            {
                // And print it to the screen
                echo $e->getMessage();
            }
            
            // To see the whole response (with all the information, uncomment
            // the following three lines
            // echo "<pre>";
            // print_r($result);
            // echo "</pre>"; */
            
            // Get title, price and image URL from the response
            $title = $result->Items->Item->ItemAttributes->Title;
            $price = $result->Items->Item->OfferSummary->LowestNewPrice->FormattedPrice;
            $image_url = $result->Items->Item->LargeImage->URL;
            
            // Print the title, price, ASIN and image URL to screen
            echo "$asin Title: $title<br />$asin Price: $price<br />$asin Image URL: $image_url<br /><br />";
            
            // Wait 1 second because of Amazon API call limit
            // Adjust it to your liking, more info here:
            // https://affiliate-program.amazon.com/gp/advertising/api/detail/faq.html
            sleep(1);
        
        // End of ASIN
        }
        
        // Close the ASIN text file
        fclose($handle);
        
?>
```

So what’s happening there?

*   We open the ASIN text file (called asins.txt in this example) with read mode on.
*   We include Amazon API PHP class.
*   We create a new Amazon API object.
*   We start while loop with fgets that returns a new line from ASINs file and puts it to variable $asin.
*   We remove new line (\\n) from the end of the ASIN.
*   We initiate try-catch statement and try to use getItemByAsin function from the Amazon API PHP class. If successful, we continue. If not, we catch the exception and print the message to screen.
*   I commented out the full response, but you can uncomment lines 31-33 to see the full response and pick the product information you want.
*   Next we fetch the product’s title, price and image URL from the response object. That’s done by retrieving paths from the object with the -> operator.
*   We echo the information to screen. You can replace the line 41 with whatever you want (for example, insert the retrieved information to database), but to make it simple in this example we just echo it.
*   We sleep (wait) one second. This is because of Amazon API’s call limits. If you’ve generated sales in the past 30 days you can reduce the waiting time. [Read more about it here](https://affiliate-program.amazon.com/gp/advertising/api/detail/faq.html).
*   We are at the end of line (ASIN), move on to the next one and start from the beginning of while loop. If this is the last line from the ASIN file, move to next line in the code.
*   We finally close the ASIN file.

Not so hard, isn’t it. This way you can retrieve plenty of information from the Amazon API for your projects. This is 100% Terms of Services compliant way to do it. I’ve also found out that the API is reliable and doesn’t experience lags or other oddities. But there are some things to keep in mind…

Caveats
-------

*   Sometimes the price returned is “price too low to display” rather than actual price. This is not a bug but a feature of the API. [Read more about it here](http://docs.aws.amazon.com/AWSECommerceService/latest/DG/minimum-advertised-price.html). The only way to go around this would be to scrape the price from their website rather than using the API. But web scraping Amazon, especially the price information, is forbidden by their Terms of Services. If you publish scraped information, your Amazon Associates account could get banned.
*   You can’t return customer reviews or star ratings with the API. You can, however, return a link to the customer reviews. But that’s not very often the desired option. Again, web scraping Amazon product pages would give you the customer reviews, but publishing them would break copyright laws and the Terms of Services. So don’t do it.
*   There’s a call limit for Amazon API. That means you can only do certain amount of API calls in a second. If you haven’t generated any sales in the past 30 days, the default limit is one call per second. But when you generate sales for Amazon (and commission for yourself), the API limit changes. [Read more about it here](https://affiliate-program.amazon.com/gp/advertising/api/detail/faq.html).
*   Not every product’s information can be retrieved through the API. I’m not sure exactly why some products are off limits for the API. But that’s how it is. I’ve seen at least some “discontinued by manufacturer” products not working with the API. But rest assured that 99% of the time the product information can be retrieved.

That’s all I can think for now. Amazon API is a good, reliable tool for programmatically fetching product data. You can use use it to build sites and with some creativity, perhaps even profitable ones!