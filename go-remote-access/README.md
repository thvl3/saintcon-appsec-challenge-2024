# Go Remote Access Server

## Function
A remote administration program that allows a user to authenticate and run arbitrary commands on the host.

## Vulnerabilities
There are 2 severe vulnerabilities:
- GO-EASY
- GO-HARD

## In-scope files
- main.go

## Exclusions
- Rate-limiting. Infrastructure-level rate limiting is outside the scope of this exercise.
- Constant-time string compare for password.
- Post-auth command injection. That is the entire point of this program.
- Clear-text password storage. Yes, it is a problem. However, a rando on the internet cannot abuse this in any meaningful way without compromising the host in the first place. You are focused on the code, not the config.
