# Creating your First App

Let's create our first App for the Storefront. Create a project folder named `name-of-your-app` and open the Terminal in it.

Run `generator-vtex` with the following command:
```sh
yo vtex:storefront --simple
```

And answer the questions with:

- Name it `name-of-your-app`
- Type `name-of-your-company` as vendor

In some node installations, the command above might throw an error message. If you have problems, try running it with `sudo`.

This process will create the basic scaffolding and initial files for your App.

## Folder Structure

A basic App for the Storefront has the following folders and files:

```
.
├── storefront/
│   ├── assets/
│   ├── areas/
│   ├── components/
│   ├── routes/
│   └── resources/
├── .vtexignore
└── meta.json
```

### assets/

Here will rest all files that can be publicly accessed, such as Javascript files, CSS, images, SVGs, fonts, etc.

### areas/

Here are defined which components will be responsible for rendering a page and where a component should plug into the site's structure.

### components/

This folder has the definitions of the components used by Storefront's server.

### routes/

The files in this page define new routes.

### resources/

These files define API calls to be used in component files and in Javascript code.

### meta.json

Every App installed in the Gallery need the `meta.json` file. It keeps several information about your App, such as name (`name`), friendly name (`title`), description (`description`) and dependencias from other apps (`dependencies`).

### .vtexignore

This file is used by the Toolbelt. It lists which files and folders should not be sent to the Gallery. If you're familiar with Git, it works the same was as a `.gitignore` file — in case you want to know more, see [the official documentation for Git](https://git-scm.com/docs/gitignore#_pattern_format).

---

So far, things aren't working yet! Now that we have everything set up, let's get our hands dirty and make this "Hello World!" happen.

## Hello World!

Let's upload our App to the Gallery. Open the Terminal in your App folder and type:

```sh
vtex watch
```

See that running the command will ask you to login. This is necessary so we can send the files to the Gallery. Don't worry, once you're logged in your access will last 24 hours.

Once you login, use `dreamstore` as account and follow with yout VTEX credentials.

After you login, you'll see the Toolbelt will show something like this:

```
Watching name-of-your-app

U meta.json
U storefront/assets/index.js
U storefront/components/HomePage.json
U storefront/areas/home.json
U storefront/routes/home.json

... files uploaded

Your URL: http://sualoja.beta.myvtex.com/?workspace=sb_seuemail
```

What the Toolbelt just did was:

- Read from the `meta.json` file, the name and vendor of your App
- Read the `.vtexignore` file and keep which ones it shouldn't upload
- Upload all files that are not in the `.vtexignore` file list

Open the URL for the store in development by clicking or copying the link made available by the Toolbelt.

>**(?)**
>
>`/?workspace=sb_youremail` is a querystring that points your browser to the development environment instead of your site in production.

You should be reading "Hello World!" in your screen.

The Toolbelt is listening to any modification made in your App files. We can test this opening the `assets/index.js` file and changing the "Hello World" text. Save the file and you'll see the Toolbelt uploaded the changes to the development environment -- the page also auto-refreshed because of the livereload.
