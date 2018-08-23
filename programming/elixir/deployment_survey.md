## Elixir deployment survey

Nanobox prefers Mix to Release when deploying Elixir app.
https://content.nanobox.io/elixir-app-deployment-with-nanobox/

Which one is your deployment way and Why?

**Mix** vs **Release**

alisdair [11:09 AM] 
releases are much more convenient when you have any sort of continuous delivery pipeline

cdegroot [9:01 PM] 
@jinkyou YMMV. I prefer releases for a dockerized environment; but yeah, once you have migrations and stuff running in production as part of your deployment (question - do you want that? Often the answer for larger setups turns out to be a firm "nay") it's probably easier to stick with Mix-in-prod.