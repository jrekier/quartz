---
tags:
  - "🔧Technical"
  - "🖍️Learning"
---
I like running code on my workstation and operate via `ssh` from my laptop. For jupyter notebook, I do:
```
❯ jupyter lab --no-browser --port=8080
```
Then I tunnel to remote with:
```
❯ ssh -L 8080:localhost:8080 jrekier@watson-pc
```
Then I open http://localhost:8080 in my laptop browser.