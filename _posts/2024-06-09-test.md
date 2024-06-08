---
layout: post
title:  "Creating a GitHub Pages Site with Jekyll on Linux: A Step-by-Step Guide"
date:   2024-06-09 01:54:55 +1200
author: cloudy
categories: jekyll update
---
Creating a personal website or blog has never been easier thanks to GitHub Pages and Jekyll. Whether you’re a developer looking to showcase your projects or a writer wanting to share your thoughts, GitHub Pages offers a free and easy way to host your site directly from a GitHub repository. Jekyll, a static site generator, integrates seamlessly with GitHub Pages, making it a popular choice for many.

In this guide, we’ll walk through the steps to set up a GitHub Pages site using Jekyll from a Linux environment.

## Prerequisites

Before we start, ensure you have the following installed:

- **Git**: Version control system to manage your code.
- **Ruby**: Programming language required by Jekyll.
- **Bundler**: Dependency manager for Ruby.

### Step 1: Install Git, Ruby, and Bundler

Open your terminal and update your package list:

```bash
sudo apt-get update
```

Install Git:

```bash
sudo apt-get install git
```

Install Ruby and its development dependencies:

```bash
sudo apt-get install ruby-full build-essential zlib1g-dev
```

Configure your environment to avoid installing Ruby gems (software packages) as the root user:

```bash
echo '# Install Ruby Gems to ~/.gem' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/.gem"' >> ~/.bashrc
echo 'export PATH="$HOME/.gem/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Install Bundler:

```bash
gem install bundler
```

### Step 2: Create a New Jekyll Site

First, install Jekyll:

```bash
gem install jekyll
```

Navigate to the directory where you want to create your site and create a new Jekyll site:

```bash
jekyll new my-awesome-site
cd my-awesome-site
```

### Step 3: Build and Serve the Site Locally

Before deploying your site to GitHub Pages, it’s a good idea to test it locally. Use Bundler to install Jekyll dependencies and serve the site:

```bash
bundle install
bundle exec jekyll serve
```

Open your web browser and go to `http://localhost:4000` to see your new site in action.

### Step 4: Create a GitHub Repository

Go to GitHub and create a new repository. You can name it `username.github.io`, where `username` is your GitHub username, to create a user site. Alternatively, name it anything you like for a project site.

### Step 5: Push Your Site to GitHub

Initialize a new Git repository in your site’s directory, add your files, and push to GitHub:

```bash
git init
git remote add origin https://github.com/username/repository.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

Replace `username` and `repository` with your GitHub username and the repository name, respectively.

### Step 6: Configure GitHub Pages

Go to your repository on GitHub, click on `Settings`, and scroll down to the `GitHub Pages` section. Under `Source`, select the branch you want to use (usually `master` or `main`). Click `Save`.

GitHub will now build your site using Jekyll and host it at `https://username.github.io/repository` (for project sites) or `https://username.github.io` (for user sites).

### Step 7: Customize Your Jekyll Site

Now that your site is live, you can start customizing it. Edit the `_config.yml` file to change the site settings. Add new posts in the `_posts` directory, and customize your layout and styles in the `_layouts` and `_sass` directories.

### Conclusion

Setting up a GitHub Pages site using Jekyll from a Linux environment is straightforward and rewarding. With these steps, you have a solid foundation to build and share your personal website or blog. Explore Jekyll’s extensive documentation and GitHub Pages’ features to take your site to the next level.

Happy coding!
