## Header Writeup [OSINT]

First of all, the name of the challenge is almost always important, this one indicated something about headers..

To solve an OSINT challenge we need to collect as much information we can.

While looking into the message we can see a couple of important things:

```txt
ElosoCynem is an arrogant dev who claims to be a member of anonymous. Follow the trail and find the flag
ElosoCynem ~~~~~~~~~~~~~~ dev ```

We now have 2 pieces of information, '**ElosoCynem**' that can be an name / alias / username and that he is someone who is in the programming / hacker field.

So we open a tool for this challenge: `https://osintframework.com/` and went for the 'Username' section because he might have a username under this name.
We will use 'Namecheckup' but you can use any tool in that section.

Once we run the name 'ElosoCynem' 1 site gets popped up pink (which indicates that it's taken) and it was GitHub!

After finding the GitHub it's pretty much straight forward.

The account had only 1 repository with one file (MyWork → README.md).
When opening the context of the file we can see the following message:

```txt
Hello. I am a popular hacker and I leak many databases and put them on pastebin
I am member of anonymous.```

This doesn't give much, but we can see it had 4 commits! Maybe there is something that was taken out?
Indeed in the 3rd commit ('leak add') there was a link to a pastebin!

This is really going pretty smooth so the name of the challenge (Header) is still something that we need to search for.

After looking into the patebin we can't see much inside it that can help up, but we can see it's linked to an account!
(In an OSINT challenge it's always good to find more information about the target we got, and websites account are the best for information)

When you open up the account you can see 2 pastebins registered to the account, so there must be something new in the one we didn't see yet, exciting!

Opening the second pastebin reveals us a twitter account he is using: (and like said earlier, the more the merrier!)

`My twitter @OsoricFeran`

When you open up twitter and search up the account you can easily find it.
My first guess was to take a look into the website that he had in his bio

`https://osoricferan.netlify.app/`

The website had only 1 sentence in it: "**I AM A PRO ELITE 1337 HACKER. YOU ALL ARE NOOBS!!!!!!!!***"
You may think this isn't sufficient, but remember once again the name of the challenge i.e, **Headers**.

So we will open our browser dev panel and open the 'Network' section to search in the headers, and before we know, there's the flag..


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1625058259045/_ifnDIX3V.png)
