# metadata101.github.io

This repository contains the source code for the [metadata101.org](https://www.metadata101.org) website, which is hosted using GitHub Pages.

## About

The metadata101 project provides resources, documentation, and tools for understanding and working with metadata standards and best practices.

## Website Content

The website is built using Jekyll and includes the following sections:

- **Schema Documentation** - Information about metadata schemas

## Local Development

### Prerequisites

- Ruby 2.7 or higher
- [Bundler](https://bundler.io/)

### Setup

1. Clone the repository:
```bash
git clone https://github.com/metadata101/metadata101.github.io.git
cd metadata101.github.io
```

2. Install dependencies:
```bash
cd website
bundle install
```

3. Serve the site locally:
```bash
bundle exec jekyll serve
```

The site will be available at `http://localhost:4000`

## Building the Site

To build the site for production:

```bash
cd website
bundle exec jekyll build
```

The generated static files will be in the `website/_site/` directory.

## Directory Structure

```
website/
├── _config.yml          - Jekyll configuration
├── _posts/              - Blog posts and news
├── _site/               - Generated static site (not in the repository)
├── assets/              - Images, CSS, and other assets
├── index.md             - Homepage
└── Gemfile              - Ruby dependencies
```

## Publishing

This repository uses GitHub Pages. Any changes pushed to the main branch will automatically be built and published to https://www.metadata101.org

## License

This project is licensed under the CC0 1.0 Universal License. See the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to:

- Report issues or suggest improvements
- Submit pull requests with enhancements
- Contribute documentation or examples

For major changes, please open an issue first to discuss proposed changes.

## Contact

For questions or feedback about the metadata101 project, please visit [https://www.metadata101.org](https://www.metadata101.org) or open an issue in this repository.
