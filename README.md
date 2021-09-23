## jules32.github.io
 
Code for my website, [jules32.github.io](jules32.github.io).  

Jekyll theme based on [Freelancer bootstrap theme ](http://startbootstrap.com/templates/freelancer/)


## Adding Jekyll SEO Tag with Bryce Mecum April 30. 

> "Does anyone have recs for improving SEO metadata in a `_config.yml` for an (old) jekyll/github pages site? Thanks in advance". 

These are brief notes from [a tweet](https://twitter.com/juliesquid/status/1388164639138058243) where Bryce pointed me to and helped me install <https://jekyll.github.io/jekyll-seo-tag/installation/>. 

My site doesn't have a Gemfile like the instructions say. Bryce: "ah, I bet GitHub pages lets you skip specifying one if you can get by with the stock config".

So we went for Option 2 to install a plugin: <https://jekyllrb.com/docs/plugins/installation/>. It was a can of worms and here is how. I ran bash code from my terminal within RStudio:

sudo preceding `gem install jekyll-seo-tag`. This failed because of Ruby versions. So —

Using homebrew (https://brew.sh/) i updated Ruby (`brew install chruby` and `brew install ruby-install`) and saw I had `chruby ruby-2.6.3`, good news

`which ruby` was pointing me to the wrong place though: `/usr/bin/ruby`

We thought I needed macOS Command Line Tools. But `lowndes$ xcode-select --install` returned
`xcode-select: error: command line tools are already installed, use "Software Update" to install updates`. Then did `brew config` and saw that my Command Line Tools (CLTs) were fine. 

Taking a different path, we did `brew install chruby` and `brew install ruby-install`. When `chruby` installed, there was a Caveat:

```
==> Caveats
Add the following to the ~/.bash_profile or ~/.zshrc file:
  source /usr/local/opt/chruby/share/chruby/chruby.sh
```

And so I had to `nano ~/.bash_profile` and paste in `source /usr/local/opt/chruby/share/chruby/chruby.sh` (and remember how to save and exit: control-X and return)

Then: `ruby-install ruby-2.6.3`. Now `chruby` should list that version. 

`chruby ruby-2.6.3`. Then:

```
which ruby
/Users/lowndes/.rubies/ruby-2.6.3/bin/ruby
```

woo!

sudo preceding `gem install jekyll-seo-tag` then worked!

Now, back to serving Jekyll locally. 

`jekyll serve`. woop!

But now need to check if the jekyll-seo-tag is working. A final thing I needed to do listed https://github.com/jekyll/jekyll-seo-tag/blob/master/docs/installation.md, and I did in these commits: [1](https://github.com/jules32/jules32.github.io/commit/2c3e731354a240f6a0ffb57ee977f86bf9b40de8) and [2](https://github.com/jules32/jules32.github.io/commit/5de699c0fac7c24cd469bfe41acb0a9b55dc59c5#diff-e241bda4e3c3c6dc1c0b00185b61f6ce19b5eb16e294dd955ca9fa6d01befb0e). Bryce knew what to look for here, knowing what jekyll-seo-tag was trying to generate but being blocked by old code, and also just the setup of my (old) files structure and knowing what my template(s) were.

To check it's working, right-click View Source or Inspect a page in your locally-served site in your browser and see its traces (i.e "Begin Jekyll SEO ta v2.7.1"). I never saw this locally, but when I pushed to GitHub, the live site did reflect this. 

So we did it! 

Today Bryce also helped me upgrade to https: <https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https>

THANK YOU SO MUCH BRYCE!!!

