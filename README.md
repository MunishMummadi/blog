# My Personal Blog

This is the repository for my personal blog, where I share my thoughts on technology and other things.

## Development

To run the development server, you'll need to have [Zola](https://www.getzola.org/) installed. Once you have Zola installed, you can run the following command to start the local development server:

```bash
zola serve
```

This will start a local server at `http://127.0.0.1:1111` and automatically rebuild the site when you make changes.

## Production

To build the site for production, run the following command:

```bash
zola build
```

This will create a `public` directory with the static files for the site. You can then deploy the contents of this directory to your web server.
