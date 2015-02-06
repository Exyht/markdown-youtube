# markdown-youtube
Adding Youtube video just like adding an Image.

    ![isyoutube](youtube link here)// it's that simple
For example, **markdown-youtube** will convert the following line **virtually**:

    ![isyoutube](https://www.youtube.com/watch?v=Wwp9eaVVW_8)
to:

    <iframe src="https://www.youtube.com/embed/Wwp9eaVVW_8"></iframe>
Manage `iframe` `height, width, border, margin`, etc. using CSS. Something like:

    iframe {
      width: 80%;
      height:350px;
      border: 0;
      margin: 0 auto;
      display:block;
    }
## Why use it?
You can't let your user to use **IFrame** for adding video in Markdown for Security reason.

## In JavaScript
I've modified [Pagedown's](https://code.google.com/p/pagedown/) `Markdown.Converter.js` and `Markdown.Sanitizer.js` to Support Youtube video.

## In PHP
I've also modified [michelf's](https://github.com/michelf/php-markdown) php-markdown `Markdown Extra` in `markdown.php` to Support Youtube video.

## How does this work?
In JavaScript,

1. Check for `isyoutube`,
2. `Given url` characters are escaped,
3. Match `Given url host` to `www.youtube.com`,
4. Slice `v`'s value from the URL,
5. Now place it inside `'<iframe src="https://www.youtube.com/embed/'+value of v+'"></iframe>'`,
6. This `iframe` is sanitized in `Markdown.Sanitizer.js`. Just similar to `img` tag sanitization.

In `Markdown.php` you need to use `Markdown Extra`. The working process is almost same as in JavaScript except sanitization.

For Sanitization process I used **HTMLPurifier**.

     $config->set('HTML.Trusted', true);
     $config->set('Filter.YouTube', true);
