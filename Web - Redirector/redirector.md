## Redirector

_200 points, 76 solves_

You’re attempting to find sensitive information on a villain organization’s website, however, you are not having much luck. You notice that the site uses a lot of redirects, with some information on those redirect pages. However, you cannot inspect that information quick enough before you are redirected.

[Link](http://www.jerseyctf.net)

### Requirements
* Burp Suite Community/Professional
* Patience


### Approach

This challenge had something to do with redirection, as the challenge title suggests. The first thing I did was to open up the page in a web browser. However, seems like this leads to another page saying it is not being redirected properly. We can see the initial url has  a "`/i`" appended to it... Interesting...

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/webpage.png)

I decided to use burp proxy to capture and analyse the traffic sent to the web server, as well as the headers. (Remember to turn `Intercept` On).

Removing the argument and reloading the page thereafter, we get a Intercept prompt, we get a change after the `GET` method--`j`... hmm this is suspicious and yet reminds me of a challenge I've done in the past in class.

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/intercept.png)

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/j.png)

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/c.png)

Forwarding the traffic once more we get a `c` - wow! I was starting to think we got the flag since the format was `jctf{xxx}`. After forwarding the traffic a couple more times, we hit the end? After further inspection of the HTTP History tab, we see this and are able to roughly decipher the flag--`j... c... t... f... {... y... 0... u... %7B... l... 1... k... E... m... Y... -... R... e... d... i...`. Since url encoding is used, `%7B` can be decoded as underscore (`_`). So what we have now is `jctf{y0u_l1kEmY-Redi`... is this the flag? hmm not quite... 

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/partial_flag.png)

Tried to enter this but sadly got rejected. I thought maybe I mistyped something and went back to triple check. Then I asked for tech support thinking that there was some typo lol!

So the support guy gave me some clues that unexpectedly helped me figure out what to use (but he never heard of it himself apparently!)

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/convo.png)

After he said `The last part is cut off! Perhaps, you need to extend the your redirects.` I got an idea--to use burp repeater. So for every response given, I edited the letter behind the `GET /`. Take not you will want to have a notepad at this point to document all the characters output as they will **not** be shown in the HTTP History tab.

We will first send any one of the response with a character to the Repeater Tab.

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/send2repeater.png)

We then hit `Go` to send the request manually, since the web browser way didn't work... well it didn't fully (till the entire flag was printed).

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/repeater-go.png)

Ok now we have some response with another character - `r`. Now what we need to do is replace `i`, which was our initial request with `r` (the next request). i.e. the previous response will become the next request... you get the idea

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/repeater-go2.png)

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/repeater-go3.png)

After we reach the end of the flag format (character `}`, we will want to stop. This finally lead to the flag (we can now stop here!): `jctf{y0u_l1kEmY-Redir3CTs}`.

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Web%20-%20Redirector/repeater-stop.png)

## Reflection

This was a rather meaningful challenge which reinforced my understanding of redirects and the use of burp repeater and burp as a whole, an invaluable tool for web-app pentesting.
