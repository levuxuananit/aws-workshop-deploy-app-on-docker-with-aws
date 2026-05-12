# AWS FCAJ Hugo Theme Template

This repository contains a **Hugo theme** based on the great **Grav Learn Theme**, customised for **AWS First Cloud Journey (FCJ)** student projects.  
It can be used as a **starting template** for your static site.

> **Note**: The content of the workshop follows the documentation style from [https://learn.netlify.app/en/](https://learn.netlify.app/en/)

---

## 📌 Overview

- **Framework**: [Hugo](https://gohugo.io/)
- **Theme**: Based on Grav Learn Theme
- **Purpose**: Provide a quick-start template for FCJ students

---

## 🚀 Getting Started

### 1. Fork this repository
1. Click **Fork** at the top-right corner of this repository to copy it to your GitHub account.
2. Follow the instructions at [https://www.youtube.com/watch?v=IlxlD-BWI88](https://www.youtube.com/watch?v=IlxlD-BWI88) to configure GitHub Action


### 2. Install Hugo & Make your workshop
1. Follow the [Hugo installation guide](https://gohugo.io/installation/) for your OS.
2. Verify installation:
```
hugo version
```
3. Run locally
```
cd <your_project>
hugo server
```
4. Open your browser and go to [http://localhost:1313](http://localhost:1313)
5. Make edits to the workshop content according to the topic you have chosen.

### 3. Change Author & Team Name
To update author/team details, edit:
```
layouts/partials/menu-footer.html
```

### 4. GitHub Actions (CI/CD)
You can automate the build & deploy process with GitHub Actions to deploy to GitHub Pages.
Watch this guide for setting up GitHub Actions with Hugo:
📺 [GitHub Actions Setup Video](https://www.youtube.com/watch?v=IlxlD-BWI88)


### 📚 Documentation
For more details on Hugo and theme customization:
- Hugo Docs: [https://gohugo.io/documentation/](https://gohugo.io/documentation/)
- Netlify Learn: [https://learn.netlify.app/en/](https://learn.netlify.app/en/)
