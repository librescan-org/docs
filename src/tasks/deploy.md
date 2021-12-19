# DevOps magicians

The core of efficiency and transparency lies in proper structuring of microservices orchestrated to provide the backbone of Librescan.

The default setup looks like the following:

```yaml
version: '3.7'

services:

  # THE USER FACING WEBSITE
  web:
    image: librescan/web:v0.0.1
    networks:
      - frontend

  # SERVES INCOMING API REQUESTS FROM THE FRONTEND
  api:
    image: librescan/api:v0.0.1
    volumes:
      - config:/config # PERMANENT CONFIG M
    networks:
      - frontend # EXPOSE AT /api URL VIA INGRESS
      - backend # MUST ACCESS DB READ REPLICA

  # SERVES AS A READ-ONLY REPLICA FOR API REQUESTS
  db-read:
    image: librescan/db:v0.0.1
    command: read # INSTRUCTS CONTAINER TO LAUNCH IN READ-ONLY REPLICA MODE
    volumes:
      - db-read:/var/lib/pgsql/data # MOUNT READ-HEAVY VOLUME
    networks:
      - backend # MUST ACCESS WRITABLE DB TO REPLICATE FROM

  # RECEIVES STRUCTURED DATA FROM SCRAPER, OFFERS REPLICATION
  db-write:
    image: librescan/db:v0.0.1
    command: write # INSTRUCTS CONTAINER TO LAUNCH IN WRITABLE MODE
    volumes:
      - db-write:/var/lib/pgsql/data # MOUNT WRITE-HEAVY VOLUME
    networks:
      - backend # MUST BE ACCESSIBLE FOR SCRAPER

  # SCRAPES DATA OFF ETH RPC, STRUCTURES IT AND WRITES IT TO DB
  scraper:
    image: librescan/scraper:v0.0.1
    environment:
      RPC: https://example.com/rpc # ETH COMPATIBLE RPC ENDPOINT
    networks:
      - backend # MUST ACCESS WRITABLE DB TO WRITE TO

networks:

  # THE FRONTEND NETWORK IS CONNECTED TO INGRESS CTL
  frontend:
    driver: bridge

  # BACKEND NETWORK IS FOR BACKEND SVC ONLY
  backend:
    driver: bridge

volumes:

  config: # VOLUME FOR PERSISTENT CONFIGURATION
  db-read: # RESIDES ON SEPARATE READ-HEAVY TUNED DRIVE
  db-write: # RESIDES ON SEPARATE WRITE-HEAVY TUNED DRIVE
```

We are looking for DevOps wizards responsible for fine-tuning the microservice structure.

The first requirement is to translate above docker-compose manifest file into various Kubernetes manifests (deployments, services, ingresses, PV & PVCs, etc.)

---

## Choice of orchestrator(s)

We have to support everything here really.
This is not a subjective question since this part of the application is vastly different from other components.
The other modules can be chosen by us developers, but we surely must not force users to adopt to new container orchestration systems.

### Deployment targets to be supported

- [Kubernetes](https://kubernetes.io)
- [Docker Swarm](https://docs.docker.com/engine/swarm/)
- [Docker Compose](https://docs.docker.com/compose/)

# [> register <](https://forms.gle/92JWCf18ejMaaFSF6) as a contributor

The detailed roadmap of LibreScan will be laid out in January 2022.
It is highly important that the team has a ballpark overview how many contributors we can expect!

If you share the same mindset and you are willing to add value to the crypto community sign up via [this link](https://forms.gle/92JWCf18ejMaaFSF6).
