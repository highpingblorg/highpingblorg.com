+++
title = 'This Website'
date = 2024-05-28
draft = false
+++
In today's digital age, a personal portfolio website is essential for showcasing your skills, projects, and experiences. Whether you're a developer, designer, writer, or any other professional, having an online presence can significantly boost your visibility and credibility. This article will explain how I created this website.

## Why Hugo?

Hugo is one of the most popular open-source static site generators. It's known for its speed, flexibility, and ease of use. Here are a few reasons why Hugo is an excellent choice for your portfolio:

- Blazing Fast: Hugo builds your site in milliseconds, making the development process smooth and efficient.
- Flexible and Powerful: With a wide range of themes and customization options, Hugo allows you to create a unique and professional-looking website.
- Easy to Learn: Hugo's straightforward setup and comprehensive documentation make it accessible even for beginners.

## Step-by-Step Guide to Creating `highpingblorg.com`

### 1. Install Hugo and Git on the system

### 2. Creating a New Hugo Site

Opened my terminal and run the following commands:

```sh
# Create a new Hugo site
hugo new site highpingblorg.com

# Navigate to the new site directory
cd highpingblorg.com
```

### 3. Choosing and Installing a Theme

You can browse themes at [Hugo Themes](https://themes.gohugo.io/). For this guide, we'll use the Risotto theme.

```sh
# Initialize a new Git repository
git init

# Add the risotto theme as a Git submodule
git submodule add https://github.com/joeroe/risotto themes/risotto

# Add the theme to my site configuration
echo 'theme = "risotto"' >> config.toml
```

### 4. Creating Content

Hugo uses Markdown files to create content. Let’s create a few sample pages.

```sh
# Create a new post
hugo new posts/my-first-post.md

# Create an about page
hugo new about.md
```

### 5. Building and Serving Your Site Locally

To see my site in action locally, I ran:

```sh
hugo server
```
Open my browser and navigated to http://localhost:1313 to see my portfolio in action.

### 6. Deploying to GitHub Pages

First, I created a new repository on GitHub named highpingblorg.com. Then, in your terminal, run:

```sh
# Add your GitHub repository as a remote
git remote add origin https://github.com/highpingblorg/highpingblorg.com.git

# Push your Hugo site to GitHub
git add .
git commit -m "Initial commit"
git push -u origin main
```

Now, it's time to create a GitHub Action workflow to build and deploy your site to GitHub Pages. I created a .github/workflows/gh-pages.yml file in your repository with the following content:

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: 'latest'

    - name: Build
      run: hugo

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./public
```

I committed and pushed this file to the repository:

```
git add .github/workflows/gh-pages.yml
git commit -m "Add GitHub Actions workflow for deploying site"
git push

```

After that I could access my website at https://highpingblorg.github.io/highpingblorg.com.

### 7. Custom Domain

Since I used cloudflare to purchase the domain, I used their built in DNS to just forward traffic that visits https://highpingblorg.com to https://highpingblorg.github.io/highpingblorg.com. 
