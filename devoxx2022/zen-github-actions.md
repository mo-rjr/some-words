# [The Zen School of GitHub Actions](https://www.devoxx.co.uk/talk/?id=6468)
Jonathan Ruckwood

This was a very good talk with lots of practical advice.  

The slides are online:  
[https://github.com/jon-ruckwood/devoxx-2022/](https://github.com/jon-ruckwood/devoxx-2022/) 
and [so is the video](https://www.youtube.com/watch?v=J0X82xUApD4)

Therefore I am just going to summarise the main points:
* tips
  * use caching (free, up to 10Gb per repo)
  * set limits for time and concurrency
  * you can reuse and compose workflows, including from other repos
  * there are secret values you can add for debugging
  * you can (try to) run your GitHub Actions locally using [nektos/act](https://github.com/nektos/act) -- requires Docker
* design
  * keep design simple and lean, using standard build tools
  * have a back-up plan if GitHub Actions could prevent deployment (we might need to think about what this means -- they have an in-person playbook they can substitute in)
  * treat your repo as an API -- treat the workflow as an interface -- don't do something yourself, get the repo to do it
  * you can chain workflows across repos
  * but beware of coupling...
* security
  * DO NOT trust the marketplace
  * follow [GitHub's security hardening guide](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)
  * do not allow workflows from fork PRs
  * when using an action, do not reference it by version but by SHA
  * limit token permissions
  * watch [Bob Ros on 'How to Use GitHub Actions with Security in Mind](https://www.youtube.com/watch?v=Ers-LcA7Nmc)
* summary
  * there will be pain, accept that
  * don't sweat the small stuff
  * DO NOT ignore security
