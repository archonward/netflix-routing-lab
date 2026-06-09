# Nginx Deployment Notes

## What Nginx Is
Nginx is a web server that can serve static files like HTML and CSS to a browser. In this project, Nginx will eventually be used on each EC2 instance to return the correct page for that instance.

## Why Each EC2 Instance Needs Its Own Deployment Folder
Each future EC2 instance in this lab is meant to behave like a small, dedicated service for one route. Giving each instance its own deployment folder makes it clear which exact files belong on that server and keeps the routing demo simple.

## Future EC2 Mapping
- `deploy/home/` will map to the future home EC2 server.
- `deploy/trending/` will map to the future trending EC2 server.
- `deploy/series/` will map to the future series EC2 server.
- `deploy/movies/` will map to the future movies EC2 server.
- `deploy/new/` will map to the future new releases EC2 server.

## Expected Nginx Web Root On EC2
These files will eventually be copied into an Nginx web root such as `/usr/share/nginx/html/` on each EC2 instance.

## Why The Deployed HTML Uses Absolute Paths
The deployment copies use route paths like `/movies` instead of local relative links. This matches how the AWS Application Load Balancer will later forward requests by path.

## Local Deploy Package Test
Each folder under `deploy/` is designed to behave like the web root of one future EC2 instance running Nginx.

To test one deploy package locally, open a terminal in the project root and run:

```powershell
cd deploy/movies
python -m http.server 8080
```

Then visit:

```text
http://localhost:8080
```

This simulates the Movies EC2 server serving its own static page.

### What Should Work
- The Movies page itself should load correctly.
- The shared CSS in `deploy/movies/assets/styles.css` should load correctly.

### Important Limitation
- Navigation links such as `/series` or `/trending` may not work during this local single-folder test because the local server is only serving the Movies package.
- Those cross-route links are expected to work later when the AWS Application Load Balancer routes each path to the correct EC2 server.

## Scope Of This Step
This step only prepares static deployment-ready folders. It does not create AWS infrastructure yet.
