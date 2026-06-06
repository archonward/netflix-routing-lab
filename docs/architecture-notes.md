# Architecture Notes

## What Path-Based Routing Means
Path-based routing is a load balancer feature that sends traffic to different backend targets based on the URL path in the incoming request. In this project, each path will eventually map to a separate target group so the routes can be served independently.

## Future AWS Notes
This section is a placeholder for later documentation about the Application Load Balancer, listeners, listener rules, target groups, EC2 instances, security groups, and deployment steps.

## Planned Route Mapping

| Route | Future Target Group |
| --- | --- |
| `/` | `tg-home` |
| `/trending` | `tg-trending` |
| `/series` | `tg-series` |
| `/movies` | `tg-movies` |
| `/new` | `tg-new` |
