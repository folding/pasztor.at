# Abstract

This is the Jekyll and architecture source code of the [pasztor.at](https://pasztor.at) website.

## License

Text and images are protected by copyright, everything else is free for learning / copypasting. 

## Contents

Notable parts of this repository:

- [_ansible](_ansible): contains the Ansible source code to deploy the CDN behind the website
- [_docker](_docker): contains the Docker containers running on the aforementioned CDN
- [_includes](_includes), [_layouts](_layouts), [_plugins](_plugins), [_sass](_sass): Jekyll theme stuff
- [_posts](_posts): Blog posts and events for Jekyll
- [assets](assets): Contains graphics and other assets for the site.
- [.build.sh](.build.sh): The Jekyll build script
- [.cssh.sh](.cssh.sh): Cluster SSH to all CDN nodes
- [.deploy.sh](.deploy.sh): rsync script to deploy the generated content
- [.dns.json](.dns.json): The Route53 DNS settings
- [.dns.sh](.dns.sh): The script to deploy Route53 DNS settings
- [.optimize.sh](.optimize.sh): Script to optimize PNG images using optipng

## About the CDN

The CDN is a collection of machines that receive requests based on latency via Amazon Route53. The theory behind it is
described in [this blog post](https://pasztor.at/blog/building-your-own-cdn). The CDN is deployed
[using Ansible](_ansible/cdn.yml).

Each node is running three servers: traefik to handle SSL and forward requests, nginx to serve the actual content and
PHP-FPM to handle PHP requests. These nodes are run in separate Docker containers using
[docker-compose](_docker/docker-compose.yml).

Content is [deployed using rsync](.deploy.sh) after it is generated by Jekyll.
