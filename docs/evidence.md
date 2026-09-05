# Submission evidence

The following links open the workflow results directly in the public repository:

* [Frontend Continuous Integration - successful run](https://github.com/mohit8890/cd12354-Movie-Picture-Pipeline/actions/runs/33885187996)
* [Backend Continuous Integration - successful run](https://github.com/mohit8890/cd12354-Movie-Picture-Pipeline/actions/runs/33885210353)
* [Frontend Continuous Deployment - successful run](https://github.com/mohit8890/cd12354-Movie-Picture-Pipeline/actions/runs/33860215924)
* [Backend Continuous Deployment - successful run](https://github.com/mohit8890/cd12354-Movie-Picture-Pipeline/actions/runs/33861888239)

The frontend deployment workflow now waits for the frontend rollout to complete, polls the
LoadBalancer until it is reachable, and confirms the app returns HTTP 200 before declaring success.
The LoadBalancer URL is printed in the workflow logs as:

```
==>>>> FRONTEND_MICROSERVICE_URL http://<hostname>
```

**Verification screenshot (required):** the browser address bar must show the frontend
LoadBalancer URL, **not** `localhost`. Fetch the URL with:

```bash
kubectl get service frontend -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'
```

Then open `http://<that-hostname>` in a browser. The Movie List page must render (Top Gun:
Maverick, Sonic the Hedgehog, A Quiet Place) — proving the deployed frontend pulled data from
the backend API through the `REACT_APP_MOVIE_API_URL` environment variable. The URL must be
visible in the screenshot's address bar.

The backend API is available at:

http://a5036c43ff125488bb9bf22d514dedb6-1835778001.us-east-1.elb.amazonaws.com/movies

## Student Note

Copy the following plain-text information into the Udacity submission:

Public GitHub repository: https://github.com/mohit8890/cd12354-Movie-Picture-Pipeline

Backend LoadBalancer: http://a5036c43ff125488bb9bf22d514dedb6-1835778001.us-east-1.elb.amazonaws.com

Frontend LoadBalancer: (paste the hostname from ``kubectl get service frontend``, or from the
``FRONTEND_MICROSERVICE_URL`` line in the workflow logs)

The four successful workflow links above are the CI/CD evidence. Also attach a screenshot of the Movie List page with the frontend LoadBalancer in the browser address bar and a screenshot (or curl output) of the backend `/movies` URL above.
