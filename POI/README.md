\# SemanticGuard: Semgrep Rules for PHP Object Injection (POI) Detection



\## Overview



SemanticGuard is a curated collection of Semgrep rules focused on detecting PHP Object Injection (POI) vulnerabilities. This project helps security researchers and DevSecOps engineers integrate automated POI scans into their CI/CD pipelines and code reviews.



\## Features



\* \*\*POI-Focused Rules\*\*: Comprehensive patterns for sinks (`unserialize`, `igbinary\_unserialize`, etc.) and magic methods (`\_\_wakeup`, `\_\_destruct`, `\_\_get`, `\_\_invoke`, etc.).

\* \*\*Taint Detection\*\*: Rules targeting user-controlled input sources (`$\_GET`, `$\_POST`, `$\_COOKIE`, `php://input`, `session\_start()`).

\* \*\*Modular Design\*\*: Easily extendable YAML-based rules that you can mix and match for your codebase.



\## Getting Started



\### Prerequisites



\* PHP project (any framework or custom code)

\* \[Semgrep](https://semgrep.dev/) v1.x or later

\* Git and a Unix-like shell (WSL, Linux, macOS)



\### Installation



1\. Clone this repository:



&nbsp;  ```bash

&nbsp;  git clone https://github.com/yourusername/SemanticGuard.git

&nbsp;  cd SemanticGuard

&nbsp;  ```

2\. (Optional) Create a Python virtual environment and install Semgrep:



&nbsp;  ```bash

&nbsp;  python3 -m venv .venv

&nbsp;  source .venv/bin/activate

&nbsp;  pip install semgrep

&nbsp;  ```



\## Usage



\### Running the POI Ruleset



Execute the provided rules against your PHP code:



```bash

semgrep --config poi\_full\_rules.yml /path/to/your/php/project

```



\### Example Output



```text

models/IceCreamModel.php

&nbsp; └─ Magic method \_\_invoke() detected; object can be called like a function.

models/PizzaModel.php

&nbsp; └─ Magic method \_\_destruct() detected; may be abused in a gadget chain.

```



\### Customization



You can include or exclude specific rules by editing `poi\_full\_rules.yml`. For example, to disable the `php-preg-eval` rule, comment it out:



```yaml

\# - id: php-preg-eval

\#   pattern: ...

```



\## Rule Structure



\* \*\*ID\*\*: Unique identifier for each pattern.

\* \*\*Pattern\*\*: PHP code snippet or `pattern-either` list.

\* \*\*Message\*\*: Clear description of the issue.

\* \*\*Severity\*\*: `ERROR`, `WARNING`, or `INFO`.

\* \*\*Metadata\*\*: Optional fields like CWE references.



\## Contributing



Contributions are welcome! To add new rules:



1\. Fork the repository.

2\. Create a new branch: `git checkout -b feature/new-vulnerability`

3\. Add or update YAML rule files under the root directory.

4\. Add tests or examples in the `examples/` folder.

5\. Submit a pull request and describe your changes.



\## Roadmap



\* Expand beyond POI to detect:



&nbsp; \* SQL Injection (SQLi)

&nbsp; \* Cross-Site Scripting (XSS)

&nbsp; \* Remote Code Execution (RCE)

&nbsp; \* Insecure Configuration (e.g. cookie flags, headers)

\* Add taint propagation rules (Semgrep Pro style)

\* Integrate with GitHub Actions for CI/CD scans



\## License



This project is licensed under the \[MIT License](LICENSE).



\## Acknowledgments



\* \[Semgrep Community](https://semgrep.dev/)

\* Public CVE databases (NVD, Mitre)

\* Contributors and security researchers



