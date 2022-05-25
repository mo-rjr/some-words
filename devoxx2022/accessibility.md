# [Julian Dubois: Purple Pound - Accessibility in the UK and becoming a Master Accessible Author](https://www.devoxx.co.uk/talk/?id=3886)

[Video on YouTube](https://www.youtube.com/watch?v=ESemhlchigY)

The speaker, Julian Dubois, works at Microsoft, and started by saying that recently they'd had to do some work on Internet Explorer. 
Microsoft said that because 5% of users use it, it's important to them.
But an estimated 15% of users have accessibility needs (plus there's all their family and friends who want to use the same tech as them).
So it's definitely worth your time.

He said that it's not about disabilities as such, it's about a mismatch between ability and expectations.
An example of this, he said, would be his strong French accent when talking to us, an Anglophone audience.  (To hear him say empathy as uhn-pattee was delightful.)

He set out ten points
1. define accessibility (its importance and benefits)
2. convince your boss (because some things will cost a bit of time/money)
3. use user personas -- he pointed to [an excellent set made by gov.uk](https://alphagov.github.io/accessibility-personas/). (They also have [ways of simulating their experiences](https://alphagov.github.io/accessibility-personas/setup/#setting-up-personas).)
4. start testing with one, and then extend to many
5. learn from diversity -- don't assume people have the same experiences
6. iterate in small steps -- do not leave accessibility to the last sprint but have it there from the start
7. use tools -- he recommends the [accessibility insights](https://accessibilityinsights.io/) plugin.  (This is not one of the ones we've been using.)
8. automate and add to CI to prevent regressions: the accessibility insights tool is also available as a GitHub action, for example
9. you can innovate from a starting point of accessibility (unlike supporting IE) -- accessibility needs can drive new things that are good for everyone, like subtitles
   1. he mentioned the immersive reader on Teams -- in a chat, go to the three dots at the top right, choose immersive reader, and something that started out for accessibility requirements now has extra options like syllable marking, parts-of-speech marking, translations, even a picture dictionary feature, which can help children and EFL speakers as well
10. there is also training: e.g [Microsoft's Accessibility Fundamentals](https://docs.microsoft.com/en-gb/learn/paths/accessibility-fundamentals/?WT.mc_id=accessibility-35940-cxa)

My takeaway from this was that I wanted to share the gov.api accessibility personas, and investigate the Accessibility Insights tooling in our team. 
Plus I really like his insight about how it's about all mismatches between expectations and abilities.