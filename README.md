# ultimate_football_hunt
Writeup of my first OSINT CTF.

The event was organised by organised by APT42.
## Summary



## The team
We were a team of 5 people, mostly beginners. It turned out we were pretty complementary. 

- jgreau
- tlebouvi
- cclaude
- vchan
- tsamson

## The challenge

### WHY-FI

The first challenge was just here to confirm that everyone was physically present at 42 school Paris.
A Wifi source was there with the flag as name. Nothing more to say here.

### Who's in Paris

For this challenge, we were given 2 ressources :

- A link to a [youtube video](https://youtu.be/cpWVm0iZz4s)
- A screenshot of a building.

challenge was to find the name we could see in the photo.

On the same youtube channel was an other video giving more interesting informations.
tl;dw the video gave us informations about the location : they are near Champs Élysées at Paris and we can see the building in the video.
After a quick check on google maps, we found the name of the building and were able to move on to the next challenge.

### Internship 1

We had now to find who was behing those videos.
Luckily enough, there was a commentary on the second video, leading us to an other [youtube channel](https://www.youtube.com/channel/UCnfNZ9ExuNlYssiAgI4qXhg).
On this channel, there is a stage report video of a 42 student. As any 42 student, he has a profile on the 42 intranet.
On his profile, Messi Palaiseau has a resume and, finally, on his resume, a Linkedin profile. The flag was on this Linkedin profile.

### Croiser les sources

Now that we had the profile of one of the people we were looking for, we had to find his associates.
To do so, we searched on Messi's Linkedin profile and found a conversation where he answered to another person : jean Neymar.
Funfact : we found a fake flag in his profile, written in JSFuck. We never had a use for this flag.
On Jean Neymar's profile, she told us to keep continuing the search.

The only post that seemed interesting on her profile for our hunt was her resume.
On this resume was a website. We went on the website, this was some kind of troll website.
In the footer was another website for somethind that looked like a fake company that apparently made the website.
They made something like 8 other websites.
We checked all of these, every line of HTML code, every page of every site, and found nothing.
This was our first rabbit hole.

After 2 hours of unsuccessful researches, an admin told us that the website linked in Jean Neymar's resume wasn't their and that we had to focus on the resume.
We did so and looked for the address, fake address, nothing else found.
Maybe the mail ? A quick check on Epios told us a Flickr account existed with this mail.
Let's take a look. And we found her !
Finally, on her [flickr profile](https://www.flickr.com/people/196951899@N06/) we found the flag.

### Ctrl+z

Next step was to find more informations about her. We found 2 informations on her Flickr profile :

- She's looking for a Mastodon host.
- She went on a trip recently (or at least, she had holidays).

A quick check of her name on Mastodon and we found [her profile](https://mastodon.social/@JeanNeymar).
On her Mastodon, she talks about a friend called Paul.
We also learn that there was another photo on her flickr, which was deleted.
Let's check at her profile on wayback machine then to see if a backup does exist.
And it does ! We can see the photo but can't access it at the moment.
To get to the photo, we had to check for the source code on WayBackMachine, check for the link wrapping the photo, and finally get to that link.
We had our flag now.

### Souriez et dites Ouistiti !

Now that we had the photo, we had to find the location of it.
To do so, we had to donwnload the original.
The problem is : the photo doesn't load on the link we found.
Once again, we searched in the HTML code of the page, found the id of the photo and used this id to access the "see all sizes" page pf hte photo.
There we found the original photo, downloaded it and extracted GPS point from the photo metadatas with jimpl.
The point was at Corvo, a little island in the middle of the atlantic ocean.
On Jean's mastodon profile, we also lear that The friend she met during her trip was on twitter.
That's where we used specific keywords to precise our search on a specific area, on specific dates in a specific language : `lang:fr since:2022-11-01 until:2022-12-01 near:Corvo`.
With this search, we found [Samuel Osintiti's twitter account](https://twitter.com/OsintitiSamuel).
In one of his tweets was this code : QVBUNDJ7Z2VvdGFnaW5nX2lzX2Vhc3ksX25vXz99.
Once converted from base 64 to UTF8, we found out that it was finally the key we were looking for.

### Enjoy the ride

Now, we need to find more about Samuel.
We learn on his twitter profile that Samuel likes geocaching.
He also uses an application named strava to record his bike runs.
We found [his profile](https://www.strava.com/athletes/104074564) on this map and the flag was there, split in 3 parts.

### Let the hunt begin

Now that we found his profile, we can check on his runs and see if there are some places he is used to.
We found a square named Jean Leclerc. It was near 42 Paris, we had to go there by ourselves.
After some fun IRL part (some juggles with a baloon with Messy Palaiseau, a geogache and some lockpicing and a quizz), we got the flag and came back to the school to keep eating graphic cards and keyboards.

### Come to the dork side

After our little walk, we came back to Samuel's twitter profile.
There, we found an [old friend of us](https://twitter.com/MessiparaMessi), Messi.
On his profile, we found 2 interesting informations :
- He has a website. As avan.com is already taken, he had to take Saint Helena domain name. Therefore, his website must be [avan.sh](avan.sh).
- There is a hidden article on his website.

Let's find it !
Funfact : looking for PDF on the website with dorks, we found a flag from another CTF (an older one).
After some tries, we finally found the "hidden" article with this search on google : `"osintiti" site:avan.sh`.
We found pour key, and the link to a new [facebook profile](https://www.facebook.com/people/Franck-Tarte-Aux-Framboises/100087765854784/).

### Destination finale

On franck's profile was a photo showing the view of a city from the sky. Franck mentionned a review he did on a "greenery".
First of all, we had to find the city on the photo. The wing of the plane told us the company which was TAP air portugal.
We checked on flight radar an foud that there was only 2 destinations with this company from Paris : Porto and Lisbon.
We focused on Lisbon because the water in the background was matching with google maps.
Our search time was pretty long but we found an area matching with the street patterns at some point.
We then checked for google reviews of the local greeneries, matching the date, from people called franck and in french language.
We found one, giving us access to Franck's [google profile](https://www.google.com/maps/contrib/108690436304588953670/reviews/@38.7374112,-18.1195569,5z/data=!4m3!8m2!3m1!1e1?hl=fr).
The flag was on his profile photo.
We just had to change the URL of the link of the photo to get the full size original photo and be able to read the flag.

### Geoguessing 1

Back to Franck's facebook profile, he gave us a link to a [google drive](https://photos.app.goo.gl/XWRWhx2GYqbXh3qa8) in his own photo comment.
On this photo, we can see a tiny 42 logo on the sign in the first plan.
We looked at every 42 campus until we found 42 Prague's campus.
It was our first Geoguessing key.

### Geoguessing 2

For the second key, another photo was given.
It was pretty straight forward, the name of the building was written on it in big golden letters.

### Geoguessing 3

Another geoguessing, another photo.
An SK Slavia PRaha logo can be seen. Searching it on google maps and it points to an area near a staduim.
Our point is in the streets surounding the staduim.

### Geoguessing 4

Last geoguessing key, we have to find the name of the staduim. Just clickrd on the point on gmap and we got it.

### La chance du débutant

For this challenge, we had an [Instagram profile](https://www.instagram.com/girouscopee/).
In a photo, Girouscopee is mentioning APT42 collector stickers we can find and buy on the internet.
We found them [on vinted](https://www.vinted.fr/member/120522419-dingocrypto).
The seller seems to be the crypto enthusiastic Messi talked about on his linkedin.
Let's check his [twitter profile](https://twitter.com/crypt0dingo) linked on his vinted.
The flag is in his twitter bio.

### FC NTF

Last flag to find.
We checked the profile of our cryptobro and found [a tweet](https://twitter.com/crypt0dingo/status/1595064168159547392?s=20&t=UHASTsvhplhIeLXJT9RMcA) linking a smartcontract on the eth blockchain and the code of this smartcontract.
We went to the smart contract address on ethscan and checked for more details.
In the details we got some input datas. We extracted them in the UTF8 format.
The data seems kind of corrupted, but as there are some understandable sentences, we might get something interesting.
We're liikong for parts that seems "less corupted" and in the end of the string, there are a long part that doesn't contain corrupted datas.
Moreover, these 3 last lines looks like hexadecimal datas.
Let's convert it into UTF8 again. We got the first part of our key for the first lines ! But the 2 other lines can't be converted.
Looking more closely at the 2 other lines, there seems to be 2 words and an uppercase before we get an actual hexa address.
Let's try to convert them now. It can be converted but it was not a part of a key.
But it looked like base 64 datas. Let's convert it again from base 64 to UTF8.
It worked again, we have our 2 last parts ! But something is off with the last part, it means nothing.
It looks like caesar code, and a rotation function does confirm that, we got our last part and the last key of this CTF is complete !

## Conclusion

On a personal note it was an awesome first experience.
We came at the CTF as beginners, aiming to resolve a maximum of half of the challenges and in the end we were the first and only group to solve it on time.
Even if we did 4th place in the end due to the points count I am pretty proud of our performance.

Thanks again to my team members : jgreau, tlebouvi, cclaude and vchan for the day, we really found ourselves and completed each other competences.
A last thank to APT42 for the organisation of this CTF, which was very fun.
