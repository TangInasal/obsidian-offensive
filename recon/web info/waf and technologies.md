<h2>technologies</h2>

site: builtwith.com
extension: wappalyzer
tool: whatweb

<h2>waf</h2>

<h4>nuclei</h4>
`nuclei -u <target.com> -t ~/.local/nuclei-templates/http/technologies/waf-detect.yaml`

<h4>wafwoof </h4>
`wafw00f -a <target.com>
