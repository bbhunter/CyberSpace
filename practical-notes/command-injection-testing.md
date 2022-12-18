# Command Injection Testing

| Parameter                                                                   | Objective                                                              |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `-h` or `/?`                                                                | What is the system output from using help menu commands?               |
| <p><code>;</code>,<br><code>; echo whoami</code></p>                        | Unix only; run echo after initial command                              |
| <p><code>|</code>,<br><code>echo whoami|</code></p>                         | Perl-specific injection to open files                                  |
| <p><code>||</code>,</p><p><code>|| echo whoami</code></p>                   | Run command if the initial command returns non-zero as the exit status |
| <p><code>&#x26;</code> ,<br><code>&#x26; echo whoami</code></p>             | Run initial command as background task and run next task immediately   |
| <p><code>&#x26;&#x26;</code> ,<br><code>&#x26;&#x26; echo whoami</code></p> | Run if the initial command returns zero as the exit status             |
| `$(whoami)`                                                                 | Unix-only; Bash command execution                                      |
| `` `whoami` ``                                                              | Unix only; using generic process substitution                          |
| `>(whoami)`                                                                 | Unix only; using process substitution                                  |
