# Interview Kit

A technical application security interview exercise built around a chat application with services written in Java, C#, Go, Ruby, JavaScript, and TypeScript.

## Interview exercise

Review the application for security issues, explain their impact and exploitability, and propose practical fixes. Implement agreed changes while preserving the application's expected behavior. Be prepared to discuss your reasoning, tradeoffs, and how you validated your work.

The interviewer will define the services to review, the time available, and the expected deliverables. Service README files describe functionality and review scope. The files in `allowed_files.txt` provide a starting point for code changes; confirm the interview scope with your interviewer.

The application uses `localhost` and `irc.local` as hostnames.

## Prerequisites

- Docker with Docker Compose
- Python 3 if using the optional packaging script
- Several gigabytes of free disk space for container images
- Linux is recommended; local tests may require troubleshooting on macOS or Windows

## Running locally

This application intentionally contains security weaknesses. Run it in an isolated development environment with Docker, and restrict access to your machine. Review port bindings in `docker-compose.yml` before starting; PostgreSQL currently publishes port `42110` on all host interfaces.

Start all services:

```sh
docker compose up --build -d
```

Open <http://localhost:42101>.

Rebuild and restart a specific service:

```sh
docker compose up --build -d java-api
```

Replace `java-api` with the relevant service name from `docker-compose.yml`.

Stop services:

```sh
docker compose down
```

Remove containers and volumes, including local database state:

```sh
docker compose down -v --remove-orphans
```

## Testing

Stop running services before using the test scripts. The scripts build and start the environment, run functional tests in Docker, and then tear down the environment, including its volumes. Test runs reset local application data.

Linux or macOS:

```sh
./runtests.sh
```

Windows PowerShell:

```powershell
.\runtests.ps1
```

Windows Command Prompt:

```bat
runtests.bat
```

Passing functional tests helps confirm that expected behavior is preserved. Validate security fixes separately and explain any limitations in your verification.

## Deliverables

Follow the interviewer's instructions for sharing findings and code changes. Include the affected component, impact, supporting evidence, proposed remediation, and validation results for each finding.

If a code archive is requested, run:

```sh
python3 make_package.py
```

The script creates `appsec-submission.zip` containing only files matched by `allowed_files.txt`. Changes outside that list will not be included.

## License

See [LICENSE.md](LICENSE.md) for the MIT license and copyright notice.
