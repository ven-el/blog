# Contributing to Venel Blog

## How to Contribute

1. **Fork the Repository**: Click the “Fork” button on the top right to create your own copy of this repository.

2. **Clone Your Fork**: Clone the forked repository to your local machine:

   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_FORK.git
   ```
3. Create a New Branch: Create a new branch for your changes:

   ```bash
   git checkout -b feature/your-feature-name
   ```
4. Add Your Blog Post: Create a new Markdown file in the content/posts/ directory. Use the following front template at the top of your file:

```
---
title: Title of the post
description:
date:
tldr: (optional)
draft: true/false (optional)
tags: [tag names] (optional)
toc: true/false (optional)
---
```

5. Add Images: Place any images you want to include in your blog post in the static/ directory. You can organize them into subdirectories as needed. For example, you might create a folder like static/your-folder-name/.

6. Reference Images in Your Post: To add images in your Markdown file, use the following syntax:

   ```bash
   ![](/your-folder-name/your-image-file.jpg)
   ```

7. Commit Your Changes: Add and commit your post:

   ```bash
   git add content/posts/your-post-file.md static/images/your-folder-name/your-image-file.jpg
   git commit -m "Add your post title"
   ```
8. Push and Create a Pull Request: Push your changes and create a pull request on the original repository.
