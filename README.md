# SemBlog

[![pipeline status](https://gitlab.semrush.net/flame-team/semblog/semblog/badges/master/pipeline.svg)](https://gitlab.semrush.net/flame-team/semblog/semblog/-/commits/master)
[![coverage report](https://gitlab.semrush.net/flame-team/semblog/semblog/badges/master/coverage.svg)](https://gitlab.semrush.net/flame-team/semblog/semblog/-/commits/master)


Create an AWESOME blog!

##How to run project:

1. `make docker-pull` will pull all needed images
2. `make up` run all containers
3. `make enable-nfs` setup native NFS for Docker
4. `make composer-install` install all needed packages   
5. `make generate-env` will generate base .env file
6. `make db-migrate` run migrations
7. Follow the link `localhost/api/documentation` to use interactive api doc

## API Doc
RC page - https://semblog-rc.rc-k2.semrush.net/api/documentation 

PROD page - https://semblog-prod.k1.semrush.net/api/documentation

## PhpMetrics
https://flame-team.pages.semrush.net/semblog/semblog/master/metrics/index.html

And next time xdebuk will do "knock-knock" to used ip address.

## Developer tools

### Developer commands (from Makefile)
- [Running project](#running-project)
- [XDebug](#xdebug)
- [Database](#database)
- [Building images](#building-images)
- [Elasticsearch](#elasticsearch)
- [Redis](#redis)
- [Composer](#composer)
- [Fixing code](#fixing-code)
- [Log and Bash](#log-and-bash)
- [Install semver](#install-semver)
- [Building all images in Gitlab](#building-all-images-in-Gitlab)
- [Other](#other)

#### Running project
| Command                | Description|
| ---------------------- | ------------------------------------------ |
| `make docker-pull`     | pull all needed images for running project |
| `make up`              | up containers |
| `make up up-blackfire` | run containers with blackfire |
| `make down`            | down containers |
| `make generate-env`    | generate base .env file |
| `make enable-nfs`      | setup native NFS for Docker |

#### XDebug
| Command                     | Description|
| --------------------------- | ------- |
| `make up-xdebug`            | up containers with XDebug |
| `make set-xdebug-ip`        | setup XDebug ip |
| `make set-xdebug-mac-ip`    | setup XDebug ip for Mac |
| `make docker-xdebug-build`  | build php-core-xdebug and php-fpm-xdebug |

#### Database
| Command                 | Description|
| ----------------------- | ------- |
| `make db-migrate`       | run migrations |
| `make db-migrate-fresh` | drop all tables and re-run all migrations |
| `make db-fresh`         | drop all tables, re-run all migrations and seed the database with records|
| `make up-test-db`       | build test-mysql |
| `make seed-feature`     | re-run all migrations and seed records with class=FeatureMainSeeder |

#### Building images
| Command                 | Description|
| ----------------------- | ------- |
| `make rebuild-images`   | rebuild images (php-core, php-fpm, php-composer, nginx)|
| `make push-images`      | push images (php-core, php-fpm, php-composer, nginx) |
| `make build-files`      | build files (copy different files with --chown=1000:1000 into image) |
| `make push-files`       | push files |
| `make build-core`       | build php-core |

#### Elasticsearch
| Command                 | Description|
| ----------------------- | ------- |
| `make build-el`         | build elasticsearch |
| `make up-elastic`       | up elasticsearch |

#### Redis
| Command                 | Description|
| ----------------------- | ------- |
| `make redis-cli`        | run redis-cli |

#### Composer
| Command                 | Description|
| ----------------------- | ------- |
| `make composer`         | open bash php-composer |
| `make composer-install` | run command `composer install` |
| `make composer-da`      | run command `composer dump-autoload` |

#### Fixing code
| Command                    | Description|
| -------------------------- | ------- |
| `make larastan`            | check php by larastan |
| `make codestyle-fix`       | fix codestyle for the whole project |
| `make generate-models-doc` | run command `php artisan ide-helper:models` (after changing eloquent models you can regenerate phpdoc for models) |
| `make generate-swaggger`   | run generating swaggger |
| `make fix-everything`      | run generate-models-doc, codestyle-fix and larastan|

#### Log and Bash
| Command            | Description|
| ------------------ | ------- |
| `make log`         | show logs |
| `make bash`        | run bash in working environment |
| `make bash-xdebug` | open bash php-core-xdebug |

#### Install semver
| Command                | Description|
| ---------------------- | ------- |
| `make install-semver`  | install semver |

#### Building all images in Gitlab
| Command              | Description|
| -------------------- | ------- |
| `make build-feature` | build all images in Gitlab (docker-rc-'hash') in feature branch |
| `make build-rc`      | pull master and build all images in Gitlab (docker-rc-‘hash’) for rc stage|
| `make build-prod`    | pull master and build all images in Gitlab (docker-prod-‘hash’) for prod stage |

#### Other
| Command                | Description|
| ---------------------- | ------- |
| `make run-horizon`     | run command `php artisan horizon` |

### Useful kubectl commands
Delete all pods with errors

`kubectl get pods | grep Error | cut -d' ' -f 1 | xargs kubectl delete pod`

### Profile with Blackfire

Run containers with blackfire and without xdebug: `make up up-blackfire`

Then run url for profiling: `docker exec -it semblog_blackfire_1 blackfire curl http://nginx/blog/api/v3/categories`
