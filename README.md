# DISCONTINUED — Kool PHPQA

**Discontinued as of 2026-11-14.** This project receives no maintenance, security updates, or new releases. Existing `kooldev/phpqa` images are provided as-is and are not recommended for new projects.

For new or migrated projects, manage QA tools and their versions within your project and run them on maintained PHP images.

Image publishing and Docker Hub description workflows are disabled. The source, image references, and usage examples below are retained for historical reference.

## Historical description

Minimal PHP QA Docker image focused on local/CI static analysis, styling and other tools.

It's plays nicely with [kool.dev](https://github.com/kool-dev/kool) managed environments, but can fit in any other PHP use-case.

### Tools included in the image

#### Static analysis

- Phan - static analyzer for PHP (`phan`)
- PHP Mess Detector (`phpmd`)
- PHP Copy/Paste Detector (`phpcpd`)

#### Code Style

- PHP Coding Standards Fixer (`php-cs-fixer`)

#### Security

- Local PHP Security Checker (`local-php-security-checker`)

#### Testing

- PHPUnit 9.5 (`phpunit`)
- PHPUnit 10 (`phpunit10`, previously listed as cutting-edge testing)

## Historical usage

Just execute any QA tool available straight from a new container. Using [`kool`](https://github.com/kool-dev/kool) is the prefered way:

```sh
cd my-laravel-project/
kool docker kooldev/phpqa:7.4 phan
kool docker kooldev/phpqa:7.4 php-cs-fixer
```

With vanilla Docker you would need to run:

```sh
docker run --rm --init -it -v $(pwd):/app -w /app kooldev/phpqa:7.4
```

## Historical tags

The image built is [`kooldev/phpqa`](https://hub.docker.com/r/kooldev/phpqa/tags?page=1&ordering=last_updated) with tags:

- [**`8.3`**](https://github.com/kool-dev/docker-phpqa/blob/main/8.3/Dockerfile)
- [**`8.2`**](https://github.com/kool-dev/docker-phpqa/blob/main/8.2/Dockerfile)
- [**`8.1`**](https://github.com/kool-dev/docker-phpqa/blob/main/8.1/Dockerfile)
- [**`8.0`**](https://github.com/kool-dev/docker-phpqa/blob/main/8.0/Dockerfile)
- [**`7.4`**](https://github.com/kool-dev/docker-phpqa/blob/main/7.4/Dockerfile)

## Historical `kool.yml` examples

Examples of what you can do in a `kool` powered environment. Add to your `kool.yml` file:

```yaml
# kool.yml
scripts:
  # just an alias to the PHPQA container
  phpqa: kool docker kooldev/phpqa:8.1
  # using the alias to call each tool with predefined parameters
  # assuming your application code is located in a `app/` folder
  phan: kool run phpqa phan --color -p -l app -iy 5
  phpcpd: kool run phpqa phpcpd --fuzzy app
  # ...
```

## Historical development reference

Development has ended. The template instructions below are retained only to explain how the historical image files were generated.

### Update images with templates

You should change `fwd-template.json` for configuration and `template/` folder for the actual base templates.

After any changes, we need to run `kool run template` to parse the templates and generate all versions folder/files.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
