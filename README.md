# hugo-blog
Blog source, using Hugo

Using the `story` theme: https://github.com/xaprb/story.git

```shell
git submodule add https://github.com/xaprb/story.git themes/story
```

Change the current directory to `hugo-blog`:

```shell
cd hugo-blog
```

Start server:

```shell
hugo server -D
```

With a web browser, visit `http://localhost:1313/`.

Generate site files (quit server first):

```shell
hugo
```

Publish:

```shell
hugo && ./publish
```
