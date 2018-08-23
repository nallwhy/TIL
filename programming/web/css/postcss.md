## PostCSS

### What is PostCSS?

It’s a tool that helps to provide feature extensions when writing CSS.

A traditional preprocessor like Sass gives you a whole bunch of functionality all bundled into one tool, irrespective of whether you need or will use all of those features.

On the flip side, PostCSS is a blank slate; you can add as many or as few features to your process as you require.

These features come in the shape of PostCSS plugins. Think of these like using LEGO, where each piece is a different feature that can transform your CSS in some way. PostCSS lets you stick together these pieces so that you can build up your own feature set, adding and removing plugins as and when you need them.


### Why PostCSS?

#### Poct

I love the idea of writing future CSS syntax today and using tooling more aligned with other tools I'm used to

I. Sass 같은 것을 쓰다보면 

I love using Sass. It’s a hugely powerful tool that gives me features that I’d genuinely find it hard to live without.

II. Extensibility

If you wanted to extend the functionality of a preprocessor like Sass, it’s not simple. The codebase for projects like this are quite large and you’d have to understand what’s going on under the hood before trying to contribute to that project.

As PostCSS is made up of plugins, extending it is much easier. You can simply write your own plugin to transform your CSS in the way you require and add it into your PostCSS compilation step. You can then make that plugin available for others to use on their own projects if you wish.

One feature that the PostCSS team has been keen to highlight is that you can start writing CSS with respect to new specifications right now by using plugins like cssnext.


If speed of compilation floats your boat, PostCSS is also incredibly fast – apparently around 3x faster than libsass and 4x faster than Less. Whether that speed is noticeable in your build process probably comes down to the amount of CSS you’re working with; I’d imagine for most users the difference in speed would be barely noticeable (as we’re talking hundredths of milliseconds).

### How to use?


Reference:  
https://ashleynolan.co.uk/blog/postcss-a-review  
https://tylergaw.com/articles/sass-to-postcss
