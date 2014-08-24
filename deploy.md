Hey Daniel,

I usually use Heroku for hosting simple Keystone sites, it's really easy so I thought I'd share my workflow. (and, it starts at free, which is nice!)

And as a bonus, Keystone comes completely set up to install on heroku in a couple of steps.

First of all, sign up for a heroku account and install the heroku toolbelt. Log in with it and you're ready to go.

Note: Heroku uses git to deploy so I always create a new repo on github, clone it, then use yo keystone to create a site. You can set up git later but I find it easier to start there.

Go into your keystone project's root folder and run:

heroku create

It will generate an app name for you (something like beautiful-island-4327) and set up a git remote called heroku to use for identification (for deployment, etc)

Rename it to something more useful like this:

heroku apps:rename your-app-name

Now you need to add a database. I usually use mongolab which gives you <= 512mb for free, there are a few provides you can choose from though in their add ons directory.

To use mongolab, do this:

heroku addons:add mongolab:sandbox

You'll have to set up billing to do this (it won't charge you; they just want a credit card on file)

Also note you can point your Keystone site at any database provider by customising the MONGO_URI environment variable (just remove the mongolab addon first!)

I also usually add a logging system, my favourite is currently papertrail. This gives you a nice web ui to your application logs (i.e. console.log()) and lets you set up alerts for errors, etc.

The basic plan for papertrail is also free :)

heroku addons:add papertrail:choklad

Finally, you'll want to set up a cloudinary account. You can do this yourself (the dashboard gives you the ENV variable to set up) or you can add it as an add-on to your heroku account like mongolab and paper trail - but I usually do this manually as I want to use the account in development and staging as well, rather than having it tied to a single heroku app.

Bonus: if you click through to the signup page from the keystone docs (http://keystonejs.com/docs/configuration/#services-cloudinary) you should get access to a special cheaper low-tier plan for Keystone users. Also free for light traffic though.

Finally, when you've created your app and got the database (at least) configured, just commit all your code to git and run this command to make your site go live:

git push heroku master

Your site will now be hosted at http://your-app-name.herokuapp.com !

Log into your account to add a real domain for it, and then just point your DNS at heroku and you're off.

You can also set up SSL and whatever else you need.

The only thing to be aware of is that Heroku doesn't keep any changes to the local file system so you can't keep user-uploaded images (etc) without putting them on a 3rd party site / service, hence the Cloudinary / Azure / S3 integration.


It's been a while since I ran through this from scratch, so check out their getting started docs for node.js if you hit any hurdles:

https://devcenter.heroku.com/articles/getting-started-with-nodejs

Hope this helps, let me know if you've got any more questions.

Cheers,
Jed.