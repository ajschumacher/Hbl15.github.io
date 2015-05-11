---
layout: post
title: Silent Mistakes.
---

#Silent Mistakes in Coding

I know we all have that moment when we are excitedly waiting for our program to print out the result, and all we get are these ** <span style="color:red">bright red lines</span>** on the screen saying there are **errors**...Don't know about you, but some of those times make me wanna pull my hair out :p.

Well, the next time those things appear, remind yourself that they are your best friends. Because sometimes, when they don't appear even when you make a mistake, those are dealy mistakes.
(To think about it, only your real friend point out your mistake baltanly, but they are those who really help you improve.. :D)

So here are some of the silent mistakes that I encounter recently:

### Listen to your teacher, don't mess with the FOR condition:

I came across this while working on my Beson project. For Beson, I had to take the MTA turnstile data and group the total entries for all turnstile at the same station in the same day... (phew that was a mouth full). 
This is how the data looks like :

```
C/A,UNIT,SCP,STATION,LINENAME,DIVISION,DATE,TIME,DESC,ENTRIES,EXITS                                     
A002,R051,02-00-00,LEXINGTON AVE,NQR456,BMT,05/02/2015,16:00:00,REGULAR,0005117403,0001732748                                     
A002,R051,02-00-00,LEXINGTON AVE,NQR456,BMT,05/02/2015,20:00:00,REGULAR,0005117774,0001732779                                     
A002,R051,02-00-00,LEXINGTON AVE,NQR456,BMT,05/03/2015,00:00:00,REGULAR,0005117965,0001732825                                     
A002,R051,02-00-00,LEXINGTON AVE,NQR456,BMT,05/03/2015,04:00:00,REGULAR,0005118004,0001732837                                     
A002,R051,02-00-00,LEXINGTON AVE,NQR456,BMT,05/03/2015,08:00:00,REGULAR,0005118018,0001732859 

```     

So for starter, I just wanna find a list of date without repeat (I was just starting Python then..so no judgment here.)
This is what I thought to be my <strike>clever</strike> solution:

* Take the date column, put them into a list and called them list of dates.

* Run For loop through this **list of dates**,  for each date, I will make into a key in my dictionary. I then will go through my entire file, and find all datas with the same day, and put them together


* Not so clever step: After I am done with each date, I will remove it from my **list of dates**. It means that you won't create the same key twice and overwrite your data.

```python
#Creat a new dictionary where key = (C/A,Unit,Station)
#but group all same day count for each key together

Updated_CUS = {}

for CUS_k, CUS_v in tempdict.items():
   Updated_CUS[CUS_k]=[]
   
     for l in CUS_v:
#         print 'l is', l
        CUS_date = l[0]
         CUS_counts = l[1]
         CUS_v.remove(l)
#         print 'CUS_v is', CUS_v
        
         for h in CUS_v:
#             print 'h is', h
             if h[0] == CUS_date:
                 CUS_counts += h[1]
                 CUS_v.remove(h)
#                 print 'CUS_v in inner loop is', CUS_v
        
         Updated_CUS[CUS_k].append([CUS_date,CUS_counts])

            
# print Updated_CUS.values()
```

All sounds good right? I don't even have those <strike>annoying</strike> error message...

### Well,  I was deadly wrong!!!
Lucky, I was running on a relatively smalle set of data that have only 7 days in total. Guess what, my result only have a dictionary of 6 days. I was consistenly missing a day without know why... 


So why? *starting to pull my hair out...*

Well, Teacher-Know-It-All came to the rescue... See all that print comment in the code? That's his debugging. 

###Where is the bug?

Apparently, For loop has its own system, and the pointer will moved based on position of the list, #NOT# the next position.

HMMM? Totally confused?
Say I have a list M = [a,b,c,a,m] and I wanna make a list of keys out of M

What I want to do is : For item in M, M[item] is a key.
But since M has repated items, I don't want to recreate the key and might accidently earease all the value I saved in that key. Best way would be go through this list, after you saved a key and its value, you remove the key from the list.

THis is how it runs:
	Step 1 : a in M, so make M[a] to  be key
			 Remove a from M
			 Now go through the rest of the list to see if you find any other a, save there data in the value of M[a], then remove them.
	Step 2 : Move on to the next item.

But here is the crucial thing. Because you remove a, now M = [b,c,m]
An For loop now go to the **second** position in M, which is **c** and entirely skip b !!!

So long story short, if you don't get whatever gibberish I am spouting, there is one lesson to take home:

### Don't modify your For loop condition While you are INSIDE that For loop...

And learn to love your error message, for without them, you might be blind side by your own mistake.

...to be continued on "Silent Mistakes"

Have a nice Sunday, and Happy Mothers Day.








