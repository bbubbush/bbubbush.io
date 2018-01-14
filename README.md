# bbubbush's Diary 

## [ Page build failed: Config file error ]

If the _config.yml file in your GitHub pages repository has syntax errors, your GitHub Pages site will not build.

If your GitHub Pages site fails to build because the _config.yml file contains syntax errors, we'll send you an email that looks like this.

>+ Subject: Page build failed  
The page build failed with the following error:  
You have an error on line 1 of your <code>_config.yml</code>file.


### Troubleshooting *_config.yml* syntax errors

>Tip: We strongly recommend running Jekyll locally so you can easily debug and fix build errors before pushing to GitHub.  
To learn more about troubleshooting options. see ["Troubleshooting GitHub Pages builds"](https://help.github.com/articles/troubleshooting-github-pages-builds/)

Check your *_config.yml* file at line referenced in the build failure email. Ensure that:

>- You are using spaces instead of tabs in the file.  
- You have included a space after the "." for each key/value pair.  
    >Correct example: <code>timezone: Africa/Nairobi</code>  
    Build fail example: <code>timezone:Africa/Nairobi</code>  
- You are only using UTF-8 characters.  
- You quote any special characters.  
    >Correct example: <code>title: "my awesome site: an adventure in parse errors"</code>  
    Build fail example: <code>title: my awesome site: an adventure in parse errors</code>

~~이정도 선에서 일단 해결이 되서 여기까지만 작성~~