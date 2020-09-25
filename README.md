<div align="center">
  <h1>gatsby-remark-twitter-cards 📇</h1>
  <p>
    <a href="https://www.npmtrends.com/gatsby-remark-twitter-cards" title="Downloads"><img src="https://img.shields.io/npm/dm/gatsby-remark-twitter-cards.svg"/></a>
    <a href="https://github.com/prettier/prettier" title="Prettier Code Formatting"><img src="https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-round"/></a>
    <a href="https://www.npmjs.org/package/gatsby-remark-twitter-cards"><img src="https://img.shields.io/npm/v/gatsby-remark-twitter-cards.svg?style=flat-round"/></a>
    <a href="https://david-dm.org/alessbell/gatsby-remark-twitter-cards" title="Dependencies Status"><img src="https://david-dm.org/alessbell/gatsby-remark-twitter-cards/status.svg"/></a>
    <a href="https://github.com/syntra/gatsby-remark-social-cards/blob/master/LICENCE.md"><img src="https://img.shields.io/github/license/syntra/gatsby-remark-social-cards.svg?style=flat-round"/></a>
  </p>
</div>

![gatsby-remark-twitter-cards in action](https://i.imgur.com/FgObEBR.jpg)

`gatsby-remark-twitter-cards` is a Gatsby plugin that allows you to create individual open graph twitter card images at build time for inclusion in your site's SEO metadata. It generates cards as JPGs with embedded text in the recommended size of 1200px x 630px.

It uses the [`wasm-twitter-card`](https://github.com/alessbell/wasm-twitter-card) library under the hood: by using Rust libraries compiled to WebAssembly, we can work around some of the limitations of the most popular dependency-free image editing library for Node.js, jimp.

It can be added to your remark plugins in `gatsby-config.js` like so:

```js
  plugins: [
    // ...
    {
      resolve: `gatsby-transformer-remark`,
      options: {
        plugins: [
          {
            resolve: `gatsby-remark-twitter-cards`,
            options: {
              title: 'anti/pattern', // website title
              separator: '|', // default
              author: 'alessia bellisario',
              background: require.resolve('./content/assets/base.png'), // path to 1200x630px file or hex code, defaults to black (#000000)
              fontColor: '#228B22', // defaults to white (#ffffff)
              titleFontSize: 96, // default
              subtitleFontSize: 60, // default
              fontStyle: 'monospace', // default
              fontFile: require.resolve('./assets/fonts/someFont.ttf'), // will override fontStyle - path to custom TTF font
              useFrontmatterSlug: false // default, if true it will use the slug defined in the post frontmatter
            },
          },
        ],
      },
    },
  ],
```

## Plugin Options

| Option             | Required | Type                                               | Default value |
| ------------------ | -------- | -------------------------------------------------- | ------------- |
| `title`            | ❌       | string                                             | `""`          |
| `separator`        | ❌       | string (character that separates title and author) | `"|"`         |
| `author`           | ❌       | string                                             | `""`          |
| `background`       | ❌       | hex or file path                                   | `"#000000"`   |
| `fontColor`        | ❌       | hex                                                | `"#ffffff"`   |
| `titleFontSize`    | ❌       | int                                                | `96`          |
| `subtitleFontSize` | ❌       | int                                                | `60`          |
| `fontStyle`        | ❌       | "monospace" or "sans-serif"                        | `monospace`   |
| `fontFile`         | ❌       | path to TTF font file                              | ❌            |

The images will be saved in your site's `/public` folder, and the link to your `twitter:image` should be an absolute URL (something like `${siteUrl}${blogPostSlug}twitter-card.jpg`) E.g. for [this blog post](https://aless.co/how-to-build-a-keyboard/) the generated image can be found at the link [https://aless.co/how-to-build-a-keyboard/twitter-card.jpg](https://aless.co/how-to-build-a-keyboard/twitter-card.jpg).

Further instructions on how to include open graph images in the metadata of your Gatsby blog can be found in the excellent documentation of the plugin that inspired this one, [`gatsby-remark-social-cards`](https://github.com/syntra/gatsby-remark-social-cards#installation)

## Roadmap

- [x] Custom TTF fonts 🎉
- [x] Monospace or sans serif font
- [x] Custom title font size
- [x] Custom subtitle font size
- [x] Custom font color
- [x] Accept path to background image
- [x] OR solid color background with hex code
