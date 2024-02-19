# Building a Personal Blog with Hugo and GitHub Pages

## Setting Up a Blog with Hugo
Hugo is a blog framework written in Go, using Markdown for writing posts and automatically generating static site files. It supports a wide range of theme configurations and allows for high customization with embedded JavaScript plugins like comment systems. Other similar frameworks include Gatsby, Jekyll, Hexo, and Ghost, which offer comparable features and usability, allowing for personal preference in choice.

## Installing Hugo
On macOS, I followed the official recommendation and installed Hugo via Homebrew, though the process is similar on other operating systems.
``brew install hugo``
To verify the installation, use:
``hugo version``

## Creating a Hugo Site
After installing Hugo, you can create, configure, and locally debug a website with the hugo new site command.
``hugo new site fatratkiller-site``
Upon completion, you'll see a message like this:
```
Congratulations! Your new Hugo site is created in /Users/Apple/fatratkiller-site.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder from https://themes.gohugo.io/ or create your own with the "hugo new theme <THEMENAME>" command.
2. Consider adding some content. Create single files with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server with "hugo server".
```

The root directory fatratkiller-site will contain files as follows:
```
.
├── archetypes # default.md is the template for new posts
├── assets # Files processed by Hugo Pipes
├── content # Markdown files for blog content
├── data # Data files processed by Hugo
├── layouts # Layout files
├── static # Static files like images, CSS, JS
├── themes # Different themes
└── config.toml # Site configuration file in JSON, YAML, or TOML format
```

## Configuring a Theme
After site creation, you need to choose and configure a theme. The Hugo community offers a wide selection of themes, which can be browsed and previewed on the official themes website.

Official Themes Website: https://themes.gohugo.io/

Recommended Theme:

Pure: https://themes.gohugo.io/hugo-theme-pure/

## Associating a Theme Repository
You can directly clone a theme repository into your project. For example, to use the Pure theme, run the following command in the root directory:
``git clone https://github.com/xiaoheiAh/hugo-theme-pure themes/pure``
This method might lead to conflicts if you modify the theme later. A more recommended approach is to fork the original theme repository to your account and link it using git submodule, allowing for easier maintenance and updates.
```
cd robin-site/
git init
git submodule add https://github.com/pseudoyu/pure themes/pure
```
Then, add the following line to your config.toml file:
``theme = "pure"``

##  Updating the Theme
If you cloned someone else's blog project, initialize submodules with:
``git submodule update --init --recursive``
To sync with the latest updates from the theme repository, use:
``git submodule update --remote``

## Creating a New Post
Create new posts with the hugo new command.
``hugo new posts/test.md``
This command creates a test.md file in the posts directory under content, where you can write your post using Markdown. By default, the draft option in the post's front matter is set to true. Change it to false to publish the post. It's recommended to edit the default.md template in the archetypes directory to set draft: false by default for new posts.

## Generating the Site
To preview your blog locally, use the hugo server command for real-time local debugging without needing to regenerate the site each time.
``hugo server -D``
This command allows you to view your site at http://localhost:1313/ in your browser. However, this is only accessible locally. To publish your site on GitHub Pages, further steps are required.

## Configuration File
The config.toml file contains various parameters for site configuration, such as baseURL for the domain name, title for the site name, and theme for the site theme. It may also include settings for comments and monetization. Refer to your theme's documentation for specific configuration options.

Before publishing, run hugo to render your new content according to the theme, with all generated files typically placed in the public subdirectory. You can configure a different directory in the config file if needed. Then, commit and push all new files to GitHub. Note that it might take some time for the changes to go live after pushing.

## Publishing a Blog with GitHub Pages
GitHub Pages is a static site hosting service that allows you to host a static website for each of your repositories without maintaining a server, offering stability and security. There are two ways GitHub Pages can host your content:

From the README.md or index.html in the root of the master branch.
From the README.md or index.html in the /docs directory of the master branch.
This means you can store your static web pages directly in the master branch and enable the GitHub Pages feature in the repository settings to access your site via a URL.

## Deploying Hugo as a GitHub Page
The process involves creating a GitHub repository named [yourgithubusername].github.io, where yourgithubusername should be replaced with your actual GitHub username. After creating posts and configuring the config.toml file with your repository's URL as the baseURL, generate the site with the hugo command. The resulting public directory contains your static site, which should be pushed to your GitHub repository.
For the first push to the master branch:
```
cd public
git init
git remote add origin https://github.com/yourusername/yourusername.github.io.git
git add .
git commit -m "Initial commit"
git push -u origin master
```
After a few minutes, your site should be accessible through your custom domain, mirroring the local preview from hugo server.

For subsequent updates, run hugo in the site directory and push the changes from the public directory:
```
git add -A
git commit -m "Update"
git push -u origin master
```

### FYR

https://jianzhnie.github.io/post/hugo_site/

https://github.com/bmpi-dev/bmpi.dev/blob/master/config.toml

https://www.bmpi.dev/dev/guide-to-setup-blog-site-with-zero-cost/1/

https://github.com/AyagawaSeirin

https://cuttontail.blog/blog/create-a-wesite-using-github-pages-and-hugo/#8-%E6%9C%AC%E5%9C%B0%E8%B0%83%E8%AF%95%E5%92%8C%E9%A2%84%E8%A7%88
