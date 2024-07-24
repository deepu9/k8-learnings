# K8 Learnings

Thanks to Nana for putting together a series of videos<sup><b>1</b></sup> on Kubernetes and Helm Charts.

### My Findings based on the Nana Video series

1. Mongo-Express v1.0.2 docker image at the time of this writing has a bug which prevents it to connect to Mongo database. So, I have to switch the Mongo-Express version to 0.54.0, same as the instructor's one in the video series.
2. Latest version of Minikube doesn't have `kubernetes-dashboard`.
3. With K8s Nginx Ingress Controller, the latest version creates a separate namespace called `ingress-nginx` and put the Ingress Controller pod and service in the namespace.
4. When creating ingress manifest file, one should set the backend server name and port under rule section to a service.

   **For ex.:** In my case, Ingress should redirect the external requests to Mongo-Express, so I set the backend name and port under rule section to Mongo-Express service.

5. No namespace is required in Ingress manifest.
6. New changes in the `backend` section:

   ```yaml
   paths:
     - path: /
       pathType: Prefix
       backend:
         service:
           name: SERVICE_NAME_GOES_HERE
           port:
             number: SERVICE_PORT_NUMBER_GOES_HERE
   ```

   **NOTE: THE ABOVE IS JUST MY FINDINGS FROM THE NANA VIDEO SERIES. THE ABOVE WORKED FOR ME, IT DOESN'T MEAN IT'LL WORK FOR EVERYONE.**

## References

1. [Kubernetes Tutorial for Beginners](https://www.youtube.com/watch?v=X48VuDVv0do) by TechWorld with Nana.
