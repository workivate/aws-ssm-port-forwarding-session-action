# AWS SSM Port Forwarding Session Action

This action starts a *local* or *remote* port forwarding session for your GitHub workflow and terminates it upon cleanup.

Forked from [aws-ssm-port-forwarding-session-action](https://github.com/gian2dchris/aws-ssm-port-forwarding-session-action).

# Usage

See [action.yml](action.yml)

# Local Port Forward Example

Forward instance's `i-1234` port `8888` on local port `8888`:
```yaml
steps:
...
- name: SSM Port Forward
  uses: workivate/aws-ssm-port-forwarding-session-action@v1.1.0
  with:
    target-id: 'i-1234'
    portNumber: 8888
    localPortNumber: 8888
- name: Curl Test
  run: |
    curl -v http://127.0.0.1:8888
```

# Remote Host Port Forward Example

Use instance `i-1234` to forward traffic to database on `postgresql-database.cluster-abcd.eu-west-1.rds.amazonaws.com` listening on port `5432`, and bind it to local port `5432`:
```yaml
steps:
...
- name: SSM Port Forward
  uses: workivate/aws-ssm-port-forwarding-session-action@v1.1.0
  with:
    target-id: 'i-1234'
    portNumber: 5432
    localPortNumber: 5432
    host: postgresql-database.cluster-abcd.eu-west-1.rds.amazonaws.com
- name: PSQL Test
  run: |
    pg_isready -h 127.0.0.1 -p 5432
```

# Limitations

At the moment Unix socket port forwarding is not supported.

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
