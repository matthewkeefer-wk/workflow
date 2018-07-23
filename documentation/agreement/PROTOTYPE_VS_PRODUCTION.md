Prototype vs Production Code 
===============================
[Back to Team Agreement](README.md)

## Prototype
* Prototype should be throw away code and should have minimal process to allow for faster development
* Code should live in packages that are designated as being prototype
* Unit tests aren't required
* TODOs / FUTUREs are ok
* Spike repo's are typically used for prototyping (i.e. the early stages of CDS repo)

## Production
* The SkaarDB repo is a Tier 1 production repo, ALL commits must have SOC1 compliance, regardless of whether they are viewed by the developer as prorotype or production.
* Production code should last a long time and will be used by customers, so the code has higher demands for quality and security
* Adheres to unit/functional/integration test requirements (code coverage percentages enforced)
* All commits must follow SOC1 ([Security Our Policy](https://connect.workiva.com/news/security-our-policy), [All About SOC Reports](https://wiki.atl.workiva.net/pages/viewpage.action?spaceKey=SECURITY&title=All+About+SOC+Reports))
* [Support / Monitoring / Feedback](SUPPORT_MONITORING_FEEDBACK.md) will be required

## Transition from Prototype to Production
* Options when moving over to production code
   * Start over - "Throw away the prototype"
   * Refactor / harden to meet all the requirements of code expectations above
      * Resolve all TODO's or FUTURE's
* A meeting should be scheduled to hand off from the architect to the team
   * Pre-requirement - Architectural Review is complete
* The team will own the code moving forward and will engage with the architects as necessary for support or check-ins moving forward.
* The individual team agile process takes over
   * Grooming / Planning
   * Epic / Story / JIRA tickets are created prior to coding (with estimates and sufficient acceptance criteria)
      * % Complete can be filtered back to top level OKRs (displayed in teamgantt or equivalent project tracking software)
