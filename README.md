![CI/CD](https://github.com/kool-dev/docker-phpqa/workflows/CI/CD/badge.svg)

## Description

Minimal PHP QA Docker image focused on loca/CI static analysis, styling and other tools.

It's plays nicely with [kool.dev](https://github.com/kool-dev/kool) managed environments, but can fit in any other PHP use-case.

#### Tools included in the image

**Static analysis**

- Phan - static analyzer for PHP (`phan`)
- PHP Mess Detector (`phpmd`)
- PHP Copy/Paste Detector (`phpcpd`)

**Code Style**

- PHP Coding Standards Fixer (`php-cs-fixer`)

**Security**

- Local PHP Security Checker (`local-php-security-checker`)

**Testing**

- PHPUnit 9.5 (`phpunit`)
- PHPUnit 10 (`phpunit10` for cutting-edge testing)

## Usage

Just execute any QA tool available straight from a new container. Using [`kool`](https://github.com/kool-dev/kool) is the prefered way:

```console
$ cd my-laravel-project/
$ kool docker kooldev/phpqa:7.4 phan
$ kool docker kooldev/phpqa:7.4 php-cs-fixer
```

With vanilla Docker you would need to run:

```
$ docker run --rm --init -it -v $(pwd):/app -w /app kooldev/phpqa:7.4
```

> We strongly recommend checking out [`kool` CLI](https://github.com/kool-dev/kool) for more benefits to your Docker environemnts.

## Available Tags

The image built is [`kooldev/phpqa`](https://hub.docker.com/r/kooldev/phpqa/tags?page=1&ordering=last_updated) with tags:

### 7.4

- [7.4](https://github.com/kool-dev/docker-phpqa/blob/main/7.4/Dockerfile)

## Using kool.yml

Examples of what you can do in a `kool` powered environment. Add to your `kool.yml` file:

```yaml
# kool.yml
scripts:
  # just an alias to the PHPQA container
  phpqa: kool docker kooldev/phpqa:7.4
  # using the alias to call each tool with predefined parameters
  # assuming your application code is located in a `app/` folder
  phan: kool run phpqa phan --color -p -l app -iy 5
  phpcpd: kool run phpqa phpcpd --fuzzy app
  # ...
```

## Contributing

Please feel free to use and open a PR with more QA tools you find useful to have! As a sort of roadmap these are the goals in our mind for the short term:

- Make tools specific configurations available for the user in a friendly manner.
- Ship boilerplate of CI snippets for popular engines (Github Actions, CircleCI, TravisCI).
- Add more tools that we find helpful.


### Update images with templates

You should change `fwd-template.json` for configuration and `template/` folder for the actual base templates.

After any changes, we need to run `kool run template` to parse the templates and generate all versions folder/files.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
