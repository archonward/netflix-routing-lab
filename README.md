# netflix-routing-lab

## Purpose
This repository is a simple static website used to learn AWS Application Load Balancer path-based routing. The project intentionally uses only HTML and CSS so the routing concept stays clear and easy to inspect.

## Learning Goal
The long-term goal is to deploy separate pages behind an AWS Application Load Balancer and route requests to different target groups based on the URL path.

## Planned Architecture
At a high level, one Application Load Balancer will listen for incoming HTTP requests and inspect the request path.

- Requests for `/` will go to the home target group.
- Requests for `/trending` will go to a trending target group.
- Requests for `/series` will go to a series target group.
- Requests for `/movies` will go to a movies target group.
- Requests for `/new` will go to a new releases target group.

Each target group is expected to point to its own EC2 instance in a later phase of the lab.

## Route Meanings
- `/` is the homepage route.
- `/trending` represents trending content.
- `/series` represents series content.
- `/movies` represents movie content.
- `/new` represents new releases.

## Current Scope
This repository currently contains only static HTML and CSS pages for local learning and browser testing.

AWS deployment, load balancer configuration, target groups, and EC2 setup will be added later.

## Deployment folder structure
The deploy/ directory contains per-route deployment copies of the static site for future Nginx-based EC2 instances. Each folder is prepared so a single server can host its own page independently while still using application paths like /movies and /series.

## Local deploy package test
Each folder under `deploy/` is meant to behave like the web root of one future EC2 instance running Nginx.

Example:

```powershell
cd deploy/movies
python -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

This simulates the Movies EC2 server serving its own static page.

Expected behavior:
- The Movies page should load correctly.
- The CSS in `deploy/movies/assets/styles.css` should load correctly.
- Links like `/series` or `/trending` may not work in this single-folder local test because only the Movies deploy package is being served.
- Those links are expected to work later when the AWS Application Load Balancer routes each path to the correct EC2 server.

