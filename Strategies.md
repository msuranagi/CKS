Strategies to efficiently search and navigate the allowed documentation under the pressure of the CKS exam clock:
## 1. Master the Built-In Search bar

* Kubernetes Docs: Use the search bar at kubernetes.io/docs. It uses an internal search engine that ranks official guides very well.
* Trivy and Falco: Both sites have custom search bars powered by Algolia. Typing exact keywords (like falco rules or trivy image) will instantly bring up the exact syntax you need to copy.

## 2. Leverage Google Site Search (site:)
Because you are limited to specific domains, you can use Google in your exam browser tab to pinpoint exact pages faster than clicking through menus. Use the site: operator:

* site:kubernetes.io/docs networkpolicy ingress
* site:falco.org/docs custom rules
* site:aquasecurity.github.io/trivy/ target

## 3. Use Browser Search (Ctrl+F or Cmd+F)
Once you are on a page, don't read it entirely. Immediately press Ctrl+F and search for the key configuration block or keyword.

* Example: On the NetworkPolicy page, search yaml to jump straight to a full, copy-pasteable manifest template.

## 4. Create a "Bookmarks" Mental Map
Since external browser bookmarks are strictly forbidden, you must memorize the fastest path to these high-frequency templates:

* Network Policies: Learn the exact path to the "Network Policies" page so you can pull up the default deny/allow templates.
* Admission Controllers: Know how to quickly find the ImagePolicyWebhook configuration block and the list of plugin names to enable in the API server.
* Kube-Bench & Trivy: Navigate directly to the "Getting Started" or "CLI" sections to copy the exact flag structures for scanning.

## 5. Sanitise Your Copy-Pastes
When copying YAML or configurations from the documentation:

* Always paste into your terminal's text editor (like vim or nano).
* Use :set paste in Vim before pasting to prevent automatic indentation from breaking the YAML structure.

Would you like a cheatsheet of the most common keywords to search for during the exam, or are you looking for practice scenarios involving Falco and AppArmor?

