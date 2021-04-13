## Redirector

_200 points_

You’re attempting to find sensitive information on a villain organization’s website, however, you are not having much luck. You notice that the site uses a lot of redirects, with some information on those redirect pages. However, you cannot inspect that information quick enough before you are redirected.

[Link](www.jerseyctf.net)


### Approach

This challenge had something to do with redirection, as the challenge title suggests. The first thing I did was to open up the page in a web browser. However, seems like this leads to another page saying it is not being redirected properly. We can see the initial url has  a "`/i`" appended to it... Interesting...

![img]()

I decided to use burp proxy to capture and analyse the traffic sent to the web server, as well as the headers. (Remember to turn `Intercept` On).

Removing the argument and reloading the page thereafter, we get a Intercept prompt, we get a change after the `GET` method--`j`... hmm this is suspicious and yet reminds me of a challenge I've done in the past in class.

![img]()

Forwarding the traffic once more we get a `c` - wow! I was starting to think we got the flag since the format was `jctf{xxx}`. After forwarding the traffic a couple more times, we hit the end? After further inspection of the HTTP History tab, we see this and are able to roughly decipher the flag--`j... c... t... f... {... y... 0... u... %7B... l... 1... k... E... m... Y... -... R... e... d... i...`. Since url encoding is used, `%7B` can be decoded as underscore (`_`). So what we have now is `jctf{y0u_l1kEmY-Redi`... is this the flag? hmm not quite... Tried to enter this but sadly got rejected. I thought maybe I mistyped something and went back to triple check. Then I asked for tech support thinking that there was some typo lol!

![img]()

So the support guy gave me some clues that unexpectedly helped me figure out what to use (but he never heard of it himself!)

![img]()

After he said `The last part is cut off! Perhaps, you need to extend the your redirects.` I got an idea--to use burp repeater. So for every response given, I edited the letter behind the `GET /`. Take not you will want to have a notepad at this point to document all the characters output.

![img]()

![img]()


This finally lead to the flag.

![img]()