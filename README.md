## Developer commands (from Makefile)
- [Running project](#running-project)
- [XDebug](#xdebug)
- [Database](#database)
- [Building images](#building-images)
- [Elasticsearch](#elasticsearch)
- [Redis](#redis)
- [Composer](#composer)
- [Fixing code](#fixing-code)
- [Log and Bash](#log-and-bash)
- [Install semver](#semver)
- [Building all images in Gitlab](#building-all-images-in-Gitlab)
- [Other](#other)

### Running project
| Command                | Description|
| ---------------------- | ------------------------------------------ |
| `make docker-pull`     | pull all needed images for running project |
| `make up`              | up containers |
| `make up up-blackfire` | run containers with blackfire |
| `make down`            | down containers |
| `make generate-env`    | generate base .env file |
| `make enable-nfs`      | setup native NFS for Docker |

### XDebug
| Command                     | Description|
| --------------------------- | ------- |
| `make up-xdebug`            | up containers with XDebug |
| `make set-xdebug-ip`        | setup XDebug ip |
| `make set-xdebug-mac-ip`    | setup XDebug ip for Mac |
| `make docker-xdebug-build`  | build php-core-xdebug and php-fpm-xdebug |

### Database
| Command                 | Description|
| ----------------------- | ------- |
| `make db-migrate`       | run migrations |
| `make db-migrate-fresh` | drop all tables and re-run all migrations |
| `make db-fresh`         | drop all tables, re-run all migrations and seed the database with records|
| `make up-test-db`       | build test-mysql |
| `make seed-feature`     | re-run all migrations and seed records with class=FeatureMainSeeder |

### Building images
| Command                 | Description|
| ----------------------- | ------- |
| `make rebuild-images`   | rebuild images (php-core, php-fpm, php-composer, nginx)|
| `make push-images`      | push images (php-core, php-fpm, php-composer, nginx) |
| `make build-files`      | build files (copy different files with --chown=1000:1000 into image) |
| `make push-files`       | push files |
| `make build-core`       | build php-core |

### Elasticsearch
| Command                 | Description|
| ----------------------- | ------- |
| `make build-el`         | build elasticsearch |
| `make up-elastic`       | up elasticsearch |

### Redis
| Command                 | Description|
| ----------------------- | ------- |
| `make redis-cli`        | run redis-cli |

### Composer
| Command                 | Description|
| ----------------------- | ------- |
| `make composer`         | open bash php-composer |
| `make composer-install` | run command `composer install` |
| `make composer-da`      | run command `composer dump-autoload` |

### Fixing code
| Command                    | Description|
| -------------------------- | ------- |
| `make larastan`            | larastan analyze |
| `make codestyle-fix`       | verify codestyle and fix it |
| `make generate-models-doc` | run command `php artisan ide-helper:models` (regenerating phpdoc for models) |
| `make generate-swaggger`   | run generating swaggger |
| `make fix-everything`      | run generate-models-doc, codestyle-fix and larastan|

### Log and Bash
| Command            | Description|
| ------------------ | ------- |
| `make log`         | show logs |
| `make bash`        | open bash php-core |
| `make bash-xdebug` | open bash php-core-xdebug |

### Install semver
| Command                | Description|
| ---------------------- | ------- |
| `make install-semver`  | install semver |

### Building all images in Gitlab
| Command              | Description|
| -------------------- | ------- |
| `make build-feature` | build all images in Gitlab (docker-rc-'hash') in feature branch |
| `make build-rc`      | pull master and build all images in Gitlab (docker-rc-‘hash’) for rc stage|
| `make build-prod`    | pull master and build all images in Gitlab (docker-prod-‘hash’) for prod stage |

### Other
| Command                | Description|
| ---------------------- | ------- |
| `make run-horizon`     | run command `php artisan horizon` |
