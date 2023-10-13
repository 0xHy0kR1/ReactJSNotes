## Deploying TextUtils
Whenever we create our application for production, we build it using the npm run build command and not by using npm start.

**npm run build:**
npm run build bundles the app into static files for production, i.e. it creates a build folder that contains your application as a static application.
For confirmation open your application in build folder.

**Note**: React Router doesn’t work perfectly with Github pages

### Steps for Hosting our React Application:
1. **Add the Home page field in your package.json:**
```json
"homepage": "https://myusername.github.io/my-app",
```

2. **Install gh-pages in your react app:**
```python
npm install --save gh-pages
```

3. **Add the script in "package.json"**
```json
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build",
```

4. **Run the npm run deploy**

**Hence our application has been hosted on Github.**
If you are facing any problem, then check out the pages section available in settings, and make sure to select the branch as gh-pages as shown below:
![[github_pages1.webp]]

## In a nutshell:
![[github_pages2.webp]]
