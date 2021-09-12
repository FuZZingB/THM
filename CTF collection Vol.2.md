### CTF collection Vol.2                       
                                                                         
<img src="https://tryhackme-badges.s3.amazonaws.com/fso3ity.png" alt="TryHackMe">

	
	
![[Screenshot_2021-09-10_04_22_12 1.png]]
	
                                                                                 
Today we are going to solved TryHackme room CTF collection Vol.2 

## Nmap

![](app://local/C%3A%5CUsers%5CElliot%5CDocuments%5CTryhackme%5CCTF%20collection%20Vol.2%5CScreenshot_2021-09-10_04_24_05.png?1631393874578)

There is nothing in nmap scan because we know past CTF collection Vol.1 where is just finding hidden flags using unique method and cryptography,steganography and many others techniques.
So in this room Vol.2 we do same but it's more harder then past and findings flag using unique methods. Let's Began.......

## Dirsearch

![[dirsearch.png]]

In dirsearch we found many things that help me to find flags in further in this room...

#### Easter 1
![](app://local/C%3A%5CUsers%5CElliot%5CDocuments%5CTryhackme%5CCTF%20collection%20Vol.2%5CScreenshot_2021-09-10_04_24_58.png?1631394069073)

We clearly see that in Dirsearch scan result dir there name robots.txt 
going throw robots.txt first because we know that robots.txt is the first priority to check for Penetration tester A robots.txt file tells *search engine crawlers which URLs the crawler can access on your site*



  Easter found in robots.txt: 45 61 73 74 65 72 20 31 3a 20 54 48 4d 7b 34 75 37 30 62 30 37 5f 72 30 6c 6c 5f 30 75 37 7d

  ** DECODE this to get the Easter** 
  
  ![[Untitled.png]]

<details>
  <summary>Easter 1:Click To View The Flag</summary>
  <p> THM{4u70b07_r0ll_0u7}</p>
	<p> Hint: Check the robots</p>
</details>


#### Easter 2
![](app://local/C%3A%5CUsers%5CElliot%5CDocuments%5CTryhackme%5CCTF%20collection%20Vol.2%5CScreenshot_2021-09-10_04_24_58.png?1631394069073)

In same directory we see there is one disallow argument we going to check that disallow directory. but this one encoded with base64 we need to decode this for getting actual directory..

> base64 > base64 > remove spaces > base64 > remove spaces > base64 


Now we get that ``/DesKel_secret_base``  and we found it there...

![](app://local/C%3A%5CUsers%5CElliot%5CDocuments%5CTryhackme%5CCTF%20collection%20Vol.2%5CScreenshot_2021-09-10_06_55_59.png?1631278560691)

<details>
  <summary>Easter 2:Click To View The Flag and Hint</summary>
  <p> THM{4u70b07_r0ll_0u7}</p>
	<p> Hint: Decode the base64 multiple times. Don't forget there are something being encoded.</p>
</details>

#### Easter 3


Easter 3 is more easy to find because in dirsearch scan /login and in that page source code we can clearly get a flag 

![[Screenshot_2021-09-10_07_07_40.png]]

<details>
  <summary>Easter 3:Click To View The Flag and Hint</summary>
  <p> THM{y0u_c4n'7_533_m3}}</p>
	<p> Hint: Directory buster with common.txt might help.</p>
</details>

#### Easter 4 

Now It's time to very hard part of this room time-based SQLi. Time-based SQL Injection is an **inferential SQL Injection technique that relies on sending an SQL query to the database which forces the database to wait for a specified amount of time** (in seconds) before responding. The response time will indicate to the attacker whether the result of the query is TRUE or FALSE. But I don't know but it take 1 hour to dump all tables and columns. 

We going to perform attack to dump data using sqlmap in /login directory..

![[Screenshot_2021-09-10_11_07_45.png]]

And yeah it take some minutes because it's time-based SQL..

**We found user and password**

![[Screenshot_2021-09-10_08_48_35.png]]

**Final Easter found in THM_f0und_m3 database.**

![[Screenshot_2021-09-10_11_07_36.png]]

<details>
  <summary>Easter 4:Click To View The Flag and Hint</summary>
  <p> THM{1nj3c7_l1k3_4_b055} </p>
	<p> Hint: time-based sqli.</p>
</details>

#### Easter 5

And using those credential we can login and garb Easter 5..

![[Screenshot_2021-09-10_11_09_15.png]]

<details>
  <summary>Easter 5:Click To View The Flag and Hint</summary>
  <p>THM{wh47_d1d_17_c057_70_cr4ck_7h3_5ql}} </p>
	<p> Hint: Another sqli.</p>
</details>

#### Easter 6

Intercepting the request throw burp suit and get a response header flag is there..

![[Screenshot_2021-09-11_12_31_30.png]]

<details>
  <summary>Easter 6:Click To View The Flag and Hint</summary>
  <p>THM{l37'5_p4r7y_h4rd} </p>
	<p> Hint: Look out for the response header.</p>
</details>

#### Easter 7

In this part again we want intercept request and send into repeater change cookies invited value to 1 and send it..

![[Screenshot_2021-09-11_12_50_09.png]]

<details>
  <summary>Easter 7:Click To View The Flag and Hint</summary>
  <p>THM{w3lc0m3!_4nd_w3lc0m3} </p>
	<p> Hint: Cookie is delicious.</p>
</details>

#### Easter 8

![[Screenshot_2021-09-11_15-44-13.png]]

There is Hint available in page saying you need safari 13 on IOS 13.1.2 to view this message please. it clearly give hint changing user-agent values to safari 13. we can get user-agent through google by search 

![[Screenshot_2021-09-11_12_53_13 1.png]]

by changing user-agent though intercepting request in burp and change user-agent into safari 13 which we found and past into your request then  we get our raster...

![[Screenshot_2021-09-11_12_53_26.png]]

<details>
  <summary>Easter 8:Click To View The Flag and Hint</summary>
  <p>THM{h3y_r1ch3r_wh3r3_15_my_k1dn3y} </p>
	<p> Hint: Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148 Safari/604.1.</p>
</details>

#### Easter 9

Hint given there and it is about redirection we go through every directory in page and capture then throw burp after investigating all request we get a /ready directory and there is our Easter...

![[Screenshot_2021-09-10_06_32_33 1.png]]

<details>
  <summary>Easter 9:Click To View The Flag and Hint</summary>
  <p>THM{60nn4_60_f457} </p>
	<p> Hint: Something is redirected too fast. You need to capture it.</p>
</details>

#### Easter 10 

![[easter 10.png]]

There is claim now option but when we click on this it's say us to buy tryhackme voucher to access this but after intercepting request we get a referrer header so we change into tryhackme.com..

![[easetr 10.png]]

**And we get our 10th Easter to.. **

![[easter 10 final.png]]

<details>
  <summary>Easter 10:Click To View The Flag and Hint</summary>
  <p>THM{50rry_dud3} </p>
	<p> Hint: Look at THM URL without https:// and use it as a referrer.</p>
</details>

#### Easter 11

![[ester 11.png]]

After few discovery we get a this. there is menu where dishes menu we can select it and click Take It but we can get through every menu one by one and salad menu we get a message `What a healthy choice, I prefer an egg ` there is egg is a key I think to get Easter. we can intercept request and change request data in of dinner value into egg which is our key and yeah after change we can get our Easter 11..

![[easter 11 final.png]]

<details>
  <summary>Easter 11:Click To View The Flag and Hint</summary>
  <p>THM{366y_b4k3y} </p>
	<p> Hint: Temper the html.</p>
</details>

#### Easter 12


![[Screenshot_2021-09-12_00-08-03.png]]

  There is fake jquery and inside this we get a decoded message with a given values...
  
  ![[Screenshot_2021-09-10_06_43_57.png]]
  
  Decode this and get a 12 Easter....
  
  ![[Screenshot_2021-09-10_06_43_41.png]]
  
  <details>
  <summary>Easter 12:Click To View The Flag and Hint</summary>
  <p>THM{h1dd3n_j5_f1l3} </p>
	<p> Hint: Fake js file</p>
</details>

  
  #### Easter 13
  
  After scrolling down we get another push button option there.
  
  ![[easter 13 1.png]]
  
  And it redirect us to Easter page directly....
  
  ![[Screenshot_2021-09-10_06_41_23.png]]
  
 
  <details>
  <summary>Easter 13:Click To View The Flag and Hint</summary>
  <p>THM{1_c4n'7_b3l13v3_17} </p>
	<p> Hint: NO HINTS.</p>
</details>

 
  
  #### Easter 14
  
  ![[easter 14.png]]
  
 
 We can in source page where is Easter 14 is here and some embed image URL we just copy this whole code and save this into .html file extension and that's it we get Easter...
 
 ![[easter 14 final.png]]
 
  <details>
  <summary>Easter 14:Click To View The Flag and Hint</summary>
  <p> THM{d1r3c7_3mb3d} </p>
	<p> Hint: Embed image code.</p>
</details>

 
 #### Easter 15
 
 When we connect to `/game1/` (found by dirsearch), we are prompted for a combination, and we see a hash proposed as hint: 51 89 77 93 126 14 93 10
 
 And now we post the correspondence of numerical values for capital letters
 
 ![[burp easter 15.jpg]]
 
 
 
Also with small latter:

![[burp easter small 15.jpg]]

we have a number related to each capital letter like this `A=100,B=101`same with small letters `a=90,b=91`
And now we can decode this by using given hints

    51 89 77 93 126 14 93 10
    G  a  m  e  O   v  e  r
  
  And then input GameOver in place of answer we can get our flag..
  
  ![[easter 15 final.png]]
  
   <details>
  <summary>Easter 15:Click To View The Flag and Hint</summary>
  <p>THM{ju57_4_64m3} </p>
	<p> Hint: Try guest the alphabet and the hash code.</p>
</details>


### Easter 16

The page has 3 forms whose action points to the same page, using the same method (POST), each containing a button.

![[easter 16.1.png]]
    
    <form method="POST">
        <input type="hidden" name="button1" value="button1">
        <button name="submit" value="submit">Button 1</button>
    </form>

    <form method="POST">
                <input type="hidden" name="button2" value="button2">
                <button name="submit" value="submit">Button 2</button>
        </form>

    <form method="POST">
                <input type="hidden" name="button3" value="button3">
                <button name="submit" value="submit">Button 3</button>
        </form>
        </body>


Is possible to push all button together at once send all button values in POST request and get Easter..



![[easter 16 final.png]]

 <details>
  <summary>Easter 16:Click To View The Flag and Hint</summary>
  <p>THM{73mp3r_7h3_h7ml} </p>
	<p> Hint: Make all inputs into one form.</p>
</details>


### Easter 17 

![[easter 17.1.png]]

**From the source code of the main page..**

Decode this binary:
   And get a final Easter..
         `dec -> hex -> ascii`
		 
 ![[easter 17 final.png]]
 
 
  <details>
  <summary>Easter 17:Click To View The Flag and Hint</summary>
  <p>THM{j5_j5_k3p_d3c0d3} </p>
	<p> Hint: bin -> dec -> hex -> ascii.</p>
</details>

### Easter 18

![[easter 18.1.png]]

_Hint: Request header. Format is egg:Yes_

Following  hint to get a Easter and intercepting request throw burp and add header egg:Yes. and acquire Easter..

![[easter 18.png]]

<details>
  <summary>Easter 18:Click To View The Flag and Hint</summary>
  <p>THM{70ny_r0ll_7h3_366} </p>
	<p> Hint: Request header. Format is egg:Yes</p>
</details>


### Easter 19  


![[easter 19.1.png]]

At the end of code we have a png file name small.png 

**The file contains the easter**

![[easter 19 final.png]]

<details>
  <summary>Easter 19:Click To View The Flag and Hint</summary>
  <p>THM{700_5m4ll_3yy} </p>
	<p> Hint: A thick dark line</p>
</details>


### Easter 20 Final

From the last line of source code of the main page..

![[easter 20.1.png]]

Now, if we send the username and password using the POST method to the main page, we are provided with the Easter egg..

![[easter 20 final.png]]

<details>
  <summary>Easter 20:Click To View The Flag and Hint</summary>
  <p>THM{17_w45_m3_4ll_4l0n6} </p>
	<p> Hint: You need to POST the data instead of GET. Burp suite or curl might help.</p>
</details>



*********


