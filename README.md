# NPM Audit Interpreter and Check MK output generator

This program takes the output of a `npm audit --json` run and interprets it.
The parameters given define the thresholds to be used, and the output is written to the given directory for check mk local checks.

Requirements:
 * An npm installation with the `npm audit` command available.

```bash
> npm_audit_checkmk -f tests/example.json -s 'frontend_vulnerabilities'
<<<local>>>
P frontend_vulnerabilities INFO=0|LOW=7;20|MODERATE=2;10;20|HIGH=55;1;3|CRITICAL=2;0;0 See `npm audit` for more details.
```

## Usage

```bash
pushd /path/to/your/project
npm audit --json | npmauditcheckmk -o /var/lib/check_mk_agent/spool/90000_npm_audit.txt
popd
```

### Help
```bash
> npm_audit_checkmk -h
usage: npm-audit-checkmk [-h] [-f FILE] [-o OUTPUT] [-s SERVICE_NAME]
                         [-d DIRECTORY] [-iw INFO_WARNING] [-ic INFO_CRITICAL]
                         [-lw LOW_WARNING] [-lc LOW_CRITICAL]
                         [-mw MODERATE_WARNING] [-mc MODERATE_CRITICAL]
                         [-hw HIGH_WARNING] [-hc HIGH_CRITICAL]
                         [-cw CRITICAL_WARNING] [-cc CRITICAL_CRITICAL]

Creates checkmk local check file for npm audit output.warning levels need to
be lower or equal than critical levels.checkmk uses > for level comparisons.

optional arguments:
  -h, --help            show this help message and exit
  -f FILE, --file FILE  Input file name. Optional. Otherwise read from stdin
                        (-).
  -o OUTPUT, --output OUTPUT
                        Output file name. Optional. Otherwise write to stdout
  -s SERVICE_NAME, --service-name SERVICE_NAME
                        The service name to be used inside the file (default:
                        "npm_audit".
  -d DIRECTORY, --directory DIRECTORY
                        The directory to run `npm audit` in, if given. Only in
                        Python >= 3.5.
  -iw INFO_WARNING, --info-warning INFO_WARNING
                        The warning level for info vulnerabilities (default:
                        None)
  -ic INFO_CRITICAL, --info-critical INFO_CRITICAL
                        The critical level for info vulnerabilities (default:
                        None)
  -lw LOW_WARNING, --low-warning LOW_WARNING
                        The warning level for low vulnerabilities (default:
                        20)
  -lc LOW_CRITICAL, --low-critical LOW_CRITICAL
                        The critical level for low vulnerabilities (default:
                        None)
  -mw MODERATE_WARNING, --moderate-warning MODERATE_WARNING
                        The warning level for moderate vulnerabilities
                        (default: 10)
  -mc MODERATE_CRITICAL, --moderate-critical MODERATE_CRITICAL
                        The critical level for moderate vulnerabilities
                        (default: 20)
  -hw HIGH_WARNING, --high-warning HIGH_WARNING
                        The warning level for high vulnerabilities (default:
                        1)
  -hc HIGH_CRITICAL, --high-critical HIGH_CRITICAL
                        The critical level for high vulnerabilities (default:
                        3)
  -cw CRITICAL_WARNING, --critical-warning CRITICAL_WARNING
                        The warning level for critical vulnerabilities
                        (default: 0)
  -cc CRITICAL_CRITICAL, --critical-critical CRITICAL_CRITICAL
                        The critical level for critical vulnerabilities
                        (default: 0)
```

