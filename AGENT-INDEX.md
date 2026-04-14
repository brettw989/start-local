# start-local Documentation Index

Generated for agent-assisted navigation.

## Overview

- Purpose: Shell-based installer that provisions local Elasticsearch and Kibana dev environments using Docker or Podman containers. Supports version selection, ES-only mode, EDOT Collector, and trial licensing. Not for production use.
- Total files: 26 (excluding .git internals)

## Files

- .editorconfig -- Editor configuration (UTF-8, indent styles per file type, LF for shell scripts)
- .env -- Bashunit test runner configuration (default path, execution time display, stop-on-failure toggle)
- .gitattributes -- Git line ending normalization rules and export-ignore settings
- .github/workflows/lint.yml -- CI workflow: runs ShellCheck, MarkdownLint, YamlLint, and ActionLint on PRs and main pushes
- .github/workflows/test.yml -- CI workflow: runs bashunit integration tests on Ubuntu 22.04/24.04 for both Docker and Podman
- .gitignore -- Ignores lib/ (bashunit install dir) and elastic-start-local/ (generated install dir)
- .markdownlint.yaml -- Markdown lint config: disables line-length (MD013) and blank-line-in-blockquote (MD028) rules
- .yamllint -- YAML lint config: disables document-start rule, sets max line length to 140
- LICENSE -- Apache License 2.0
- NOTICE -- Copyright notice for Elasticsearch B.V.
- README.md -- Primary documentation: features, system requirements, setup instructions (Docker/Podman/curl), version selection, ES-only mode, EDOT Collector, endpoints, API key usage, start/stop/uninstall, env customization, advanced ENV variables, and testing guide
- start-local.sh -- Main installer script for Docker: detects OS/arch, checks disk space, pulls ES/Kibana images, generates docker-compose.yml, creates .env with credentials, starts containers, generates API key, optional EDOT Collector support
- start-local-podman.sh -- Main installer script for Podman: same functionality as start-local.sh but uses podman/podman-compose instead of Docker, with Podman-specific networking and volume handling
- tests/basic_test.sh -- Core integration test: installs ES+Kibana, verifies .env/start/stop/uninstall files exist, checks ES (200), Kibana (200), Kibana login, connector API, API key, and telemetry reporting
- tests/docker/host_gateway.sh -- Docker-specific test: verifies host.docker.internal and model-runner.docker.internal DNS resolution from inside ES and Kibana containers
- tests/docker/proxy.sh -- Docker-specific regression test (issue #79 bug 1): verifies ES and Kibana health checks work when Docker client proxy config is set (tests --noproxy fix)
- tests/expire_license_test.sh -- License expiration test: installs with trial license, modifies expire date to 0, restarts, verifies license downgrades to basic
- tests/get_os_info_test.sh -- Regression test (issue #79 bug 2): verifies get_os_info() handles missing VERSION in /etc/os-release (Arch Linux) without crashing under set -eu
- tests/install_edot_test.sh -- EDOT Collector test: installs with --edot flag, verifies OTLP log endpoint (port 4318) and OpAMP endpoint (port 4320) return 200
- tests/install_esonly_test.sh -- ES-only mode test: installs with --esonly flag, verifies Kibana env vars absent, Kibana container not running, Kibana port unreachable
- tests/install_from_curl_test.sh -- Curl pipeline test: starts local HTTP server, pipes script through curl, verifies full installation (env, start/stop/uninstall files, ES, Kibana, login)
- tests/install_with_env_variables.sh -- ENV variable test: verifies ES_LOCAL_PASSWORD sets a custom password and ES_LOCAL_DIR changes the installation directory
- tests/install_with_version_test.sh -- Version pinning test: installs with -v 8.17.0, verifies version in .env file and in ES cluster info response
- tests/start_stop_test.sh -- Start/stop lifecycle test: verifies stop.sh removes running containers and start.sh brings them back
- tests/uninstall_test.sh -- Uninstall test: verifies uninstall from outside and inside the install folder, checks containers stopped, directory emptied, and optional image removal
- tests/utility.sh -- Shared test helpers: get_http_response_code(), login_kibana(), cap/ret output capture, check_container_service_running(), check_container_image_exists()
