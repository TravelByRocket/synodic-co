# Synodic Studio Website
## Summary
This is a Jekyll-based website using the [Minimal Mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/) theme. 

[Synodic Studio](http://127.0.0.1:4000) is my one-person iOS Development and Creative Technologies company, though on this website I solely focus on topics related to 
- iOS Development, 
- UI/UX Design, and 
- Information Visualization. 

Any other documentation I have about my Creative Technologies & Design projects (interactive art installations, 3D Printing, etc.) is at [KJ6DEV](kj6.dev), and what doesn't fit in either of these places goes to [bryancostanza.com](http://bryancostanza.com).

## Building
### Gem-Based vs Remote Theme
I started with a gem-based theme because it was very fast when building locally. In contrast, using a remote theme while building local frequently took 10s of seconds to a few minutes downloading the theme files.

Unfortunately, my gem-based theme was not successfully building on GitHub Pages, so I was changing the setting from gem-based to remote each time I pushed. 

After talking to a friend about possible solutions to this, I came up with the idea of just pointing the GitHub page to my `/docs` folder and using my pre-built site instead of having it build after pushing. 

This seems to be working well, butt based on the green checkmark on my repo it looks like it might still be building with Jekyll, though successfully. I'm happy with the performance and workflow right now, even if there might be redundancy. 

### Development on Local Machine
``` bash
bundle exec jekyll serve --livereload --baseurl ""
```

This method serves at `http://127.0.0.1:4000`, aka `http://localhost:4000`

### Deployment on GitHub Pages
``` bash
bundle exec jekyll build
```

The main difference I see is to have `sitemap.xml` build with the correct base URL.

## TO DO
- Confirm that site is being served from my build and not building again on GH Pages
	- Better yet, find how to use a remote them without reloading/re-caching on local machine
- Ensure that site is rebuilt for GH Pages in the latest commit before pushing
- Commit `/docs` only on push
- Show a "date last built" to confirm site build update