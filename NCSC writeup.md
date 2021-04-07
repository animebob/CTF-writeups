## CTF-writeups
Write ups for National Cyber Scholarship Competition 2021

## Web App Exploitation

Didn't do so well in this one so I only have writeups for a few of them.

# WE01
The site is at https://cfta-we01.allyourbases.co/
This one seems really hard but it actually turns out to be not too bad.
1. The site doesnt seem to contain much just a flashing light with some sort of language or code.
2. The code doesn't seem to be any ciphers so we do a quick google search of the symbols to see if there are any matches.
3. 
![image](https://user-images.githubusercontent.com/24442064/113928014-130cc700-97a3-11eb-9b70-6c3ea22c1840.png)

3. Nice! it seems that result 2 has some sort of link. The symbols look too alike to be coincedential so we go into the link and it seems to be a twitter post.

![image](https://user-images.githubusercontent.com/24442064/113928241-5a935300-97a3-11eb-914e-07999040d0ac.png)

4. Well how interesting so we check out the site and we find that its a way to write javascript into different languages.
5. The wierd symbols must be obscufated javascript so I stick it into console and it runs the javascript giving us the flag!

![image](https://user-images.githubusercontent.com/24442064/113928431-a47c3900-97a3-11eb-8c12-e5208d4d4eca.png)

6. Yea! This was alot easier than it looked.


# WE02
The site is at https://cfta-we02.allyourbases.co
1. Well the first thing one should do in web app is to check robots.txt for any mention of a link. (they also give a hint for this on the News Page)

![image](https://user-images.githubusercontent.com/24442064/113928744-0ccb1a80-97a4-11eb-8c2a-dc2abfbbc58e.png)

2. So we check https://cfta-we02.allyourbases.co/robots.txt
3. Viola! There seems to be a /4ext6b6.html
4. We go to https://cfta-we02.allyourbases.co/4ext6b6.html and get the flag!

# WM03
The site is at https://cfta-wm03.allyourbases.co/.
1. We take a look at inspect elements and we notice some comments. Uh oh somebody didn't remove thier TODO list. Now we know the code of the .php file that is authenticating the passowrd.
![image](https://user-images.githubusercontent.com/24442064/113929363-d8a42980-97a4-11eb-8688-60834161bc90.png)
2. First thing one would think is to take the hash and salt and enter it into hashcat. (tbh thats what I did)
3. Unfortunately after trying it with rockyou.txt and other wordlists we don't get a result.
4. Some google searching about phps and hashes get us https://www.whitehatsec.com/blog/magic-hashes/
5. Turns out the == in php messes up if the hash it is equating follows the format 0e and a bunch of numnbers.
6. Taking a look at the hash shows us that it is actually 0e and a bunch of numbers. This is too coincidential to not be intentional.
7. Now the issue is find a password that will result in a salted hash with the format 0e and a bunch of numbers.
8. We make a quick python script to iterate through numbers until it finds a hash that meets the conditions:

![image](https://user-images.githubusercontent.com/24442064/113930440-23727100-97a6-11eb-837d-0f28a5c30333.png)

9. After a while we get **15896119** as a possible password

![image](https://user-images.githubusercontent.com/24442064/113930163-cb3b6f00-97a5-11eb-9248-15f86731d3a8.png)
