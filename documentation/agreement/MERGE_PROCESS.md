Merge Process
===============================
[Back to Team Agreement](README.md)

The recommended way to merge PRs is by making an **automerge comment** on the PR using the checklist below, which includes the special mention "@Workiva/release-management-p". This will not allow PRs to merge that do not meet our minimum requirements (e.g., two +1's and one QA+1, any security or cloudops reviews, all checks passing, ...).

- [Automerge Configuration Settings](https://w-rmconsole.appspot.com/rosie/Workiva/skaardb/functions/)
  - NOTE: Manual merges require manually checking everything here!
- The **Automerge Checklist** ensures that the subsequent tag and deploy go smoothly.
    - Velocity suggestion: Copy the checklist below into your Github “autoreplies”.
![Github "Saved replies" screenshot](images/Github_Saved_replies.png)
- A PR author can automerge his/her own PR (still using the checklist).
- If you need to prevent automerging for some reason, you should use the Github label "Hold Auto-Merge". ("Hold" works too.)
- Please report any automerge anomalies promptly to Release Management (RM) so that we keep our automation tools sharp.

## Automerge Checklist

Automerge Checklist:

- [ ] [MARV](https://w-rmconsole.appspot.com/marv/dt) for skaardb correctly reflects PR's SemVer
- [ ] Deployment Changes and Deployment Notes on PR are properly communicated for subsequent deploy

@Workiva/release-management-p ready for merge.
