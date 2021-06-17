<!-- SHIELDS -->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![License][license-shield]][license-url]

<p>
  <a href="https://github.com/helsingborg-stad/dev-guide">
    <img src="images/hbg-github-logo-combo.png" alt="Logo" width="300">
  </a>
</p>
<h3>Helsingborg Developer Guidelines</h3>
<p>
  Everything you need to know to be a developer at Helsingborg Stad.
  Visit the the guideline page <a href="https://helsingborg-stad.github.io/dev-guide/">here.</a>
  <br />
  <a href="https://github.com/helsingborg-stad/dev-guide/issues">Report Bug</a>
  ·
  <a href="https://github.com/helsingborg-stad/dev-guide/issues">Request Feature</a>
</p>




## Table of Contents
- [Table of Contents](#table-of-contents)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Local development for documentation](#local-development-for-documentation)
- [Deploy](#deploy)
- [Just the docs Theme documentation](#just-the-docs-theme-documentation)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)


## Getting Started

### Prerequisites

- Ruby version 2.4.0 or higher, including all development headers (check your Ruby version using ruby -v)
- RubyGems (check your Gems version using gem -v)
- GCC and Make (check versions using gcc -v,g++ -v, and make -v)


### Local development for documentation
Run the development command in the terminal.
```
bundle exec jekyll serve --config _config-dev.yml
```
Visit http://127.0.0.1:4000/dev-guide/ to see your changes.


## Deploy

Deploy will trigger automatically with Github Actions when merging your PR into master branch.  
The action will build the page and push the changes into the `gh-pages`-branch that becomes the source of https://helsingborg-stad.github.io/dev-guide/  


## Just the docs Theme documentation
See what theme specific features that can be used in the [Just the docs documentation](https://pmarsceill.github.io/just-the-docs/)

## Roadmap

See the [open issues][issues-url] for a list of proposed features (and known issues).



## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



## License

Distributed under the [MIT License][license-url].



## Acknowledgements

- [othneildrew Best README Template](https://github.com/othneildrew/Best-README-Template)
- [Just the docs Jekyll Theme](https://github.com/pmarsceill/just-the-docs)



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/helsingborg-stad/dev-guide.svg?style=flat-square
[contributors-url]: https://github.com/helsingborg-stad/dev-guide/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/helsingborg-stad/dev-guide.svg?style=flat-square
[forks-url]: https://github.com/helsingborg-stad/dev-guide/network/members
[stars-shield]: https://img.shields.io/github/stars/helsingborg-stad/dev-guide.svg?style=flat-square
[stars-url]: https://github.com/helsingborg-stad/dev-guide/stargazers
[issues-shield]: https://img.shields.io/github/issues/helsingborg-stad/dev-guide.svg?style=flat-square
[issues-url]: https://github.com/helsingborg-stad/dev-guide/issues
[license-shield]: https://img.shields.io/github/license/helsingborg-stad/dev-guide.svg?style=flat-square
[license-url]: https://raw.githubusercontent.com/helsingborg-stad/dev-guide/master/LICENSE
