## CORS setting for custom fonts in Cloudfront

Use `gem 'font_assets'`

Add `config.font_assets.origin = "*"` to `config/application.rb`. You can specify origin also.

Run `curl -I <host>/assets/<custom font>` to check it works. It should return HTTP headers below.

```
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET
Access-Control-Allow-Headers: x-requested-with
Access-Control-Max-Age: 3628800
```

Add below headers to **Whitelist Headers** of Behavior of Cloudfront

```
Access-Control-Allow-Origin
Access-Control-Allow-Methods
Access-Control-Allow-Headers
Access-Control-Max-Age
```

Reference:  
http://kennethjiang.blogspot.kr/2014/07/set-up-cors-in-cloudfront-for-custom.html  
https://github.com/equivalent/scrapbook2/blob/master/archive/blogs/2016-09-cors-rails-assets-cdn-heroku.md  
https://gorails.com/forum/rails5-heroku-cloudfront-fonts
