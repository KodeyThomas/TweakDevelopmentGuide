# Creating A Repo With Silica

Silica is one of those tools that you don't find about till after you need it, you wanted to host your own repo but couldn't figure out how

This guide should make the process of you creating a repo simple and quick

# Hosting

So we have a few options when it comes to hosting our repo, we need to host it somewhere.

Luckily GitHub pages is there to help us. Its where this site and my repo is hosted its free and you don't ever need to worry about bandwidth
If you configure cloudflare too cache all of our files

So for the sake of this tutorial considering it is free, quick and efficient we are going to use [Github Pages](https://pages.github.com)

# Installation

So first we are going to want to `clone` the [Silica Github Repository](https://github.com/Shugabuga/Silica/)

Lets navigate to where ever we want to `clone` the repo on our computer, then type this into terminal/git command line

```bash
git clone https://github.com/Shugabuga/Silica.git
```

Then we need to navigate into that directory

```bash
cd Silica
```

Now we need to install our `Dependancies`

macOS users will have too install [`homebrew`](https://brew.sh/)

After installing `homebrew` then we need to install our `Dependancies`

```bash
brew install dpkg
brew install gnupg
```

Linux users will want to install these `Dependancies`

```bash
apt-get install gnupg
apt-get install git
```

# Setting Up Our Repo

Once the `Dependancies` are installed we now want to run the file `setup.sh`

```bash
./setup.sh
```

> If this doesn't work please run the command 'chmod +x setup.sh' then run ./setup.sh again

Sileo will then take you through a guide of configuring you repo for first time use.

It will cover things such as;

- Repo Name
- Description / Tagline
- Support email
- Website address
- Hex Tint (This can be left as default you don't have to worry about it)

Don't worry all of the settings we configured can be edited later

We are now wanting to add our `Tweaks` to our repo, so lets navigate to the `Packages` directory

# Adding Packages (Tweaks / Themes)

Our repo is configured we just need to add our tweaks

The basic file structure for our `Packages` folder looks like this

```
Packages
    My Tweak
        tweak.deb
        silica_data
            index.json
            description.md
            icon.png
            banner.png
            screenshots
                01.png
                02.png
                a_screenshot.png
    My Second Tweak
        tweak2.deb
        silica_data
            index.json
```

> Please note the tweak.deb is alone with no other files in that directory


The silica_data folder is where the icon, description, screenshot, and other package (tweak/theme) information live
This package is not put in the final package file (the ".deb" file). The following files and folders can go in this folder:

`index.json` is the only `required` file. It is a JSON file including information such as;

- bundle ID
- a short tagline description
- version compatibility
- developer information
- changelog data

> More information on this file is on silcias official github repo found [HERE](https://github.com/Shugabuga/Silica/)


`description.md` is a Markdown file that houses the package's description

`icon.png` is the package's icon as it appears in depictions and in Sileo. It should be a square PNG file.

`banner.png` is the package's banner as it appears in depictions and in Sileo. It should be a rectangular PNG file.

The screenshots folder houses any screenshots you want to be displayed alongside the package.

The `index.json` file, if missing, will be generated when running Silica.

# An Example index.json

Below is an example of the `index.json` file;

```json
{
    "bundle_id": "co.shuga.elementary-lite",
    "name": "Elementary Lite",
    "version": "1.1.2-beta",
    "tagline": "A simplistic, glyph-based theme.",
    "homepage": "https://shuga.co/repo",
    "developer": {
        "name": "Shuga",
        "email": "sileo@shuga.co"
    },
    "maintainer": {
        "name": "Shuga",
        "email": "sileo@shuga.co"
    },
    "social": [
        {
            "name": "Twitter",
            "url": "https://twitter.com/HeyItsShuga"
        },
        {
            "name": "Website",
            "url": "https://shuga.co/"
        }
    ],
    "sponsor": {
        "name": "Shuga Studios",
        "email": "studios@shuga.co"
    },
    "section": "Themes",
    "pre_dependencies": "",
    "dependencies": "com.anemonetheming.anemone",
    "conflicts": "",
    "replaces": "",
    "provides": "",
    "other_control": ["Tag: role::enduser", "SomeOtherEntryToControl: True"],

    "tint": "#55c6d3",
    "works_min": "8.0",
    "works_max": "13.0",
    "featured": "true",
    "source": "https://github.com/Shugabuga/Silica",
    "changelog": [
        {
            "version": "1.1.2-beta",
            "changes": "Thank you for participating in the Elementary beta! All future updates will be given a descriptive changelog with a list of changes."
        }
    ]
}
```

> If this file is throwing errors run it through a JSON Validator

You `MUST` include the;

- bundle_id
- name
- version
- tagline
- section
- works_min
- works_max

The other values are recommended but are not necessary

# 'Compiling' Our Repo

Once this is all done and you have added the packages you want too add we simply run this command in the main `Silica` directory

```bash
python3 index.py
```

... And the output of our repo will be in the newly created `docs` folder

# Uploading to Github Pages

Here are the steps to upload our repo to Github for the world to use

- Create a GitHub account (If you don't have one)
- Create a new repository and initialize it with a README.
- Drag-and-drop all of the contents of the docs directory to the newly-created repository.
- Type something in the text box and click the "Commit Changes" button.
- Go to your repository's settings and scroll down to the GitHub Pages section.
- Set "Source" from "None" to "master branch."

Then GitHub will give you a nice link that looks something like this

`https://kodeythomas.github.io/ExampleRepo/`

> This link does not work it is trivial

If you have a custom domain such as `something.com` then follow the steps to get [GitHub Pages connected to your custom domain](https://help.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site)

And you are done...

If we added a custom domain our repo will be available there if not it will be available at the link GitHub gave us
