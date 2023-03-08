**[Full Stack Developer Tips](https://jaeyow.github.io/fullstack-developer/)**

To build and run the blog locally do the following:
1. Using the terminal, navigate to the folder that contains `_config.yml`
2. Then run the following command in the terminal:
```
docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll --platform linux/amd64 -it -p 4000:4000 jekyll/jekyll jekyll serve
```
3. With your browser, navigate to `http://0.0.0.0:4000/`
4. Using Docker, you will not need to fiddle with Ruby dependencies ever!
5. **Profit!!!**
