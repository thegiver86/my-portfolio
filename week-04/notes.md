# Week 4: Virtualization & Containers
**Commands Used:**
- `docker run -d -p 8080:80 nginx`: I ran this to pull a lightweight web server image, run it in the background (detached), and punch a hole through the container to expose port 80 to the host's port 8080.
- `docker-compose up`: Used to orchestrate multiple containers simultaneously according to a YAML blueprint.
**TLAB-04 (Operation Fortified Node):** Completed. Built a segmented WordPress and MySQL stack, ensuring the database network was set to `internal: true` to air-gap it.
