# About 

I am starting this project to fill a gap that I see with Clojure guides and documentation, especially that geared towards beginners. I want to help create the definitive guides that help people get started with Clojure in all aspects. This means getting Java and Clojure installed (for all three major OS's), getting their editor (I will create guides for all the top editors) set up to hook into a running Clojure repl, getting a project started (I will be focusing more on deps.edn than Leiningen), and how to use the most common libraries found in the ecosystem. These guides will be written and published, on a dogfooded Clojure stack app of course, at clojureclarified.com. I hope to make them as thorough as possible (while showing more brevity maybe than what I have done here in the application, lol). 

According to the 2021 State of Clojure Community survey, almost 80% of Clojurists are using it for web development. I want to show someone exactly how to get a web app up and running, starting from first principles. This means starting with a minimal backend driven project using Ring and adding routing, templating, etc. while explaining exactly what these things are used for in web development. Then we will move on to frontend and most importantly, connecting the two which I have never found adequately explained. The guides will show how to connect to a database (using next-jdbc) and how to deploy into production. As I mention below in the next question, so many Clojure books, guides, and docs assume domain familiarity and only want to show you how to do something the Clojure way while assuming you know the underlying domain. I want to go down a level and teach better fundamentals and first principles for those who are not so experienced.  

Many times, when a Clojure library doesn't exist for a major need the general advice is to just use Java interop. Many of us newer Clojurists, however, are not familiar with Java so this can be quite intimidating. I want to write a guide showing someone how to properly interop with a major Java library in a real world project.

I will be updating the github readme with other guides I hope to write as well. As the main priorities get covered I want to write guides that cover more advanced topics such as transducers in the future. I will also be soliciting further recommendations from the Clojure community for other guides. I am highly active on the Clojure Slack and have seen the common questions that come up time and again in the #beginners channel.


# Building the website itself (this serves as an example of a full stack Clojure/ClojureScript app)
  ### backend: deps.edn, jetty, reitit, aero (for config)
  
  I've commented out some dependencies in `deps.edn`, mostly database stuff. You can just delete that if not needed.
  
  ### frontend: shadow-cljs, reagent, tailwindcss (w/ daisy ui)
  
  I've commented out re-frame for now but it will probably be added back in when needed.
  
  ### deployed through dockerfile 

Demo is currently deployed and running live through `render.com` at: https://clojure-demo-app.onrender.com/ 

It's using the free tier so first load might take a while, but when live I'm getting lighthouse scores of 97-99% Performance 
(I only get 89% here running the production release on localhost so `render.com` must be doing something nice here) 
and 100% on Accessibility, Best Practices, and SEO (but the demo is only displaying Hello World). 
The free tier allows for 512mb and this demo seems to use up to ~170mb for just the "Hello World" according to `render.com`'s metrics but I haven't looked into too much yet.

The dockerfile should allow it to be used elsewhere like `fly.io`, `railway.app`, and `heroku` but I haven't tested.

** I don't know how to actually create an official template yet so I manually have to change every occurrence of `TODO` in the repo 
to whatever I want the app name to be. Obviously not ideal so if you know how to change that, I would love to know. **

## For dev and prod: 
  `npm install`

## For dev:
### Frontend: 
`npm run dev`

HTTP server built on port `3000`

nrepl port on `3333`

I use neovim w/conjure so run your editor's equivalent of: `ConjureShadowSelect app`

This should give you hot reloading on save, including tailwind css changes.
I think something is causing postcss to run even without save sometimes, but it isn't affecting development while I track that down.

### Backend:
To start the server run `clojure -M -m TODO.core`

Start your normal repl like usual. (e.g. For me that's `clj -M:repl` and connect.)

TBH, I'm not quite sure how to have the backend and frontend connected to their respective repls and running at the same time quite yet.

## For prod: 
`npm run release`

`clojure -T:build uber`

`java -jar target/TODO-standalone.jar`
