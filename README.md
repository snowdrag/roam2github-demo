# roam2github-demo

For those who are having issues with [MatthieuBizien/roam-to-git](https://github.com/MatthieuBizien/roam-to-git/) in GitHub Actions, try my new solution:

1. Add secrets for the following values:

    - R2G_EMAIL
    - R2G_PASSWORD
    - R2G_GRAPH
    
2. Update your main.yml with the code here: https://github.com/everruler12/roam2github-demo/blob/main/.github/workflows/main.yml

    - _If you created your repo before October 1st, 2020, you may need to change the branch name from 'main' to 'master'_

This will backup JSON and EDN, but not Markdown (yet)

**See more info at https://github.com/everruler12/roam2github**

---

### Common error causes

- `R2G ERROR - Secrets error: R2G_EMAIL not found` (or `R2G_PASSWORD` or `R2G_GRAPH`)

    One of of those secrets are blank or missing. Add it in Settings > Secrets
    
- `R2G ERROR - Login error. Roam says: "There is no user record corresponding to this identifier. The user may have been deleted."`

    Your `R2G_EMAIL` secret is incorrect. Try updating it.
    
- `R2G ERROR - Login error. Roam says: "The password is invalid or the user does not have a password."`

    Your `R2G_PASSWORD` secret is incorrect. Try updating it.
    
    Make sure you're not using a Google account login, as this is not supported. (If you are, sign out of Roam, and on the sign-in page, click "Forgot your password" to set one.)
    
- Timed out with `R2G astrolabe spinning...`. Possible causes:

    - Roam's servers timed out. Try re-running the job later.
    
    - You graph is too large to be loaded within the backup timeout (default set to 10 minutes). This is highly unlikely, as it shouldn't take 10 minutes to load. But you can try increasing the timeout in main.yml

    - Your `R2G_GRAPH` secret is incorrect. Try updating it (make sure it's only the graph name, not a URL)
    
    - You don't have permission to view that graph.
    
    - Unknown cause. Test with a different graph. Let me know if it happens consistently.

- `R2G ERROR - EDN formatting error: mismatch with original`

    The file integrity check to make sure the formatted version of the EDN file matches the downloaded EDN export failed. Please let me know if this were ever to happen.
