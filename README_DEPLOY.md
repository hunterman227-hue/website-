Deployment automation and hosting helpers

Files added on branch `deploy-automation`:

- .github/workflows/deploy-github-pages.yml — Deploys the html/ folder to GitHub Pages using the official Actions for Pages.
- netlify.toml — Netlify config (publish = "html").
- .github/workflows/deploy-netlify.yml — GitHub Action using nwtgck/actions-netlify to deploy html/ to Netlify. Requires Netlify secrets.
- vercel.json — Minimal Vercel configuration for static deploy of html/.
- .github/workflows/deploy-vercel.yml — GitHub Action to trigger Vercel deployment via vercel-action. Requires Vercel secrets.
- .github/workflows/deploy-render.yml — Simple workflow to trigger a Render deploy via their API. Requires Render API key and service id.
- Dockerfile — Serves the html/ folder with nginx for Docker/VPS/Render usage.

Required repository secrets (add under Settings → Secrets → Actions):

- NETLIFY_AUTH_TOKEN — Netlify personal access token
- NETLIFY_SITE_ID — Netlify site ID
- VERCEL_TOKEN — Vercel personal token
- VERCEL_ORG_ID — Vercel organization ID
- VERCEL_PROJECT_ID — Vercel project ID
- RENDER_API_KEY — Render API key
- RENDER_SERVICE_ID — Render service ID

How to test each platform

1) GitHub Pages (no secrets required):
   - Merge `deploy-automation` into `main` (or push to main). The workflow will run and publish the `html/` folder to GitHub Pages.
   - After the workflow completes, go to the repository Settings → Pages and confirm the site is published. The Pages URL will be shown there.

2) Netlify:
   - Add NETLIFY_AUTH_TOKEN and NETLIFY_SITE_ID as repo secrets.
   - The `deploy-netlify.yml` action will run on pushes to `deploy-automation` and call Netlify to publish the `html/` folder.
   - Alternatively, connect the repo in Netlify's dashboard and set the publish directory to `html`.

3) Vercel:
   - Add VERCEL_TOKEN, VERCEL_ORG_ID, VERCEL_PROJECT_ID as repo secrets.
   - The `deploy-vercel.yml` action will trigger a deploy. You can also connect the repo via Vercel dashboard and set the root/paths as needed.

4) Render:
   - Add RENDER_API_KEY and RENDER_SERVICE_ID as repo secrets.
   - The action will trigger a deploy via Render's API; Render will pull the repo and build according to your service settings.

5) Docker / VPS:
   - Build and run locally or on a VPS: docker build -t twisted-penny-site .
   - docker run -p 80:80 twisted-penny-site

If you want, I can also:
- Create the PR and include this checklist and instructions in the PR description.
- Add a CNAME or Pages configuration for a custom domain if you provide it.

Next steps (what I will do now):
- Push these files to a new branch named `deploy-automation` and open a PR into `main` with instructions and the checklist above.

If you want me to modify any file content or add/remove any provider, tell me now and I will update before opening the PR.
